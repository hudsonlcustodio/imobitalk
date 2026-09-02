# IMOBI CRM — Runbook mínimo

## App não responde

1. `docker compose -f docker-compose.prod.yml ps`
2. consultar `/api/v1/ready`;
3. verificar logs do container `app`;
4. se readiness está 200 e `/health` está 503, investigar a dependência indicada,
   sem reiniciar o app por reflexo.

## Worker parado

Verificar healthz do worker e logs. O worker possui restart policy; restart repetido
indica falha persistente, não recuperação.

## Scheduler parado

Verificar healthcheck do scheduler e logs. Confirmar que `INTERNAL_SECRET` continua
válido e que as rotas cron respondem dentro da rede.

## Banco

Antes de migration: backup + `pnpm db:migrate:check`.
Depois: aplicar, smoke e observar erros/locks.

## Rollback

Reverter imagens para a última release conhecida e compatível. Não rodar `db reset`.
Se schema novo for incompatível, aplicar forward-fix ou procedimento de restore já testado.

## Incidente de segurança

Revogar/rotacionar credenciais afetadas, conter acesso, preservar logs relevantes,
identificar tenants/dados impactados e registrar timeline/ações.
