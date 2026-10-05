# ESTOQUE DE TECIDO PLUS+ V33

Versão corrigida para publicação no Render.

## Segurança de login

Configure no Render, em **Environment**:

- `ADMIN_USER` — usuário administrativo
- `ADMIN_PASSWORD` — senha administrativa
- `DATABASE_URL` — conexão do PostgreSQL, se estiver usando banco
- `OPENAI_API_KEY` — opcional, para os recursos de IA
- `OPENAI_MODEL` — opcional

**Nunca coloque valores secretos no GitHub, no `render.yaml` ou no HTML.**

O login agora possui:
- sessão HttpOnly;
- cookie `Secure` quando executado em HTTPS/Render;
- expiração por inatividade;
- limite de tentativas de login;
- endpoint de diagnóstico que não revela a senha;
- bloqueio das APIs protegidas sem sessão.

## Deploy no Render

Use `npm install` como build e `node server.js` como start. Depois de alterar variáveis de ambiente, escolha **Save, rebuild, and deploy** ou **Save and deploy**. O Render informa que `Save only` salva a variável mas não a aplica até um novo deploy.

## Diagnóstico

- `/api/health` mostra apenas o estado geral e se o login está configurado.
- `/api/auth/status` mostra se o login está configurado, sem expor a senha.
