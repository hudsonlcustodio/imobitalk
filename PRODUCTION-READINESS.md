# IMOBI CRM — Production Readiness

Data da revisão: 2026-09-02

Commit validado localmente: `0dd7a58`

Base remota: `a329f1db4d0804b26c9333768b88b5a23cca64c7`

Status: **Release Candidate — `GATE-PROD = BLOCKED`**

## Resultado desta revisão

- documentação pública consolidada como IMOBI CRM em PT-BR, inglês e espanhol;
- instruções de clone e caminhos corrigidos para `hudsonlcustodio/imobitalk`;
- referências Deskcomm preservadas somente como atribuição histórica ou contrato técnico;
- quatro dependências de hooks com risco de estado desatualizado corrigidas;
- lockfile reinstalado em modo congelado e auditoria de produção sem vulnerabilidades conhecidas;
- drift de readiness removido: o repositório já estava publicado e a `main` já tinha CI Linux;
- runbook expandido para deploy, rollback, migration, incidentes, backup e restore.

## Matriz de gates

| Gate | Estado | Evidência desta revisão |
|---|---|---|
| Integridade/lockfile | PASS | `pnpm install --frozen-lockfile` |
| Branding público | PASS | busca residual classificada + 266 testes de branding |
| Secrets no Git | PASS limitado | nenhum `.env` real rastreado e nenhum padrão de chave privada/token encontrado; não substitui scanner remoto |
| TypeScript | PASS | `pnpm typecheck`, heap de 8 GB |
| Lint | PASS | 0 erros; warnings reduzidos de 305 para 301 |
| Unitários focais | PASS | 266 testes de branding + 29 testes de varredura/worker |
| Unitários completos | PARTIAL local | 605 arquivos e 6.721 testes passaram; `threads` não suporta `process.chdir` e expôs uma sonda dependente de `grep`, corrigida para `rg`; focais repetidos passaram |
| Dependency audit | PASS | `pnpm security:audit`: nenhuma vulnerabilidade conhecida |
| Build padrão | BLOCKED local | panic interno do Turbopack no Windows; CI Linux da base passou em `a329f1d` |
| Build alternativo | FAIL local | webpack alcançou compilação e revelou resolução ausente de `client-only`/`server-only`; não é o caminho usado pelo CI |
| Shell/packaging | BLOCKED local | todas as provas executadas passaram, exceto modo POSIX `0600`, que NTFS/Git Bash não representa |
| DB/RLS invariants | BLOCKED | Docker client existe, daemon ausente |
| E2E | BLOCKED local | harness exige Docker/Supabase; último E2E remoto da base passou |
| Docker build/boot | BLOCKED local | daemon Docker ausente; workflow remoto da base passou |
| CodeQL/security remoto | PASS na base | workflow `security` verde em `a329f1d`; novo commit ainda sem CI |
| GHCR | PASS na base / NOT VERIFIED para release | imagens foram publicadas pela `main`; não há tag/release imutável confirmada |
| Branch protection | FAIL | API não retornou ruleset e não há proteção comprovada |
| Release imutável + `stable` | BLOCKED | nenhuma tag/release Git; não promover antes dos demais gates |
| Staging | BLOCKED | infraestrutura e credenciais não fornecidas |
| Migration dry-run/aplicação | BLOCKED | `SUPABASE_DB_ADMIN_URL` de staging não fornecida |
| Backup/restore | BLOCKED | staging isolado não fornecido; backup sem restore não fecha o gate |
| Observabilidade | CONDITIONAL | Sentry permanece opt-in; destino próprio deve ser configurado |
| Runbook/rollback | PASS documental | `RUNBOOK-IMOBI.md` usa tags imutáveis e separa rollback de schema |

## Evidência remota da base

Consultado em 2026-09-02 via GitHub CLI. Para `a329f1d`, os workflows `ci`, `e2e`,
`perf`, `security` e `Publicar imagem Docker (GHCR)` concluíram com sucesso. Essa evidência
prova a base, não substitui o CI da branch desta revisão.

## Bloqueadores mínimos

1. CI Linux verde para o commit final desta branch.
2. Proteção da `main` exigindo os nomes reais dos checks críticos e proibindo force-push/deletion.
3. Tag/release imutável somente depois dos gates técnicos; confirmar as três tags no GHCR.
4. Staging separado com Supabase/Postgres, Redis, WAHA de teste, domínio/TLS e secrets próprios.
5. Em staging: preflight, migration dry-run, backup, migration, invariantes, E2E/smoke e observação.
6. Restore do backup em ambiente isolado, aplicação iniciada e smoke aprovado.

Até esses seis itens terem evidência, `GATE-PROD` permanece **BLOCKED**.
