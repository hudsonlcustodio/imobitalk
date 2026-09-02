# PROJECT-STATE — IMOBI CRM

Status: Release Candidate / pronto para primeiro push; Production Readiness in progress  
Repository target: `hudsonlcustodio/imobitalk`

## Decisões vigentes

- DEC-001: O produto será apresentado como **IMOBI CRM**.
- DEC-002: DeskcommCRM é base funcional; não haverá rewrite.
- DEC-003: Branding será centralizado em tokens e camada white-label.
- DEC-004: Identificadores técnicos legados podem permanecer quando sua troca gerar breaking change.
- DEC-005: Production-ready exige evidência de CI/build/test/staging/migration/security/recovery.

## Gate atual

`GATE-PROD: in-progress`

## Próxima ação

Fazer o primeiro push da branch `main` e deixar os workflows Linux executarem os gates
que esta máquina Windows não mede com fidelidade (`test:shell`, Docker/RLS, E2E e imagens).
Não promover `GATE-PROD` antes de staging, migrations, smoke e restore.
