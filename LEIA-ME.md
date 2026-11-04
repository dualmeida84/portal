# Portal Sperandio (versão 3D): como publicar

Arquivos desta pasta:

- `index.html`: o portal inteiro em um único arquivo (o Three.js, biblioteca do 3D, é carregado de um CDN confiável, o cdnjs).
- `og-image.png`: imagem de prévia quando o link é compartilhado (WhatsApp, Instagram, Facebook).
- `CNAME`: diz ao GitHub qual endereço usar (`portal.sperandio.com.br`).
- `.nojekyll`: evita processamento desnecessário no GitHub Pages.

Não precisa instalar nada nem usar linha de comando. Este caminho **não mexe** no site do Wix nem no blog: só cria um endereço novo.

## Passo 1: criar o repositório e subir os arquivos

1. Entre em github.com com a conta da imobiliária (ou crie uma, é gratuito) e clique em **New repository**.
2. Nome: `portal`. Deixe como **Public** (o GitHub Pages gratuito exige repositório público; o portal é um site aberto de qualquer forma). Clique em **Create repository**.
3. Na tela do repositório, clique em **uploading an existing file** (ou **Add file > Upload files**).
4. Arraste os 4 arquivos: `index.html`, `og-image.png`, `CNAME` e `.nojekyll`. Se o `.nojekyll` ficar escondido no seu computador, pode deixá-lo de fora.
5. Clique em **Commit changes**.

## Passo 2: ligar o GitHub Pages

1. No repositório, vá em **Settings > Pages**.
2. Em **Source**, escolha **Deploy from a branch**, branch **main**, pasta **/ (root)**, e clique em **Save**.
3. Em 1 ou 2 minutos aparece um endereço provisório, no formato `https://SEU-USUARIO.github.io/portal/`. Abra e confira se o portal funciona (o 3D, os links e a rolagem).

## Passo 3: apontar o subdomínio no Wix

1. No Wix, vá em **Domínios**, escolha `sperandio.com.br` e abra **Gerenciar registros DNS**.
2. Crie um registro **CNAME**: nome `portal`, valor `SEU-USUARIO.github.io` (sem `https://` e sem `/portal`).
3. Volte em **Settings > Pages** no GitHub. Em **Custom domain** deve aparecer `portal.sperandio.com.br`. Quando o GitHub terminar de verificar o DNS (de minutos a algumas horas), marque **Enforce HTTPS**.

Pronto: o portal fica em `https://portal.sperandio.com.br`. Os subdomínios `avalia` e `ficha` e o blog seguem como estão.

## Passo 4 (opcional): fazer o www.sperandio.com.br levar ao portal

Hoje o `www.sperandio.com.br` é uma página do Wix cujo código manda o visitante para `www.imobiliariasperandio.com.br`. Para mandar para o portal, **sem mexer em DNS**, só troque esse código.

**Faça isto só depois de conferir que `https://portal.sperandio.com.br` está no ar.**

1. No editor do Wix, abra a página inicial (a "Redireciona") com o Modo desenvolvedor ligado.
2. **Guarde uma cópia do código atual** (para poder voltar atrás).
3. Troque o código inteiro por este:

```js
import wixLocation from 'wix-location';

$w.onReady(function () {
  wixLocation.to('https://portal.sperandio.com.br/');
});
```

4. Clique em **Publicar**. A partir daí, quem abrir `www.sperandio.com.br` cai no portal.

Observações: cartões, QR codes e assinaturas que usam `www.sperandio.com.br` vão passar a cair no portal em vez de cair direto no site principal (o portal tem o link "Site" para chegar lá). O endereço sem `www` (`sperandio.com.br`) e o blog não mudam.

## Se o endereço não for `portal.sperandio.com.br`

Troque o texto nos arquivos `CNAME` e `index.html` (as linhas `og:url` e `og:image`) pelo endereço real, e use o mesmo nome no registro CNAME do Wix.

## Atualizar depois

No repositório, abra o arquivo, clique no lápis, cole o novo conteúdo e faça o commit. O site atualiza sozinho em cerca de 1 minuto.

## Conferir depois de publicar

- O telhado 3D aparece no topo e muda de lado e de cor conforme a rolagem.
- Os 8 links abrem a página certa em nova aba.
- No celular, a página rola normalmente e o objeto fica na parte de cima.
- Cole o endereço no WhatsApp e veja a imagem de prévia (o WhatsApp guarda a prévia em cache, então pode demorar a atualizar).

## Observações técnicas

- O 3D usa WebGL. Sem WebGL, o telhado aparece em 2D e tudo continua funcionando. Com "reduzir movimento" ativado no aparelho, o 3D é desligado e a página fica estática.
- Computadores muito antigos podem ficar lentos com a areia em 3D.
- Nenhum dado é coletado e não há cookies. Para medir visitas, dá para acrescentar o código do Google Analytics ou do Meta Pixel no `index.html`.
