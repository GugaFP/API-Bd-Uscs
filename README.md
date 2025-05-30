# API-Bd-Uscs
Readme API MongoDB Uscs

# API RESTful - Controle de Treinos e Alimentação

Este projeto consiste no desenvolvimento de uma API RESTful voltada para o gerenciamento de treinos e planos alimentares de usuários, como parte da disciplina de Banco de Dados Não Relacionais. A aplicação utiliza o MongoDB como base de dados, aplicando os conceitos de CRUD (Create, Read, Update, Delete) em coleções específicas. O projeto foi desenvolvido em Node.js com o framework Express.

## Objetivos do Projeto

- Implementar operações básicas de CRUD com MongoDB.
- Integrar dados de treinos e alimentação por usuário.
- Facilitar a consulta rápida dos planos diários por meio de uma única rota.
- Realizar testes via Thunder Client e documentar o funcionamento da API.

---

## Tecnologias Utilizadas

- Node.js
- Express.js
- MongoDB
- Mongoose
- Dotenv
- Thunder Client (testes)

---

## Estrutura de Pastas e Arquivos

```
api-treinos-alimentacao/
├── .env                        # Variáveis de ambiente
├── package.json               # Dependências e scripts
├── src/
│   ├── config/
│   │   └── database.js        # Conexão com o MongoDB
│   ├── controllers/           # Lógica de controle das rotas
│   │   ├── userController.js
│   │   ├── treinoController.js
│   │   └── alimentacaoController.js
│   ├── models/                # Definições dos Schemas Mongoose
│   │   ├── User.js
│   │   ├── Treino.js
│   │   └── Alimentacao.js
│   ├── routes/                # Definição das rotas
│   │   ├── userRoutes.js
│   │   ├── treinoRoutes.js
│   │   └── alimentacaoRoutes.js
│   └── index.js               # Ponto de entrada da aplicação
```

---

## Detalhamento do Banco de Dados

### Collection: Users
```js
{
  nome: String,
  email: String,
  senha: String
}
```

### Collection: Treinos
```js
{
  userId: ObjectId,
  dia: "YYYY-MM-DD",
  exercicios: [
    {
      nome: String,
      series: Number,
      repeticoes: Number,
      carga: String
    }
  ]
}
```

### Collection: Alimentacoes
```js
{
  userId: ObjectId,
  dia: "YYYY-MM-DD",
  refeicoes: [
    {
      horario: String,
      alimentos: [String],
      calorias: Number
    }
  ]
}
```

---

## Configuração do Ambiente

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/api-treinos-alimentacao.git
cd api-treinos-alimentacao
```

2. Instale as dependências:

```bash
npm install
```

3. Configure o arquivo `.env`:

```
MONGODB_URI=mongodb+srv://<usuario>:<senha>@<cluster>.mongodb.net/treinosAlimentacaoDB
```

---

## Executando a Aplicação

```bash
node src/index.js
```

A API será executada em: `http://localhost:3000`

---

## Endpoints da API

### Usuários
- POST /usuarios
- GET /usuarios
- PUT /usuarios/:id
- DELETE /usuarios/:id

### Treinos
- POST /treinos
- GET /treinos/:userId
- PUT /treinos/:id
- DELETE /treinos/:id

### Alimentações
- POST /alimentacoes
- GET /alimentacoes/:userId
- PUT /alimentacoes/:id
- DELETE /alimentacoes/:id

### Plano do Dia
- GET /usuarios/:id/hoje

Retorna treino e alimentação registrados para o dia atual.

---

## Exemplos de Requisições no Thunder Client

### Criar Usuário
```json
POST http://localhost:3000/usuarios
Content-Type: application/json

{
  "nome": "João Silva",
  "email": "joao@email.com",
  "senha": "123456"
}
```

### Buscar Plano do Dia
```json
GET http://localhost:3000/usuarios/6658e0e9f8fabe00225c679a/hoje
```

---

## Utilizando MongoDB Atlas

Para usar a aplicação em nuvem:
- Crie uma conta no MongoDB Atlas (https://www.mongodb.com/cloud/atlas).
- Crie um cluster gratuito.
- Obtenha a URI de conexão e configure-a no .env como MONGODB_URI.
- Permita acesso de IPs e crie um usuário com permissões de leitura e escrita.

---

## Integrantes do Grupo

- Nome 1
- Nome 2
- Nome 3
- Nome 4

(Substituir pelos nomes reais do grupo)

---

## Professor Responsável

Prof. Me. Ricardo Resende de Mendonça

Este projeto foi desenvolvido como atividade prática da disciplina de Banco de Dados Não Relacionais com foco no uso do MongoDB em aplicações modernas.

## Execução Local com MongoDB Instalado

Para rodar o projeto localmente utilizando o MongoDB instalado em sua máquina, siga os passos abaixo.

### Requisitos

- Node.js instalado: https://nodejs.org  
- MongoDB instalado localmente  
- MongoDB Compass (opcional, apenas para visualização)  
- VS Code (ou outro editor de sua preferência)

### Passo a Passo

1. **Clonar o repositório:**

```bash
git clone https://github.com/seu-usuario/api-treinos-alimentacao.git
cd api-treinos-alimentacao
```

2. **Instalar as dependências:**

```bash
npm install
```

3. **Criar o arquivo `.env`:**

Na raiz do projeto, crie o arquivo `.env` com o seguinte conteúdo:

```
MONGO_URI=mongodb://127.0.0.1:27017/api_treino
PORT=3000
```

4. **Iniciar o MongoDB localmente:**

Certifique-se de que o serviço do MongoDB está rodando. Se estiver no Windows, use o MongoDB Compass para conferir (opcional) ou verifique pelo Gerenciador de Tarefas.

5. **Executar a aplicação:**

```bash
node src/index.js
```

A API estará disponível em: `http://localhost:3000`

---

## Testes com Thunder Client (ou Postman)

### Criar usuário

```http
POST http://localhost:3000/usuarios
```

**Body:**
```json
{
  "nome": "Maria",
  "email": "maria@email.com"
}
```

### Listar usuários

```http
GET http://localhost:3000/usuarios
```

### Buscar plano do dia do usuário

```http
GET http://localhost:3000/usuarios/<ID_DO_USUARIO>/hoje
```

Substitua `<ID_DO_USUARIO>` pelo valor retornado na criação do usuário.

---

### Exemplo: Criar treino

```http
POST http://localhost:3000/treinos
```

**Body:**
```json
{
  "userId": "ID_DO_USUARIO",
  "dia": "2025-05-29",
  "exercicios": [
    {
      "nome": "Supino",
      "series": 3,
      "repeticoes": 15,
      "carga": "40kg"
    }
  ]
}
```

### Exemplo: Criar alimentação

```http
POST http://localhost:3000/alimentacoes
```

**Body:**
```json
{
  "userId": "ID_DO_USUARIO",
  "dia": "2025-05-29",
  "refeicoes": [
    {
      "horario": "12:00",
      "alimentos": ["Arroz", "Frango", "Salada"],
      "calorias": 600
    }
  ]
}
```

## Exemplos Visuais com Thunder Client

### Criar Usuário
![Criar Usuário](assets/criar-usuario.jpg)

### Listar Usuários
![Listar Usuários](assets/listar-usuarios.jpg)

### Buscar Plano do Dia
![Plano do Dia](assets/plano-do-dia.jpg)

### Criar Alimentação
![Criar Alimentação](assets/criar-alimentacao.jpg)
