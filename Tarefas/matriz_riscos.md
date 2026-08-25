# Matriz de Riscos — Banco Digital Seguro (BDS)

> Matriz baseada na ISO 27005, consolidando as ameaças STRIDE do `03-modelagem-de-ameacas.md` e as vulnerabilidades (CVEs) do `02-analise-de-vulnerabilidades.md`. As opções de tratamento dialogam com o pipeline do `07-plano-devsecops.md`.

## 1. Metodologia

Escala qualitativa de **Probabilidade** (frequência esperada de ocorrência) e **Impacto** (dano ao negócio, considerando CIA e contexto regulatório do setor financeiro):

| Escala | Probabilidade | Impacto |
|---|---|---|
| 1 | Rara | Insignificante |
| 2 | Improvável | Menor |
| 3 | Possível | Moderado |
| 4 | Provável | Maior |
| 5 | Quase certa | Catastrófico |

**Nível de risco = Probabilidade × Impacto** (matriz 5x5):

| Faixa | Nível |
|---|---|
| 1–4 | Baixo |
| 5–9 | Médio |
| 10–14 | Alto |
| 15–25 | Crítico |

**Tratamento (ISO 27005):** Mitigar (aplicar controles), Transferir (compartilhar o risco — seguro/terceiros), Aceitar (risco residual assumido) ou Evitar (eliminar o processo).

## 2. Matriz de Riscos

| Ameaça (STRIDE) | Vulnerabilidade | Probabilidade | Impacto | Nível de risco | Tratamento |
|---|---|---|---|---|---|
| Elevation of Privilege / Tampering | CVE-2021-44228 (Log4Shell) — RCE remoto nas APIs Java e core bancário |  |  |  | 
| Elevation of Privilege | CVE-2024-6387 (regreSSHion) — RCE remoto no OpenSSH admin |  |  |  | 
| Information Disclosure | Vazamento de dados pessoais (LGPD) — criptografia/controle de acesso insuficientes |  |  |  | 
| Tampering / Information Disclosure | CVE-2025-1094 — SQL injection no PostgreSQL (libpq) ||  |  |  | 
| Denial of Service | Indisponibilidade da plataforma/PIX — proteção anti-DDoS insuficiente |  |  |  | 
| Spoofing (supply chain) | CVE-2024-3094 — backdoor xz/liblzma no SSH (cadeia de suprimentos) |  |  |  | 
| Spoofing | CVE-2025-23419 — bypass de mTLS no nginx (retomada de sessão) |  |  |  |  | 
| Repudiation | Comprometimento de logs/auditoria — trilha alterável (sem CVE específica) |  |  |  | 
| Elevation of Privilege | CVE-2024-21626 — escape de container no runc (fd leak) |  |  |  | 