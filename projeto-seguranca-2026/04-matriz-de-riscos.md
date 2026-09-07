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

**Tratamento (ISO 27005):** Mitigar (aplicar controles), Transferir (compartilhar o risco — seguro/terceiros), Aceitar (risco residual assumido) ou Evitar (eliminar o processo).

# Matriz de Riscos — de acordo com a tarefa solicitada
> Matriz baseada na ISO 27005, consolidando as ameaças STRIDE do `03-modelagem-de-ameacas.md` e as vulnerabilidades (CVEs) do `02-analise-de-vulnerabilidades.md`. As opções de tratamento dialogam com o pipeline do `07-plano-devsecops.md`.

## 1. Modelagem de ameaças (DFD + STRIDE)

O DFD e o STRIDE do BDS estão no `03-modelagem-de-ameacas.md`. Esta matriz transforma as ameaças identificadas lá em riscos priorizados, cruzando probabilidade e impacto.

## 2. Escala de Probabilidade

Frequência esperada de ocorrência de cada ameaça no contexto do BDS:

| Nível | Probabilidade | Descrição (BDS) |
|---|---|---|
| 1 | Baixa | Rara — exige condições específicas (ex.: exploração de cadeia de suprimentos, 0-day com exploit complexo) |
| 2 | Média | Possível — vulnerabilidade conhecida em componente em produção, sem patch imediato aplicado |
| 3 | Alta | Frequente — ataque automatizado constante, comum no setor financeiro (bots, varreduras, phishing) |

## 3. Escala de Impacto

Dano ao negócio caso a ameaça se concretize, considerando CIA e o contexto regulatório do setor financeiro:

| Nível | Impacto | Descrição (BDS) |
|---|---|---|
| 1 | Baixo | Dano pontual e recuperável, sem afetar clientes nem a operação |
| 2 | Médio | Indisponibilidade parcial, custos moderados, retrabalho de equipe |
| 3 | Alto | Indisponibilidade do PIX/plataforma, vazamento de dados pessoais (LGPD), sanção regulatória (Banco Central), dano reputacional |

## 4. Matriz 3x3

**Nível de risco = Probabilidade × Impacto:**

| Probabilidade \ Impacto | Impacto 1 (Baixo) | Impacto 2 (Médio) | Impacto 3 (Alto) |
|---|---|---|---|
| Probabilidade 3 (Alta) | 3 | 6 | 9 |
| Probabilidade 2 (Média) | 2 | 4 | 6 |
| Probabilidade 1 (Baixa) | 1 | 2 | 3 |

Com a matriz 3x3, o maior nível possível é 9. Classificação:

| Faixa | Nível |
|---|---|
| 1 | Baixo |
| 2 | Médio |
| 3 – 4 | Alto |
| 6 e 9 | Crítico |

## 5. Riscos avaliados

| Ameaça (STRIDE) | Vulnerabilidade | Prob. | Imp. | Nível | Tratamento |
|---|---|---|---|---|---|
| Elevation of Privilege | CVE-2024-6387 (regreSSHion) — RCE remoto no OpenSSH de administração | 2 | 3 | 6 — Crítico | Mitigar: patch OpenSSH 9.8p1, segmentação de rede, chaves + MFA |
| Information Disclosure | Vazamento de dados pessoais (LGPD) — criptografia/controle de acesso insuficientes | 2 | 3 | 6 — Crítico | Mitigar: criptografia em repouso e em trânsito, controle de acesso, DLP |
| Tampering + Disclosure | CVE-2025-1094 — SQL injection no PostgreSQL (libpq) | 2 | 3 | 6 — Crítico | Mitigar: consultas parametrizadas, SAST (Semgrep), patch 17.3+/16.7+ |
| Denial of Service | Indisponibilidade da plataforma/PIX — proteção anti-DDoS insuficiente | 2 | 3 | 6 — Crítico | Mitigar: anti-DDoS, redundância, rate limiting; Transferir: seguro cibernético |
| Spoofing | CVE-2025-23419 — bypass de mTLS no nginx (retomada de sessão) | 2 | 2 | 4 — Alto | Mitigar: atualizar nginx (1.27.4+/1.26.3+), revisar session tickets |
| Repudiation | Comprometimento de logs/auditoria — trilha alterável (sem CVE específica) | 2 | 2 | 4 — Alto | Mitigar: logs imutáveis (WORM), assinatura de logs, SIEM |
| Spoofing (supply chain) | CVE-2024-3094 — backdoor xz/liblzma no SSH (cadeia de suprimentos) | 1 | 3 | 3 — Alto | Mitigar: SBOM, pin de versões, verificação de integridade |
| Elevation of Privilege | CVE-2024-21626 — escape de container no runc (fd leak) | 1 | 3 | 3 — Alto | Mitigar: atualizar runtime, seccomp/AppArmor, hardening de imagem |
| Elevation of Privilege | CVE-2021-44228 (Log4Shell) — RCE via log4j | 1 | 3 | 3 — Alto | Mitigar: patch, desativar JNDI, WAF |

## 6. Justificativas das avaliações

- **Probabilidade Média (2)** — vulnerabilidades conhecidas em componentes em produção, sem patch imediato aplicado; o setor financeiro sofre varreduras e ataques automatizados constantes.
- **Probabilidade Baixa (1)** — exigem condições específicas: exploit complexo (Log4Shell, runc), 0-day ou comprometimento de cadeia de suprimentos (xz).
- **Impacto Alto (3)** — afetam CIA de forma grave: indisponibilidade do PIX, vazamento de dados pessoais (LGPD) ou RCE no servidor.
- **Impacto Médio (2)** — dano relevante, porém recuperável: trilha de auditoria comprometida ou bypass de mTLS sem vazamento direto de dados.

## 7. Leitura da matriz

Nenhum risco ficou em nível Baixo ou Médio — esperado para uma instituição financeira, onde o impacto alto é a regra. É por isso que a priorização importa: os quatro riscos **Críticos (6)** são os primeiros a receber controles no `07-plano-devsecops.md`. O tratamento segue a ISO 27005: **Mitigar** (aplicar controles), **Transferir** (compartilhar — seguro/terceiros), **Aceitar** (assumir o risco residual) ou **Evitar** (eliminar o processo).


