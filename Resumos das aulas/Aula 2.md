# Resumo Expandido: Configuração do Ambiente de Desenvolvimento

**Disciplina:** Frameworks Front-end  
**Instituição:** SENAI  
**Professor:** Prof. Me. Deivison S. Takatu (`deivison.takatu@edu.senai.br`)  

---

## 1. Versionamento de Código vs. Backup Tradicional

### Diferenças Fundamentais
* **Backup:** Trata-se de uma cópia pontual e estática do estado atual do projeto. Não rastreia quem alterou, quando ou por quê, sendo limitado à restauração total do arquivo.
* **Versionamento de Código:** Registra um histórico completo e contínuo de cada modificação. Oferece rastreabilidade por autor e data, suporta colaboração simultânea sem perda de dados e permite reversão granular de alterações.

> ### 🔍 Pesquisa Adicional: O Caos Pré-Versionamento
> Antigamente, desenvolvedores recorriam a pastas com sufixos como `projeto_v1_final`, `projeto_v2_agora_vai.zip`. Isso causava sobrescrita acidental de código por múltiplos desenvolvedores, impossibilidade de saber o motivo das alterações e grande perda de tempo em resolução manual de conflitos.

---

## 2. Versionamento Semântico (SemVer)

O Versionamento Semântico é um padrão internacional para numeração de lançamentos de software no formato **MAJOR.MINOR.PATCH** (ex: `2.1.3`):

1. **MAJOR (X.0.0):** Mudanças estruturais grandes ou alterações na API que **quebram a compatibilidade** com versões anteriores.
2. **MINOR (0.X.0):** Adição de novas funcionalidades mantendo a **compatibilidade retroativa**.
3. **PATCH (0.0.X):** Correções de bugs (*bug fixes*) ou pequenas otimizações que não alteram o funcionamento público das APIs.

> ### 🔍 Pesquisa Adicional: SemVer na Prática e Gerenciamento de Dependências
> No ecossistema JavaScript/NPM, o arquivo `package.json` utiliza caracteres especiais para controlar atualizações do SemVer:
> * `^1.2.3` (Caret): Permite atualizações automáticas de **MINOR** e **PATCH** (ex: até `<2.0.0`).
> * `~1.2.3` (Tilde): Permite atualizações apenas de **PATCH** (ex: até `<1.3.0`).

---

## 3. Ferramentas Essenciais do Ambiente (Git, Node.js e NPM)

### Git e Controle de Versão
Criado por Linus Torvalds, o Git é um sistema distribuído para rastreamento de alterações no código-fonte.
* **Configuração Inicial:** Configuração global de identidade via terminal:
  ```bash
  git config --global user.name "Seu Nome"
  git config --global user.email "seu@email.com"
  ```
* **Tags e Releases:** Marcadores associados a *commits* específicos para sinalizar entregas ou versões estáveis (ex: `git tag 1.0.0` seguido de `git push origin 1.0.0`).
* **Boas Práticas:** Enviar *commits* pequenos e bem documentados, manter mensagens descritivas claras e utilizar *branches* separadas para novas funcionalidades.

### Node.js e NPM
* **Node.js:** Ambiente de execução para JavaScript fora do navegador (*server-side*), fundamental para rodar ferramentas de desenvolvimento moderno, otimizadores e servidores locais.
* **NPM (Node Package Manager):** Gerenciador de pacotes instalado junto ao Node.js.
  * `package.json`: Manifesto com as informações, scripts e dependências do projeto.
  * `package-lock.json`: Garante que todos os desenvolvedores instalem exatamente as mesmas versões das bibliotecas.
  * `node_modules`: Pasta onde os pacotes de código de terceiros baixados são armazenados (esta pasta deve ser listada no `.gitignore`).

---

## 4. Criação e Estrutura de Projetos React

A criação de aplicações React utiliza a ferramenta oficial CLI (`create-react-app`) via utilitário `npx`:

```bash
# Criar a estrutura inicial
npx create-react-app meu-projeto-react

# Entrar no diretório
cd meu-projeto-react

# Executar servidor local de desenvolvimento
npm start
```

### Estrutura do Projeto
* **`public/`:** Contém o arquivo estático `index.html` e assets públicos.
* **`src/`:** Código-fonte da aplicação.
  * `index.js`: Ponto de entrada do JavaScript que renderiza a aplicação na árvore de elementos (DOM).
  * `App.js`: Componente principal/raiz do sistema.
  * `App.css` / `index.css`: Arquivos de estilização específicos e globais.

> ### 🔍 Pesquisa Adicional: A Evolução com Vite.js
> Embora o `create-react-app` continue sendo uma referência didática tradicional, a comunidade moderna migrou predominantemente para o **Vite.js**. O Vite oferece inicialização quase instantânea e substituição de módulos em tempo real (*HMR*) usando renderização nativa de módulos ES (`ESM`).

---

## 5. Deployment e Hospedagem na Vercel

* **O que é Deploy?** O processo de empacotar, compilar e disponibilizar uma aplicação para que ela possa ser acessada publicamente na Web.
* **Vercel:** Plataforma de nuvem otimizada para ecossistemas *Front-end* modernos.
  * Conecta-se diretamente aos repositórios do GitHub/GitLab.
  * Realiza compilação (*build*) e **deploy automatizado** a cada novo `git push` na branch principal.
  * Fornece CDN global e suporte nativo a rotas, HTTPS e funções serverless.

---

## 6. Atividades Práticas da Aula 02

1. **Desenvolvimento e Publicação Prática:**
   * Criar uma aplicação em React usando o VS Code.
   * Versionar o código com Git e sincronizá-lo com um repositório no GitHub.
   * Conectar o repositório à Vercel e obter uma URL pública online.
2. **Relatório Técnico em Grupo (Continuação):**
   * Em grupos de 3 a 5 integrantes, selecionar um framework (React, Vue ou Angular) e produzir um relatório técnico em formato PDF (mínimo 5 páginas) abordando características, ecossistema e exemplos práticos.
