<div align="center">

🇧🇷 Português · [🇺🇸 English](README.en.md) · [🇪🇸 Español](README.es.md)

# 🏠 IMOBI TALK — CRM, atendimento e automação para operações imobiliárias

**Centralize leads, atendimento, funil comercial e automações em uma plataforma preparada para operações imobiliárias.**

**WhatsApp, CRM e agentes de IA trabalhando juntos — com opção de self-host e controle sobre sua própria infraestrutura.**

[![Next.js 16](https://img.shields.io/badge/Next.js-16-black?logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178c6?logo=typescript)](https://www.typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-Postgres%2BAuth%2BStorage-3ecf8e?logo=supabase)](https://supabase.com)
[![CI](https://github.com/hudsonlcustodio/imobitalk/actions/workflows/ci.yml/badge.svg)](https://github.com/hudsonlcustodio/imobitalk/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

[**⚡ Instalação**](#-instalação) ·
[**✨ Funcionalidades**](#-principais-funcionalidades) ·
[**🏗️ Arquitetura**](ARCHITECTURE.md) ·
[**🧑‍💻 Desenvolvimento**](#-desenvolvimento) ·
[**🧪 Testes**](#-testes) ·
[**🤝 Contribuir**](#-contribuindo)

</div>

---

## 🏠 Sobre a IMOBI TALK

A **IMOBI TALK** é uma plataforma de CRM, atendimento e automação projetada para centralizar a operação comercial imobiliária.

A aplicação reúne atendimento via WhatsApp, gestão de leads, contatos, funis comerciais, automações e recursos de inteligência artificial em uma única operação.

A proposta é permitir que equipes comerciais trabalhem com pessoas e agentes de IA dentro do mesmo fluxo, mantendo histórico, contexto e governança das interações.

O projeto pode ser executado em infraestrutura própria, utilizando Docker e serviços configurados pelo operador da instalação.

---

## ✨ Principais funcionalidades

### 💬 Atendimento

- Inbox centralizada para conversas.
- Atendimento humano e por agentes de IA.
- Histórico de conversas.
- Transferência entre IA e atendentes.
- Respostas rápidas.
- Radar de oportunidades sem resposta.
- Distribuição e atribuição de atendimento.

### 🏠 CRM

- Gestão de leads.
- Contatos.
- Funis comerciais.
- Kanban.
- Etapas configuráveis.
- Tags.
- Motivos de perda.
- Histórico das oportunidades.
- Métricas comerciais.

### 🤖 Inteligência Artificial

A IMOBI TALK possui infraestrutura para agentes de IA integrados ao CRM.

Entre os recursos existentes estão:

- agentes configuráveis;
- RAG por organização;
- memória;
- skills;
- roteamento por intenção;
- análise de sentimento;
- handoff IA → humano;
- follow-ups;
- controle de utilização e orçamento;
- diferentes provedores de IA.

Os provedores disponíveis dependem da configuração da instalação.

### 📲 WhatsApp

O projeto suporta integração com WhatsApp através das opções disponíveis na aplicação, incluindo:

- conexão via QR Code utilizando WAHA;
- Meta Cloud API;
- múltiplas conexões;
- envio e recebimento de mídia;
- templates quando utilizados pelo canal oficial;
- mecanismos de controle de envio.

### 🔄 Follow-ups e automações

A plataforma possui mecanismos para automatizar ações relacionadas à operação comercial.

Exemplos:

- retomada de conversas;
- gatilhos por etapa;
- movimentação de lead;
- aplicação de tags;
- atribuição de responsável;
- envio de mensagens;
- webhooks externos;
- avisos para a equipe.

### 🔌 Webhooks

Cada organização pode configurar fontes de captação através de endpoints públicos.

Uma fonte pode receber dados de:

- landing pages;
- formulários;
- integrações próprias;
- n8n;
- Zapier;
- outros sistemas capazes de enviar HTTP POST.

Os eventos recebidos podem alimentar automações dentro da plataforma.

### 👥 Equipe e governança

A aplicação possui recursos relacionados a:

- usuários;
- equipes;
- papéis e permissões;
- atribuição de atendimento;
- transferência;
- escopo de visualização;
- auditoria;
- segurança;
- MFA.

### 🔐 Multi-tenancy

A aplicação foi estruturada para trabalhar com múltiplas organizações.

O banco utiliza políticas de Row Level Security nas estruturas tenant-aware e o repositório possui testes de isolamento como parte dos mecanismos de validação.

---

## 🖥️ Principais áreas da aplicação

| Área | Recursos |
|---|---|
| **Atendimento** | Inbox · Radar · Respostas rápidas |
| **CRM** | Kanban · Contatos · Leads · Funis |
| **IA** | Agentes · Follow-ups · Roteadores · Conhecimento · Memória · Skills · Casos · Alertas · Propostas · Execuções |
| **Canais** | Conexões WhatsApp · Meta Cloud API · Webhooks |
| **Análise** | Desempenho · Métricas · Evolução da IA · Audit Log |
| **Organização** | Equipe · Distribuição · Configurações · LGPD · API Tokens · Segurança |

A disponibilidade exata de determinados recursos pode depender das integrações configuradas na instalação.

---

## 🧱 Stack

| Camada | Tecnologia |
|---|---|
| **Frontend / Backend Web** | Next.js 16 App Router |
| **UI** | React 19 |
| **Linguagem** | TypeScript |
| **Estilos** | Tailwind CSS + shadcn/ui |
| **Banco** | Supabase / PostgreSQL |
| **Autenticação** | Supabase Auth |
| **Realtime** | Supabase Realtime |
| **Storage** | Supabase Storage |
| **WhatsApp** | WAHA + Meta Cloud API |
| **Filas / Jobs** | event log + workers |
| **Cache / Rate Limit** | Redis / Upstash |
| **IA** | Vercel AI SDK + provedores configuráveis |
| **Validação** | Zod |
| **Observabilidade** | Sentry opcional |
| **Testes** | Vitest + Playwright |
| **Deploy** | Docker |

Para detalhes da arquitetura, consulte [`ARCHITECTURE.md`](ARCHITECTURE.md).

---

## ⚡ Instalação

Clone o repositório:

```bash
git clone https://github.com/hudsonlcustodio/imobitalk.git
cd imobitalk
Instalação self-host

O repositório possui ferramentas para instalação em uma VPS com Docker.

bash hostgator-setup-kit/install.sh

Antes de utilizar o instalador em produção, consulte:

hostgator-setup-kit/README.md
DEPLOYMENT-IMOBI.md
PRODUCTION-READINESS.md
RUNBOOK-IMOBI.md
Requisitos externos

Dependendo dos recursos utilizados, a instalação pode exigir:

Serviço	Finalidade
VPS com Docker	Execução da aplicação e serviços
Domínio	Acesso HTTPS
Supabase/PostgreSQL	Banco, autenticação e storage
Redis	Cache, rate limiting e recursos operacionais
WAHA ou Meta Cloud API	WhatsApp
Provedor de IA	Recursos de inteligência artificial
Sentry	Observabilidade opcional

Credenciais reais não devem ser armazenadas no repositório.

Utilize os arquivos .env*.example como referência para configuração.

🔄 Atualização

A instalação self-host possui scripts para operações de atualização e manutenção.

Entre eles:

Script	Função
install.sh	Instalação
update.sh	Atualização
backup.sh	Backup
restore.sh	Restauração
reset-password.sh	Redefinição de senha
reset-mfa.sh	Reset de MFA
healthcheck.sh	Diagnóstico dos serviços

Antes de atualizar um ambiente produtivo, faça backup e consulte a documentação da versão.

Documentação adicional:

docs/ATUALIZANDO.md

Importante: backup existente não significa recuperação comprovada. Para ambientes críticos, teste periodicamente o processo de restore.

🧑‍💻 Desenvolvimento

Para desenvolvimento local:

git clone https://github.com/hudsonlcustodio/imobitalk.git
cd imobitalk

corepack enable
pnpm install --frozen-lockfile

cp .env.example .env.local

pnpm dev

Aplicação local:

http://localhost:3000

Health check:

http://localhost:3000/api/v1/health

Consulte docs/SETUP.md para configuração das integrações necessárias ao ambiente de desenvolvimento.

🗄️ Banco de dados

O projeto utiliza PostgreSQL/Supabase.

Antes de qualquer alteração de banco em ambiente compartilhado ou produtivo, revise as migrations e faça backup.

Quando disponíveis no estado atual do projeto, utilize os scripts de validação antes de aplicar migrations:

pnpm db:migrate:check

Para aplicar a migration no ambiente explicitamente configurado:

pnpm db:migrate

Nunca execute migrations de produção sem confirmar a conexão de destino.

📁 Estrutura
imobitalk/
├── app/                    # Next.js App Router
│   ├── (admin)/            # Administração
│   ├── (public)/           # Autenticação e páginas públicas
│   ├── app/                # Aplicação autenticada
│   └── api/v1/             # API
├── components/             # Componentes React
├── lib/                    # Domínio e integrações
├── workers/                # Processamento assíncrono
├── supabase/               # Schema e migrations
├── tests/                  # Testes
├── scripts/                # Scripts operacionais
├── docs/                   # Documentação
└── hostgator-setup-kit/    # Ferramentas de self-host
🧪 Testes

O projeto possui diferentes níveis de validação.

Entre os comandos disponíveis:

pnpm typecheck
pnpm lint
pnpm test:unit
pnpm test:db
pnpm test:e2e
pnpm build

A disponibilidade de alguns testes depende de serviços auxiliares, Docker ou ambiente configurado.

O pipeline do GitHub deve ser considerado a fonte de evidência para os gates executados sobre cada revisão.

GitHub Actions

🐳 Docker

O projeto possui componentes independentes para execução da aplicação e tarefas assíncronas.

As imagens utilizadas pelo fork IMOBI incluem:

imobi-crm
imobi-worker
imobi-scheduler

Para produção, prefira imagens versionadas e imutáveis.

Evite utilizar latest como mecanismo de promoção para produção.

Consulte DEPLOYMENT-IMOBI.md.

🚀 Deploy

Antes de realizar um deploy de produção, consulte:

DEPLOYMENT-IMOBI.md
PRODUCTION-READINESS.md
SECURITY-CHECKLIST-IMOBI.md
RUNBOOK-IMOBI.md

Um build verde isoladamente não comprova readiness de produção.

Ambientes produtivos devem considerar, entre outros pontos:

secrets;
banco;
migrations;
isolamento multi-tenant;
Docker;
TLS;
health/readiness;
observabilidade;
backup;
restore;
rollback.
🔐 Segurança

Questões de segurança não devem ser abertas como issue pública quando puderem expor uma vulnerabilidade.

Consulte:

SECURITY.md

O projeto possui mecanismos relacionados a:

autenticação;
autorização;
RLS;
multi-tenancy;
MFA;
auditoria;
isolamento;
dependency scanning;
análise estática.

A existência desses mecanismos não substitui a validação da configuração do ambiente onde a aplicação será implantada.

🛡️ Privacidade e LGPD

A aplicação possui recursos relacionados a governança e tratamento de dados pessoais.

Em instalações self-host, o responsável pela infraestrutura deve avaliar suas próprias obrigações como controlador ou operador de dados conforme o contexto da operação.

O software não constitui, por si só, certificação de conformidade jurídica.

📚 Documentação
Documento	Conteúdo
README.md	Visão geral do projeto
ARCHITECTURE.md	Arquitetura
docs/SETUP.md	Ambiente de desenvolvimento
DEPLOYMENT-IMOBI.md	Deployment
PRODUCTION-READINESS.md	Gates de produção
SECURITY-CHECKLIST-IMOBI.md	Checklist de segurança
RUNBOOK-IMOBI.md	Operação e incidentes
CHANGELOG.md	Histórico de mudanças
CONTRIBUTING.md	Contribuição
SECURITY.md	Política de segurança
CODE_OF_CONDUCT.md	Código de conduta
🤝 Contribuindo

Contribuições devem preservar os requisitos de segurança, isolamento multi-tenant e compatibilidade do projeto.

Antes de abrir um PR:

Leia CONTRIBUTING.md.
Consulte AGENTS.md para convenções técnicas do repositório.
Execute os testes relevantes.
Não inclua secrets ou credenciais.
Inclua testes para alterações comportamentais.

Exemplo:

git checkout -b feat/minha-alteracao

pnpm typecheck
pnpm lint
pnpm test:unit
pnpm build

Depois abra um Pull Request para revisão.

🐛 Bugs e vulnerabilidades

Para bugs:

GitHub Issues

Para vulnerabilidades de segurança, utilize o mecanismo privado do GitHub quando habilitado:

Security Advisories

Evite publicar detalhes de vulnerabilidades exploráveis em issues públicas.

📜 Licença

Distribuído sob a licença MIT.

Consulte LICENSE para os termos completos, incluindo os avisos de copyright e atribuição que devem ser preservados quando aplicáveis.

O software é fornecido "como está", sem garantias, conforme os termos da licença.

🛟 Self-host e responsabilidade operacional

A IMOBI TALK pode ser executada em infraestrutura própria.

Nesse modelo, o operador da instalação é responsável pela configuração e operação de componentes como:

servidor;
banco de dados;
WhatsApp;
armazenamento;
credenciais;
domínio e TLS;
backup;
recuperação;
atualizações;
observabilidade.

Antes de utilizar a aplicação em ambiente produtivo, valide os gates descritos em PRODUCTION-READINESS.md.

🙏 Tecnologias e projetos

A IMOBI TALK utiliza e integra tecnologias open source e serviços de terceiros, incluindo, conforme a configuração:

Next.js
React
Supabase
WAHA
Redis
shadcn/ui
provedores de inteligência artificial
Docker

Consulte os respectivos projetos e licenças para detalhes.

<div align="center">
IMOBI TALK

CRM · Atendimento · Automação · Inteligência Artificial

Feito no Brasil para operações imobiliárias.

GitHub

</div> ```
