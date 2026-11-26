# Aula 07 — Frameworks CSS

## 1. CSS (Cascading Style Sheets)
O CSS define cores e fontes, mas também margens, alinhamentos, larguras, alturas e elementos flutuantes, garantindo páginas organizadas e responsivas.

**Sintaxe:** `seletor { propriedade: valor }`
- **Seletor:** em qual tag HTML a regra é aplicada.
- **Propriedade:** o atributo a modificar (ex.: `background-color`).
- **Valor:** a configuração desejada (ex.: `#FF0000`).

Comparação com HTML antigo: `<body bgcolor="#FF0000">` equivale a `body { background-color: #FF0000; }`, com mais flexibilidade e padronização.

### Formas de aplicar CSS
| Forma | Como | Quando usar |
|---|---|---|
| **In-line** | Atributo `style` no elemento | Testes ou ajustes pontuais |
| **Interno** | Tag `<style>` no cabeçalho | Estilo usado em uma única página |
| **Externo** | Arquivo `.css` ligado com `<link rel="stylesheet" href="...">` | **Mais recomendado**: organiza e reutiliza estilos em várias páginas |

### Principais propriedades
- **Texto e cor:** `color`, `background-color`, `font-family`, `font-size` (px, em, rem, %), `text-align`.
- **Espaçamento:** `margin` (externo), `padding` (interno).
- **Caixa:** `border`, `width`, `height`.
- **Exibição e posição:** `display` (`block`, `inline`, `flex`), `position` (`static`, `relative`, `absolute`, `fixed`) junto com `top`, `right`, `bottom`, `left`.

### Class e ID
- **Classe** (`.botao-primario`): aplica o mesmo estilo a vários elementos, garantindo consistência e facilitando a manutenção.
- **ID** (`#cabecalho-principal`): estiliza um elemento único; também serve para âncoras e para manipulação precisa via JavaScript.

## 2. Box Model
Descreve as caixas geradas pelos elementos HTML. Camadas, de dentro para fora:
1. **Content:** onde ficam texto e imagens.
2. **Padding:** espaço entre o conteúdo e a borda.
3. **Border:** linha que envolve padding e conteúdo.
4. **Margin:** espaço entre a borda e os outros elementos.

**Por que aplicar:** controlar o tamanho dos elementos, criar espaçamento e organização visual, evitar sobreposição, construir layouts previsíveis e facilitar a adaptação a diferentes telas.

## 3. Flexbox
Módulo de layout **unidimensional** para organizar itens em linhas ou colunas, com distribuição de espaço e alinhamento.

| Propriedade | Valores citados |
|---|---|
| `flex-direction` | `row`, `column` |
| `justify-content` | `flex-start`, `center`, `space-between`, `space-around` |
| `align-items` | `flex-start`, `center`, `flex-end` |
| `flex-wrap` | permite quebra de linha |
| `gap` | espaçamento entre itens |

## 4. Layouts responsivos
Técnica que adapta o conteúdo a diferentes tamanhos de tela (celular, tablet, desktop), melhora a usabilidade e reduz a necessidade de versões separadas para cada dispositivo.

## 5. O que é um Framework CSS?
Conjunto de recursos, padrões, classes e componentes que facilita a criação e a padronização de interfaces web. Componentes típicos:
- **Layout:** Grid, Flexbox e responsividade.
- **Estilos:** cores, espaços e tipografia.
- **Componentes:** botões, cards e navbar.

**Problema do CSS manual:** tudo precisa ser estilizado do zero (botões, cards, formulários, menus, grid, espaçamentos, tipografia).

## 6. Tailwind CSS
Framework baseado no conceito **Utility-First**: em vez de componentes prontos, oferece pequenas classes, cada uma com **uma responsabilidade**, que são combinadas para montar a interface. *Uma utility = uma responsabilidade; várias utilities = um componente.*

Exemplos de classes: `p-6` (padding), `text-xl` (tamanho do texto), `font-bold` (peso), `bg-blue-600` (fundo), `rounded-lg` (bordas), `px-6 py-3` (padding horizontal/vertical), `text-white` (cor do texto).

```html
<button class="bg-blue-600 text-white px-6 py-3 rounded-lg">Enviar</button>
```

### Propósitos
- Reduzir o tempo de desenvolvimento.
- Aumentar a flexibilidade da interface.
- Facilitar a customização (cores, espaçamentos, tipografia).
- Promover reutilização e consistência (classes e tokens de design).
- Simplificar o desenvolvimento responsivo (abordagem **Mobile First**).

### Ferramentas de apoio
- **Tailwind IntelliSense** (extensão de editor): autocompletar de classes, visualização dos estilos e menos erros de digitação.
- Lista de classes e documentação: `tailwindcss.com/docs`.