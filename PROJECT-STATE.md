# PROJECT-STATE — IMOBI CRM

Data: 2026-09-02

Branch: `codex/production-readiness-imobi`

Commit validado localmente: `0dd7a58`

Status: **Release Candidate — produção bloqueada por gates externos**

## Decisões vigentes

- DEC-001: o produto é apresentado como **IMOBI CRM**.
- DEC-002: DeskcommCRM é a base funcional atribuída; não haverá rewrite.
- DEC-003: identificadores técnicos legados permanecem quando sua troca puder quebrar contratos.
- DEC-004: produção usa imagens com tag imutável; `latest` não é atalho para release.
- DEC-005: staging, migration dry-run, smoke e restore são gates, não recomendações.

## Estado comprovado

- o repositório já está publicado em `hudsonlcustodio/imobitalk`;
- a `main` remota em `a329f1d` teve CI, E2E, security, perf e publicação de imagens verdes;
- as alterações desta revisão passaram em install congelado, typecheck, lint, auditoria de
  dependências e testes focais; o CI do novo commit ainda precisa ser executado;
- não existem releases nem tags Git no repositório e não existe ruleset retornado pela API;
- o daemon Docker local está indisponível;
- não foi fornecido ambiente de staging nem credenciais de banco.

## Gates atuais

- `GATE-STAGING = BLOCKED`
- `GATE-RECOVERY = BLOCKED`
- `GATE-PROD = BLOCKED`

## Próxima ação

Publicar esta branch e obter CI Linux verde. Depois, configurar proteção da `main`, prover
staging isolado, executar migration/backup/smoke/restore e só então decidir uma primeira
release versionada e a promoção das três imagens para `stable`.
