🔖 Descrição

API simples para gerenciar usuários utilizando Express e Prisma com MongoDB como banco de dados. Ideal como exemplo rápido de CRUD usando Prisma Client.

📂 Estrutura (arquivos principais que você enviou)

server.js — servidor Express com rotas CRUD em /user

prisma/schema.prisma — modelo User

.env — DATABASE_URL (conexão MongoDB)

prisma.config.js — configuração do Prisma

🚀 Requisitos

Node.js (recomendo v18+)

MongoDB (Atlas ou local)

NPM ou Yarn

Dependências: express, @prisma/client, prisma, cors, (opcional: dotenv, nodemon)

⚙️ Instalação e execução (passo a passo)

Clone / entre na pasta do projeto

git clone <url-do-repo>
cd <repo>


Instale dependências

npm init -y
npm i express @prisma/client prisma cors
npm i -D nodemon dotenv


Configurar .env
Não comite este arquivo (ver seção segurança abaixo). Exemplo .env:

DATABASE_URL="mongodb+srv://<usuario>:<senha>@cluster.mongodb.net/<nomeDoDB>?retryWrites=true&w=majority"
PORT=3000


Gerar Prisma Client
Após configurar prisma/schema.prisma:

npx prisma generate


Para sincronizar o modelo com o banco MongoDB (sem migrations SQL), use prisma db push (Prisma não oferece migrate para MongoDB — use db push ou gerencie manualmente índices). 
Prisma
+1

Scripts sugeridos no package.json

"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js",
  "prisma:generate": "npx prisma generate",
  "prisma:push": "npx prisma db push"
}


Rodar o servidor

npm run dev
# ou
npm start


A aplicação escuta por padrão na porta 3000 (ou process.env.PORT se você adaptar o código).

📡 Endpoints (conforme server.js)

Base: http://localhost:3000

GET /user

Lista todos os usuários.

Se você passar query params (name, age, email) o código tenta filtrar por igualdade:

Ex.: GET /user?name=Luana&age=30

Observação: if (req.query) sempre é verdadeiro (objeto vazio também). Recomendo checar Object.keys(req.query).length para saber se há filtros.

POST /user

Cria usuário. Body JSON:

{
  "email": "a@ex.com",
  "name": "Ana",
  "age": "30"
}


Retorna 201 com os dados enviados.

PUT /user/:id

Atualiza usuário por id (campo id mapeado como ObjectId no Prisma).

Hoje retorna 201 — o ideal é 200 (ou 204 sem corpo).

DELETE /user/:id

Deleta usuário por id.

Retorna 200 com mensagem de sucesso.
