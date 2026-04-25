# estudo-git

Referência extensa dos comandos mais usados do Git, cobrindo trabalho diário, colaboração, histórico, limpeza, configuração e comandos internos avançados.

---

## Índice

1. [Configuração](#1-configuração)
2. [Inicialização e Clonagem](#2-inicialização-e-clonagem)
3. [Trabalho Diário](#3-trabalho-diário)
4. [Branches](#4-branches)
5. [Colaboração (Remoto)](#5-colaboração-remoto)
6. [Histórico](#6-histórico)
7. [Desfazendo Alterações](#7-desfazendo-alterações)
8. [Limpeza](#8-limpeza)
9. [Stash](#9-stash)
10. [Tags](#10-tags)
11. [Submódulos](#11-submódulos)
12. [Comandos Internos Avançados](#12-comandos-internos-avançados)

---

## 1. Configuração

Configurações globais e locais do Git.

```bash
# Definir nome de usuário global
git config --global user.name "Seu Nome"

# Definir e-mail global
git config --global user.email "seu@email.com"

# Definir editor padrão
git config --global core.editor "vim"

# Definir ferramenta de diff
git config --global diff.tool vimdiff

# Ativar cores no terminal
git config --global color.ui auto

# Exibir todas as configurações
git config --list

# Exibir uma configuração específica
git config user.name

# Configuração apenas para o repositório local (omitir --global)
git config user.name "Outro Nome"

# Criar alias para comandos
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate --all"

# Definir estratégia de rebase no pull
git config --global pull.rebase true

# Configurar credencial helper (cache por 1 hora)
git config --global credential.helper "cache --timeout=3600"
```

---

## 2. Inicialização e Clonagem

```bash
# Inicializar um novo repositório no diretório atual
git init

# Inicializar com nome de branch padrão
git init -b main

# Clonar um repositório remoto
git clone https://github.com/usuario/repositorio.git

# Clonar em um diretório específico
git clone https://github.com/usuario/repositorio.git meu-projeto

# Clonar apenas um branch específico
git clone -b develop --single-branch https://github.com/usuario/repositorio.git

# Clonar com profundidade (histórico limitado)
git clone --depth 1 https://github.com/usuario/repositorio.git
```

---

## 3. Trabalho Diário

### Status e Diferenças

```bash
# Ver status dos arquivos (modificados, staged, untracked)
git status

# Ver status resumido
git status -s

# Ver diferenças entre o working tree e o índice (staged)
git diff

# Ver diferenças já no stage (prontas para commit)
git diff --staged

# Ver diferenças entre dois commits ou branches
git diff main feature/nova-funcionalidade

# Ver diferenças de um arquivo específico
git diff HEAD arquivo.txt
```

### Adicionando ao Stage (Index)

```bash
# Adicionar arquivo específico ao stage
git add arquivo.txt

# Adicionar todos os arquivos modificados e novos
git add .

# Adicionar interativamente (escolher partes do arquivo)
git add -p arquivo.txt

# Adicionar todos os arquivos já rastreados (não inclui untracked)
git add -u
```

### Commits

```bash
# Criar um commit com mensagem
git commit -m "feat: adiciona nova funcionalidade"

# Adicionar ao stage e commitar em um passo (somente arquivos rastreados)
git commit -am "fix: corrige bug no login"

# Editar o último commit (mensagem ou conteúdo)
git commit --amend

# Editar mensagem do último commit sem abrir editor
git commit --amend -m "feat: mensagem corrigida"

# Commit vazio (útil para disparar CI/CD)
git commit --allow-empty -m "chore: trigger CI"
```

### Removendo e Movendo Arquivos

```bash
# Remover arquivo do repositório e do disco
git rm arquivo.txt

# Remover do stage mas manter no disco (untrack)
git rm --cached arquivo.txt

# Mover ou renomear arquivo
git mv nome-antigo.txt nome-novo.txt
```

---

## 4. Branches

```bash
# Listar branches locais
git branch

# Listar todas as branches (locais e remotas)
git branch -a

# Listar branches com último commit
git branch -v

# Criar nova branch
git branch feature/login

# Mudar para uma branch existente
git checkout feature/login

# Criar e mudar para nova branch (forma clássica)
git checkout -b feature/login

# Criar e mudar para nova branch (forma moderna)
git switch -c feature/login

# Renomear branch atual
git branch -m novo-nome

# Deletar branch (apenas se já mesclada)
git branch -d feature/login

# Forçar deleção de branch
git branch -D feature/login

# Criar branch a partir de um commit específico
git branch hotfix abc1234

# Comparar branches
git diff main..feature/login
```

### Merge

```bash
# Mesclar uma branch na branch atual
git merge feature/login

# Merge sem fast-forward (preserva histórico da branch)
git merge --no-ff feature/login

# Abortar merge em andamento com conflito
git merge --abort

# Mesclar apenas o commit (squash)
git merge --squash feature/login
```

### Rebase

```bash
# Fazer rebase da branch atual sobre main
git rebase main

# Rebase interativo dos últimos 3 commits
git rebase -i HEAD~3

# Continuar rebase após resolver conflito
git rebase --continue

# Abortar rebase
git rebase --abort

# Pular commit atual durante rebase
git rebase --skip
```

### Cherry-pick

```bash
# Aplicar um commit específico na branch atual
git cherry-pick abc1234

# Aplicar múltiplos commits
git cherry-pick abc1234 def5678

# Cherry-pick sem criar commit (apenas aplica as mudanças)
git cherry-pick -n abc1234
```

---

## 5. Colaboração (Remoto)

```bash
# Exibir repositórios remotos configurados
git remote -v

# Adicionar um remoto
git remote add origin https://github.com/usuario/repositorio.git

# Remover um remoto
git remote remove origin

# Renomear um remoto
git remote rename origin upstream

# Baixar alterações sem mesclar
git fetch origin

# Baixar todas as branches remotas
git fetch --all

# Baixar e mesclar na branch atual
git pull

# Pull com rebase em vez de merge
git pull --rebase

# Enviar branch local ao remoto
git push origin feature/login

# Definir upstream e enviar
git push -u origin feature/login

# Forçar envio (use com cuidado!)
git push --force

# Forçar envio com segurança (verifica se remoto não mudou)
git push --force-with-lease

# Enviar todas as branches
git push --all origin

# Deletar branch remota
git push origin --delete feature/login

# Enviar tags ao remoto
git push origin --tags
```

---

## 6. Histórico

```bash
# Exibir histórico de commits
git log

# Histórico resumido (uma linha por commit)
git log --oneline

# Histórico com gráfico de branches
git log --oneline --graph --decorate --all

# Histórico dos últimos N commits
git log -n 5

# Histórico de um arquivo específico
git log -- arquivo.txt

# Histórico com diff de cada commit
git log -p

# Histórico por autor
git log --author="Guilherme"

# Histórico por data
git log --since="2024-01-01" --until="2024-12-31"

# Pesquisar nos commits por uma string
git log --grep="bug fix"

# Pesquisar commits que adicionaram ou removeram uma string no código
git log -S "nome_da_funcao"

# Ver quem alterou cada linha de um arquivo
git blame arquivo.txt

# Ver detalhes de um commit específico
git show abc1234

# Ver árvore de diretórios de um commit
git ls-tree --name-only HEAD

# Comparar dois commits
git diff abc1234..def5678
```

---

## 7. Desfazendo Alterações

```bash
# Descartar mudanças no working tree (não staged)
git checkout -- arquivo.txt

# Descartar todas as mudanças não staged
git checkout -- .

# Remover arquivo do stage (manter mudanças no disco)
git restore --staged arquivo.txt

# Desfazer o último commit, mantendo as mudanças no stage
git reset --soft HEAD~1

# Desfazer o último commit, mantendo as mudanças no working tree
git reset --mixed HEAD~1

# Desfazer o último commit e descartar as mudanças (CUIDADO!)
git reset --hard HEAD~1

# Reverter um commit (cria novo commit que desfaz o anterior)
git revert abc1234

# Reverter sem criar commit automaticamente
git revert -n abc1234

# Restaurar arquivo ao estado de um commit específico
git checkout abc1234 -- arquivo.txt
```

---

## 8. Limpeza

```bash
# Exibir arquivos que seriam removidos (dry-run)
git clean -n

# Remover arquivos não rastreados
git clean -f

# Remover arquivos e diretórios não rastreados
git clean -fd

# Remover também arquivos ignorados (.gitignore)
git clean -fdx

# Remover interativamente
git clean -i

# Remover arquivos de merge em andamento (após resolver conflito)
git checkout --merge arquivo.txt

# Remover referências a branches remotas deletadas
git remote prune origin

# Otimizar o repositório (garbage collection)
git gc

# Verificar integridade do repositório
git fsck
```

---

## 9. Stash

```bash
# Guardar mudanças temporariamente
git stash

# Guardar com mensagem descritiva
git stash push -m "WIP: ajuste no formulário"

# Guardar incluindo arquivos untracked
git stash -u

# Listar stashes disponíveis
git stash list

# Aplicar o stash mais recente (mantém no stash)
git stash apply

# Aplicar um stash específico
git stash apply stash@{2}

# Aplicar e remover o stash mais recente
git stash pop

# Remover um stash específico
git stash drop stash@{1}

# Remover todos os stashes
git stash clear

# Ver o conteúdo de um stash
git stash show -p stash@{0}

# Criar uma branch a partir de um stash
git stash branch feature/ajuste stash@{0}
```

---

## 10. Tags

```bash
# Listar tags
git tag

# Criar tag leve
git tag v1.0.0

# Criar tag anotada (com mensagem e autoria)
git tag -a v1.0.0 -m "Release versão 1.0.0"

# Criar tag em um commit específico
git tag -a v1.0.0 abc1234 -m "Release 1.0.0"

# Ver detalhes de uma tag
git show v1.0.0

# Enviar tag ao remoto
git push origin v1.0.0

# Enviar todas as tags ao remoto
git push origin --tags

# Deletar tag local
git tag -d v1.0.0

# Deletar tag remota
git push origin --delete v1.0.0

# Verificar tag assinada com GPG
git tag -v v1.0.0
```

---

## 11. Submódulos

```bash
# Adicionar um submódulo
git submodule add https://github.com/usuario/lib.git libs/lib

# Inicializar submódulos após clonar
git submodule init

# Baixar conteúdo dos submódulos
git submodule update

# Inicializar e atualizar em um único passo
git submodule update --init --recursive

# Atualizar submódulo para o commit mais recente do remoto
git submodule update --remote

# Remover submódulo
git submodule deinit -f libs/lib
git rm -f libs/lib
```

---

## 12. Comandos Internos Avançados

### Bisect (busca binária de bugs)

```bash
# Iniciar bisect
git bisect start

# Marcar commit atual como ruim
git bisect bad

# Marcar commit sabidamente bom
git bisect good v1.0.0

# Automatizar bisect com script de teste
git bisect run ./test.sh

# Encerrar bisect e voltar ao HEAD original
git bisect reset
```

### Worktrees (múltiplos diretórios de trabalho)

```bash
# Criar worktree para uma branch
git worktree add ../hotfix hotfix/critico

# Listar worktrees
git worktree list

# Remover worktree
git worktree remove ../hotfix
```

### Reflog (histórico de referências)

```bash
# Ver reflog do HEAD (todos os movimentos)
git reflog

# Ver reflog de uma branch específica
git reflog show feature/login

# Recuperar commit perdido via reflog
git checkout -b recuperado abc1234
```

### Filter-branch / filter-repo (reescrita de histórico)

```bash
# Remover um arquivo de todo o histórico (requer git-filter-repo instalado)
git filter-repo --path arquivo-secreto.txt --invert-paths

# Alterar e-mail em todo o histórico (filter-branch, built-in)
git filter-branch --env-filter '
OLD_EMAIL="errado@email.com"
NEW_NAME="Nome Correto"
NEW_EMAIL="correto@email.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]; then
  export GIT_COMMITTER_NAME="$NEW_NAME"
  export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]; then
  export GIT_AUTHOR_NAME="$NEW_NAME"
  export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

### Objetos Git (plumbing)

```bash
# Calcular o hash de um arquivo sem adicioná-lo
git hash-object arquivo.txt

# Escrever objeto no banco de dados do Git
git hash-object -w arquivo.txt

# Ver tipo de um objeto pelo hash
git cat-file -t abc1234

# Ver conteúdo de um objeto pelo hash
git cat-file -p abc1234

# Listar entradas do índice (staging area)
git ls-files --stage

# Criar objeto tree a partir do índice
git write-tree

# Criar commit a partir de uma tree
git commit-tree <tree-hash> -m "mensagem" -p <parent-hash>

# Atualizar referência manualmente
git update-ref refs/heads/main <novo-hash>
```

### Rerere (reuso de resolução de conflitos)

```bash
# Ativar rerere
git config --global rerere.enabled true

# Ver conflitos registrados
git rerere status

# Limpar registro de rerere
git rerere clear
```

### Notes (anotações em commits)

```bash
# Adicionar nota a um commit
git notes add -m "Revisado por QA" abc1234

# Ver nota de um commit
git notes show abc1234

# Enviar notas ao remoto
git push origin refs/notes/*
```

---

## Recursos Adicionais

- [Documentação oficial do Git](https://git-scm.com/doc)
- [Pro Git (livro gratuito)](https://git-scm.com/book/pt-br/v2)
- [Git Cheat Sheet - GitHub](https://education.github.com/git-cheat-sheet-education.pdf)
- [Conventional Commits](https://www.conventionalcommits.org/pt-br/)
