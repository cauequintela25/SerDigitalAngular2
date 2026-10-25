# Git Semantic — Estrutura de Commits

## 1. Estrutura recomendada

O padrão **Conventional Commits** define uma estrutura consistente para mensagens de commit:

```text
<tipo>(<escopo opcional>): <descrição>

<corpo opcional>

<rodapé opcional>
```

Cada parte possui uma finalidade específica e ajuda a manter o histórico do Git organizado e fácil de entender.

---

## 2. Cabeçalho (Header)

O cabeçalho é a primeira linha do commit. Ele contém o tipo, o escopo opcional e uma descrição curta da alteração.

### Estrutura

```text
tipo(escopo): descrição
```

- **Tipo:** indica a natureza da alteração, como `feat`, `fix` ou `docs`.
- **Escopo:** indica a área do projeto afetada, como `login`, `header` ou `auth`. É opcional.
- **Descrição:** resume o que foi feito de forma clara e objetiva.

### Exemplos

```text
feat(login): adiciona formulário de autenticação
fix(header): corrige alinhamento do menu
docs: atualiza guia de instalação
```

---

## 3. Corpo (Body) — Opcional

O corpo explica o motivo da alteração, o problema resolvido ou os detalhes que não cabem no cabeçalho.

### Exemplo

```text
feat(login): adiciona formulário de autenticação

Implementa os campos de e-mail e senha para permitir
que os usuários acessem a aplicação.
```

Utilize o corpo quando uma explicação adicional ajudar quem estiver lendo o histórico do projeto.

Commits simples geralmente não precisam de corpo.

---

## 4. Rodapé (Footer) — Opcional

O rodapé registra informações complementares, como referências a tarefas, issues e alterações incompatíveis com versões anteriores.

### Exemplo com referência a uma issue

```text
feat(login): adiciona validação de formulário

Adiciona validação dos campos de e-mail e senha
para impedir o envio de dados inválidos.

Refs: #42
```

### Exemplo de alteração incompatível (Breaking Change)

```text
feat(auth): altera contrato de autenticação

BREAKING CHANGE: o endpoint de login agora exige
o campo email em vez de username.
```

**`BREAKING CHANGE:`** indica que a alteração pode exigir adaptações no código existente ou nos sistemas que dependem dessa funcionalidade.

---

## 5. Exemplo completo

```text
feat(login): adiciona validação de formulário

Adiciona validação dos campos de e-mail e senha
para impedir o envio de dados inválidos.

Refs: #42
```

Nesse exemplo:

- **Cabeçalho:** `feat(login): adiciona validação de formulário`
- **Corpo:** explica o que a alteração implementa e por quê.
- **Rodapé:** referencia a issue `#42`.

---

## 6. Modelo para utilizar nos commits

Copie este modelo como referência:

```text
<tipo>(<escopo opcional>): <descrição>

<corpo opcional>

<rodapé opcional>
```

### Regras práticas

- Utilize o cabeçalho para resumir a alteração.
- Utilize o corpo para explicar o motivo ou os detalhes importantes.
- Utilize o rodapé para referências e informações especiais.
- Separe o cabeçalho, o corpo e o rodapé com linhas em branco quando essas seções forem utilizadas.
- Não adicione corpo ou rodapé desnecessariamente.
- Prefira mensagens claras, objetivas e escritas no presente.
- Utilize o escopo quando ele ajudar a identificar a área afetada.

---

## 7. Tipos comuns de Conventional Commits

| Tipo | Finalidade |
|---|---|
| `feat` | Adiciona uma funcionalidade. |
| `fix` | Corrige um erro. |
| `docs` | Altera a documentação. |
| `style` | Altera formatação sem modificar a lógica, como espaços ou ponto e vírgula. |
| `refactor` | Reestrutura o código sem alterar seu comportamento externo. |
| `test` | Adiciona ou modifica testes. |
| `build` | Altera o sistema de build ou dependências de build. |
| `ci` | Altera configurações de integração contínua. |
| `perf` | Melhora o desempenho. |
| `chore` | Realiza tarefas gerais de manutenção. |

---

**Referência:** [Conventional Commits](https://www.conventionalcommits.org/pt-br/v1.0.0/)
