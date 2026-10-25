# CUBE CSS — Composition, Utility, Block, Exception

## 1. Objetivo

CUBE CSS é uma abordagem de arquitetura CSS que organiza os estilos considerando quatro dimensões:

- **C — Composition:** organiza a relação entre os elementos.
- **U — Utility:** aplica pequenas regras específicas e reutilizáveis.
- **B — Block:** define os componentes e suas características visuais.
- **E — Exception:** representa alterações específicas em relação ao comportamento padrão.

O objetivo é criar uma arquitetura CSS flexível, reutilizável e fácil de manter, evitando que cada componente precise controlar sozinho todas as características de sua apresentação.

## 2. C — Composition

Composition define como os elementos se organizam e se relacionam dentro de um layout.

Seu papel é estabelecer regras estruturais, como direção, alinhamento, distribuição, espaçamento e organização dos elementos.

Exemplos:

```css
.l-stack {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.l-cluster {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 1rem;
}

.l-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1.5rem;
}
```

### Exemplo de utilização

```html
<section>
  <h1>Produtos</h1>

  <div class="l-grid">
    <article class="c-product-card">...</article>
    <article class="c-product-card">...</article>
    <article class="c-product-card">...</article>
  </div>
</section>
```

O layout `l-grid` não precisa conhecer os produtos. Ele apenas organiza seus elementos filhos em uma grade.

### Quando usar?

- Distribuir cards em uma grade.
- Organizar campos de um formulário verticalmente.
- Agrupar botões e ações.
- Posicionar conteúdo e sidebar.
- Organizar cabeçalhos e rodapés.
- Criar estruturas reutilizáveis para diferentes páginas.

### Regra importante

A Composition deve ser tão genérica quanto necessário para permitir a reutilização.

Evite incorporar nela regras visuais exclusivas de um componente, como a cor específica de um botão ou a sombra particular de um card.

## 3. U — Utility

Utility representa uma pequena regra CSS que executa uma tarefa específica.

Uma utility pode ser utilizada em diferentes componentes e contextos sem precisar criar uma variação específica para cada um.

Exemplos:

```css
.u-text-center {
  text-align: center;
}

.u-width-full {
  width: 100%;
}

.u-hidden {
  display: none;
}

.u-margin-auto {
  margin-inline: auto;
}
```

### Exemplo de utilização

```html
<button class="c-button u-width-full">
  Comprar agora
</button>
```

Nesse exemplo:

- `c-button`: representa o componente visual.
- `u-width-full`: faz o botão ocupar toda a largura disponível.

### Quando usar?

Quando uma característica pequena e reutilizável não precisa fazer parte da identidade permanente de um componente.

### Regra importante

Evite criar utilities que acumulam muitas responsabilidades ou representam componentes inteiros.

Uma utility deve ser pequena, previsível e fácil de compreender pelo nome.

## 4. B — Block

Block representa um componente ou uma unidade visual com identidade própria.

Exemplos:

```text
c-button
c-product-card
c-login-form
c-modal
c-alert
c-navigation
```

### Exemplo de utilização

```html
<article class="c-product-card">
  <img
    class="c-product-card__image"
    src="product.jpg"
    alt="Fone Bluetooth"
  >

  <h2 class="c-product-card__title">
    Fone Bluetooth
  </h2>

  <p class="c-product-card__description">
    Fone sem fio com cancelamento de ruído.
  </p>

  <span class="c-product-card__price">
    R$ 299,90
  </span>

  <button class="c-button">
    Comprar
  </button>
</article>
```

```css
.c-product-card {
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 0.75rem;
  background: white;
  color: #222;
}

.c-product-card__title {
  font-size: 1.25rem;
}

.c-product-card__price {
  font-size: 1.5rem;
  font-weight: 700;
}
```

O Block define as características visuais do componente. O BEM pode ser utilizado para nomear suas partes e variações.

### Quando usar?

Quando uma unidade da interface possui identidade visual própria e precisa ser reutilizada em diferentes partes da aplicação.

### Regra importante

Não faça o Block assumir sozinho todas as responsabilidades do layout externo.

Por exemplo, a distribuição de vários cards pode pertencer à Composition, enquanto a aparência de cada card pertence ao Block.

## 5. E — Exception

Exception representa uma alteração específica em relação às regras habituais de um elemento ou componente.

Uma exceção pode ser identificada por um Modifier, uma classe de estado ou um atributo HTML, dependendo da necessidade.

### Exemplo com Modifier BEM

```html
<article class="c-product-card c-product-card--featured">
  ...
</article>
```

```css
.c-product-card {
  border: 1px solid #ddd;
}

.c-product-card--featured {
  border: 2px solid #7001fd;
}
```

O componente mantém sua aparência básica, mas recebe uma variação visual específica.

### Exemplo com estado

```html
<button class="c-button is-disabled" disabled>
  Indisponível
</button>
```

```css
.c-button.is-disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Quando usar?

- Destacar um produto.
- Representar um estado visual específico.
- Alterar uma característica pontual em determinado contexto.
- Tratar uma necessidade que não deve se tornar a regra geral de todos os componentes.

### Regra importante

Antes de criar uma exceção, pergunte:

**Essa alteração é realmente específica ou deveria fazer parte do estilo padrão do componente?**

Se todos os cards precisam da mesma característica, provavelmente ela pertence ao Block, não a uma exceção.

## 6. Combinando as quatro dimensões

Imagine uma página de produtos:

```html
<section>
  <h1 class="u-text-center">Produtos</h1>

  <div class="l-grid">
    <article class="c-product-card">
      <div class="l-stack">
        <h2 class="c-product-card__title">
          Fone Bluetooth
        </h2>

        <p class="c-product-card__description">
          Cancelamento de ruído.
        </p>

        <button class="c-button u-width-full">
          Comprar
        </button>
      </div>
    </article>

    <article class="c-product-card c-product-card--featured">
      <div class="l-stack">
        <h2 class="c-product-card__title">
          Teclado Mecânico
        </h2>

        <p class="c-product-card__description">
          Switches mecânicos.
        </p>

        <button class="c-button u-width-full">
          Comprar
        </button>
      </div>
    </article>
  </div>
</section>
```

Identificando as responsabilidades:

```text
l-grid
└── Composition: organiza os cards

l-stack
└── Composition: organiza o conteúdo verticalmente

u-text-center
└── Utility: centraliza o texto

u-width-full
└── Utility: ocupa toda a largura disponível

c-product-card
└── Block: aparência do card

c-product-card__title
└── Element BEM: título do card

c-product-card--featured
└── Modifier BEM: variação visual do card
```

A mesma interface utiliza diferentes responsabilidades sem exigir que uma única classe faça tudo.

## 7. CUBE CSS em projetos Angular

O CUBE CSS pode ser aplicado em projetos Angular independentemente de você utilizar estilos globais ou estilos encapsulados por componente.

Exemplo de estrutura:

```text
src/
└── app/
    ├── components/
    │   └── product-card/
    │       ├── product-card.ts
    │       ├── product-card.html
    │       └── product-card.css
    └── ...
```

**`product-card.html`**

```html
<article class="c-product-card">
  <div class="l-stack">
    <h2 class="c-product-card__title">
      Fone Bluetooth
    </h2>

    <button class="c-button u-width-full">
      Comprar
    </button>
  </div>
</article>
```

**`product-card.css`**

```css
.c-product-card {
  padding: 1.5rem;
  border-radius: 0.75rem;
}

.c-product-card__title {
  font-size: 1.25rem;
}
```

As classes seguem a convenção de nomenclatura do projeto. A organização física dos arquivos CSS pode ser definida separadamente, de acordo com a estrutura do Angular.

### Observação sobre encapsulamento

No Angular, os estilos de um componente normalmente são encapsulados por padrão por meio do mecanismo `ViewEncapsulation.Emulated`.

Se um layout ou uma utility precisar ser reutilizado globalmente, defina seus estilos em uma folha global apropriada ou adote uma estratégia consistente para disponibilizá-los. Não presuma que uma classe declarada no CSS de um componente estará automaticamente disponível em todos os outros.

## 8. CUBE CSS, BEM e Namespace

Essas abordagens podem trabalhar juntas porque não possuem exatamente o mesmo objetivo.

| Abordagem | Pergunta principal |
|---|---|
| BEM | Como nomear Blocks, Elements e Modifiers? |
| Namespace | Qual é a responsabilidade da classe? |
| CUBE CSS | Como distribuir as responsabilidades dos estilos? |

Exemplo:

```html
<div class="l-grid">
  <article class="c-product-card c-product-card--featured">
    <h2 class="c-product-card__title">
      Fone Bluetooth
    </h2>

    <button class="c-button u-width-full">
      Comprar
    </button>
  </article>
</div>
```

Interpretação:

- `l-grid`: Namespace `l-` associado a uma Composition.
- `c-product-card`: Namespace `c-` associado a um Block.
- `c-product-card__title`: Element BEM pertencente ao Block.
- `c-product-card--featured`: Modifier BEM que representa uma variação.
- `u-width-full`: Namespace `u-` associado a uma Utility.

**Importante:** os quatro conceitos do CUBE são dimensões de uma abordagem CSS, não quatro prefixos obrigatórios. Um Block pode utilizar BEM, e uma Composition pode utilizar a convenção de Namespace escolhida pelo projeto.

## 9. Regras do projeto

- Utilize Composition para organizar a relação entre elementos.
- Utilize Utilities para pequenas regras reutilizáveis.
- Utilize Blocks para definir a identidade visual dos componentes.
- Utilize Exceptions para alterações específicas em relação ao padrão.
- Evite concentrar layout, identidade visual e todas as variações em uma única classe.
- Combine CUBE, BEM e Namespace de maneira consistente.
- Não crie uma exceção para uma característica que deveria ser padrão.
- Não confunda CUBE CSS com uma estrutura obrigatória de pastas ou arquivos.

## 10. Mapa mental

```text
CUBE CSS
│
├── C — Composition
│   └── Como os elementos se organizam?
│
├── U — Utility
│   └── Qual pequena regra preciso aplicar?
│
├── B — Block
│   └── Qual é o componente visual?
│
└── E — Exception
    └── O que precisa ser diferente do padrão?
```

## 11. Referências

- Piccalilli — CUBE CSS: https://piccalil.li/blog/cube-css/
- DPW — CUBE CSS: https://dpw.dev/css/cube-css/

---

**Escopo deste documento:** CUBE CSS e sua integração com BEM e Namespace.

CSS Layers, Native CSS Nesting, Design Tokens e estratégias responsivas serão documentados separadamente.
