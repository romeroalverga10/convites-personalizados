# 🚀 SETUP: Conectar ao GitHub

Siga estes passos para conectar seu repositório local ao GitHub com auto-sync:

## Passo 1: Criar Repositório no GitHub

1. Acesse https://github.com/new
2. Digite o nome do repositório (ex: `r-e-convites`)
3. Selecione **Private** ou **Public** (como preferir)
4. **Não** selecione "Add a README"
5. Clique em "Create repository"

## Passo 2: Gerar Personal Access Token (PAT)

1. Vá para https://github.com/settings/tokens?type=classic
2. Clique em "Generate new token (classic)"
3. Preencha:
   - **Note**: `GitHub Actions Auto-Sync`
   - **Expiration**: Selecione um período (ex: 90 dias ou sem expiração)
   - **Scopes**: Selecione `repo` (full control of private repositories)
4. Clique "Generate token"
5. **Copie o token** (você não poderá vê-lo novamente!)

## Passo 3: Conectar Repositório Local

Execute no terminal (na pasta do projeto):

```bash
git remote add origin https://github.com/{seu-usuario}/{seu-repositorio}.git
git branch -M main
git push -u origin main
```

Substitua:
- `{seu-usuario}` por seu username do GitHub
- `{seu-repositorio}` pelo nome do repositório criado

## Passo 4: Configurar Secret no GitHub

1. Acesse seu repositório no GitHub
2. Vá em **Settings** → **Secrets and variables** → **Actions**
3. Clique em "New repository secret"
4. **Name**: `GITHUB_TOKEN`
5. **Value**: Cole o PAT gerado no Passo 2
6. Clique "Add secret"

## Passo 5: Ativar GitHub Actions

1. No repositório, vá em **Actions**
2. Clique em "I understand my workflows, go ahead and enable them"
3. Pronto! O workflow está ativado

## ✅ Tudo Pronto!

Agora, a cada mudança nos arquivos:
- **Automático a cada 2 horas** (verificação programada)
- **Automático ao fazer push** (se houver mudanças em `index.html` ou `CLAUDE.md`)

Você pode acompanhar os syncs em **Actions** no seu repositório GitHub.

## 📝 Para Fazer Edições Locais

Se quiser fazer mudanças no seu computador e sincronizar:

```bash
# Fazer mudanças em index.html ou CLAUDE.md
# Então:
git add .
git commit -m "Descrição da mudança"
git push
```

O GitHub Actions vai pegar automaticamente!

---

💡 **Dica**: Se o workflow não funcionar, verifique:
- O `PAT` está definido corretamente no `Secrets`
- GitHub Actions está ativado no repositório
- Os arquivos modificados são `index.html` ou `CLAUDE.md`
