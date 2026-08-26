# Matriz de Riscos — Banco Digital Seguro (BDS)

> Matriz baseada na ISO 27005, consolidando as ameaças STRIDE do `03-modelagem-de-ameacas.md` e as vulnerabilidades (CVEs) do `02-analise-de-vulnerabilidades.md`. As opções de tratamento dialogam com o pipeline do `07-plano-devsecops.md`.

## 1. Metodologia

Escala qualitativa de **Probabilidade** (frequência esperada de ocorrência) e **Impacto** (dano ao negócio, considerando CIA e contexto regulatório do setor financeiro):

| Escala | Probabilidade | Impacto |
|---|---|---|
| 1 | Baixo | Baixo |
| 2 | Médio | Médio |
| 3 | Alto | Alto |

**Nível de risco = Probabilidade × Impacto**:


Lembre-se que, utilizando uma matriz 3x3, o maior valor de nível será 9, neste caso o nível de risco será

| Faixa | Nível |
| --- | --- |
|  1  | Baixo |
|2 | Médio |
|3 - 4| Alto  |
| 6 e 9  | Crítico |

> Atenção, sugestão usar este modelo no seu projeto, preenchendo a planilha disponível em [AQUI](https://ifcedubr-my.sharepoint.com/:x:/g/personal/angelita_araujo_ifc_edu_br/IQAR2iUfihiDR7spR15Jc8R0ASEwju2n8VKmE8XeBxT2zZ4)

Se você usar uma matriz 5 x 5, dependendo do seu nível de maturidade, pode usar a seguinte tabela

| Faixa | Nível |
|---|---|
| 1–4 | Baixo |
| 5–9 | Médio |
| 10–14 | Alto |
| 15–25 | Crítico |

## 2. Matriz de Riscos

| Ameaça (STRIDE) | Vulnerabilidade | Probabilidade | Impacto | Nível de risco | Tratamento |
|---|---|---|---|---|---|
| Elevation of Privilege / Tampering | CVE-2021-44228 (Log4Shell) — RCE remoto nas APIs Java e core bancário | Alto (3) | Alto (3) |  |  |
| Elevation of Privilege | CVE-2024-6387 (regreSSHion) — RCE remoto no OpenSSH admin | Médio (2) | Alto (3) |  |  |
| Information Disclosure | Vazamento de dados pessoais (LGPD) — criptografia/controle de acesso insuficientes |  |  |
| Tampering / Information Disclosure | CVE-2025-1094 — SQL injection no PostgreSQL (libpq) | Médio (2) | Alto (3) |  |  |
| Denial of Service | Indisponibilidade da plataforma/PIX — proteção anti-DDoS insuficiente | Médio (2) | Alto (3) |  |  |
| Spoofing (supply chain) | CVE-2024-3094 — backdoor xz/liblzma no SSH (cadeia de suprimentos) | Baixo (1) | Alto (3) |  |  |
| Spoofing | CVE-2025-23419 — bypass de mTLS no nginx (retomada de sessão) | Médio (2) | Médio (2) |  |  |
| Repudiation | Comprometimento de logs/auditoria — trilha alterável (sem CVE específica) | Médio (2) |  |  |
| Elevation of Privilege | CVE-2024-21626 — escape de container no runc (fd leak) | Baixo (1) | Alto (3) |  |  |
