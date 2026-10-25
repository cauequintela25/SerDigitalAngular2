# Semantic Versioning (SemVer)

## 1. O que é SemVer?

**Semantic Versioning (SemVer)** é um padrão de versionamento que utiliza números para identificar versões de um software e comunicar o impacto das alterações realizadas.

O formato padrão é:

```text
MAJOR.MINOR.PATCH
```

Exemplo:

```text
2.4.1
```

- **MAJOR:** alterações incompatíveis com versões anteriores.
- **MINOR:** novas funcionalidades compatíveis com versões anteriores.
- **PATCH:** correções compatíveis com a versão atual.

### Como funciona?

| Tipo | Exemplo | Quando utilizar |
|---|---|---|
| MAJOR | `1.0.0` → `2.0.0` | Quando uma alteração quebra a compatibilidade. |
| MINOR | `1.2.0` → `1.3.0` | Quando uma funcionalidade é adicionada sem quebrar a compatibilidade. |
| PATCH | `1.2.3` → `1.2.4` | Quando um bug é corrigido sem quebrar a compatibilidade. |

Ao incrementar uma parte da versão, as partes à direita voltam para zero.

Exemplos:

```text
1.2.3 → 1.2.4  # PATCH
1.2.3 → 1.3.0  # MINOR
1.2.3 → 2.0.0  # MAJOR
```

---

## 2. Como utilizar SemVer no GDS?

O GDS (General Design System) é um Design System que poderá fornecer tokens, componentes e padrões reutilizáveis para diferentes projetos.

Por isso, o versionamento é importante para identificar mudanças e ajudar os projetos consumidores a entender se uma atualização é segura ou se exige adaptações.

Uma estratégia possível é utilizar versões `0.x.x` durante o desenvolvimento experimental e estabelecer a versão `1.0.0` quando a primeira versão estável estiver pronta.

### Fase experimental — `0.x.x`

Antes da versão `1.0.0`, o projeto está em desenvolvimento inicial. A API pública pode mudar com maior frequência, e ainda não há garantia de estabilidade.

Exemplos:

| Versão | Possível finalidade |
|---|---|
| `0.1.0` | Estrutura inicial e primeiros tokens. |
| `0.2.0` | Adição dos primeiros componentes. |
| `0.3.0` | Implementação de componentes de formulário. |
| `0.4.0` | Expansão e refinamento dos componentes existentes. |
| `0.5.0` | Melhorias de acessibilidade e documentação. |
| `0.9.0` | Preparação para a primeira versão estável. |
| `0.10.0` | Novas funcionalidades antes da versão estável. |

Esses números são apenas um exemplo de planejamento. Você não precisa utilizar todas essas versões nem seguir uma sequência fixa.

Durante a fase `0.x.x`, você pode adicionar funcionalidades e fazer mudanças incompatíveis, mas é recomendável documentar as alterações que exigem adaptações.

**Importante:** a versão `0.4.0` não significa automaticamente que o projeto está 40% concluído. O número identifica uma versão, não uma porcentagem de progresso.

### Primeira versão estável — `1.0.0`

A versão `1.0.0` representa o marco em que você considera a API pública do GDS estável o suficiente para ser utilizada por outros projetos.

Antes de chegar a essa versão, procure garantir:

- [ ] Tokens de design organizados e documentados.
- [ ] Componentes principais implementados e testados.
- [ ] Padrões de nomenclatura consistentes.
- [ ] Acessibilidade considerada nos componentes.
- [ ] Documentação de instalação e utilização.
- [ ] Critérios claros para futuras mudanças incompatíveis.

A versão `1.0.0` não exige que absolutamente todos os componentes imaginados estejam prontos. O importante é definir um escopo inicial útil, funcional e estável.

**Publicação e deploy são conceitos diferentes:** você pode lançar a versão `1.0.0` como um pacote ou release e publicar a documentação em produção em uma etapa separada.

---

## 3. Como atualizar as versões do GDS?

Depois da versão `1.0.0`, utilize as regras do SemVer para decidir qual número incrementar.

### PATCH — Correções

Exemplo:

```text
1.0.0 → 1.0.1
```

Utilize quando corrigir um problema sem introduzir uma quebra de compatibilidade.

Exemplos no GDS:

- Corrigir o alinhamento de um botão.
- Corrigir um erro visual em um componente.
- Corrigir um token aplicado incorretamente, preservando o contrato público.

Commit relacionado:

```text
fix(button): corrige alinhamento do ícone
```

### MINOR — Novas funcionalidades

Exemplo:

```text
1.0.1 → 1.1.0
```

Utilize quando adicionar funcionalidades compatíveis com as anteriores.

Exemplos no GDS:

- Adicionar um novo componente de card.
- Criar novos tokens sem remover os existentes.
- Adicionar uma nova variante de botão sem alterar o comportamento das variantes anteriores.

Commit relacionado:

```text
feat(card): adiciona componente de card
```

### MAJOR — Mudanças incompatíveis

Exemplo:

```text
1.1.0 → 2.0.0
```

Utilize quando uma mudança incompatível exigir adaptações nos projetos que utilizam o GDS.

Exemplos:

- Renomear ou remover um token público utilizado pelos projetos.
- Alterar uma API pública de um componente de forma incompatível.
- Remover uma propriedade obrigatória ou mudar seu significado.

Commit relacionado:

```text
feat(button)!: altera a API pública do componente
```

Uma mudança incompatível também pode ser registrada com o rodapé `BREAKING CHANGE:`.

---

## 4. Como SemVer trabalha com Conventional Commits?

Os dois padrões possuem funções diferentes:

- **Conventional Commits:** padroniza as mensagens dos commits.
- **SemVer:** padroniza os números das versões.

Exemplo de histórico:

```text
feat(tokens): adiciona tokens de espaçamento
feat(card): adiciona componente de card
fix(button): corrige alinhamento do ícone
feat(button)!: altera a API pública do componente
```

Uma ferramenta de versionamento automático pode analisar esses commits e determinar a próxima versão, conforme suas regras de configuração.

Em um fluxo convencional após a versão `1.0.0`:

| Tipo de commit | Incremento típico |
|---|---|
| `fix:` | PATCH |
| `feat:` | MINOR |
| `feat!:` | MAJOR |
| `fix!:` | MAJOR |
| `docs:` | Normalmente não gera uma nova versão por si só |

Uma `BREAKING CHANGE` pode acompanhar qualquer tipo de commit. Ela indica que a mudança exige um incremento MAJOR, conforme as regras do Conventional Commits.

Durante a fase `0.x.x`, as regras de versionamento automático podem ser configuradas de maneira diferente, pois o projeto ainda não declara estabilidade.

---

## 5. Versões experimentais e pré-lançamentos

Além de `0.x.x`, o SemVer permite identificar versões de pré-lançamento usando um hífen.

Exemplos:

```text
1.0.0-alpha.1
1.0.0-beta.1
1.0.0-rc.1
1.0.0
```

- **alpha:** fase inicial de experimentação.
- **beta:** fase de testes e refinamento.
- **rc (Release Candidate):** versão candidata a lançamento, caso não sejam encontrados problemas relevantes.
- **versão sem sufixo:** versão estável, conforme a política de lançamento do projeto.

Uma versão de pré-lançamento possui precedência inferior à versão final correspondente. Por exemplo, `1.0.0-rc.1` vem antes de `1.0.0`.

Você pode usar essas identificações quando quiser testar uma versão candidata do GDS antes de disponibilizá-la como estável.

---

## 6. Boas práticas para o versionamento do GDS

1. Defina o que será considerado parte da API pública do Design System.
2. Mantenha `0.x.x` enquanto estiver experimentando mudanças estruturais e refinando os componentes.
3. Considere `1.0.0` quando a API pública inicial estiver documentada e estável.
4. Utilize PATCH para correções, MINOR para funcionalidades compatíveis e MAJOR para mudanças incompatíveis após `1.0.0`.
5. Registre mudanças importantes em um `CHANGELOG.md`.
6. Utilize tags Git para identificar versões publicadas, como `v1.0.0`.
7. Não confunda um commit com uma versão: vários commits podem compor uma única versão.
8. Não confunda uma versão com um deploy: uma versão pode existir sem estar implantada em produção.

### Exemplo de criação de uma tag

Depois de preparar a versão estável e registrar as alterações:

```bash
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

Esses comandos criam uma tag anotada e a enviam ao repositório remoto. Eles não publicam automaticamente um pacote nem fazem o deploy da documentação.

---

## 7. Resumo

| Fase | Exemplo | Objetivo |
|---|---|---|
| Desenvolvimento experimental | `0.1.0` até `0.9.x` | Construir, experimentar e refinar o GDS. |
| Pré-lançamento | `1.0.0-alpha.1` ou `1.0.0-rc.1` | Validar uma possível versão estável. |
| Primeira versão estável | `1.0.0` | Declarar estabilidade da API pública inicial. |
| Manutenção | `1.0.1`, `1.0.2` | Corrigir bugs. |
| Evolução compatível | `1.1.0`, `1.2.0` | Adicionar funcionalidades compatíveis. |
| Nova versão principal | `2.0.0` | Introduzir mudanças incompatíveis. |

**Regra para lembrar:**

- `0.x.x`: desenvolvimento inicial, com estabilidade ainda não garantida.
- `1.x.x`: API pública estável, conforme o compromisso do projeto.
- `PATCH`: correções.
- `MINOR`: funcionalidades compatíveis.
- `MAJOR`: mudanças incompatíveis.

Referências oficiais:

- [Semantic Versioning 2.0.0](https://semver.org/lang/pt-BR/)
- [Conventional Commits 1.0.0](https://www.conventionalcommits.org/pt-br/v1.0.0/)
