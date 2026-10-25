# Git Semantic — Escopos de Commits

## 1. O que são escopos?

Os escopos (*scopes*) identificam a área do projeto afetada por um commit semântico. Eles são opcionais e ajudam a tornar o histórico do Git mais organizado, legível e fácil de pesquisar.

**Estrutura:**

```text
<tipo>(<escopo>): <descrição>
```

**Exemplo:**

```text
feat(login): adiciona validação de formulário
fix(header): corrige alinhamento do menu
docs: atualiza documentação do projeto
```

> [!NOTE]
> Não existe uma lista universal obrigatória de escopos. Os nomes devem ser definidos conforme a arquitetura e as necessidades do projeto.

---

## 2. Escopos mais comuns

### 2.1. Front-end

| Escopo | Finalidade | Exemplo |
|---|---|---|
| `ui` | Interface visual | `feat(ui): adiciona tema escuro` |
| `layout` | Estrutura e disposição da página | `fix(layout): corrige espaçamento` |
| `header` | Cabeçalho | `feat(header): adiciona navegação` |
| `footer` | Rodapé | `fix(footer): corrige alinhamento` |
| `nav` | Navegação e menus | `feat(nav): adiciona menu lateral` |
| `routing` | Rotas e navegação entre páginas | `feat(routing): adiciona rota de perfil` |
| `styles` | Estilos CSS | `style(styles): ajusta tipografia` |
| `assets` | Imagens, ícones e recursos estáticos | `chore(assets): organiza ícones` |
| `forms` | Formulários | `feat(forms): adiciona validação` |
| `components` | Componentes reutilizáveis | `refactor(components): simplifica botão` |

### 2.2. Funcionalidades e páginas

| Escopo | Finalidade | Exemplo |
|---|---|---|
| `home` | Página inicial | `feat(home): adiciona seção de destaque` |
| `login` | Tela de login | `feat(login): adiciona campo de senha` |
| `auth` | Autenticação e autorização | `fix(auth): corrige validação do token` |
| `profile` | Perfil do usuário | `feat(profile): adiciona edição de dados` |
| `dashboard` | Painel principal | `feat(dashboard): adiciona resumo de métricas` |
| `settings` | Configurações | `feat(settings): adiciona preferências` |
| `search` | Pesquisa | `feat(search): adiciona filtros` |

### 2.3. Lógica e integração

| Escopo | Finalidade | Exemplo |
|---|---|---|
| `api` | Comunicação com APIs | `fix(api): trata resposta inválida` |
| `services` | Serviços da aplicação | `refactor(services): simplifica requisições` |
| `state` | Gerenciamento de estado | `fix(state): corrige atualização dos dados` |
| `models` | Modelos de dados | `refactor(models): ajusta tipos de usuário` |
| `validation` | Regras de validação | `fix(validation): corrige regra de e-mail` |
| `database` | Banco de dados | `feat(database): adiciona índice de usuários` |
| `auth` | Autenticação e autorização | `feat(auth): adiciona renovação de token` |

### 2.4. Infraestrutura e qualidade

| Escopo | Finalidade | Exemplo |
|---|---|---|
| `deps` | Dependências | `chore(deps): atualiza dependências` |
| `config` | Arquivos de configuração | `chore(config): ajusta configuração do TypeScript` |
| `build` | Processo de compilação | `build: ajusta compilação de produção` |
| `ci` | Integração contínua | `ci: adiciona verificação de testes` |
| `tests` | Testes automatizados | `test(login): adiciona testes de validação` |
| `docs` | Documentação | `docs: atualiza guia de instalação` |
| `types` | Tipos e interfaces | `refactor(types): organiza interfaces` |
| `security` | Segurança | `fix(security): corrige validação de permissões` |
| `performance` | Desempenho | `perf(api): reduz requisições duplicadas` |

---

## 3. Escopos recomendados para o projeto Angular

Para manter o histórico simples e consistente, comece com os seguintes escopos:

| Escopo | Finalidade |
|---|---|
| `components` | Componentes reutilizáveis |
| `layout` | Estrutura geral da aplicação |
| `routing` | Rotas da aplicação |
| `home` | Página inicial |
| `login` | Tela de login |
| `profile` | Perfil do usuário |
| `auth` | Autenticação |
| `api` | Comunicação com o backend |
| `styles` | CSS e estilos globais |
| `config` | Configurações |
| `deps` | Dependências |
| `tests` | Testes automatizados |

Essa lista é um ponto de partida. Adicione novos escopos quando houver uma necessidade real, como `dashboard`, `forms` ou `state`.

---

## 4. Boas práticas

### 4.1. Mantenha a consistência

Escolha nomes padronizados e utilize-os em todo o projeto.

```text
feat(styles): adiciona tokens de espaçamento
fix(styles): corrige contraste do botão
```

Evite alternar entre `styles`, `css` e `estilos` para representar a mesma área.

### 4.2. Evite escopos genéricos

Prefira nomes que indiquem claramente a área afetada.

```text
# Preferível
fix(header): corrige alinhamento do menu

# Evitar
fix(update): corrige alinhamento do menu
```

### 4.3. Não crie escopos desnecessários

O escopo é opcional. Se o tipo e a descrição já comunicam a alteração, não é necessário acrescentá-lo.

```text
docs: atualiza guia de instalação
chore: configura arquivos do projeto
```

### 4.4. Prefira domínios quando fizer sentido

Quando uma funcionalidade representa uma área de negócio, o escopo pode indicar esse domínio.

```text
feat(auth): adiciona renovação de token
feat(users): adiciona cadastro de usuários
feat(payments): adiciona validação de pagamento
```

### 4.5. Não confunda tipo com escopo

O **tipo** informa a natureza da alteração. O **escopo** identifica a área afetada.

```text
feat(login): adiciona formulário
fix(login): corrige validação
test(login): adiciona testes
docs(login): documenta autenticação
```

Nos exemplos, `feat`, `fix`, `test` e `docs` são tipos; `login` é o escopo.

---

## 5. Referência rápida

| Tipo | Significado |
|---|---|
| `feat` | Nova funcionalidade |
| `fix` | Correção de erro |
| `docs` | Documentação |
| `style` | Alterações de formatação que não modificam o significado do código |
| `refactor` | Reestruturação sem mudança intencional de comportamento |
| `test` | Testes |
| `build` | Build e ferramentas de compilação |
| `ci` | Integração contínua |
| `perf` | Melhoria de desempenho |
| `chore` | Tarefas de manutenção |
| `revert` | Reversão de uma alteração anterior |

> [!TIP]
> Os tipos seguem a convenção Conventional Commits. Os escopos são definidos pelo projeto e não precisam corresponder exatamente aos nomes das pastas do Angular.

---

## 6. Modelo de commit semântico

```text
<tipo>(<escopo opcional>): <descrição>

<corpo opcional>

<rodapé opcional>
```

**Exemplos:**

```text
feat(components): adiciona botão reutilizável
fix(login): corrige validação de formulário
refactor(layout): simplifica estrutura da página
test(auth): adiciona testes de autenticação
docs: atualiza documentação do projeto
chore(deps): atualiza dependências do Angular
```

## 7. Regra geral

- **Tipo:** o que mudou?
- **Escopo:** onde mudou?
- **Descrição:** qual foi a alteração?
- **Corpo:** por que a alteração foi necessária ou como funciona?
- **Rodapé:** existem referências ou mudanças incompatíveis?

**Objetivo:** criar um histórico de commits claro, consistente e fácil de manter durante a evolução do projeto.
