# Tutorial Completo de Git - Do Básico ao Avançado

## 1. COMEÇANDO COM GIT

### 1.1 Instalação
```bash
# Windows
# Baixe em: https://git-scm.com/download/win

# Linux (Ubuntu/Debian)
sudo apt-get install git

# macOS
brew install git
```

### 1.2 Configuração Inicial
```bash
# Definir nome de usuário
git config --global user.name "Seu Nome"

# Definir email
git config --global user.email "seu@email.com"

# Verificar configurações
git config --list

# Configurar editor padrão (opcional)
git config --global core.editor "code --wait"  # VS Code
```

### 1.3 Criando um Repositório

#### Opção A: Criar novo repositório local
```bash
# Entrar na pasta do projeto
cd /caminho/do/projeto

# Inicializar repositório
git init

# Verificar status
git status
```

#### Opção B: Clonar repositório existente
```bash
# Clonar via HTTPS
git clone https://github.com/usuario/repositorio.git

# Clonar via SSH
git clone git@github.com:usuario/repositorio.git

# Clonar em pasta específica
git clone https://github.com/usuario/repositorio.git nome-da-pasta
```

---

## 2. COMANDOS BÁSICOS DO DIA A DIA

### 2.1 Verificar Status
```bash
# Ver arquivos modificados/não rastreados
git status

# Versão resumida
git status -s
```

### 2.2 Adicionar Arquivos (Stage)
```bash
# Adicionar arquivo específico
git add arquivo.txt

# Adicionar todos os arquivos modificados
git add .

# Adicionar todos arquivos de um tipo
git add *.cs

# Adicionar interativamente
git add -p
```

### 2.3 Fazer Commit
```bash
# Commit com mensagem
git commit -m "Mensagem do commit"

# Commit adicionando tudo automaticamente
git commit -am "Mensagem do commit"

# Commit com descrição detalhada
git commit
# (abrirá o editor para escrever mensagem longa)

# Corrigir último commit (antes de push)
git commit --amend -m "Nova mensagem"
```

### 2.4 Ver Histórico
```bash
# Ver histórico completo
git log

# Ver histórico resumido
git log --oneline

# Ver histórico gráfico
git log --graph --oneline --all

# Ver últimos N commits
git log -n 5

# Ver commits de um arquivo específico
git log -- arquivo.txt

# Ver diferenças de cada commit
git log -p
```

### 2.5 Ver Diferenças
```bash
# Ver mudanças não staged
git diff

# Ver mudanças staged (prontas para commit)
git diff --staged

# Ver diferenças de um arquivo específico
git diff arquivo.txt

# Ver diferenças entre branches
git diff branch1..branch2
```

---

## 3. TRABALHANDO COM BRANCHES

### 3.1 Criar Branches
```bash
# Criar nova branch
git branch nome-da-branch

# Criar e mudar para a branch
git checkout -b nome-da-branch

# Criar branch a partir de um commit específico
git branch nome-da-branch abc1234
```

### 3.2 Listar Branches
```bash
# Listar branches locais
git branch

# Listar todas as branches (locais e remotas)
git branch -a

# Listar branches remotas
git branch -r

# Listar branches com último commit
git branch -v
```

### 3.3 Mudar de Branch
```bash
# Mudar para branch existente
git checkout nome-da-branch

# Criar e mudar (forma nova)
git switch -c nome-da-branch

# Voltar para branch anterior
git checkout -
```

### 3.4 Renomear Branch
```bash
# Renomear branch atual
git branch -m novo-nome

# Renomear branch específica
git branch -m nome-antigo novo-nome
```

### 3.5 Deletar Branch
```bash
# Deletar branch local (seguro - só deleta se já foi merged)
git branch -d nome-da-branch

# Forçar deleção (mesmo sem merge)
git branch -D nome-da-branch

# Deletar branch remota
git push origin --delete nome-da-branch
```

---

## 4. SINCRONIZANDO COM REPOSITÓRIO REMOTO

### 4.1 Adicionar Remoto
```bash
# Adicionar origem remota
git remote add origin https://github.com/usuario/repo.git

# Listar remotos
git remote -v

# Ver detalhes de um remoto
git remote show origin

# Renomear remoto
git remote rename origin novo-nome

# Remover remoto
git remote remove origin
```

### 4.2 Push (Enviar)
```bash
# Enviar branch atual
git push origin nome-da-branch

# Enviar e criar branch remota
git push -u origin nome-da-branch

# Enviar todas as branches
git push --all

# Enviar tags
git push --tags

# Forçar push (CUIDADO!)
git push --force origin nome-da-branch
```

### 4.3 Pull (Baixar e Mesclar)
```bash
# Baixar e mesclar branch atual
git pull

# Pull de branch específica
git pull origin nome-da-branch

# Pull com rebase
git pull --rebase

# Pull sem merge automático
git pull --no-commit
```

### 4.4 Fetch (Baixar sem Mesclar)
```bash
# Baixar todas as atualizações
git fetch

# Baixar de origem específica
git fetch origin

# Baixar e limpar branches deletadas remotamente
git fetch --prune

# Baixar tags
git fetch --tags
```

### 4.5 Fetch + Prune (Limpar)
```bash
# Limpar referências de branches remotas deletadas
git fetch --prune

# Ou
git remote prune origin

# Configurar para sempre fazer prune no fetch
git config --global fetch.prune true
```

---

## 5. DESFAZENDO MUDANÇAS

### 5.1 Descartar Mudanças Locais
```bash
# Descartar mudanças de um arquivo
git checkout -- arquivo.txt

# Descartar todas as mudanças não staged
git checkout .

# Descartar mudanças staged (unstage)
git reset HEAD arquivo.txt

# Descartar tudo e voltar ao último commit
git reset --hard HEAD
```

### 5.2 Reset (Desfazer Commits)
```bash
# Voltar 1 commit mantendo mudanças staged
git reset --soft HEAD~1

# Voltar 1 commit mantendo mudanças unstaged
git reset --mixed HEAD~1
# ou simplesmente
git reset HEAD~1

# Voltar 1 commit descartando TUDO
git reset --hard HEAD~1

# Voltar para commit específico
git reset --hard abc1234

# Voltar N commits
git reset --hard HEAD~3
```

### 5.3 Revert (Reverter Commit)
```bash
# Reverter último commit (cria novo commit)
git revert HEAD

# Reverter commit específico
git revert abc1234

# Reverter sem criar commit automaticamente
git revert --no-commit HEAD
```

### 5.4 Restaurar Arquivos (Git 2.23+)
```bash
# Descartar mudanças de arquivo
git restore arquivo.txt

# Unstage arquivo
git restore --staged arquivo.txt

# Restaurar arquivo de commit específico
git restore --source=abc1234 arquivo.txt
```

---

## 6. MERGE E REBASE

### 6.1 Merge (Mesclar)
```bash
# Mesclar branch na branch atual
git merge nome-da-branch

# Merge sem fast-forward (sempre cria commit)
git merge --no-ff nome-da-branch

# Abortar merge em caso de conflito
git merge --abort
```

### 6.2 Rebase
```bash
# Rebase da branch atual com main
git rebase main

# Rebase interativo (últimos 3 commits)
git rebase -i HEAD~3

# Continuar rebase após resolver conflitos
git rebase --continue

# Pular commit durante rebase
git rebase --skip

# Abortar rebase
git rebase --abort
```

### 6.3 Resolver Conflitos
```bash
# 1. Editar arquivos em conflito manualmente
# 2. Marcar como resolvido
git add arquivo-resolvido.txt

# 3. Continuar merge/rebase
git merge --continue
# ou
git rebase --continue
```

---

## 7. STASH (GUARDAR MUDANÇAS TEMPORARIAMENTE)

```bash
# Guardar mudanças atuais
git stash

# Guardar com mensagem
git stash save "Mensagem descritiva"

# Listar stashes
git stash list

# Aplicar último stash (mantém na lista)
git stash apply

# Aplicar e remover último stash
git stash pop

# Aplicar stash específico
git stash apply stash@{2}

# Ver conteúdo do stash
git stash show -p

# Deletar stash específico
git stash drop stash@{0}

# Deletar todos os stashes
git stash clear

# Criar branch a partir do stash
git stash branch nome-da-branch
```

---

## 8. TAGS (VERSÕES)

```bash
# Criar tag leve
git tag v1.0.0

# Criar tag anotada (recomendado)
git tag -a v1.0.0 -m "Versão 1.0.0"

# Criar tag em commit específico
git tag -a v1.0.0 abc1234 -m "Versão 1.0.0"

# Listar tags
git tag

# Ver detalhes de uma tag
git show v1.0.0

# Enviar tag para remoto
git push origin v1.0.0

# Enviar todas as tags
git push origin --tags

# Deletar tag local
git tag -d v1.0.0

# Deletar tag remota
git push origin --delete v1.0.0

# Fazer checkout de uma tag
git checkout v1.0.0
```

---

## 9. COMANDOS AVANÇADOS

### 9.1 Cherry-pick (Copiar Commit)
```bash
# Aplicar commit específico na branch atual
git cherry-pick abc1234

# Aplicar múltiplos commits
git cherry-pick abc1234 def5678

# Cherry-pick sem commit automático
git cherry-pick --no-commit abc1234
```

### 9.2 Reflog (Histórico de Referências)
```bash
# Ver histórico de todas as ações
git reflog

# Recuperar commit "perdido"
git reflog
git checkout abc1234
git checkout -b branch-recuperada
```

### 9.3 Bisect (Buscar Bug)
```bash
# Iniciar busca binária
git bisect start

# Marcar commit atual como ruim
git bisect bad

# Marcar commit antigo como bom
git bisect good abc1234

# Git vai testando... marque cada commit
git bisect good  # ou
git bisect bad

# Finalizar
git bisect reset
```

### 9.4 Blame (Ver Autor de Linhas)
```bash
# Ver quem modificou cada linha
git blame arquivo.txt

# Ver de linha específica
git blame -L 10,20 arquivo.txt
```

### 9.5 Clean (Limpar Arquivos Não Rastreados)
```bash
# Ver o que seria deletado (modo dry-run)
git clean -n

# Deletar arquivos não rastreados
git clean -f

# Deletar arquivos e diretórios
git clean -fd

# Incluir arquivos ignorados
git clean -fx
```

---

## 10. WORKFLOWS COMUNS

### 10.1 Feature Branch Workflow
```bash
# 1. Criar branch da feature
git checkout -b feature/nova-funcionalidade

# 2. Trabalhar e commitar
git add .
git commit -m "Adiciona nova funcionalidade"

# 3. Enviar para remoto
git push -u origin feature/nova-funcionalidade

# 4. Após aprovação, mesclar com main
git checkout main
git pull origin main
git merge feature/nova-funcionalidade
git push origin main

# 5. Deletar branch
git branch -d feature/nova-funcionalidade
git push origin --delete feature/nova-funcionalidade
```

### 10.2 Gitflow Workflow
```bash
# Criar branch de desenvolvimento
git checkout -b develop

# Feature
git checkout -b feature/nome develop
# ... trabalhar ...
git checkout develop
git merge --no-ff feature/nome
git branch -d feature/nome

# Release
git checkout -b release/1.0.0 develop
# ... ajustes finais ...
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0
git checkout develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0

# Hotfix
git checkout -b hotfix/1.0.1 main
# ... corrigir bug ...
git checkout main
git merge --no-ff hotfix/1.0.1
git tag -a v1.0.1
git checkout develop
git merge --no-ff hotfix/1.0.1
git branch -d hotfix/1.0.1
```

---

## 11. ARQUIVO .gitignore

```bash
# Criar .gitignore na raiz do projeto
touch .gitignore

# Exemplos de conteúdo para C#/.NET
bin/
obj/
*.user
*.suo
.vs/
*.log
*.tmp

# Exemplos gerais
node_modules/
.env
*.log
.DS_Store
Thumbs.db
```

### Ignorar arquivo já rastreado
```bash
# Parar de rastrear mantendo arquivo local
git rm --cached arquivo.txt

# Adicionar ao .gitignore
echo "arquivo.txt" >> .gitignore

# Commitar
git commit -m "Remove arquivo.txt do rastreamento"
```

---

## 12. COMANDOS DE EMERGÊNCIA

### 12.1 Desfazer Push Acidental
```bash
# Ver histórico
git log --oneline

# Resetar para commit anterior
git reset --hard HEAD~1

# Forçar push (CUIDADO!)
git push --force origin nome-da-branch
```

### 12.2 Recuperar Commit Deletado
```bash
# Ver histórico completo
git reflog

# Criar branch no commit perdido
git checkout -b recuperado abc1234
```

### 12.3 Resolver "Detached HEAD"
```bash
# Criar branch no HEAD atual
git checkout -b nome-da-branch

# Ou voltar para branch anterior
git checkout main
```

### 12.4 Limpar Repositório Corrompido
```bash
# Verificar integridade
git fsck

# Limpeza agressiva
git gc --aggressive --prune=now
```

---

## 13. ALIASES ÚTEIS

```bash
# Configurar aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --graph --oneline --all"
git config --global alias.undo "reset --soft HEAD~1"

# Usar aliases
git st
git co main
git lg
```

---

## 14. DICAS E BOAS PRÁTICAS

### 14.1 Mensagens de Commit
```
✅ Boas mensagens:
- "Adiciona validação de email no formulário de login"
- "Corrige bug de memória no módulo de upload"
- "Refatora classe UserService para melhor performance"

❌ Mensagens ruins:
- "fix"
- "mudanças"
- "teste"
- "asdfasdf"
```

### 14.2 Quando Fazer Commit
- Faça commits pequenos e frequentes
- Cada commit deve ter uma única responsabilidade
- Commite código que funciona (compila)
- Commite antes de trocar de branch

### 14.3 Quando NÃO Fazer Force Push
- Nunca em branches compartilhadas (main, develop)
- Nunca após outros terem feito pull
- Apenas em branches pessoais antes de merge

### 14.4 Backup Antes de Operações Perigosas
```bash
# Criar branch de backup
git branch backup-antes-do-reset

# Fazer operação arriscada
git reset --hard HEAD~5

# Se der errado, recuperar
git checkout backup-antes-do-reset
```

---

## 15. COMANDOS RÁPIDOS DE REFERÊNCIA

```bash
# Status
git status -s

# Adicionar tudo
git add .

# Commit
git commit -m "mensagem"

# Push
git push

# Pull
git pull

# Criar branch
git checkout -b nome

# Trocar branch
git checkout nome

# Merge
git merge nome

# Ver histórico
git log --oneline

# Desfazer mudanças
git reset --hard HEAD

# Limpar branches remotas deletadas
git fetch --prune
```

---

## 16. TROUBLESHOOTING COMUM

### Conflito ao fazer pull
```bash
git stash
git pull
git stash pop
# Resolver conflitos manualmente
git add .
git commit
```

### "Your branch is ahead of origin/main by N commits"
```bash
git push origin main
```

### "Your branch and origin/main have diverged"
```bash
git pull --rebase origin main
# ou
git pull origin main
```

### Commit em branch errada
```bash
git stash
git checkout branch-correta
git stash pop
git add .
git commit -m "mensagem"
```

---

**Este tutorial cobre os principais cenários do Git. Pratique em um repositório de teste antes de usar em projetos reais!**
