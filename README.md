# Estudo Git

Repositorio criado para praticar comandos Git na rotina real de versionamento.

## Objetivo

Este estudo foi feito para aprender, na pratica:

- criacao de repositorio local e remoto
- fluxo de alteracao, commit e push
- trabalho com branches
- abertura e entendimento de PR
- merge entre branches com historicos diferentes
- publicacao de arquivos na branch padrao do GitHub

## O que foi praticado

Durante o estudo, foram executados comandos como:

- `git init`
- `git status`
- `git add .`
- `git commit -m "mensagem"`
- `git branch`
- `git checkout -b nome-da-branch`
- `git switch nome-da-branch`
- `git push --set-upstream origin branch`
- `git remote -v`
- `git merge`
- `git log --oneline`
- `git ls-tree --name-only origin/main`

## Aprendizado importante

Um ponto chave do estudo foi entender que o arquivo pode estar no remoto, mas nao aparecer na pagina principal do GitHub quando:

1. ele foi enviado para outra branch (ex.: `master` ou `inclusao`)
2. a branch padrao do repositorio e `main`

Tambem foi praticado o caso de historicos sem ancestral comum e como resolver merge nesses cenarios.

## Estrutura do projeto

- `index.html`: pagina com topicos e comandos Git organizados por ancora
- `README.md`: resumo do estudo e referencia do que foi praticado

## Como reproduzir o fluxo basico

```bash
git clone <url-do-repositorio>
cd git
git checkout -b minha-branch
# editar arquivos
git add .
git commit -m "Minha alteracao"
git push -u origin minha-branch
```

Depois, no GitHub:

1. abrir Pull Request
2. revisar as alteracoes
3. aprovar (quando aplicavel)
4. fazer merge na branch desejada

## Proximos passos sugeridos

- praticar `rebase` com seguranca em branch de estudo
- testar resolucao de conflitos em dois arquivos
- configurar protecao de branch no GitHub