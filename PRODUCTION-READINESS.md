# IMOBI CRM — Production Readiness

Data do pass: 2026-09-01  
Status: **Release Candidate — condicionado a gates externos**

## Estado real

Este fork recebeu um pass de hardening de produção focado em evitar que a customização
visual seja publicada com acoplamentos operacionais do upstream.

### Correções aplicadas

- branding IMOBI CRM centralizado, logo e paleta preservados;
- telemetria Sentry mudou de opt-out para **opt-in**: DSN vazio não envia dados a terceiros;
- `next.config.ts` não fixa mais organização/projeto Sentry do upstream;
- `/api/v1/ready` adicionado para readiness do processo/configuração, separado do health de dependências;
- healthcheck do container do app passou de TCP puro para `/api/v1/ready`;
- `db:migrate` deixou de ser placeholder e passou a executar `supabase db push --db-url`;
- `db:migrate:check` executa o dry-run;
- imagens Docker de produção não possuem mais fallback silencioso para GHCR do Deskcomm;
- workflow GHCR publica `imobi-crm`, `imobi-worker` e `imobi-scheduler` no owner do fork;
- labels OCI não apontam para o repositório upstream;
- kit self-host não usa mais o repositório/GHCR do upstream como default;
- User-Agent Nuvemshop e assunto de e-mail de alarme não expõem Deskcomm;
- backup operacional passou a gerar `imobi-*.dump`;
- `preflight:prod` valida configuração sem imprimir secrets;
- workflow `security.yml` adiciona audit de dependências e CodeQL `security-extended`.

## Gates

| Gate | Estado | Evidência / pendência |
|---|---|---|
| Branding | PASS estrutural | identidade IMOBI aplicada; referências técnicas legadas mantidas quando contrato |
| Config | PASS no código | Zod + `preflight:prod`; precisa rodar com `.env` real |
| DB migration | CORRIGIDO / não executado | comando real criado; exige DB staging/produção |
| Unit/type/lint | PARCIAL COM EVIDÊNCIA | typecheck e lint passam; unit aprovou 6.727 casos e teve 4 timeouts de concorrência no Windows, todos aprovados isoladamente (16/16) |
| DB/RLS invariants | PENDENTE | exige Docker/Postgres/pgvector |
| E2E | PENDENTE | exige Supabase local/dependências/browser |
| Build Next.js | PASS local | `pnpm build` concluiu com Next.js 16.3.3 e 47 páginas estáticas |
| Docker build/runtime | PENDENTE | daemon Docker indisponível nesta máquina; exige runner Linux |
| Dependency audit | PENDENTE | workflow criado; depende de registry/rede |
| CodeQL | PENDENTE | workflow criado; roda no GitHub |
| Backup | IMPLEMENTADO | restore precisa ser testado em staging |
| Observability | CONDICIONAL | Sentry agora é opt-in; configure DSN próprio ou outra stack |
| DR | BLOQUEADO por requisito | RTO/RPO não fornecidos; restore/failover não podem ser inventados |
| Capacity | BLOQUEADO por workload | RPS/concurrency/storage/SLO ainda não fornecidos |

## Bloqueadores antes de produção

1. Publicar o fork em um repositório próprio e tornar as imagens GHCR do fork disponíveis.
2. Rodar todos os checks obrigatórios do GitHub Actions com resultado verde.
3. Criar ambiente de staging com banco separado.
4. Executar `pnpm db:migrate:check` e depois `pnpm db:migrate` em staging.
5. Rodar testes de RLS/invariantes e E2E contra staging/local representativo.
6. Construir e iniciar as três imagens Docker; verificar readiness/health.
7. Executar backup + restore de staging e medir o tempo.
8. Configurar Sentry/observabilidade própria ou aceitar explicitamente operar sem ela.
9. Definir domínio, TLS, credenciais Supabase/WAHA/Redis e secrets com rotação.
10. Fazer smoke pós-deploy das jornadas críticas.

## Critério de promoção

Só promover para produção quando os checks de CI/security estiverem verdes, migrations
tiverem sido provadas em staging, restore tiver sido testado e os secrets/URLs reais
passarem em `pnpm preflight:prod`.

## Evidência executada neste pass

- YAML parse de workflows e `docker-compose.prod.yml`: PASS.
- `node --check` em `db-migrate.mjs` e `production-preflight.mjs`: PASS.
- `bash -n` nos scripts shell alterados: PASS.
- `tests/shell/update-guard.test.sh`: PASS completo.
- `production-preflight.mjs` com configuração sintética válida: PASS.
- `pnpm typecheck` com heap de 8 GB: PASS.
- `pnpm lint`: PASS com 0 erros e 305 warnings preexistentes.
- `lint:channels` e `lint:role-rank`: PASS.
- `pnpm build`: PASS com acesso de rede para baixar Google Fonts.
- suíte unitária: 6.727 aprovados, 1 expected-fail e 4 timeouts sob concorrência no Windows; os quatro arquivos foram repetidos com um worker e passaram 16/16.
- testes focais de branding/contraste/packaging/workflows: 104/104 PASS; régua congelada: 2/2 PASS após sincronização.
- `test:shell`: a lógica passou até a prova de modo `0600`; o conjunto agregado falha no Windows porque NTFS/Git Bash não preserva a semântica POSIX de permissões. Requer confirmação no CI Linux.
- Next.js resolvido no lockfile: 16.3.3, versão que corrige os advisories críticos publicados em 2026-08-25.
- `pnpm test:db` e `pnpm test:e2e`: não executados porque o daemon Docker está indisponível.
- Build/start das três imagens: não executado porque o daemon Docker está indisponível.
- `hostgator-setup-kit/test-validators.sh` não concluiu dentro do limite de execução disponível; permanece gate de CI.
