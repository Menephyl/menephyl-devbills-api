# 🧠 Diário de Aprendizados

Este documento registra desafios encontrados, conceitos aprendidos e soluções arquiteturais adotadas ao longo do desenvolvimento do projeto.

---

## 📅 [23/09/2026] - O Dilema dos Módulos: ESM vs CommonJS no TypeScript

### 🐛 Os Sintomas (O que aconteceu?)
1. **Erro de TypeScript (`verbatimModuleSyntax`):** O compilador avisou que "ECMAScript imports and exports cannot be written in a CommonJS file...".
2. **Erro em tempo de execução (Fastify):** A aplicação crachou com `FastifyError: Plugin must be a function or a promise. Received: 'object'`.

A primeira tentativa de resolver foi adicionar `.js` na importação de um arquivo Typescript (`import routes from "./routes/index.js"`), o que resolveu o problema, mas causou grande estranheza por parecer completamente anti-padrão (importar js num arquivo ts).

### 🔍 A Causa Raiz
O ecossistema Node.js está na transição entre dois padrões:
- **CommonJS (Antigo):** Usa `require()`. Era inteligente e resolvia caminhos de forma mágica, não precisava de extensão.
- **ESM - ECMAScript Modules (Novo):** Usa `import/export`. O Node exige que todo caminho relativo possua a **extensão explícita do arquivo final**. 

Como nossa aplicação estava sendo migrada para ESM (`"type": "module"` no `package.json`), o Node passou a exigir as extensões.
O TypeScript (`"module": "nodenext"`) entende essa exigência, mas tem uma regra rígida de design: **O compilador TS não modifica os caminhos de importação**. Se o Node vai ler um arquivo `.js` no futuro, você *tem* que escrever `.js` dentro do código TypeScript. É contraintuitivo, mas é como a equipe da Microsoft desenhou a linguagem.

O erro bizarro do Fastify ("Received: object") aconteceu exatamente por essa confusão de módulos no momento de resolução do arquivo `./routes`, que retornava um objeto de módulo ES em vez da função de rotas pura.

### 💡 A Decisão Arquitetural
**Escolhemos a abordagem de abstração via Bundler:**
Em vez de sujar todo o código fonte escrevendo `.js` nos imports, mudamos a configuração no `tsconfig.json`:
- `"module": "ESNext"`
- `"moduleResolution": "bundler"`

**O que isso significa na prática?**
Informamos ao Typescript: *"Fique tranquilo, haverá um empacotador (bundler) inteligente o suficiente para resolver os caminhos e extensões, você não precisa me forçar a usar a regra purista do Node"*. 
No ambiente de desenvolvimento, a biblioteca **`tsx`** assume esse papel e faz tudo funcionar brilhantemente permitindo imports limpos (`import routes from "./routes"`).

*(Lembrete anotado em `NOTAS_PRODUCAO.md`: No deploy real para produção, teremos que buildar o projeto usando um bundler como `tsup` em vez de compilar via `tsc` puro).*
