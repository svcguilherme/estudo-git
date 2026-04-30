# Estudo - Guia Git com Tópicos  
**by Guilherme Sant' Anna**

> Referência extensa dos comandos mais usados do Git, incluindo comandos de trabalho diário, colaboração, histórico, limpeza, configuração e comandos internos avançados.

---

## 📚 Índice

1. [Início e configuração](#inicio-e-configuracao)
2. [Fluxo diário](#fluxo-diario)
3. [Branches e integração](#branches-e-integracao)
4. [Comandos de merge](#comandos-de-merge)
5. [Repositórios remotos](#repositorios-remotos)
6. [Histórico e comparação](#historico-e-comparacao)
7. [Desfazer e recuperar](#desfazer-e-recuperar)
8. [Stash e limpeza](#stash-e-limpeza)
9. [Tags e releases](#tags-e-releases)
10. [Submódulos e subárvores](#submodulos-e-subarvores)
11. [Manutenção e desempenho](#manutencao-e-desempenho)
12. [Comandos internos](#comandos-internos)

---

## 🚀 Início e configuração

- `git init` → Cria um repositório local  
- `git clone URL` → Baixa um repositório remoto  
- `git config --global user.name "Seu Nome"`  
- `git config --global user.email "email@dominio.com"`  
- `git config --list`  
- `git config --global init.defaultBranch main`

---

## 🔄 Fluxo diário

- `git status`
- `git add arquivo`
- `git add .`
- `git commit -m "mensagem"`
- `git commit --amend`
- `git mv origem destino`
- `git rm arquivo`
- `git restore arquivo`
- `git restore --staged arquivo`

---

## 🌿 Branches e integração

- `git branch`
- `git branch nome`
- `git switch nome`
- `git switch -c nome`
- `git checkout nome`
- `git merge branch`
- `git rebase branch`
- `git cherry-pick hash`
- `git branch -d nome`
- `git branch -D nome`

---

## 🔀 Comandos de merge

- `git merge nome-da-branch`
- `git merge --no-ff nome-da-branch`
- `git merge --ff-only nome-da-branch`
- `git merge --squash nome-da-branch`
- `git merge --no-commit nome-da-branch`
- `git merge -m "mensagem" nome-da-branch`
- `git merge --abort`
- `git merge --continue`
- `git mergetool`
- `git log --merges`

---

## 🌍 Repositórios remotos

- `git remote -v`
- `git remote add origin URL`
- `git fetch`
- `git pull`
- `git pull --rebase`
- `git push`
- `git push -u origin branch`
- `git push --force-with-lease`
- `git remote rename antigo novo`
- `git remote remove nome`

---

## 📊 Histórico e comparação

- `git log`
- `git log --oneline --graph --decorate --all`
- `git show hash`
- `git diff`
- `git diff --staged`
- `git diff A..B`
- `git blame arquivo`
- `git shortlog -sn`
- `git reflog`

---

## ⏪ Desfazer e recuperar

- `git reset --soft HEAD~1`
- `git reset --mixed HEAD~1`
- `git reset --hard HEAD~1`
- `git revert hash`
- `git checkout -- arquivo`
- `git restore --source=HEAD~1 arquivo`

---

## 📦 Stash e limpeza

- `git stash`
- `git stash push -m "nota"`
- `git stash list`
- `git stash pop`
- `git stash apply`
- `git clean -n`
- `git clean -fd`

---

## 🏷️ Tags e releases

- `git tag`
- `git tag v1.0.0`
- `git tag -a v1.0.0 -m "release"`
- `git show v1.0.0`
- `git push origin v1.0.0`
- `git push origin --tags`
- `git tag -d v1.0.0`

---

## 🔗 Submódulos e subárvores

- `git submodule add URL caminho`
- `git submodule update --init --recursive`
- `git submodule foreach 'git pull'`
- `git subtree add --prefix=pasta URL main --squash`
- `git subtree pull --prefix=pasta URL main --squash`

---

## ⚙️ Manutenção e desempenho

- `git gc`
- `git fsck`
- `git prune`
- `git repack -a -d`
- `git count-objects -vH`
- `git maintenance run`

---

## 🧠 Comandos internos (plumbing)

- `git hash-object arquivo`
- `git cat-file -p hash`
- `git ls-files`
- `git ls-tree -r HEAD`
- `git rev-parse HEAD`
- `git update-index`
- `git write-tree`
- `git commit-tree`
- `git mktree`
- `git unpack-objects`
- `git pack-objects`
- `git verify-pack`
