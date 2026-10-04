# ESTOQUE DE TECIDO PLUS+ — V31 PRODUÇÃO

Sistema web para controle de estoque de tecido, cortes, romaneios, aviamentos, histórico e assistência por IA.

## Produção no Render
- Tipo: Web Service
- Runtime: Node
- Build: `npm install`
- Start: `node server.js`
- Variável obrigatória para banco: `DATABASE_URL` (PostgreSQL)
- Variável opcional para IA: `OPENAI_API_KEY`
- Modelo opcional: `OPENAI_MODEL` (padrão configurado no servidor)

## Melhorias V31
- Health check real do PostgreSQL com latência.
- Transações para saída de tecido, evitando baixa parcial/inconsistente.
- Bloqueio de linha (`FOR UPDATE`) para evitar duas saídas simultâneas do mesmo estoque.
- Movimentação de aviamentos atômica no banco.
- Proteção contra estoque negativo mesmo com múltiplos dispositivos.
- Controle de versão para alterações manuais de aviamentos.
- Índices para histórico e atualização de estoque.
- Validação de OC e quantidade de peças na saída.
- Backup local continua disponível pelo menu.
- Operação local continua disponível quando o banco estiver indisponível.

## Banco
O servidor cria as tabelas automaticamente no primeiro acesso ao PostgreSQL configurado. Para produção, mantenha o PostgreSQL com backup automático/point-in-time recovery no provedor.

## Teste rápido
Abra `/api/health`. Em produção, o retorno deve indicar `database: true` quando o PostgreSQL estiver conectado.
