# GITHUB

## Resetar para o commit anterior

Para resetar para o commit anterior no Git, você tem algumas opções dependendo do que deseja fazer:

## 1. **Desfazer mudanças locais não commitadas** (mais seguro)
```bash
git reset --hard HEAD
```
Isso descarta todas as mudanças locais e volta ao último commit.

## 2. **Voltar para o commit anterior e descartar o último commit**
```bash
git reset --hard HEAD~1
```
Isso remove o último commit completamente e volta ao anterior.

## 3. **Voltar para um commit específico**
Primeiro, veja o histórico:
```bash
git log --oneline
```

> Exemplo após executar o `git log --oneline`:

```bash
C:\Users\Programacao\CSharp\Seu-Projeto>git log --oneline 
ed4f4f8 ajuste
13b5ade feat: alguns ajuste minimos
156f780 feat: janela MasterPrincipal add
ee892ab Adicionar arquivos de projeto.
8fb7b86 Adicione .gitattributes, .gitignore e README.md.
```

Depois, copie o hash do commit desejado e use:
```bash
git reset --hard <hash-do-commit>
```

> Exemplo de como usar `git reset --hard <hash-do-commit>`

```bash
C:\Users\Programacao\CSharp\Seu-Projeto>git reset --hard 13b5ade
HEAD is now at 13b5ade feat: alguns ajuste minimos
```

## 4. **Se já fez push para o repositório remoto**
```bash
git reset --hard HEAD~1
git push --force origin <nome-da-branch>
```
⚠️ **CUIDADO**: `--force` reescreve o histórico. Use apenas se tiver certeza e se estiver trabalhando sozinho na branch.

## 5. **Opção mais segura: Reverter sem perder o histórico**
```bash
git revert HEAD
```
Isso cria um novo commit que desfaz as mudanças do último commit, mantendo o histórico intacto.

---

**Qual situação se aplica a você?**
- Ainda não fez commit das mudanças do FormBase?
- Já fez commit mas não fez push?
- Já fez push para o repositório remoto?

Me informe para eu te dar o comando exato que você precisa.
