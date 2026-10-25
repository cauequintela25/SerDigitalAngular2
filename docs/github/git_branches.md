# Git Branches — Convenções e Organização

## 2. O que são branches semânticas?

Branches semânticas são branches nomeadas de acordo com sua finalidade. O nome indica o tipo de trabalho que será realizado, facilitando a identificação e a organização do desenvolvimento.

Não existe uma especificação universal obrigatória para os nomes das branches. A equipe pode definir suas próprias convenções.

### Estrutura recomendada

```text
<tipo>/<descricao>
```

Exemplos:

```text
feat/design-tokens
fix/button-alignment
docs/installation-guide
chore/project-structure
```

O tipo identifica a finalidade da branch, enquanto a descrição informa o trabalho que será realizado.

---

## 3. Tipos de branches

### 3.1. `main` — Branch principal

Contém a versão estável do projeto, validada e pronta para publicação.

- **Tipo:** permanente.
- **Finalidade:** manter o histórico oficial e as versões estáveis do projeto.

Exemplo:

```text
main
```

### 3.2. `develop` — Desenvolvimento integrado

Reúne funcionalidades em desenvolvimento antes de serem integradas à branch principal.

- **Tipo:** permanente, se necessário.
- **Finalidade:** integrar e validar alterações antes de publicá-las.

Exemplo:

```text
develop
```

A branch `develop` é comum no Git Flow, mas não é obrigatória em todos os projetos.

### 3.3. `feat/` ou `feature/` — Funcionalidades

Utilizada para desenvolver novas funcionalidades de maneira isolada.

Exemplos:

```text
feat/design-tokens
feature/button-component
feature/color-palette
```

### 3.4. `fix/` ou `bugfix/` — Correções

Utilizada para corrigir problemas que não exigem uma intervenção urgente em produção.

Exemplos:

```text
fix/button-alignment
bugfix/login-validation
```

### 3.5. `hotfix/` — Correções urgentes

Utilizada para corrigir problemas críticos em uma versão publicada.

Normalmente, a branch parte de `main`, e a correção também é integrada à linha de desenvolvimento futuro, quando aplicável.

Exemplos:

```text
hotfix/critical-token-error
hotfix/security-vulnerability
```

### 3.6. `release/` — Preparação de versões

Utilizada para preparar uma versão para lançamento, permitindo testes finais, correções e ajustes de documentação.

Exemplos:

```text
release/0.4.0
release/1.0.0
```

É mais comum em fluxos como o Git Flow. Projetos menores podem publicar diretamente a partir de `main`, sem manter branches de release.

### 3.7. `exp/` ou `experiment/` — Experimentação

Utilizada para testar ideias, arquiteturas ou componentes que ainda não estão prontos para integrar ao projeto.

Exemplos:

```text
exp/new-token-architecture
experiment/css-layer-strategy
```

### 3.8. `chore/` — Manutenção

Utilizada para tarefas de configuração, dependências e organização que não representam diretamente novas funcionalidades.

Exemplos:

```text
chore/project-structure
chore/update-dependencies
```

### 3.9. `docs/` — Documentação

Utilizada para alterações na documentação técnica do projeto.

Exemplos:

```text
docs/semantic-versioning-guide
docs/installation-guide
```

### 3.10. `test/` — Testes

Utilizada para implementar, corrigir ou organizar testes automatizados.

Exemplos:

```text
test/button-accessibility
test/token-validation
```

---

## 4. Branches `beta`, `alpha`, `exp` e `staging`

Esses nomes também podem ser utilizados, mas possuem finalidades diferentes.

| Nome       | Finalidade | Recomendação |
|------------|---|---|
| `beta`     | Manter uma linha de desenvolvimento para testes beta. | Utilize somente se precisar de uma linha beta contínua. |
| `alpha`    | Manter uma linha de experimentação inicial. | Geralmente, uma branch temporária é suficiente. |
| `exp`      | Abreviação informal de experimentação. | Prefira `exp/` ou `experiment/` para maior clareza. |
| `staging`  | Preparar ou validar uma versão antes da produção. | Utilize quando seu fluxo de deploy precisar dessa etapa. |
| `support/` | Manter versões antigas que ainda recebem correções. | Útil quando há suporte a múltiplas versões. |

### Alternativa para versões beta

Não é necessário criar uma branch permanente chamada `beta` apenas para publicar versões de teste.

Você pode utilizar pré-lançamentos SemVer, como:

```text
0.4.0-alpha.1
0.4.0-beta.1
1.0.0-rc.1
1.0.0
```

Esses identificadores distinguem versões experimentais, beta, candidatas a lançamento e estáveis.

---

## 5. Estrutura recomendada para o GDS

Como o General Design System está em desenvolvimento inicial e possui um único desenvolvedor, é recomendável começar com uma estrutura simples.

### Branches permanentes

| Branch | Responsabilidade |
|---|---|
| `main` | Manter a versão estável e as releases oficiais. |
| `develop` | Integrar alterações antes da publicação, caso essa separação seja necessária. |

A branch `develop` é opcional. Você pode trabalhar apenas com `main` e branches temporárias enquanto o projeto for pequeno.

### Branches temporárias

| Prefixo | Utilização | Exemplo |
|---|---|---|
| `feat/` | Novas funcionalidades | `feat/design-tokens` |
| `fix/` | Correções | `fix/button-alignment` |
| `docs/` | Documentação | `docs/installation-guide` |
| `chore/` | Manutenção | `chore/project-structure` |
| `exp/` | Experimentação | `exp/new-color-system` |
| `test/` | Testes | `test/button-accessibility` |
| `refactor/` | Reestruturação do código | `refactor/token-architecture` |

As branches temporárias devem ser integradas à branch de destino após a conclusão do trabalho e podem ser excluídas depois da integração.

---

## 6. Como criar e utilizar uma branch?

Exemplo: desenvolver os tokens de design do GDS.

### 6.1. Atualizar a branch principal

```bash
git switch main
git pull origin main
```

### 6.2. Criar a branch de funcionalidade

```bash
git switch -c feat/design-tokens
```

O comando cria a branch e muda para ela.

### 6.3. Registrar as alterações

```bash
git add .
git commit -m "feat(tokens): adiciona tokens iniciais"
```

### 6.4. Enviar a branch para o GitHub

```bash
git push -u origin feat/design-tokens
```

### 6.5. Integrar as alterações

Abra um Pull Request no GitHub para integrar a branch em `main` ou em `develop`, caso você utilize essa branch intermediária.

Após a integração, a branch temporária poderá ser excluída.

---

## 7. Boas práticas

- Utilize nomes curtos, claros e descritivos.
- Escolha um padrão de nomenclatura e mantenha a consistência.
- Prefira letras minúsculas e hífens para separar palavras.
- Crie branches temporárias para tarefas específicas.
- Evite manter branches permanentes que não possuem uma finalidade clara.
- Mantenha `main` estável de acordo com a política do projeto.
- Utilize Pull Requests quando quiser revisar ou validar as alterações antes da integração.
- Não confunda o nome da branch com a mensagem do commit: são convenções diferentes.

### Diferença entre branch e commit

Branch:

```text
feat/design-tokens
```

Commit:

```text
feat(tokens): adiciona tokens iniciais
```

A branch identifica a linha de trabalho. O commit descreve uma alteração específica registrada no histórico.

---

## 8. Resumo

Para o GDS, comece com:

- `main` — versão estável.
- `feat/` — novas funcionalidades.
- `fix/` — correções.
- `docs/` — documentação.
- `chore/` — manutenção.
- `exp/` — experimentação.
- `test/` — testes.
- `refactor/` — reestruturação do código.

Adicione `develop`, `release/`, `beta` ou `staging` somente quando o fluxo de desenvolvimento e publicação justificar essa complexidade.

**Referências:**

- [Git — documentação oficial](https://git-scm.com/docs)
- [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow)
- [Conventional Commits](https://www.conventionalcommits.org/pt-br/v1.0.0/)
- [Semantic Versioning](https://semver.org/lang/pt-BR/)
