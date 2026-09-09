---
impacto: instalacao
secao: corrigido
titulo: Instalador detecta os nomes reais das portas do Traefik
---

O instalador deixa de presumir `web` e `websecure` quando a hospedagem usa outros
nomes, como `http` e `https`. Os valores declarados manualmente continuam tendo
prioridade.
