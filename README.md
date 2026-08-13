# Git — Comandos úteis para ambiente profissional de desenvolvimento

## 1. Configuração inicial

### Verificar configurações

```bash
git config --list
```

### Configurar nome

```bash
git config --global user.name "Seu Nome"
```

### Configurar e-mail

```bash
git config --global user.email "seu@email.com"
```

### Definir branch padrão como `main`

```bash
git config --global init.defaultBranch main
```

---

## 2. Criar e iniciar repositórios

### Inicializar um repositório

```bash
git init
```

### Clonar um repositório

```bash
git clone <URL_DO_REPOSITORIO>
```

### Clonar uma branch específica

```bash
git clone -b <branch> <URL_DO_REPOSITORIO>
```

---

## 3. Verificar o estado do projeto

### Ver alterações

```bash
git status
```

### Ver histórico de commits

```bash
git log
```

### Histórico resumido

```bash
git log --oneline
```

### Ver alterações não commitadas

```bash
git diff
```

### Ver alterações já adicionadas ao stage

```bash
git diff --staged
```

---

## 4. Staging e commits

### Adicionar um arquivo

```bash
git add arquivo.js
```

### Adicionar vários arquivos

```bash
git add arquivo1.js arquivo2.js
```

### Adicionar todas as alterações

```bash
git add .
```

### Fazer commit

```bash
git commit -m "feat: adiciona autenticação"
```

### Alterar a mensagem do último commit

```bash
git commit --amend -m "feat: adiciona autenticação"
```

### Adicionar alterações ao último commit

```bash
git add .
git commit --amend --no-edit
```

---

## 5. Branches

### Listar branches locais

```bash
git branch
```

### Listar todas as branches

```bash
git branch -a
```

### Criar uma branch

```bash
git branch feature/nova-funcionalidade
```

### Criar e entrar na branch

```bash
git switch -c feature/nova-funcionalidade
```

### Trocar de branch

```bash
git switch nome-da-branch
```

### Deletar branch local

```bash
git branch -d nome-da-branch
```

### Forçar exclusão de branch

```bash
git branch -D nome-da-branch
```

---

## 6. Trabalhando com branches remotas

### Atualizar informações do servidor

```bash
git fetch
```

### Buscar todas as branches remotas

```bash
git fetch --all
```

### Criar branch local baseada em uma remota

```bash
git switch -c feature/login origin/feature/login
```

### Ver branches remotas

```bash
git branch -r
```

---

## 7. Push e Pull

### Enviar uma branch para o GitHub

```bash
git push
```

### Enviar uma nova branch e configurar upstream

```bash
git push -u origin feature/login
```

Depois disso, normalmente basta:

```bash
git push
```

### Baixar alterações e fazer merge automaticamente

```bash
git pull
```

### Atualizar sem criar merge commit

```bash
git pull --rebase
```

---

## 8. Fetch vs Pull

### `fetch`

```bash
git fetch
```

Baixa informações do repositório remoto **sem modificar a branch atual**.

### `pull`

```bash
git pull
```

Basicamente combina:

```bash
git fetch
git merge
```

ou, dependendo da configuração:

```bash
git fetch
git rebase
```

Uma boa prática é usar `fetch` antes de decidir como integrar as alterações, assim voce tem certeza do que vai vir.

---

## 9. Merge

### Mesclar uma branch

Primeiro entre na branch que receberá as alterações:

```bash
git switch main
```

Depois:

```bash
git merge feature/login
```

### Abortar um merge

```bash
git merge --abort
```

Útil quando aparecem conflitos e você decide cancelar a operação.

---

## 10. Rebase

### Atualizar sua branch usando outra como base

```bash
git switch feature/login
git rebase main
```

### Continuar um rebase após resolver conflitos

```bash
git add .
git rebase --continue
```

### Abortar o rebase

```bash
git rebase --abort
```

### Pular um commit durante o rebase

```bash
git rebase --skip
```

Obs.: Evite fazer rebase de branches compartilhadas por outras pessoas. Rebase altera o histórico.

---

## 11. Resolver conflitos

Depois de um merge/rebase, verifique:

```bash
git status
```

Edite os arquivos conflitantes e depois:

```bash
git add .
```

Se estiver fazendo merge:

```bash
git commit
```

Se estiver fazendo rebase:

```bash
git rebase --continue
```

---

## 12. Desfazer alterações

### Descartar alterações de um arquivo

```bash
git restore arquivo.js
```

### Descartar todas as alterações não commitadas

```bash
git restore .
```

Obs.: Essas alterações podem ser perdidas permanentemente.

### Remover arquivo do stage

```bash
git restore --staged arquivo.js
```

---

## 13. Reverter commits

### Criar um novo commit que desfaz outro

```bash
git revert <HASH>
```

Essa é geralmente a opção **mais segura em branches compartilhadas**, porque preserva o histórico.

Exemplo:

```bash
git revert a1b2c3d
```

---

## 14. Reset

### Voltar o HEAD mantendo as alterações no stage

```bash
git reset --soft HEAD~1
```

### Voltar o commit mantendo as alterações nos arquivos

```bash
git reset --mixed HEAD~1
```

### Apagar o commit e as alterações

```bash
git reset --hard HEAD~1
```

Obs.: `git reset --hard` é perigoso, pois Pode apagar trabalho que ainda não foi salvo em outro lugar.

---

## 15. Stash

Útil quando você precisa trocar de branch sem querer fazer um commit ainda.

### Guardar alterações temporariamente

```bash
git stash
```

### Guardar incluindo arquivos não rastreados

```bash
git stash -u
```

### Listar stashs

```bash
git stash list
```

### Recuperar o último stash

```bash
git stash pop
```

### Aplicar stash sem removê-lo

```bash
git stash apply
```

### Remover um stash

```bash
git stash drop
```

### Limpar todos os stashs

```bash
git stash clear
```

---

## 16. Tags e versões

### Criar uma tag

```bash
git tag v1.0.0
```

### Criar tag anotada

```bash
git tag -a v1.0.0 -m "Release v1.0.0"
```

### Listar tags

```bash
git tag
```

### Enviar uma tag

```bash
git push origin v1.0.0
```

### Enviar todas as tags

```bash
git push origin --tags
```

---

## 17. Remotes

### Ver repositórios remotos

```bash
git remote -v
```

### Adicionar um remote

```bash
git remote add origin <URL>
```

### Alterar URL do remote

```bash
git remote set-url origin <URL>
```

### Remover um remote

```bash
git remote remove origin
```

---

## 18. Investigar problemas

### Ver quem modificou cada linha

```bash
git blame arquivo.js
```

### Procurar um commit específico

```bash
git log --all --oneline -- <arquivo>
```

### Pesquisar por uma mensagem de commit

```bash
git log --grep="autenticação"
```

### Ver detalhes de um commit

```bash
git show <HASH>
```

### Descobrir quais arquivos foram alterados em um commit

```bash
git show --stat <HASH>
```

---

## 19. Git Diff

### Comparar arquivos modificados

```bash
git diff
```

### Comparar duas branches

```bash
git diff main..feature/login
```

### Comparar dois commits

```bash
git diff <HASH1> <HASH2>
```

---

## 20. Limpeza

### Ver arquivos não rastreados que seriam removidos

```bash
git clean -n
```

### Remover arquivos não rastreados

```bash
git clean -f
```

### Remover arquivos e diretórios não rastreados

```bash
git clean -fd
```

---

## 21. Sincronização com a `main`

Um fluxo comum:

```bash
git switch main
git pull
git switch feature/minha-feature
git rebase main
```

Depois:

```bash
git push
```

Se o rebase alterou uma branch que já foi enviada ao remoto:

```bash
git push --force-with-lease
```

Obs.: É preferivel `--force-with-lease` em vez de `--force`, pois ele oferece uma proteção contra sobrescrever alterações remotas que você não conhece.

---

## 22. Fluxo

Um exemplo de fluxo baseado em Pull Request:

```bash
git switch main
git pull

git switch -c feature/login

# desenvolvimento...

git status
git add .
git commit -m "feat: adiciona autenticação"

git push -u origin feature/login
```

Depois:

1. Abrir Pull Request no GitHub/GitLab.
2. CI/CD executa testes e validações.
3. Code review.
4. Corrigir comentários.
5. Fazer novos commits.
6. Após aprovação, fazer merge.
7. Excluir a branch.

---

## 23. Conventional Commits

Um padrões utilizados para mensagens de commit:

```text
feat: nova funcionalidade
fix: correção de bug
docs: documentação
style: formatação
refactor: refatoração
test: testes
chore: tarefas de manutenção
perf: melhoria de performance
build: alterações no sistema de build
ci: alterações no CI/CD
```

Exemplos:

```bash
git commit -m "feat: adiciona tela de login"
```

```bash
git commit -m "fix: corrige validação do formulário"
```

```bash
git commit -m "refactor: reorganiza serviço de autenticação"
```

```bash
git commit -m "docs: atualiza README"
```

---

## 24. Comandos para dominar primeiro

```bash
git clone
git status
git add
git commit
git log
git diff
git branch
git switch
git fetch
git pull
git push
git merge
git rebase
git stash
git revert
git reset
```

## Observações Gerais

* Sempre verificar o `git status` antes de executar comandos importantes, principalmente antes de commit, merge, rebase ou reset.

* Antes de usar comandos destrutivos como `git reset --hard`, `git clean -f` ou `git push --force`, ter certeza do que estou fazendo, porque posso perder alterações.

* Sempre que possível, preferir `git push --force-with-lease` em vez de `git push --force`.

* Evitar fazer `rebase` em branches que outras pessoas estão utilizando, porque isso altera o histórico da branch.

* Em projetos profissionais, evitar trabalhar diretamente na `main`. O ideal é criar uma branch para cada funcionalidade, correção ou tarefa.

* Fazer commits pequenos e com mensagens claras. Isso facilita bastante a revisão e também descobrir onde um problema foi introduzido.

* Antes de começar uma tarefa, atualizar minha branch com as alterações mais recentes da `main`.

* Antes de abrir um Pull Request, verificar se os testes estão passando e se não estou enviando arquivos desnecessários.

* Não colocar senhas, tokens, chaves de API ou arquivos `.env` no Git.

* Usar `.gitignore` para evitar enviar arquivos que não devem fazer parte do repositório.

* `git revert` normalmente é mais seguro que `git reset` quando o commit já foi enviado para uma branch compartilhada.

* `git fetch` serve para atualizar as referências do repositório remoto sem alterar meu código local. Já o `git pull` busca as alterações e tenta integrá-las.

* Antes de executar qualquer comando destrutivo, parar e verificar se existe algum trabalho local que ainda não foi salvo ou enviado.
