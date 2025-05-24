---
title: "🚀 Como gerar um site estático com Next.js e evitar problemas com imagens"
description: "Aprenda a configurar seu Next.js para gerar páginas estáticas e evitar erros comuns com imagens ao usar a tag <Image />."
pubDate: "May 24 2025"
author: "Arthur Rodrigues"
tags: "ArcaWave, DevOps, Next.js, Build, Deploy"
heroImage: "/jpg/not-found.jpg"
---

Você está tentando fazer o build do seu site Next.js **como páginas estáticas**, mas está tendo problemas com imagens? Então essa dica é pra você!

## Passo 1: Configure o Next.js para gerar HTML estático no build

No seu arquivo `next.config.ts` (ou `next.config.js`), adicione a diretiva abaixo:

```ts
import type {NextConfig} from "next";

const nextConfig: NextConfig = {
  output: "export",
};

export default nextConfig;
```

## Passo 2: Rode o comando padrão do Next.js para build

Isso irá gerar uma pasta `out` na raiz do seu projeto

```shel
npm run build
```

## Passo 3: Rode o comando para servir os arquivos estáticos localmente

```shel
npx serve@latest out
```

<small>Obs: Isso irá instalar o pacote `server` globalmente na sua máquina</small>

## ⚠️ Atenção com as imagens!

Ao servir os arquivos estáticos localmente, você irá perceber que as imagens podem não estar aparecendo isso ocorre
quando você usa o componente `<Image />` do Next.js, pois ele depende da rota especial `/_next/image` para otimizar e
servir as imagens, o que não funciona no modo estático.

Resultado: ao abrir o site estático, suas imagens podem não aparecer, dando erro 404.

## 🔑 A solução simples

Substitua o `<Image />` por tags `<img />` padrão:

```ts
// TROQUE
import Image from "next/image";

<Image src="/logo.png" width={200} height={100} alt="Logo" />;

// POR
<img src="/logo.png" width={200} height={100} alt="Logo" />;
```

Após isso gere o build novamente

<hr/>

<small class="thanks">
Imagem "Not found" de <a href="https://pixabay.com/pt/users/draguth-1837346/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2384304" target="_blank" rel="noopener noreferrer">Draguth Leon</a> por <a href="https://pixabay.com/pt//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2384304" target="_blank" rel="noopener noreferrer">Pixabay</a>
</small>
