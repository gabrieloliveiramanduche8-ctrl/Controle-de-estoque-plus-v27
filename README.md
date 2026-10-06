# ESTOQUE DE TECIDO PLUS+ — V35.1

## V35 MULTIEMPRESA + OWNER + OFICINAS + HISTÓRICO

Esta versão transforma o sistema em uma base multiempresa.

### Hierarquia
- OWNER: dono da plataforma (conta inicial `admin` / `admin123`, trocar imediatamente).
- ADMIN: administrador de uma empresa.
- OPERADOR: usuário operacional da empresa.

### Multiempresa
- Empresas são isoladas por `company_id`.
- Usuários comuns só acessam os dados da própria empresa.
- O OWNER pode criar empresas e selecionar a empresa ativa.
- Dados existentes da V34 são migrados para a empresa principal criada automaticamente.

### Oficinas e aviamentos
- Cadastro de oficinas por empresa.
- Registro de envios de aviamentos para cada oficina.
- Cada envio guarda empresa, oficina, OC, usuário, data, observação e todos os itens enviados.
- O estoque é baixado dentro da mesma transação do registro do envio; se faltar estoque, o envio inteiro é cancelado.
- Histórico de até 500 envios recentes por empresa.

### Banco
Use PostgreSQL com `DATABASE_URL` no Render. O sistema cria/migra as tabelas automaticamente na inicialização.

### Segurança
- Senhas com scrypt.
- Sessão HTTP-only.
- Limite de tentativas de login.
- Isolamento por empresa no backend.
- O OWNER não fica preso a uma empresa; ele trabalha com uma empresa ativa por vez.

### Render
- Web Service Node.
- Build: `npm install`
- Start: `node server.js`
- Health: `/api/health`

Antes de uma migração importante, faça um backup do Postgres. Render oferece exports lógicos e, em instâncias pagas, recuperação point-in-time. Consulte a documentação oficial: https://render.com/docs/postgresql-backups


### V35.1 — SEM LOGIN TEMPORARIAMENTE
O acesso por senha foi desativado temporariamente. Em ambiente Render com PostgreSQL, o servidor cria uma sessão administrativa temporária automaticamente para permitir o uso do sistema. **Esta versão não deve ser usada como versão pública definitiva**, pois qualquer pessoa com acesso ao site poderá entrar enquanto o login estiver desativado.
