# Resumo Expandido: Consumindo APIs no Front-end

**Disciplina:** Frameworks Front-end  
**Instituição:** SENAI  
**Professor:** Prof. Me. Deivison S. Takatu (`deivison.takatu@edu.senai.br`)  

---

## 1. Introdução às APIs e Arquitetura REST

### O que é uma API?
Uma **API (Application Programming Interface)** é um conjunto de protocolos, rotinas e ferramentas que define regras de comunicação entre diferentes componentes de software. Ela permite que sistemas distintos e heterogêneos interajam de maneira padronizada e transparente.

### O Estilo Arquitetural REST (Representational State Transfer)
REST é um modelo arquitetural para desenvolvimento de serviços web distribuídos. Seus pilares fundamentais incluem:
* **Comunicação Cliente-Servidor Sem Estado (Stateless):** Cada requisição do cliente ao servidor deve conter todas as informações necessárias para ser processada; o servidor não armazena contexto do cliente entre requisições.
* **Uso Padrão dos Métodos HTTP:** Operações de leitura, criação, atualização e exclusão são mapeadas diretamente para verbos do protocolo HTTP.
* **Identificação de Recursos via URIs:** Cada recurso (ex: usuário, produto) possui uma URI/URL única.
* **Representação de Dados:** Dados são trocados em formatos padronizados, sendo o **JSON** o mais utilizado.

---

## 2. O Protocolo HTTP e Métodos

O **HTTP (Hypertext Transfer Protocol)** é o protocolo base da World Wide Web, definindo as regras de troca de mensagens entre **clientes** (ex: navegadores, aplicações front-end) e **servidores**.

### Principais Métodos HTTP

| Método | Finalidade | Principais Características |
| :--- | :--- | :--- |
| **GET** | Recuperar informações do servidor | **Seguro** (não altera dados no backend) e **Idempotente** (múltiplas chamadas iguais geram o mesmo resultado). |
| **POST** | Criar novos recursos no servidor | **Não Idempotente** (chamadas repetidas criam múltiplos recursos novos). |
| **PUT** | Substituir completamente um recurso | **Idempotente**; atualiza todas as propriedades do recurso especificado. |
| **PATCH** | Atualizar parcialmente um recurso | Altera apenas os campos enviados no corpo da requisição. |
| **DELETE** | Remover um recurso específico | **Idempotente**; remover um recurso já apagado não altera o estado do sistema. |

### Fluxo de uma Requisição na Prática
1. **Navegador / Front-end:** O usuário interage com a interface (clique, navegação).
2. **Requisição HTTP:** O cliente envia uma mensagem HTTP (GET, POST, PUT, DELETE) com cabeçalhos e/ou corpo de dados.
3. **Servidor (Backend / Express.js):** Recebe a requisição, valida os dados e executa a lógica de negócio.
4. **Banco de Dados / Serviço Externo:** O servidor consulta, grava ou altera registros.
5. **Resposta JSON:** O servidor retorna uma resposta padronizada (código de status + dados em JSON).
6. **Atualização da Tela:** O front-end processa os dados retornados e atualiza a interface de forma reativa.

---

## 3. Endpoints e Formato JSON

### Endpoints
Um **Endpoint** é a URL específica através da qual um recurso ou funcionalidade de uma API é acessado (ex: `https://api.exemplo.com/v1/users`).
* `GET /users`: Lista todos os usuários.
* `POST /users`: Adiciona um novo usuário.

### JSON (JavaScript Object Notation)
O **JSON** é um formato leve e de fácil leitura (por humanos e máquinas) para troca de dados.
* **Estrutura Básica:**
  * **Objetos:** Coleções de pares chave/valor delimitados por chaves `{}`.
  * **Arrays:** Listas ordenadas de valores delimitadas por colchetes `[]`.
* **Tipos de Dados Suportados:** Strings, Números, Booleanos (`true`/`false`), Objetos, Arrays e `null`.

---

## 4. Servidor Backend, Express.js e CORS

### Servidor Backend e Web Services
* **Servidor Backend:** Processa a lógica de negócio, gerencia autenticação e manipula bancos de dados.
* **Web Service:** Serviço acessível pela web que viabiliza a integração entre sistemas desenvolvidos em tecnologias distintas.

### Framework Express.js
O **Express.js** é um framework minimalista e flexível para Node.js que simplifica a criação de servidores HTTP e APIs REST, oferecendo roteamento intuitivo e suporte a middlewares (como logs e controle de segurança).

```javascript
// Exemplo de servidor básico com Express.js e CORS
import express from 'express';
import cors from 'cors';

const app = express();
app.use(cors()); // Libera requisições de diferentes origens (CORS)

app.get('/', (req, res) => {
  res.json({
    date: new Date().toLocaleString('pt-BR'),
    status: 'API funcionando com sucesso!'
  });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Servidor rodando na porta ${PORT}`));
```

### Mecanismo CORS (Cross-Origin Resource Sharing)
O **CORS** é uma política de segurança dos navegadores que restringe requisições HTTP feitas a domínios diferentes daquele que serviu a página web. O pacote `cors` no Express habilita essas permissões de acesso entre origens distintas.

---

## 5. Hospedagem e Deploy em Nuvem com Render

O **Render** é uma plataforma PaaS (*Platform as a Service*) moderna para hospedagem de aplicações Node.js e APIs:
* **Integração Git:** Conexão direta com repositórios GitHub para *Continuous Deployment* (CD) automático.
* **Configuração:**
  * **Build Command:** `npm install` (ou `node`)
  * **Start Command:** `node api.js`
* **Benefícios:** Suporte a portas dinâmicas via `process.env.PORT`, certificado SSL/HTTPS gratuito e plano inicial gratuito.

---

## 6. Atividades Práticas da Aula 04

### Atividade 01: Pesquisa de APIs e Projetos no GitHub
* Pesquisar e clonar **10 projetos no GitHub** que utilizem integração com APIs.
* Analisar cada projeto identificando o framework front-end utilizado e as APIs consumidas.
* Criar um arquivo Markdown contendo uma tabela detalhada com os projetos e suas respectivas especificações.

### Atividade 02: Construção e Publicação de API + Front-end
1. **Desenvolvimento da API (Backend):**
   * Criar uma API em Node.js com **Express** e **CORS** contendo uma rota que retorne a data e hora atuais.
   * Realizar o deploy do serviço no **Render**.
2. **Desenvolvimento da Aplicação Front-end:**
   * Utilizar um **repositório separado** no GitHub para a interface.
   * Consumir a API hospedada no Render e exibir a data/hora atualizada na tela.
   * Publicar o Front-end (ex: no **Vercel**).
3. **Documentação e Entrega:**
   * Montar um documento em PDF/Markdown com capturas de tela (*prints*) do código, da aplicação rodando, dos painéis do Render/Vercel e os links de ambos os repositórios.
