# Git Fundamentos — Guia de Comandos

> [!info] Objetivo
> Guia de referência dos principais comandos Git para versionamento, commits, branches, repositórios remotos, recuperação de arquivos, stash e tags.
>
> **Legenda:** 🟢 Uso comum · 🟡 Atenção · 🔴 Comando destrutivo

## 1. Fundamentos do Git

### `git init`

**O que faz:** inicializa um repositório Git na pasta atual.

**Sintaxe:**

```bash
git init
```

**Exemplo prático:**

```bash
mkdir meu-projeto
cd meu-projeto
git init
```

A partir desse momento, o Git passa a acompanhar o histórico do projeto por meio do repositório local.

### `git status`

**O que faz:** mostra o estado atual do repositório, incluindo arquivos modificados, novos arquivos e alterações preparadas para commit.

```bash
git status
```

**Exemplo prático:**

Você alterou `index.html` e criou `style.css`. Execute:

```bash
git status
```

O Git mostrará quais arquivos estão modificados ou ainda não são rastreados.

**Boa prática:** execute `git status` antes de preparar alterações e antes de fazer um commit.

### `git --help`

**O que faz:** exibe a ajuda geral do Git.

```bash
git --help
```

Para consultar a documentação de um comando específico:

```bash
git commit --help
git branch --help
git push --help
```

### `git log`

**O que faz:** exibe o histórico de commits do repositório.

```bash
git log
```

**Exemplo prático:**

```bash
git log --oneline
```

Mostra uma versão resumida do histórico, com o identificador e a mensagem de cada commit.

Para visualizar o histórico com todas as branches:

```bash
git log --oneline --graph --decorate --all
```

---

## 2. Adicionar arquivos e criar commits

### `git add .`

**O que faz:** prepara as alterações dos arquivos do diretório atual e de seus subdiretórios para o próximo commit.

```bash
git add .
```

**Exemplo prático:**

Você criou `index.html` e `CSS/style.css` e quer preparar os dois arquivos:

```bash
git add .
git status
```

O `git status` mostrará as alterações preparadas para o commit.

> [!important] Atenção
> `git add .` não cria um commit. Ele prepara as alterações na *staging area* (área de preparação).

Para preparar somente um arquivo:

```bash
git add index.html
```

### `git commit -m`

**O que faz:** registra as alterações preparadas em um novo commit.

```bash
git commit -m "mensagem do commit"
```

**Exemplo prático:**

```bash
git add .
git commit -m "feat: adiciona estrutura HTML inicial"
```

Nesse exemplo, `feat` indica uma nova funcionalidade, seguindo uma convenção de commits semânticos.

**Fluxo recomendado:**

```bash
git status
git add .
git status
git commit -m "feat: adiciona estrutura HTML inicial"
```

### `git commit -a -m`

**O que faz:** prepara automaticamente alterações e exclusões em arquivos já rastreados pelo Git e cria um commit.

```bash
git commit -a -m "mensagem do commit"
```

**Exemplo prático:**

```bash
git commit -a -m "style: ajusta estilos da página inicial"
```

**Limitação importante:** arquivos novos e ainda não rastreados não são incluídos. Para incluí-los, utilize `git add`.

### `git commit index.html -m`

**O que faz:** cria um commit considerando as alterações do arquivo especificado, sem exigir que você execute `git add index.html` antes.

```bash
git commit index.html -m "mensagem do commit"
```

**Exemplo prático:**

```bash
git commit index.html -m "feat: adiciona estrutura HTML"
```

**Recomendação:** para aprender e manter o fluxo mais previsível, prefira separar as etapas:

```bash
git add index.html
git commit -m "feat: adiciona estrutura HTML"
```

Assim, fica mais fácil revisar o que será registrado.

---

## 3. Configurar a branch principal

### `git branch -M main`

**O que faz:** renomeia a branch atual para `main`. A opção `-M` permite forçar a renomeação caso exista uma branch com esse nome.

```bash
git branch -M main
```

**Exemplo prático:**

Depois de inicializar um repositório local:

```bash
git init
git branch -M main
```

A branch atual passa a se chamar `main`.

> [!note]
> Esse comando renomeia a branch atual. Ele não cria um repositório remoto nem envia arquivos para o GitHub.

---

## 4. Conectar ao GitHub e enviar código

### `git remote add origin`

**O que faz:** adiciona um repositório remoto com o nome `origin`.

```bash
git remote add origin URL_DO_REPOSITORIO
```

**Exemplo prático com SSH:**

```bash
git remote add origin git@github.com:USUARIO/REPOSITORIO.git
```

**Exemplo prático com HTTPS:**

```bash
git remote add origin https://github.com/USUARIO/REPOSITORIO.git
```

Substitua os valores de exemplo pelos dados do seu repositório.

Para verificar o endereço configurado:

```bash
git remote -v
```

### `git push -u origin main`

**O que faz:** envia a branch local `main` para o remoto `origin` e configura a relação de acompanhamento entre as branches.

```bash
git push -u origin main
```

**Exemplo prático:**

Depois de criar o primeiro commit e conectar o repositório:

```bash
git push -u origin main
```

Nas próximas vezes, normalmente você poderá usar apenas:

```bash
git push
```

### `git push`

**O que faz:** envia os commits locais para o repositório remoto, usando a configuração de acompanhamento da branch atual.

```bash
git push
```

**Exemplo prático:**

```bash
git add .
git commit -m "feat: adiciona página de login"
git push
```

### `git pull`

**O que faz:** busca as atualizações do remoto e integra essas alterações à branch local atual.

```bash
git pull
```

**Exemplo prático:**

Outra pessoa atualizou o repositório no GitHub:

```bash
git pull
```

O Git tentará integrar as atualizações à sua branch atual. Podem ocorrer conflitos se as alterações forem incompatíveis.

### `git clone`

**O que faz:** copia um repositório remoto para uma nova pasta local, incluindo seu histórico Git.

```bash
git clone URL_DO_REPOSITORIO
```

**Exemplo prático:**

```bash
git clone https://github.com/USUARIO/REPOSITORIO.git
cd REPOSITORIO
```

Use esse comando quando quiser baixar um projeto existente para trabalhar nele.

---

## 5. Remover, renomear e restaurar arquivos

### `git rm`

**O que faz:** remove um arquivo do diretório de trabalho e prepara sua exclusão para o próximo commit.

```bash
git rm arquivo
```

**Exemplo prático:**

```bash
git rm house2.html
git commit -m "refactor: remove arquivo HTML obsoleto"
```

A exclusão só passa a fazer parte do histórico quando você cria o commit.

### `git mv`

**O que faz:** renomeia ou move um arquivo e prepara essa alteração para o próximo commit.

```bash
git mv arquivo-antigo arquivo-novo
```

**Exemplo prático:**

```bash
git mv text2.txt newtext.txt
git commit -m "refactor: renomeia arquivo de texto"
```

O Git detecta renomeações ao analisar o histórico; elas não são armazenadas como um tipo separado de objeto.

### `git checkout .\CSS\style.css`

**O que faz:** na sintaxe antiga, `git checkout` seguido de um caminho pode restaurar um arquivo a partir do índice, descartando suas alterações não preparadas.

No Windows PowerShell, a forma moderna e mais clara é:

```bash
git restore CSS/style.css
```

**Exemplo prático:**

Você modificou `CSS/style.css`, mas quer descartar as alterações locais ainda não preparadas:

```bash
git restore CSS/style.css
```

> [!danger] Cuidado
> O comando descarta as modificações não preparadas desse arquivo. Se quiser preservá-las, faça um commit ou use `git stash` antes.

Para restaurar um arquivo ao estado preparado no índice, quando houver alterações preparadas:

```bash
git restore --staged CSS/style.css
```

Esse segundo comando retira as alterações da staging area, mas mantém o conteúdo modificado no arquivo.

### `git reset --hard origin/main`

**O que faz:** move a branch atual para o commit apontado por `origin/main` e redefine o índice e os arquivos rastreados para esse estado.

```bash
git fetch origin
git reset --hard origin/main
```

**Exemplo prático:**

Você quer que sua branch local atual corresponda exatamente à versão remota `origin/main`.

> [!danger] Risco de perda de código
> Esse comando pode apagar alterações locais não commitadas, inclusive alterações que estavam preparadas. Commits locais que não estejam no histórico de destino também podem deixar de ser alcançáveis pela branch.
>
> Antes de utilizá-lo, confira:
>
> ```bash
> git status
> git log --oneline --decorate -10
> ```
>
> Se necessário, crie uma branch de segurança ou faça um backup. Só execute o `reset --hard` quando tiver certeza de que deseja descartar as alterações locais.

---

## 6. Git Branch — trabalhar com branches

Uma **branch** é uma linha de desenvolvimento que permite trabalhar em mudanças sem precisar realizá-las diretamente na branch principal.

### `git branch`

**O que faz:** lista as branches locais. A branch atual aparece marcada com `*`.

```bash
git branch
```

Para listar também as branches remotas:

```bash
git branch -a
```

### `git branch primeiro_branch`

**O que faz:** cria uma branch local com o nome informado, mas não muda para ela.

```bash
git branch primeiro_branch
```

**Exemplo prático:**

```bash
git branch feature/footer
git branch
```

A branch é criada a partir do commit em que você está atualmente.

### `git branch -d primeiro_branch`

**O que faz:** exclui uma branch local quando o Git considera que suas alterações já foram integradas.

```bash
git branch -d primeiro_branch
```

**Exemplo prático:**

```bash
git switch main
git branch -d feature/footer
```

A branch deve estar desativada para ser excluída.

A opção `-D` força a exclusão, mesmo quando há alterações não integradas:

```bash
git branch -D feature/footer
```

Use `-D` somente quando tiver certeza de que não precisa preservar o trabalho daquela branch.

### `git checkout footer_home`

**O que faz:** troca para uma branch existente chamada `footer_home`.

```bash
git checkout footer_home
```

**Forma moderna equivalente:**

```bash
git switch footer_home
```

### `git checkout -b teste_criacao2`

**O que faz:** cria uma nova branch e muda para ela imediatamente.

```bash
git checkout -b teste_criacao2
```

**Forma moderna equivalente:**

```bash
git switch -c teste_criacao2
```

**Exemplo prático:**

```bash
git switch main
git switch -c feature/footer
```

A nova branch começa no commit em que `main` está naquele momento.

> [!important] Atenção ao ponto de partida
> Uma branch nova não copia automaticamente outra branch pelo nome. Ela começa a partir do commit da branch atual.
>
> Se você executar `git switch -c teste_criacao2` enquanto estiver na branch `teste_criacao`, a nova branch partirá do commit atual de `teste_criacao`.
>
> Se quiser criar uma branch a partir de `main`, primeiro troque para `main` ou informe explicitamente o ponto de partida:
>
> ```bash
> git switch -c feature/footer main
> ```

### `git merge teste_criacao`

**O que faz:** integra os commits da branch `teste_criacao` à branch atual.

```bash
git merge teste_criacao
```

**Exemplo prático:**

Você terminou uma funcionalidade e deseja integrá-la à branch principal:

```bash
git switch main
git merge teste_criacao
```

Atenção: o `merge` sempre atua sobre a branch atual. Se houver conflitos, resolva-os e conclua o processo de integração.

**Fluxo resumido de uma funcionalidade:**

```bash
git switch main
git switch -c feature/login

# Desenvolva a funcionalidade
git add .
git commit -m "feat: adiciona formulário de login"

# Integre a funcionalidade
git switch main
git merge feature/login
```

---

## 7. Git Stash — guardar alterações temporariamente

O `stash` permite guardar temporariamente alterações locais sem criar um commit. É útil quando você precisa trocar de branch antes de terminar o trabalho atual.

### `git stash`

**O que faz:** guarda alterações locais temporariamente e limpa essas alterações do diretório de trabalho. Por padrão, inclui modificações em arquivos rastreados; arquivos novos não rastreados não são incluídos.

```bash
git stash
```

**Exemplo prático:**

Você começou a modificar a página de login, mas precisa corrigir um erro urgente em outra branch:

```bash
git stash
git switch main
```

Para incluir também arquivos novos não rastreados:

```bash
git stash -u
```

### `git stash list`

**O que faz:** lista as alterações guardadas no stash.

```bash
git stash list
```

Exemplo de saída:

```text
stash@{0}: WIP on feature/login: ...
stash@{1}: WIP on main: ...
```

### `git stash show -p`

**O que faz:** mostra as diferenças detalhadas de um stash.

```bash
git stash show -p
```

Para consultar um stash específico:

```bash
git stash show -p "stash@{0}"
```

### `git stash pop`

**O que faz:** reaplica as alterações guardadas mais recentes e remove essa entrada do stash se a aplicação for concluída com sucesso.

```bash
git stash pop
```

**Exemplo prático:**

```bash
git stash
git switch main

# Resolva o trabalho urgente

git switch feature/login
git stash pop
```

### `git stash apply`

**O que faz:** reaplica as alterações de um stash, mas mantém a entrada guardada na lista.

```bash
git stash apply
```

Use essa opção quando quiser reaplicar as alterações sem remover o backup temporário.

### `git stash clear`

**O que faz:** remove todas as entradas do stash.

```bash
git stash clear
```

> [!danger] Cuidado
> A remoção de todas as entradas pode tornar difícil ou impossível recuperar as alterações guardadas. Confira `git stash list` antes de executar.

---

## 8. Git Tag — marcar versões e checkpoints

Uma **tag** identifica um commit específico, normalmente para marcar versões ou releases, como `v1.0.0` e `v2.0.0`.

Diferentemente do stash, uma tag não guarda alterações locais não commitadas. Ela marca um commit já existente.

### `git tag -a nome -m "mensagem"`

**O que faz:** cria uma tag anotada, associada a um commit, com mensagem e metadados.

```bash
git tag -a v1.0.0 -m "Primeira versão estável"
```

**Exemplo prático:**

Depois de concluir e registrar a primeira versão do projeto:

```bash
git add .
git commit -m "feat: finaliza versão inicial"
git tag -a v1.0.0 -m "Release 1.0.0"
```

Por padrão, a tag é criada no commit atual. Você também pode indicar um commit específico:

```bash
git tag -a v1.0.0 ID_DO_COMMIT -m "Release 1.0.0"
```

### `git show nome`

**O que faz:** exibe os detalhes de uma tag, incluindo sua mensagem e o commit associado.

```bash
git show v1.0.0
```

### `git tag`

**O que faz:** lista as tags locais.

```bash
git tag
```

Para pesquisar tags por padrão:

```bash
git tag -l "v1.*"
```

### `git checkout nome`

**O que faz:** quando `nome` é uma tag, permite consultar o projeto exatamente no commit marcado por ela.

```bash
git checkout v1.0.0
```

**Forma moderna equivalente:**

```bash
git switch --detach v1.0.0
```

> [!important] Detached HEAD
> Ao consultar uma tag dessa forma, você não estará em uma branch normal. Para continuar desenvolvendo a partir daquela versão, crie uma branch:
>
> ```bash
> git switch -c hotfix/v1.0.0 v1.0.0
> ```

### `git push origin v2.0.0`

**O que faz:** envia uma tag específica ao repositório remoto.

```bash
git push origin v2.0.0
```

**Exemplo prático:**

```bash
git tag -a v2.0.0 -m "Release 2.0.0"
git push origin v2.0.0
```

Para enviar todas as tags locais:

```bash
git push origin --tags
```

As tags enviadas ficam disponíveis para os outros desenvolvedores que acessam o repositório.

**Importante:** criar uma tag não envia automaticamente os commits para o GitHub. Envie a branch e a tag quando necessário.

---

## 9. Diferença entre Branch, Stash e Tag

| Recurso | Finalidade | Exemplo |
|---|---|---|
| Branch | Desenvolver funcionalidades isoladamente | `feature/login` |
| Stash | Guardar alterações temporariamente | `git stash` |
| Tag | Marcar um commit ou versão | `v1.0.0` |
| Commit | Registrar alterações no histórico | `git commit -m "feat: login"` |

### Quando utilizar cada um?

- **Branch:** quando começar uma funcionalidade, correção ou experimento.
- **Stash:** quando precisar guardar alterações incompletas para trocar temporariamente de contexto.
- **Tag:** quando quiser marcar uma versão importante do projeto.
- **Commit:** quando tiver um conjunto coerente de alterações para registrar no histórico.

---

## 10. Fluxos práticos para o dia a dia

### Criar um projeto e enviar ao GitHub pela primeira vez

```bash
git init
git branch -M main
git add .
git commit -m "chore: inicia projeto"
git remote add origin URL_DO_REPOSITORIO
git push -u origin main
```

### Atualizar o projeto depois de modificar arquivos

```bash
git status
git add .
git commit -m "feat: adiciona nova funcionalidade"
git push
```

### Trabalhar em uma funcionalidade isolada

```bash
git switch main
git pull
git switch -c feature/nova-funcionalidade

# Faça as alterações

git add .
git commit -m "feat: adiciona nova funcionalidade"
git push -u origin feature/nova-funcionalidade
```

Depois, integre a branch por meio de um merge ou de um Pull Request no GitHub.

### Marcar e publicar uma versão

```bash
git status
git log --oneline -5
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin main
git push origin v1.0.0
```

### Consultar o histórico e o estado atual

```bash
git status
git log --oneline --graph --decorate --all
git branch -a
git tag
```

---

## 11. Referência rápida

| Objetivo | Comando |
|---|---|
| Inicializar repositório | `git init` |
| Verificar estado | `git status` |
| Adicionar alterações | `git add .` |
| Criar commit | `git commit -m "mensagem"` |
| Ver histórico | `git log --oneline` |
| Criar branch | `git branch nome` |
| Trocar de branch | `git switch nome` |
| Criar e trocar de branch | `git switch -c nome` |
| Integrar branch | `git merge nome` |
| Conectar remoto | `git remote add origin URL` |
| Enviar commits | `git push` |
| Buscar e integrar atualizações | `git pull` |
| Clonar repositório | `git clone URL` |
| Renomear arquivo | `git mv antigo novo` |
| Remover arquivo | `git rm arquivo` |
| Restaurar arquivo modificado | `git restore arquivo` |
| Guardar alterações | `git stash` |
| Listar stashes | `git stash list` |
| Reaplicar e remover stash | `git stash pop` |
| Criar tag anotada | `git tag -a v1.0.0 -m "mensagem"` |
| Enviar tag | `git push origin v1.0.0` |

## 12. Boas práticas

1. Confira `git status` antes de criar commits.
2. Faça commits pequenos, com mensagens que expliquem a mudança.
3. Utilize nomes de branches descritivos, como `feature/login` e `fix/navbar`.
4. Não utilize `git reset --hard` sem entender quais alterações serão descartadas.
5. Não confunda tags com backups completos do projeto.
6. Antes de executar comandos destrutivos, considere criar um commit ou backup.
7. Mantenha o repositório remoto atualizado com `git pull` quando apropriado.
8. Use `.gitignore` para evitar enviar arquivos locais, segredos, dependências e arquivos gerados.

> [!tip] Regra de ouro
> **Branch para desenvolver, commit para registrar, stash para guardar temporariamente e tag para marcar versões.**
