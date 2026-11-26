# Aula 09 — Projeto React 02

## 1. State e useState
- **State** é uma informação que o componente guarda (um contador, uma mensagem). Quando o estado muda, o React **renderiza o componente novamente** para atualizar a tela.
- **Por que uma variável comum não basta?** Alterá-la não dispara nova renderização, e as variáveis locais são recriadas a cada execução do componente. O state guarda valores **entre renderizações** e atualiza a interface quando mudam.

### Hooks
Funções especiais que permitem usar recursos do React em componentes funcionais. Os nomes começam com `use` (`useState`, `useEffect`) e devem ser chamados no início do componente ou de outros Hooks, seguindo as regras do React.

### useState
Retorna **dois elementos**: o valor atual e a função para atualizá-lo; recebe um valor inicial.

```jsx
import { useState } from "react";
function Contador() {
  const [contador, setContador] = useState(0);
  return (
    <section>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>
    </section>
  );
}
```

## 2. Formulários
Permitem que o usuário informe dados (cadastros, buscas, login, preferências). Em React usam **campos HTML, eventos e estado**; o envio pode validar os dados e exibir uma mensagem.

### Campos controlados
Campos cujo valor é controlado pelo estado do React:
- `value` define o valor exibido;
- `onChange` atualiza o estado conforme o usuário digita (`e.target.value` traz o texto).
- Fluxo: **digitação → evento → atualização do estado**.

```jsx
const [nome, setNome] = useState("");
<input value={nome} onChange={(e) => setNome(e.target.value)} />
```

### Envio
- `onSubmit` executa uma função quando o formulário é enviado.
- `e.preventDefault()` impede a ação padrão do navegador (recarregar a página), permitindo que o React controle o que acontece após o envio.

```jsx
function enviar(e) { e.preventDefault(); alert("Formulário enviado!"); }
<form onSubmit={enviar}><button type="submit">Enviar</button></form>
```

## 3. useEffect
Hook para **sincronizar o componente com sistemas externos**: alterar o título da aba, usar temporizadores, buscar dados de APIs. Recebe uma função (o efeito) e, opcionalmente, uma **lista de dependências** que controla quando o efeito roda de novo.

```jsx
useEffect(() => { document.title = titulo; }, [titulo]);
```
- `[]` vazio: executa na montagem do componente.
- `[titulo]`: executa de novo quando `titulo` muda. A dependência deve refletir os valores usados pelo efeito.

### Limpeza do efeito
Efeitos que criam recursos (eventos, temporizadores, conexões) devem liberá-los retornando uma **função de limpeza**. Ela roda antes de uma nova configuração do efeito (quando as dependências mudam) e quando o componente deixa de ser usado. Em buscas de dados, ajuda a evitar atualizações desnecessárias.

```jsx
useEffect(() => {
  window.addEventListener("resize", atualizar);
  return () => window.removeEventListener("resize", atualizar);
}, []);
```
**Conceito-chave:** tudo o que for configurado e precisar ser encerrado deve ter uma limpeza adequada.

## 4. Consumo de APIs
**API** (Application Programming Interface) permite a comunicação entre sistemas; no React, serve para buscar e enviar dados a serviços externos (produtos, usuários, publicações, indicadores).

### fetch
- Faz requisições HTTP e é **assíncrono** (usa `await`).
- `response.json()` interpreta o JSON.
- Verifique `response.ok` para detectar erros HTTP.

### Buscando dados com useEffect + useState
`useEffect` inicia a busca quando o componente é exibido (`[]`) e `useState` armazena os dados e atualiza a interface.

```jsx
useEffect(() => {
  async function carregar() {
    const resposta = await fetch(url);
    const dados = await resposta.json();
    setPublicacoes(dados);
  }
  carregar();
}, []);
```

### Enviando dados com POST
Use `method: "POST"`, `headers` com `Content-Type: application/json` e `body: JSON.stringify(objeto)`. Sempre verifique se a resposta foi bem-sucedida.

### Cuidados importantes
- Tratar erros de rede e verificar o status HTTP (`try/catch`).
- Considerar estados de carregamento, vazio e serviço indisponível.
- Evitar requisições repetidas por dependências incorretas no `useEffect`.
- **Não expor chaves secretas** no código do navegador.
- Respeitar autenticação, limites de uso e políticas de **CORS**.

## 5. React Router
Biblioteca que organiza a navegação: **associa URLs a componentes** e permite navegar entre páginas **sem recarregar todo o documento** a cada clique. Evita concentrar toda a lógica em um único componente.

### Conceitos
- **Rota:** regra que associa um caminho a uma interface.
- **URL:** endereço da página atual.
- **Link:** elemento para navegar entre rotas (preferível ao link tradicional dentro da aplicação).
- **Parâmetro:** parte variável do caminho.
- **Rota aninhada:** rota organizada dentro de uma estrutura pai.

### Configuração
```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

<BrowserRouter>
  <nav>
    <Link to="/">Início</Link>
    <Link to="/sobre">Sobre</Link>
  </nav>
  <Routes>
    <Route path="/" element={<Inicio />} />
    <Route path="/sobre" element={<Sobre />} />
  </Routes>
</BrowserRouter>
```
- `BrowserRouter` envolve a aplicação; `Routes` agrupa as rotas; `Route` define caminho e componente.

### Parâmetros de rota
Úteis para páginas de detalhes; `useParams()` acessa os valores.
```jsx
// Rota: /conceitos/:id
const { id } = useParams();
return <h1>Conceito: {id}</h1>;
```