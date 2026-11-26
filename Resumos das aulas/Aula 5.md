# Aula 05 — Criando APIs para o Front-end

## 1. Conceitos fundamentais

### Métodos HTTP
| Método | Finalidade | Características |
|---|---|---|
| **GET** | Recuperar informações | Seguro (não altera dados) e idempotente |
| **POST** | Criar novos recursos | Não idempotente (chamadas repetidas criam vários recursos) |
| **PUT** | Substituir completamente um recurso | Usado para atualização |
| **PATCH** | Atualizar parcialmente um recurso | Usado para atualização |
| **DELETE** | Remover um recurso | Idempotente (apagar algo já apagado não causa erro) |

### Endpoint
URL específica que dá acesso a um recurso ou funcionalidade da API; é o ponto de comunicação entre cliente e servidor. Um mesmo endpoint pode responder de formas diferentes conforme o método (ex.: GET lista, POST adiciona).

### JSON
Formato leve de troca de dados, fácil de ler por humanos e de processar por máquinas. Baseia-se em duas estruturas: **objetos** (pares nome/valor) e **arrays** (listas ordenadas).

### Servidor Backend e Web Service
- **Servidor backend:** processa requisições, gerencia dados e responde a clientes (apps, navegadores). Funções: armazenar/recuperar dados, executar regras de negócio e fornecer APIs.
- **Web Service:** serviço acessível via HTTP/HTTPS que permite a comunicação padronizada entre sistemas heterogêneos (linguagens, plataformas e tecnologias diferentes).

## 2. Express.js
Framework minimalista e flexível para Node.js, usado para criar servidores e APIs.

- **Simplifica o Node.js puro**, que exige mais código para rotas e middlewares.
- **Roteamento:** facilita definir rotas como `/users` e `/products`.
- **Middlewares:** funções que processam requisições/respostas (autenticação, logs etc.).
- **Quando usar:** APIs REST, integração com bancos de dados, backends escaláveis, prototipagem rápida e páginas com templates.
- **Quando evitar:** aplicações em tempo real (preferir WebSockets) e processamento pesado (usar Workers).

### Primeira API (passo a passo)
1. Criar a pasta do projeto e abrir no VS Code.
2. `npm install express`
3. `npm install cors express` (CORS é um mecanismo de segurança que controla o acesso entre domínios diferentes no navegador).
4. Criar o arquivo `api.js`.
5. Executar com `node api.js`.

## 3. Publicando no Render
Plataforma de hospedagem em nuvem com suporte a Node.js e Python, deploy contínuo via GitHub, plano gratuito, SSL incluso e interface simples (boa para projetos acadêmicos).

1. Enviar o projeto para um repositório no GitHub.
2. Criar conta em `dashboard.render.com`.
3. Criar um novo **Web Service** e conectar o repositório.
4. Definir os comandos (no slide: Start Command `node api.js`).
5. Fazer o deploy e usar a URL `seu-projeto.onrender.com`.

## 4. Projeto: API de Notas (CRUD)
Evolução do projeto: uma aplicação Express que permite **criar, visualizar, editar e excluir notas**, usando um **arquivo JSON** (`data.json`) como armazenamento e um `server.js` que configura o servidor.

### Rotas
| Operação | Rota | Observações |
|---|---|---|
| Listar | `GET /api/notes` | Retorna todas as notas |
| Criar | `POST /api/notes` | Exige `titulo` e `texto`; ID gerado com `Date.now().toString()` |
| Obter por ID | `GET /api/notes/:id` | Retorna uma nota específica |
| Atualizar | `PUT /api/notes/:id` | Exige `titulo` e `texto`; retorna 404 se não existir |
| Excluir | `DELETE /api/notes/:id` | Remove a nota pelo ID |

### Passos
1. Criar a pasta `projeto-notas`.
2. `npm install express`.
3. `npm install body-parser` (permite ao servidor ler o corpo JSON de requisições POST/PUT).
4. Criar `server.js` (importa Express, body-parser e `fs`; porta 3000; arquivo `data.json`; libera CORS com header `Access-Control-Allow-Origin`; funções `readNotes()` e `saveNotes()` para ler/gravar o JSON).
5. Criar `data.json` com notas de exemplo (`id`, `titulo`, `texto`, `criadoEm`).
6. Executar com `node server.js`.
7. Criar o front-end em **React** que lista, cadastra, edita e exclui notas consumindo a API.
8. Publicar o back-end no **Render**.
9. Trocar `http://localhost:3000/api/notes` no React pela URL pública do Render.
10. Publicar o front-end na **Vercel**.

> **Observação sobre os slides:** o texto descreve que cada nota recebe data de criação e que o DELETE retorna 204, mas o código mostrado cria a nota sem `criadoEm` e responde ao DELETE com uma mensagem JSON. Vale conferir esse ponto ao implementar.

## 5. Documentando uma API com Postman
A documentação de uma API descreve endpoints, métodos HTTP, parâmetros, formatos de resposta e exemplos de requisição.

**Postman** é uma ferramenta para criar, testar, documentar e monitorar requisições HTTP:
- Envia GET, POST, PUT, DELETE etc. e analisa respostas, sem linha de comando.
- Permite **coleções** de requisições, variáveis de ambiente, scripts pré-request e testes automatizados.
- Gera documentação automática e integra com CI/CD via **Newman** (CLI).
- Recursos avançados: **Mock Servers**, monitoramento, GraphQL, WebSockets e OAuth 2.0.