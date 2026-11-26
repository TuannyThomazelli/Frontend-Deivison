# Aula 08 — Projeto React

# Parte 1 — Revisão de JavaScript

## Onde inserir JS
- Diretamente no HTML com a tag `<script>`.
- Em **arquivos externos** via `src` (recomendado em projetos maiores).
- Em atributos de evento, como `onclick` e `onblur`.

## Variáveis e tipos
- Podem ser declaradas em qualquer ponto do script e são **case sensitive** (`nome`, `Nome` e `NOME` são diferentes).
- `var`: escopo de **função** (global se fora de função). `let`: escopo de **bloco** `{ }`, mais previsível. `const`: valor constante.
- **Tipos:** String, Number, Boolean, Undefined, Null, Object, Array, Symbol, BigInt. `typeof` verifica o tipo.

## Operadores
| Categoria | Exemplos |
|---|---|
| Aritméticos | `+ - * / % ** ++ --` |
| Comparação | `==` (valor, com conversão), `===` (valor e tipo), `!=`, `!==`, `> < >=` |
| Lógicos | `&&` (E), `\|\|` (OU), `!` (NÃO) |
| Atribuição | `= += -= *= /= %=` |

## Estruturas de controle
- **Condicionais:** `if / else if / else` e o operador ternário (`cond ? a : b`).
- **Repetição:** `for`, `while`, `do...while`, `break` (interrompe) e `continue` (pula para a próxima iteração).

## Funções
Blocos que executam uma tarefa e podem retornar valor com `return`. Podem ser tradicionais (`function nome() {}`) ou **arrow functions** (`const nome = () => {}`). Funções úteis: `console.log`, `alert/prompt/confirm`, `getElementById`, `querySelector`, `addEventListener`, `innerHTML/textContent`.

## Arrays e objetos
- **Arrays:** vários valores em uma variável, acessados por índice; métodos como `forEach`, `filter`, `length`.
- **Objetos:** propriedades (dados), métodos (funções associadas) e `this` (referência ao próprio objeto).

## DOM
Representação em árvore da página, que permite ao JavaScript alterar seu conteúdo.
- **Selecionar:** `getElementById()`, `querySelector()`, `querySelectorAll()`.
- **Alterar:** `textContent`, `value`, `classList`, `createElement()`, `appendChild()`.

```js
const botao = document.querySelector("#botao");
const texto = document.querySelector("#mensagem");
botao.addEventListener("click", () => {
  texto.textContent = "Olá! O conteúdo foi alterado.";
});
```

# Parte 2 — React

## 1. JSX
Extensão de sintaxe do JavaScript que permite escrever estruturas semelhantes a HTML dentro do código, descrevendo a interface dos componentes. Facilita a leitura e a manutenção e relaciona dados ao conteúdo exibido. É transformado em JavaScript antes da execução.

- **Expressões:** chaves `{ }` inserem JavaScript (`<h1>Olá, {nome}!</h1>`, `{a + b}`).
- **Diferenças em relação ao HTML:**
  - `className` em vez de `class`;
  - `htmlFor` em vez de `for`;
  - elementos sem conteúdo devem ser fechados (`<img />`);
  - o componente retorna **um elemento raiz** ou usa Fragment;
  - valores JavaScript entram entre `{ }`.

## 2. Componentes
Unidades **independentes e reutilizáveis** da interface; normalmente funções JavaScript que retornam elementos React (geralmente em JSX). Dividir a interface melhora a organização e permite reaproveitar partes em outras páginas (ex.: `Cabecalho`, `Busca`, `Produto`, `Rodape` em uma loja virtual).

- O nome da função começa com **letra maiúscula** e o componente é usado como `<NomeDoComponente />`.
- Um mesmo componente pode ser usado várias vezes.
- A aplicação forma uma **árvore de componentes**: `App` contém `Cabecalho`, `BarraDePesquisa`, `ListaDeConceitos` (com vários `CardConceito`) e `Rodape`.

```jsx
function Cabecalho() { return <h1>Catálogo React</h1>; }
function App() {
  return (<main><Cabecalho /><p>Explore os principais conceitos.</p></main>);
}
```

## 3. Props
*Properties*: dados recebidos por um componente, enviados do **pai para o filho**. Permitem reutilizar o mesmo componente com conteúdos diferentes (a estrutura permanece, os dados mudam) e tornam explícitos os dados que cada componente usa.

```jsx
function Saudacao({ nome }) { return <h1>Olá, {nome}!</h1>; }
<Saudacao nome="Joao" />
<Saudacao nome="Maria" />
```

- **Fluxo de dados:** em geral descendente (pai → filho), o que facilita saber de onde vêm as informações.
- **Tipos aceitos:** strings (entre aspas), números e booleanos (entre chaves), arrays, objetos, funções e elementos React.

## 4. DOM e Virtual DOM
- **DOM:** representação estruturada do documento HTML no navegador; pode ser consultada e modificada por JavaScript. Em interfaces complexas, alterá-lo manualmente dificulta a manutenção.
- **Virtual DOM:** representação da interface em memória, usada pelo React para coordenar atualizações. O desenvolvedor **descreve o resultado esperado** em vez de indicar cada alteração visual.

### Como a interface é atualizada
1. **Mudança:** ocorre uma interação ou atualização de dados.
2. **Renderização:** o React executa de novo os componentes relevantes para calcular a nova descrição da interface.
3. **Reconciliação:** compara a nova descrição com a anterior.
4. **Atualização:** aplica apenas as alterações necessárias ao DOM do navegador.

Na reconciliação, o React considera o **tipo do elemento** e sua **posição na árvore**; em listas, usa a propriedade `key`. Nem toda nova renderização exige mudanças no DOM.

## 5. Listas e Keys
- Dados em **arrays** viram elementos de interface com **`map()`**, que gera um elemento para cada item.
- **`key`:** propriedade especial que identifica cada item entre irmãos, ajudando o React a reconhecer o que foi mantido, adicionado, removido ou reordenado. Deve ser **estável**, normalmente um identificador do dado (ex.: `aluno.id`).
- Combinação com **`filter()`** (seleciona itens) e `map()` (transforma em JSX). Quando a lista está em estado, **crie novos arrays** em vez de modificar o existente.

```jsx
{alunos.map((aluno) => (<li key={aluno.id}>{aluno.nome}</li>))}
```

## 6. Renderização condicional
Mostra, oculta ou altera partes da interface conforme uma condição (props, estado ou dados recebidos).
- **`if` + `return`:** indicado quando as partes da interface são bem diferentes; o `return` pode encerrar o componente mais cedo.
- **Lista vazia:** exibir mensagem como "Nenhum resultado encontrado" quando `resultados.length === 0`.
- **Operador ternário:** `condicao ? valorSeVerdadeiro : valorSeFalso`, útil para alternar entre carregamento e resultado (`Buscando...` / `Busca finalizada.`). Em apps maiores, carregamento, erro e sucesso podem precisar de tratamentos distintos.