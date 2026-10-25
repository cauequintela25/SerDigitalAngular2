# Namespace — CSS Naming Conventions

## 1. Objetivo

Namespace é uma convenção de nomenclatura que utiliza prefixos para identificar a responsabilidade de uma classe CSS.

Enquanto o BEM organiza os nomes em Blocks, Elements e Modifiers, o Namespace indica o papel que cada classe desempenha na aplicação.

Exemplo:

```html
<article class="c-product-card c-product-card--featured">
  ...
</article>
```

Nesse exemplo:

- `c-`: identifica um componente de interface.
- `product-card`: identifica o Block segundo o BEM.
- `--featured`: identifica uma variação do componente.

**BEM define a estrutura do nome; Namespace identifica a função da classe.**

## 2. Component — `c-`

O prefixo `c-` identifica um componente de interface com identidade visual e responsabilidade próprias.

Exemplos:

```text
c-button
c-card
c-modal
c-navbar
c-product-card
c-login-form
c-alert
```

### Exemplo

```html
<article class="c-product-card">
  <h2 class="c-product-card__title">
    Fone Bluetooth
  </h2>
</article>
```

```css
.c-product-card {
  padding: 1rem;
}

.c-product-card__title {
  font-size: 1.25rem;
}
```

### Quando usar?

Quando a classe representa um componente visual específico, como um botão, um card, um formulário ou um modal.

Evite utilizar `c-` para regras que representam apenas espaçamento, alinhamento ou outras pequenas responsabilidades genéricas.

## 3. Object — `o-`

O prefixo `o-` identifica estruturas reutilizáveis que organizam elementos sem representar necessariamente um componente visual específico.

Exemplos:

```text
o-grid
o-media
o-list
o-layout
```

### Exemplo

```html
<div class="o-grid">
  <article class="c-product-card">...</article>
  <article class="c-product-card">...</article>
  <article class="c-product-card">...</article>
</div>
```

```css
.o-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1.5rem;
}
```

O mesmo objeto pode organizar produtos, usuários, artigos ou outros conteúdos.

### Object vs. Component

- `o-grid`: organiza elementos em uma estrutura.
- `c-product-card`: representa um componente visual específico.

O objeto cuida da organização reutilizável; o componente cuida da sua própria identidade e apresentação.

## 4. Utility — `u-`

O prefixo `u-` identifica uma classe utilitária que executa uma tarefa pequena e específica.

Exemplos:

```text
u-hidden
u-text-center
u-width-full
u-margin-auto
```

### Exemplo

```html
<button class="c-button u-width-full">
  Entrar
</button>
```

```css
.u-width-full {
  width: 100%;
}
```

O componente define o que o elemento representa. A utility acrescenta uma característica pontual.

### Quando usar?

Quando uma regra pequena pode ser reutilizada em diferentes componentes sem precisar criar um novo componente ou modificar o estilo interno de cada um.

Evite transformar utilities em conjuntos grandes de regras que assumam a responsabilidade de componentes inteiros.

## 5. Layout — `l-`

O prefixo `l-` identifica classes responsáveis pela estrutura e pelo posicionamento de regiões da interface.

Exemplos:

```text
l-header
l-main
l-footer
l-sidebar
l-stack
l-cluster
l-switcher
l-grid
l-center
```

### Exemplo

```html
<div class="l-stack">
  <h1>Entrar na conta</h1>
  <p>Informe seus dados de acesso.</p>
  <form class="c-login-form">
    ...
  </form>
</div>
```

```css
.l-stack {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
```

### Layout vs. Object

Os conceitos podem se sobrepor dependendo da convenção adotada.

Para este projeto, utilize:

- `l-` para estruturas de layout identificadas pela sua responsabilidade no posicionamento da interface.
- `o-` para padrões estruturais genéricos e reutilizáveis.

O importante é manter uma regra consistente em todos os projetos.

## 6. State — `is-`

O prefixo `is-` identifica um estado atual de um elemento ou componente.

Exemplos:

```text
is-active
is-open
is-disabled
is-loading
is-selected
is-expanded
```

### Exemplo

```html
<button class="c-button is-loading" disabled>
  Entrando...
</button>
```

```css
.c-button.is-loading {
  cursor: progress;
  opacity: 0.7;
}
```

Um estado pode ser aplicado ou removido conforme o comportamento da interface.

### State vs. Modifier

Compare:

```text
c-button--primary
is-loading
```

- `c-button--primary`: variação definida para o componente.
- `is-loading`: estado atual do componente.

Um Modifier também pode representar estados ou condições em determinadas convenções BEM. Nesta arquitetura, prefira `is-` para estados dinâmicos e `--` para variações nomeadas do componente.

## 7. Condition — `has-`

O prefixo `has-` comunica a presença de uma característica ou condição relevante.

Exemplos:

```text
has-icon
has-error
has-discount
has-sidebar
has-image
```

### Exemplo

```html
<article class="c-product-card has-discount">
  ...
</article>
```

A leitura é: o componente possui desconto.

O prefixo pode ser utilizado quando essa condição precisa ser representada explicitamente por uma classe.

Não o utilize como substituto automático de `is-`.

- `is-disabled`: está desabilitado.
- `has-discount`: possui desconto.

Nem toda condição precisa de uma classe. Quando possível, prefira representar características com a estrutura HTML e os dados do componente, utilizando classes somente quando forem úteis para o estilo ou comportamento.

## 8. JavaScript — `js-`

O prefixo `js-` identifica um ponto de referência destinado ao comportamento JavaScript, sem representar uma decisão visual.

Exemplo em HTML tradicional:

```html
<button class="c-button js-add-cart">
  Comprar
</button>
```

```javascript
document.querySelectorAll('.js-add-cart');
```

Separar o gancho de comportamento da classe visual evita que alterações de estilo quebrem seletores de JavaScript.

### Uso em Angular

Em componentes Angular, prefira os mecanismos nativos do framework para eventos e estado.

```html
<button class="c-button" (click)="addToCart()">
  Comprar
</button>
```

```typescript
addToCart(): void {
  // Adiciona o produto ao carrinho.
}
```

Não é necessário adicionar `js-` quando o Angular já conecta o evento diretamente ao método do componente.

Reserve esse prefixo para situações em que um gancho de seleção por classe seja realmente necessário.

## 9. Quality Assurance — `qa-`

O prefixo `qa-` identifica seletores destinados a testes automatizados.

Exemplo:

```html
<button class="c-button" qa-add-cart>
  Comprar
</button>
```

Um teste automatizado pode localizar o botão por esse atributo.

### Recomendação para Angular

Para projetos Angular, considere também utilizar atributos de teste padronizados, como `data-testid`:

```html
<button
  class="c-button"
  data-testid="add-cart"
>
  Comprar
</button>
```

O teste pode localizar o elemento pelo identificador de teste, sem depender das classes CSS.

Não utilize seletores de teste para definir aparência visual.

## 10. Theme — `t-`

O prefixo `t-` identifica uma classe que representa um tema ou contexto visual.

Exemplos:

```text
t-light
t-dark
t-high-contrast
t-brand
```

### Exemplo

```html
<body class="t-dark">
  ...
</body>
```

```css
.t-dark {
  color-scheme: dark;
}
```

Em aplicações Angular, um tema também pode ser aplicado a um elemento raiz da aplicação ou a uma região específica da interface.

Utilize o tema para identificar um contexto visual abrangente, não para nomear componentes individuais.

## 11. Scope — `s-`

O prefixo `s-` identifica uma classe utilizada para delimitar um contexto no qual determinadas regras CSS se aplicam.

Exemplo:

```html
<section class="s-article">
  <h2>Documentação</h2>
  <p>Conteúdo da documentação.</p>
</section>
```

```css
.s-article h2 {
  font-size: 1.5rem;
}

.s-article p {
  line-height: 1.7;
}
```

O escopo indica que essas regras estão relacionadas ao contexto de conteúdo do artigo.

### Quando usar?

Quando um conjunto de regras precisa ser associado a uma região específica, como conteúdo editorial, texto rico ou conteúdo incorporado.

Não confunda `s-` com o encapsulamento de estilos do Angular. O namespace identifica uma convenção de classe; o Angular possui seus próprios mecanismos de encapsulamento.

## 12. Combinando Namespace e BEM

Os dois padrões podem coexistir na mesma classe.

Exemplo:

```html
<article class="c-product-card c-product-card--featured">
  <h2 class="c-product-card__title">
    Fone Bluetooth
  </h2>

  <button class="c-button c-button--primary u-width-full">
    Comprar
  </button>
</article>
```

Interpretação:

```text
c-product-card
├── c-                 → Component
├── product-card       → Block BEM
└── __title             → Element BEM

c-product-card--featured
├── c-                 → Component
└── --featured         → Modifier BEM

c-button--primary
├── c-                 → Component
└── --primary          → Modifier BEM

u-width-full
└── u-                 → Utility
```

Cada convenção resolve um problema diferente, sem precisar competir com a outra.

## 13. Referência rápida

| Namespace | Responsabilidade | Exemplo |
|---|---|---|
| `c-` | Componente de interface | `c-button` |
| `o-` | Objeto estrutural reutilizável | `o-grid` |
| `u-` | Regra utilitária | `u-hidden` |
| `l-` | Layout e posicionamento | `l-sidebar` |
| `is-` | Estado atual | `is-active` |
| `has-` | Presença de característica | `has-discount` |
| `js-` | Gancho para JavaScript | `js-add-cart` |
| `qa-` | Gancho para testes | `qa-add-cart` |
| `t-` | Tema visual | `t-dark` |
| `s-` | Contexto ou escopo | `s-article` |

## 14. Regras do projeto

- Utilize prefixos de forma consistente.
- Combine Namespace com BEM quando isso tornar a responsabilidade mais clara.
- Não crie namespaces novos sem uma necessidade concreta.
- Não utilize classes de apresentação como seletores de teste ou comportamento.
- Prefira eventos e estado do Angular para comportamentos internos dos componentes.
- Utilize `data-testid` quando um identificador de teste explícito for necessário.
- Não confunda Namespace com uma arquitetura CSS completa.

## 15. Referências

- Andrey Berry — BEM, CSS Namespaces and ITCSS: https://dev.to/andberry/bem-css-namespaces-and-itcss-4lp9
- Harry Roberts — More Transparent UI Code with Namespaces: https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/

---

**Escopo deste documento:** convenções de Namespace e sua combinação com BEM.

CUBE CSS, CSS Layers, Native CSS Nesting, Design Tokens e estratégias responsivas serão documentados separadamente.
