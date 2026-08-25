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
| Elevation of Privilege / Tampering | CVE-2021-44228 (Log4Shell) — RCE remoto nas APIs Java e core bancário | Provável (4) | Catastrófico (5) | **Crítico (20)** | Mitigar — patch imediato (Log4j 2.17.1+), WAF, SCA no build, monitoramento |
| Elevation of Privilege | CVE-2024-6387 (regreSSHion) — RCE remoto no OpenSSH admin | Possível (3) | Catastrófico (5) | **Crítico (15)** | Mitigar — patch OpenSSH 9.8p1+, segmentação, chaves + MFA |
| Information Disclosure | Vazamento de dados pessoais (LGPD) — criptografia/controle de acesso insuficientes | Possível (3) | Catastrófico (5) | **Crítico (15)** | Mitigar + Transferir — criptografia AES, anonimização, controle de acesso; seguro cibernético |
| Tampering / Information Disclosure | CVE-2025-1094 — SQL injection no PostgreSQL (libpq) | Possível (3) | Maior (4) | **Alto (12)** | Mitigar — patch 17.3+/16.7+, consultas parametrizadas (SAST), banco em rede interna |
| Denial of Service | Indisponibilidade da plataforma/PIX — proteção anti-DDoS insuficiente | Possível (3) | Maior (4) | **Alto (12)** | Mitigar + Transferir — redundância multi-AZ, WAF/anti-DDoS gerenciado |
| Spoofing (supply chain) | CVE-2024-3094 — backdoor xz/liblzma no SSH (cadeia de suprimentos) | Improvável (2) | Catastrófico (5) | **Alto (10)** | Mitigar — verificação de integridade de dependências, SBOM, pin de versões |
| Spoofing | CVE-2025-23419 — bypass de mTLS no nginx (retomada de sessão) | Possível (3) | Moderado (3) | **Médio (9)** | Mitigar — atualizar nginx (1.27.4+/1.26.3+), revisar session tickets/cache |
| Repudiation | Comprometimento de logs/auditoria — trilha alterável (sem CVE específica) | Possível (3) | Moderado (3) | **Médio (9)** | Mitigar — logs imutáveis (append-only/WORM), centralização, monitoramento |
| Elevation of Privilege | CVE-2024-21626 — escape de container no runc (fd leak) | Improvável (2) | Maior (4) | **Médio (8)** | Mitigar — patch do runtime (1.1.12+), seccomp/AppArmor, hardening de imagem |

## 3. Detalhamento do tratamento

**Críticos — ação imediata (primeiras 24–72h):**
- **Log4Shell (20):** atualizar Log4j em todas as APIs e no core; bloquear payloads JNDI no WAF; varrer dependências (Trivy) até zerar ocorrências.
- **regreSSHion (15):** atualizar OpenSSH para 9.8p1+ nos servidores de administração; restringir SSH a rede interna/VPN.
- **Vazamento LGPD (15):** reforçar criptografia em repouso (AES) e controle de acesso; revisar anonimização; acionar seguro cibernético como transferência do risco residual.

**Altos — primeira janela de manutenção (até 30 dias):**
- **PostgreSQL (12):** aplicar patch (17.3+/16.7+/15.11+); corrigir consultas vulneráveis detectadas no SAST; manter banco fora da internet.
- **DoS (12):** ativar proteção anti-DDoS gerenciada e redundância multi-AZ no load balancer.
- **xz (10):** confirmar ausência das versões 5.6.0/5.6.1; adotar SBOM e verificação de assinaturas no pipeline (processo contínuo).

**Médios — ciclo normal de manutenção:**
- **nginx (9):** atualizar para 1.27.4+/1.26.3+; revisar configuração de session tickets nos vhosts default.
- **Logs (9):** implementar armazenamento append-only e alertas de tentativa de alteração/apagamento.
- **runc (8):** atualizar runtime dos containers (1.1.12+); aplicar seccomp/AppArmor e hardening de imagem.

Nenhum risco foi **evitado** (todos os serviços são essenciais ao negócio) nem **aceito** integralmente — os riscos residuais pós-mitigação (ex.: vulnerabilidades não cobertas por patch) podem ser aceitos com registro formal e reavaliação semestral.

## 4. Priorização (mapa de calor)

- **Zona crítica (15–25):** Log4Shell, regreSSHion, vazamento LGPD — 3 riscos que exigem resposta imediata e bloqueiam outras entregas.
- **Zona alta (10–14):** SQLi no PostgreSQL, DoS, backdoor xz — tratados na primeira janela de manutenção.
- **Zona média (5–9):** bypass mTLS, comprometimento de logs, escape de container — ciclo normal, com monitoramento contínuo.

## 5. Conexão com o portfólio

Os riscos derivam das ameaças STRIDE (`03`) e das CVEs (`02`); as mitigações usam as ferramentas do pipeline DevSecOps (`07` — Semgrep, Trivy, WAF, OpenVAS/nmap). Os riscos **críticos e altos** alimentam diretamente a política de segurança (`05`), o mapa de conformidade (`06` — LGPD, PCI-DSS, BC) e o plano de resposta a incidentes (`08`), que tratará os cenários de maior impacto.