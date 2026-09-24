# 🚀 DevBills API

Uma API RESTful robusta e performática desenvolvida para o gerenciamento de finanças pessoais (DevBills). Este projeto é construído em **Node.js** e foca em tipagem forte, validação de dados e uma arquitetura limpa, seguindo as melhores práticas do mercado.

## 🛠️ Tecnologias Utilizadas

A API foi construída com um ecossistema moderno e focado em produtividade e segurança:

- **[Node.js](https://nodejs.org/)** - Ambiente de execução
- **[TypeScript](https://www.typescriptlang.org/)** - Superconjunto JavaScript para tipagem estática
- **[Fastify](https://fastify.dev/)** - Framework web focado em alta performance e baixo overhead
- **[MongoDB](https://www.mongodb.com/)** - Banco de dados NoSQL orientado a documentos
- **[Zod](https://zod.dev/)** - Validação de esquemas e dados (Rotas e Variáveis de Ambiente)
- **[Biome](https://biomejs.dev/)** - Toolchain super rápida para linting e formatação de código
- **tsx** - Execução nativa de TypeScript em desenvolvimento

## 📦 Funcionalidades e Rotas

A aplicação gerencia categorias e transações financeiras com as seguintes capacidades principais:

### 🏷️ Categorias
- **Criação de Categorias**: Cadastro de novas categorias para classificar os gastos/receitas.
- **Listagem de Categorias**: Consulta das categorias disponíveis.

### 💸 Transações
- **Criar Transação**: Registro de uma nova movimentação financeira (receita ou despesa).
- **Listar Transações por Data**: Filtro avançado para buscar transações num período específico.
- **Resumo Financeiro (Dashboard)**: Agregação de dados para fornecer o balanço e resumo das transações.
- **Deletar Transação**: Remoção de registros financeiros.

## 🚀 Como Rodar o Projeto Localmente

### 1. Pré-requisitos
Certifique-se de ter instalado em sua máquina:
- [Node.js](https://nodejs.org/en/) (Versão LTS recomendada)
- [Yarn](https://yarnpkg.com/) ou NPM
- Uma instância do MongoDB (Local ou via MongoDB Atlas)

### 2. Passos para Execução

1. **Clone o repositório:**
```bash
git clone https://github.com/Menephyl/menephyl-devbills-api.git
```

2. **Acesse a pasta do projeto:**
```bash
cd menephyl-devbills-api
```

3. **Instale as dependências:**
```bash
yarn install
```

4. **Configure as Variáveis de Ambiente:**
Crie um arquivo `.env` na raiz do projeto e preencha conforme necessário (validadas pelo Zod):
```env
PORT=3001
DATABASE_URL="sua_string_de_conexao_mongodb"
```

5. **Inicie o servidor em modo de desenvolvimento:**
```bash
yarn dev
```
A API estará rodando em `http://localhost:3001`.

## 📚 Estrutura do Curso / Cronograma de Implementação
Este projeto segue a evolução arquitetural baseada nos seguintes módulos:
- Configuração inicial e por que TypeScript.
- Setup de ferramentas (Biome, Tsx, etc).
- Estruturação do projeto.
- Conexão e modelagem de Schemas no MongoDB.
- Criação das rotas de Categorias.
- Criação das rotas de Transações.
- Validação rígida usando Zod (tanto para Body/Params quanto para o `.env`).
- Funcionalidades complexas (Filtro por data, Resumo e Exclusão).

## 📝 Licença
Este projeto está sob a licença ISC. Sinta-se à vontade para utilizá-lo para seus estudos!
