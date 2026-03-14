# Encompasso · Controle de Materiais — NA

App mobile para controle de pedidos do Encompasso Unificado (CSA Novo & CSA Virtual).

---

## Estrutura do projeto

```
materiais-evento/
├── index.html            ← app principal
├── vercel.json           ← configuração da Vercel
├── api/
│   └── config.js         ← função serverless (protege o token)
└── data/
    ├── materiais.json     ← catálogo de materiais (você edita aqui)
    └── pedidos.json       ← banco de dados dos pedidos
```

---

## Passo a passo completo

### 1. Subir os arquivos no GitHub

No repositório `otavio-cyber/materiais-evento`, certifique-se que todos os arquivos
estão no branch `main` com a estrutura acima.

Se o repo estava vazio, pode usar o upload direto no GitHub.com ou via git:

```bash
git add .
git commit -m "primeiro commit"
git push origin main
```

---

### 2. Criar o Personal Access Token do GitHub

1. Acesse: https://github.com/settings/tokens/new
2. **Note**: `encompasso-materiais`
3. **Expiration**: No expiration (ou 1 ano)
4. **Scopes**: marque apenas `repo` (acesso total a repositórios)
5. Clique em **Generate token**
6. **COPIE O TOKEN** — ele aparece uma única vez!

---

### 3. Conectar na Vercel

1. Acesse https://vercel.com e faça login com sua conta GitHub
2. Clique em **Add New → Project**
3. Importe o repositório `materiais-evento`
4. Na tela de configuração, **antes de clicar em Deploy**, vá em:
   - **Environment Variables**
   - Adicione:
     - **Name**: `GITHUB_TOKEN`
     - **Value**: cole o token que você copiou no passo 2
5. Clique em **Deploy**

Pronto! Em ~1 minuto o app estará no ar com uma URL do tipo:
`https://materiais-evento.vercel.app`

---

### 4. Adicionar novos materiais

Edite o arquivo `data/materiais.json` diretamente no GitHub:

```json
[
  { "id": "camiseta", "nome": "Camiseta", "emoji": "👕", "preco": 50 },
  { "id": "caneca",   "nome": "Caneca",   "emoji": "☕", "preco": 35 },
  { "id": "caneta",   "nome": "Caneta",   "emoji": "✏️", "preco": 10 },
  { "id": "adesivo",  "nome": "Adesivo",  "emoji": "🏷️", "preco": 5  }
]
```

⚠️ **Importante**: o campo `id` deve ser único, sem espaços e em minúsculo.
Após salvar, o app já carrega os novos itens automaticamente.

---

## Como o app funciona

- **Resumo**: totais por material, recebido vs pendente
- **Pedidos**: lista com filtros (pago, pendente, por material)
- **Novo**: formulário para registrar um pedido
- Cada pedido tem: nome, telefone, itens com quantidade, status de pagamento
- Ao salvar, os dados vão direto para o `data/pedidos.json` no GitHub
- O token fica seguro na Vercel (nunca aparece no código)
- Funciona offline com dados em cache (localStorage)

---

## Problemas comuns

| Problema | Solução |
|---|---|
| "Sem token" no badge | Verificar a variável `GITHUB_TOKEN` na Vercel |
| "Erro ao salvar" | Token expirado ou sem permissão `repo` |
| Dados não atualizam | Recarregar a página (pull do GitHub) |
