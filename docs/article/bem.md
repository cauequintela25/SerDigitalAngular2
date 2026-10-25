# BEM — Block, Element, Modifier

## 1. Objetivo

BEM é uma convenção de nomenclatura CSS que organiza as classes em três conceitos:

- **Block:** componente independente.
- **Element:** parte pertencente a um Block.
- **Modifier:** variação de um Block ou Element.

O objetivo é criar nomes previsíveis, facilitar a manutenção e permitir a reutilização dos estilos.

## 2. Block

O Block representa um componente independente da interface.

Exemplo:

```html
<article class="product-card">
  ...
</article>
```

```css
.product-card {
  padding: 1rem;
  border-radius: 0.5rem;
}
```

Outros exemplos de Blocks:

- `login-form`
- `product-card`
- `site-header`
- `user-profile`
- `primary-navigation`

Um Block deve representar uma unidade lógica da interface, sem depender da posição em que aparece na página.

## 3. Element

O Element representa uma parte pertencente a um Block.

A convenção utiliza dois sublinhados (`__`) entre o nome do Block e o nome do Element.

Exemplo:

```html
<article class="product-card">
  <img
    class="product-card__image"
    src="product.jpg"
    alt="Fone Bluetooth"
  >

  <div class="product-card__content">
    <h2 class="product-card__title">
      Fone Bluetooth
    </h2>

    <p class="product-card__description">
      Fone sem fio com cancelamento de ruído.
    </p>

    <span class="product-card__price">
      R$ 299,90
    </span>

    <button class="product-card__button">
      Comprar agora
    </button>
  </div>
</article>
```

Nomenclatura utilizada:

```text
product-card
├── product-card__image
├── product-card__content
├── product-card__title
├── product-card__description
├── product-card__price
└── product-card__button
```

### Regra importante

O nome do Element é associado diretamente ao Block, e não à profundidade da estrutura HTML.

Evite:

```css
.product-card__content__title {}
```

Prefira:

```css
.product-card__title {}
```

Mesmo quando o título está dentro de `product-card__content`, ele continua pertencendo logicamente ao Block `product-card`.

## 4. Modifier

O Modifier representa uma variação de aparência ou estado de um Block ou Element.

A convenção utiliza dois hífens (`--`).

Exemplo:

```html
<article class="product-card product-card--featured">
  ...
</article>
```

```css
.product-card--featured {
  border: 2px solid #7001fd;
}
```

O Modifier não substitui a classe original. As duas classes devem estar presentes para que o componente mantenha seus estilos básicos.

Outros exemplos:

```text
product-card
product-card--featured
product-card--compact

product-card__button
product-card__button--disabled
```

Exemplo de uso:

```html
<button
  class="product-card__button product-card__button--disabled"
  disabled
>
  Indisponível
</button>
```

## 5. Reutilização

O mesmo Block pode ser utilizado diversas vezes, com ou sem modificadores.

```html
<article class="product-card">
  ...
</article>

<article class="product-card">
  ...
</article>

<article class="product-card product-card--featured">
  ...
</article>
```

Isso permite reutilizar os estilos sem criar uma classe completamente nova para cada ocorrência do componente.

## 6. BEM em projetos Angular

No Angular, cada componente pode ter seu próprio conjunto de classes BEM.

Exemplo de estrutura:

```text
product-card/
├── product-card.ts
├── product-card.html
└── product-card.css
```

**`product-card.html`**

```html
<article class="product-card">
  <h2 class="product-card__title">
    Fone Bluetooth
  </h2>

  <button class="product-card__button">
    Comprar agora
  </button>
</article>
```

**`product-card.css`**

```css
.product-card {
  padding: 1rem;
}

.product-card__title {
  font-size: 1.25rem;
}

.product-card__button {
  padding: 0.75rem 1rem;
}

.product-card--featured {
  border: 2px solid #7001fd;
}
```

O BEM é uma convenção de nomenclatura, não um recurso exclusivo do Angular. Ele pode ser utilizado com os estilos encapsulados de um componente ou em folhas de estilo globais.

## 7. Regras de nomenclatura

| Conceito | Convenção | Exemplo |
|---|---|---|
| Block | `block` | `product-card` |
| Element | `block__element` | `product-card__title` |
| Modifier | `block--modifier` | `product-card--featured` |
| Element com Modifier | `block__element--modifier` | `product-card__button--disabled` |

### Boas práticas

- Utilize nomes descritivos e consistentes.
- Prefira nomes baseados na função do componente ou elemento.
- Não crie nomes de Elements com múltiplos níveis de `__`.
- Mantenha a classe original quando utilizar um Modifier.
- Evite depender da estrutura HTML para definir o nome das classes.
- Não crie uma nova classe apenas porque o componente aparece em outra página.

## 8. O que o BEM resolve?

O BEM responde à seguinte pergunta:

**Como nomear componentes, partes de componentes e suas variações em CSS?**

Ele não define, por si só, a ordem da cascata, a organização de camadas, a estratégia responsiva ou a arquitetura completa dos estilos.

Esses assuntos serão documentados separadamente.

## 9. Referência oficial

Documentação original do BEM:

https://getbem.com/introduction/

---

**Escopo deste documento:** somente BEM.

Não misturar, neste momento, Namespace, CUBE CSS, CSS Layers, Native CSS Nesting ou outras técnicas de arquitetura CSS.
