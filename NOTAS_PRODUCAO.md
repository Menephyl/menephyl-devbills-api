# 🚀 Notas para Produção: Resolução de Módulos (ESM)

Você configurou o TypeScript com `"moduleResolution": "bundler"` no seu `tsconfig.json`.

## Por que fizemos isso?
Isso permite que você importe arquivos sem precisar especificar a extensão compilada (ex: `import rotas from "./routes"` em vez de `"./routes/index.js"`). Durante o desenvolvimento, o pacote **`tsx`** (usado no seu script `yarn dev`) é inteligente o suficiente para resolver essas extensões automaticamente, mesmo usando ECMAScript Modules (`"type": "module"` no `package.json`).

## ⚠️ O Problema em Produção

Quando você for preparar este código para produção (fazer o build), você provavelmente vai usar o comando `tsc` para compilar o TypeScript em JavaScript.

O grande detalhe é que **o `tsc` não altera os caminhos de importação**. Ele vai gerar arquivos `.js` contendo exatamente os mesmos imports que você escreveu:
```javascript
// O arquivo compilado (dist/app.js) terá isso:
import routes from "./routes";
```

Se você tentar rodar o código compilado com o Node.js puro em produção (`node dist/server.js`), **o Node.js vai quebrar**, porque o Node ESM estrito exige a extensão do arquivo e não sabe resolver `"./routes"`.

## 🛠️ Como resolver quando for para produção?

Você terá duas alternativas quando for preparar o build de produção:

1. **Usar um Bundler (Recomendado com a configuração atual):**
   Em vez de usar apenas o `tsc` para gerar o build, use uma ferramenta de bundling backend que saiba resolver os arquivos e juntar tudo, como:
   - **Tsup** (`npm install tsup -D` -> `tsup src/server.ts`)
   - **Vite**, **Esbuild**, **Rollup**, ou **Webpack**.
   O `tsup` é a opção mais fácil e moderna para APIs Node.js hoje em dia.

2. **Reverter a configuração e adotar o padrão NodeNext:**
   Se quiser apenas usar `tsc` puro para o build, você precisará voltar o `tsconfig.json` para `"module": "NodeNext"` (e `"moduleResolution": "NodeNext"`) e corrigir manualmente todos os imports no seu projeto para incluir a extensão `.js` (ex: `import rotas from "./routes/index.js"`).

---
*Dica de Engenharia: Hoje em dia, compilar APIs Node com ferramentas como o `tsup` (que usa `esbuild` por baixo dos panos) é super comum, deixa o build absurdamente rápido e resolve de vez esse problema de extensões.*
