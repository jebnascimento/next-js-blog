---
title: 'Git Learning Session'
date: '2020-08-20'
---

# Git Learning(unfinished)

# Inicializando Projetos

**`$ git init`**

- Inicia um repositório local de arquivos no diretório atual.

**`$ git clone <repositório  remoto>`**

- inicia um repositório local com **git init** e clona o repositório remoto para o diretório atual

> **<repositório remoto>: https://github.com/jebnascimento/git-learning.git**

# Configurando Repositório Remoto

**`$ git remote -v`**

- Lista os repositórios remotos com apelido(origin) e url
- o **git remote -v** em repositórios iniciados apenas localmente retorna nada. Deve-se criar um repositório remoto no github e adicionar ao repositório local.

**`$ git remote add origin [https://github.com/jebnascimento/git-learning.git](https://github.com/jebnascimento/git-learning.git)`**

- Adiciona ao repositório local um link com repositório remoto, habilitando o envio dos arquivos ao github

# Arquivos de Configurações do Git

**`$ git config --list`**

- Lista as configurações atuais dos 3 níveis.
- Existem **3 níveis** de configurações do git:
    - Configurações do Sistema
    - Configurações do Usuário
    - Configurações do Projeto

### Configuração do Sistema

Qualquer configuração de sistema vale para qualquer usuário e qualquer projeto, ou seja, define uma configuração global.

**`$ git config --system --edit`**

- Abre o arquivo de configuração de sistema. Geralmente não mexemos muito nesse arquivo.

### Configuração de Usuário

Qualquer configuração de usuário vale para qualquer projeto.

**`$ git confi --global --edit`**

- Abre o arquivo de configuração do seu usuário.

**`$ git config --global core.editor code`**

- Define qual editor será utilizado para abrir o arquivo de configuração. Nesse caso abrirá com o vscode. Pode-se também alterar o arquivo diretamente.

### Configuração local de projeto

Configuração específica de cada projeto.

**`$ git config --local --edit` ou `$ git config --edit`**

- Abre o arquivo de configuração local do projeto.

> O arquivo de configuração local tem prioridade sobre o arquivo de configuração do usuário que tem prioridade sobre arquivo de configuração do sistema.

# Estado dos Arquivos no Git

**`$ git status` ou `git status -s`** 

- Mostra o estado dos arquivos no repositório local.

### Arquivos modificados que não entrarão no próximo commit

- Untracked → Arquivos que o git ainda não conhece
- Unstaged → Arquivos que o git conhece, foram modificados e não sofreram `$ git add`

**`$ git add <nome-do-arquivo>` ou `git add .`**

- Joga o arquivo específico ou todos os arquivos do diretório atual para a **Staged Area**. Os arquivos na staged area serão adicionados ao próximo commit.

**`$ git add --all` ou `$ git add --A`**

- Joga todos os arquivos no diretório atual e nos subdiretórios para a staged area.

### Arquivos modificados que entrarão no próximo commit

- Staged → Arquivos que o git conhece e sofreram `$ git add` anteriormente.

# Commitando arquivos

**`$ git commit -m "mensagem atrelada ao commit"`**

- Remove os arquivos da staged area commitando todos eles, ou seja, registra-se um snapshot único de todos os arquivos com estado staged. Além disso é criado um ponto de save com uma hash para identificar o commit, autor do commit, data e a mensagem atrelada ao commit.

**`$ git commit -amend --no-edit`**

- Commita todos os arquivos com estado staged junto ao último commit, ou seja, não é criado um novo ponto de save com uma nova hash e data.

**`$ git log`**

- Lista todos os commits

# Padronizando os Commits

### Exemplos de commit

> <type>[optional scope]: <description>
[optional body]
[optional footer(s)]

> - feat: allow provided config object to extend other configs
- refactor!: drop support for Node 6
- docs: correct spelling of CHANGELOG
- feat(lang): add polish language
- fix: correct minor typos in code
- chore: add commit linter

### Fonte: [https://www.conventionalcommits.org/en/v1.0.0/](https://www.conventionalcommits.org/en/v1.0.0/)

### Adicionando Linter para Commits

`$ npm install git-commit-msg-linter -D`

- Essa lib garante que nosso commit esteja com o padrão seguido pelo convetional commits.

    > `commit message: add commit linter
    correct format: <**type**>(<**scope**>): <**subject**>
    example: docs: update README

    **types:**
    -**feat** a new feature;
    -**fix** a bug fix;
    -**docs** documentation only changes;
    -**style** changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc);
    -**refactor** a code change that neither fixes a bug nor adds a feature;
    -**test** adding missing tests or correcting existing ones;
    -**chore** changes to the build process or auxiliary tools and libraries such as documentation generation;
    -**perf** a code change that improves performance;
    -**ci** changes to your CI configuration files and scripts;
    -**temp** temporary commit that won't be included in your CHANGELOG;
    **scope:**
    - Optional, can be anything specifying the place of the commit change.
    For example $location, $browser, $compile, $rootScope, ngHref, ngClick, ngView, etc.
    In App Development, scope can be a page, a module or a component.
    **subject:**
    - A very short description of the change in one line.`

# Tirando um snapshot do projeto sem commitar

**`$ git stash`**

- Tira um snapshot do estado atual do projeto, gerando um ponto de save com um identificador e desfaz todas as alterações(CTRL + Z) até o ponto do último commit.

**`$ git stash list`**

- Mostra uma lista de todos os stashs criados

**`$ git stash apply`**

- Retorna para o estado do último stash(CTRL + Y) e o mantém na lista de stashs

**`$ git stash pop`**

- Retorna para o estado do último stash(CTRL + Y) e o remove da lista de stashs

**`$ git stash clear`**

- Limpa a lista de stashs

# Logs

**`$ git log`**

- Lista todos os commits, isto é, sua hash, author, data e mensagem de commit

**`$ git log --oneline`**

- Lista todos os commits em uma linha, mostrando apenas os últimos 7 caracteres da hash e a mensagem atrelada ao commit

**`$ git log --pretty=format:'%H'`**

- Lista todos os commits em uma linha, mostrando apenas a hash completa

**`$ git log --pretty=format:'%h'`**

- Lista todos os commits em uma linha, mostrando apenas a hash reduzida.

**`$ git log --pretty=format:'%cn'`**

- Lista todos os commits em uma linha, mostrando apenas o nome do autor

**`$ git log --pretty=format:'%h %d %s - %cn, %cr'`**

- Lista todos os commits em uma linha, mostrando na ordem: hash reduzida, branch, mensagem, autor e data

**`$ git log --pretty=format:'%C(blue)%h %d %s - %cn, %cr'`**

- Lista todos os commits em uma linha, mostrando na ordem: hash reduzida, branch, mensagem, autor e data na cor azul

**`$ git log --pretty=format:'%C(blue)%h %C(red)%d %C(white)%s - %C(cyan)%cn, %C(yellow)%cr'`**

> a442996 (HEAD -> master) chore: add commit linter - jebnascimento, 21 minutes ago
276d55c verify git stash feat - jebnascimento, 23 minutes ago

> Dica: git config --global core.pager cat → retira o pager(END) do log.

# Tags

Uma tag nada mais é do que um ponteiro para um commit.

**`$ git tag`**

- Lista todas as tags criadas

**`$ git tag <tag>`**

- Cria uma tag atrelada ao último commit
- Ex: git tag 1.0 → cria a tag 1.0 atrelada ao último commit

**`$ git show 1.0`**

- Lista um log com informações da tag atrelada ao commit

**`$ git tag 1.0 -m "mensagem da tag"`**

- Cria uma tag anotada atrelada ao último commit
- Ex: git tag 1.0 -m "release 1.0"

**`$ git tag -a "identificador da tag" -m "mensagem da tag" <id de um commit>`** 

- Cria uma tag anotada atrelada ao id de um commit específico
- Ex: git tag -a "0.1.beta" -m "release 0.1.beta" 12f3183

**`$ git tag -d 1.0`**

- Remove a tag de identificador 1.0

# Revertendo coisas no git

## reset

### Revertendo um git add

**`$ git reset <nome-do-arquivo>` ou `$ git reset`**

- Operação reversa do **git add**, ou seja, remove do índice(index ou stage area) todos os arquivos que lá estiverem ou algum arquivo específico, retornando o arquivo ao estado anterior(untracked ou unstaged). O código do arquivo não é desfeito.

### Revertendo um Commit

**`$ git reset <id-do-commit> --soft`**

- Remove todos os commits acima do commit especificado, fazendo a branch apontar para o id passado e tornando esse commit como head da árvore. Além disso, retorna para o estado anterior todos os arquivos acima daquele commit, ou seja, retornam para o estado que estavam antes de serem commitados.

Exemplo de uso: renomear um commit que esteja com a mensagem incorreta, executando um **git reset** para o commit anterior ao último e realizando um **git commit -m "mensagem"** com a mensagem correta.

**`$ git reset HEAD~n`**

- Retorna n commits para trás.

**`$ git reset HEAD~1 --mixed` ou `$ git reset HEAD~1`**

- Remove o último commit e aponta para o penúltimo commit da árvore. Além disso, retorna os arquivos do último commit para o estado que estavam antes do **git add** ou seja, untracked ou unstaged.

**`$ git reset HEAD~1 --hard`**

- Remove o último commit e aponta para o penúltimo commit da árvore. Além disso, retorna os arquivos do último commit para o estado que estavam antes do **git add** ou seja, untracked ou unstaged. Os arquivos untracked serão deletados e os arquivos unstaged sofrerão um CTRL+Z para o estado do penúltimo commit.

**`$ git reset HEAD --hard` ou `$ git reset --hard`**

- Retorna os arquivos do commit atual para o estado inicial do mesmo commit, ou seja, desfaz todas as modificações que foram feitas a partir do commit atual, uma espécie de CTRL+Z. Esse comando não surte efeito em arquivos untracked.

## revert

**`$ git revert <id-do-commit>`**

- Reverte ou desfaz todas as modificações do commit especificado, mantendo todos os commits e criando um novo commit que se torna head da árvore. Uma mensagem de commit será aberta pelo editor padrão mostrando o que foi desfeito.

    > Geralmente esse comando poderá gerar conflitos, caso seja desfeito algo em que haja algum tipo de dependência nos commits acima. Nesse caso é necessário indentificar os arquivos que estão em conflito e decidir se permanecerão no estado atual ou não.

**`$ git revert <id-do-commit> --no-edit`**

- Reverte ou desfaz todas as modificações do commit especificado, mantendo todos os commits e criando um novo commit que se torna head da árvore. A editor padrão não irá abrir com a mensagem, porém a mensagem do commit foi gerada.

**`$ git revert <id-do-commit> --no-edit`**

- Reverte ou desfaz todas as modificações do commit especificado, mantendo todos os commits, porém não gera um novo commit.

## checkout

**`$ git checkout <nome-do-arquivo>` ou `$ git checkout .`**

- Reverte ou desfaz todas as modificações de um arquivo ou de vários que foram editados e estão na unstaged area. Não funciona para arquivos untracked e também não funciona para arquivos que estejam na staged area.

**`$ git checkout <id-do-commit>` ou  `$ git checkout <id-da-tag>`**

- Permite investigar um commit específico. Ele retorna a um ponto específico desfazendo código e removendo todos os arquivos acima do commit especificado. Além disso, é criado uma branch virtual temporária desacoplada da branch master, ou seja, a nova branch que guarda todo o histórico dos commits até o commit especificado.

**`$ git checkout master`**

- Muda de branch. Nesse caso estamos indo para branch master.

> **OBS**: Quando estamos na branch virtual e mudamos de branch, a branch virtual temporária some.

**`$ git checkout -b <nome-da-branch>`**

- Cria uma nova branch com nome especificado a partir da branch atual.

## clean

**`$ git clean -f`**

- Remove arquivos untracked do diretório atual.

**`$ git clean -n`**

- Lista os arquivos untracked do diretório atual que serão removidos com **git clean.**

**`$ git clean -nd`**

- Lista todos os arquivos untracked que serão removidos com **git clean.**

**`$ git clean -fd`**

- Remove todos os arquivos untracked, inclusive os que estão em diretórios diferentes. ****

## rm

**`$ git rm <nome-do-arquivo>`**

- Remove o arquivo especificado que o git já conhece, ou seja, que não esteja untracked.

**`$ git rm -r <nome-do-pasta>`**

- Remove a pasta especificado que o git já conhece, ou seja, que não esteja untracked.

**`$ git rm <nome-do-arquivo> --chached`**

- Deixa de trackear o arquivo.

# Fetch

**`$ git fetch <url-do-rep-remoto>`**

- O comando git fetch traz do repositório remoto todas informações sobre ele que ainda não estão no seu repositório local. O git fetch **não** incorpora essas mudanças, ou seja não realiza um merge.

# Push

**`$ git push origin <nome-da-branch>`**

- Realiza upload dos arquivos locais de origem para o nome da branch especificada.

# Pull

**`$ git pull <url-do-rep-remoto>`**

- O git vai buscar as alterações de código dos outros desenvolvedores e tentar fazer o merge daquelas alterações no seu código. Caso o Git não consiga fazer o merge automático ele marcará as seções do código onde há conflito e você precisará juntar os código manualmente

**`$ git pull <branch-de-origem> <nome-da-branch>`**

- Traz o código fazendo a junção da outra branch para sua branch de origem.

# Merge

**`$ git merge <nome-da-branch>`**

- Traz o código da branch especificada para a branch atual e realiza o merge.

    > Geralmente esse comando poderá gerar conflitos, caso seja desfeito algo em que haja algum tipo de dependência nos commits acima. Nesse caso é necessário indentificar os arquivos que estão em conflito e decidir se permanecerão no estado atual ou não.

# Enviando tags para o servidor remoto

Por padrão o comando `$ git push origin master` não envia as tags para o github, apenas os commits.

**`$ git push origin master --tags`**

- Envia todas as tags para o servidor remoto, inclusive as não anotadas.

**`$ git push origin master --follow-tags`**

- Envia para o servidor apenas as tags anotadas.

**`$ git push --delete origin "identificador da tag"`**

- Deleta do servidor a tag anotada com o identificador específico
- Ex: git push —delete origin "0.1.beta"

    > OBS: Antes de executar o comando acima, deve-se remover a tag localmente com o comando git tag -d

# .gitignore

- O .gitignore é um arquivo oculto que define quais arquivos ou diretórios o git irá ignorar, ou seja, todas as modificações nesses arquivos e diretórios não serão contabilizadas nos commit, é como se não existissem para o engine do git.
- Esse arquivo deve ficar na raiz do seu repositório local.

> **OBS:** arquivos que são colocados no .gitignore e que já foram trackeados pelo git, ainda continuam sendo trackeados.

# Criando Alias para os Comandos

Vamos nas configurações do git em nível de usuário.

`$ git config --global --edit`

```jsx
[user]
	email = eduardonascimento@poli.ufrj.br
	name = jebnascimento
[core]
	editor = code
	pager = cat
[alias]
	s = !git status -s
	c = !git add -A && git commit -m
	l = !git log --pretty=format:'%C(blue)%h %C(red)%d %C(white)%s - %C(cyan)%cn, %C(yellow)%cr'
[push]
	followTags = true
```

- `s = !git status -s` → `$ git s = $ git status -s` a exclamação indica que será um comando do shell.
- `c = !git add -A && git commit -m` → executa `$ git add -A` e  `$ git commit -m` através do `$ git c`
- FollowTags = true → define por padrão que as tags anotadas serão enviadas ao github