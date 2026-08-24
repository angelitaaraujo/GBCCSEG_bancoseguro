# Análise de Vulnerabilidades — Banco Digital Seguro (BDS)

> Documento que consolida a tarefa **Busca de CVEs** e a **parte 2 da tarefa de DevSecOps**. Os serviços e achados derivam dos ativos do `01-cenario-e-ativos.md` e alimentam a matriz de riscos (`04-matriz-de-riscos.md`) e o pipeline do `07-plano-devsecops.md`.

## 1. Ferramenta de Scan Selecionada

**Ferramenta:** nmap

**Justificativa:** O Banco Seguro mantém serviços expostos na internet (nginx e APIs) e serviços internos (PostgreSQL e SSH) na nuvem AWS. O nmap permite mapear portas, serviços e versões de forma rápida — a base para correlacionar com CVEs e priorizar a remediação. É leve, gratuito e o ponto de partida do ciclo de gestão de vulnerabilidades, antecedendo scans completos como o OpenVAS.

## 2. Serviços Identificados (simulados para o meu cenário)

| Serviço | Versão | CVE encontrada | CVSS | Prioridade |
|---|---|---|---|---|
| nginx (reverse proxy) | 1.26.2 | CVE-2025-23419 | 4.3 | Média |
| Apache Log4j2 (APIs Java) | 2.14.1 | CVE-2021-44228 | 10.0 | Crítica |
| PostgreSQL (banco de dados) | 16.6 | CVE-2025-1094 | 8.1 | Alta |
| OpenSSH (acesso administrativo) | 9.6p1 | CVE-2024-6387 | 8.1 | Alta |
| runc (runtime de containers) | 1.1.11 | CVE-2024-21626 | 8.6 | Alta |
| xz utils / liblzma (biblioteca) | 5.6.1 | CVE-2024-3094 | 10.0 | Crítica |

**Origem dos achados:** nginx, PostgreSQL e OpenSSH foram identificados pelo scan de rede (nmap). Log4j2, runc e xz foram identificados na varredura de dependências e imagens de container (Trivy), no build do pipeline DevSecOps. As versões são simuladas como vulneráveis para fins didáticos; todas as CVEs são reais (NVD). O achado do OpenSSH (CVE-2024-6387) é uma descoberta adicional do scan, além das 5 CVEs exigidas na tarefa Busca de CVEs — mas não poderia ficar de fora, por ser RCE remoto sem autenticação no acesso administrativo.

## 3. CVEs identificadas — Tarefa "Busca de CVEs"

### CVE 1 — Banco de dados
- **CVE:** CVE-2025-1094
- **Produto:** PostgreSQL (libpq/psql)
- **CVSS Base Score:** 8.1 (High)
- **Vetor CVSS:** AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H
- **Descrição (1 frase):** Falha na neutralização de aspas nas funções de escape do libpq (PQescapeLiteral, PQescapeIdentifier, PQescapeString, PQescapeStringConn) permite injeção de SQL em certos padrões de uso.
- **Conexão com meu cenário (1 frase):** O Banco Seguro usa PostgreSQL como banco central de contas e saldos; qualquer aplicação ou ferramenta que monte consultas usando essas funções de escape poderia ter o banco comprometido por SQL injection.

### CVE 2 — Proxy / TLS
- **CVE:** CVE-2025-23419
- **Produto:** nginx (TLS session resumption)
- **CVSS Base Score:** 4.3 (Medium)
- **Vetor CVSS:** AV:N/AC:L/PR:L/UI:N/S:U/C:L/I:N/A:N
- **Descrição (1 frase):** Com servidores virtuais compartilhando IP e porta em TLS 1.3, um atacante pode usar retomada de sessão para burlar a autenticação por certificado de cliente (mTLS).
- **Conexão com meu cenário (1 frase):** O nginx do Banco Seguro atua como proxy/reverse proxy na borda; burlar a autenticação por certificado permitiria a um atacante se passar por uma integração autorizada (como parceiros do SPI/PIX).

### CVE 3 — APIs Java
- **CVE:** CVE-2021-44228 (Log4Shell)
- **Produto:** Apache Log4j2
- **CVSS Base Score:** 10.0 (Critical)
- **Vetor CVSS:** AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
- **Descrição (1 frase):** Injeção via JNDI no Log4j2 permite execução remota de código (RCE) sem autenticação por meio de mensagens de log manipuladas.
- **Conexão com meu cenário (1 frase):** As APIs REST e o core bancário do Banco Seguro, se desenvolvidos em Java com Log4j2, ficariam expostos a RCE total na camada de aplicação.

### CVE 4 — Cadeia de suprimentos
- **CVE:** CVE-2024-3094
- **Produto:** xz utils / liblzma
- **CVSS Base Score:** 10.0 (Critical)
- **Vetor CVSS:** AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
- **Descrição (1 frase):** Backdoor inserido nas versões 5.6.0 e 5.6.1 do xz intercepta a autenticação do sshd, permitindo acesso não autorizado aos servidores.
- **Conexão com meu cenário (1 frase):** Como backdoor de cadeia de suprimentos, afeta a infraestrutura Linux e o pipeline CI/CD do Banco Seguro, podendo comprometer o acesso SSH aos servidores em nuvem (AWS).

### CVE 5 — Nuvem / containers
- **CVE:** CVE-2024-21626
- **Produto:** runc
- **CVSS Base Score:** 8.6 (High)
- **Vetor CVSS:** AV:L/AC:L/PR:N/UI:R/S:C/C:H/I:H/A:H
- **Descrição (1 frase):** Vazamento de file descriptors no runc permite que um processo de container escape para o filesystem do host.
- **Conexão com meu cenário (1 frase):** O Banco Seguro roda serviços em containers na AWS (ECS/EKS); um escape de container poderia dar ao atacante acesso ao host e, daí, a outros serviços da plataforma.

## 4. Prioridade de remediação

**CVE-2025-1094 (PostgreSQL, 8.1) — Prioridade alta.** Embora o CVSS seja 8.1 e o vetor exija complexidade de ataque alta (AC:H), o PostgreSQL é o ativo mais crítico do Banco Seguro — se comprometido, o negócio para. A CVE já foi explorada em ataques reais (BeyondTrust, Tesouro dos EUA), o que indica risco concreto de exploração. Como o banco pode estar exposto via APIs internas, a correção deve ser imediata, atualizando para as versões corrigidas (17.3+, 16.7+, 15.11+).

**CVE-2025-23419 (nginx, 4.3) — Prioridade média.** O CVSS é baixo porque exige privilégio prévio (PR:L) e impacto limitado (C:L). Porém, o nginx está na borda da rede, exposto à internet, e a falha afeta justamente o mTLS que protege as integrações com parceiros (SPI/PIX). Como a exploração depende de um atacante já autenticado, a urgência é menor que a do banco, mas a correção deve entrar no próximo ciclo de manutenção, pois o impacto reputacional de uma integração falsa é alto.

**CVE-2021-44228 (Log4Shell, 10.0) — Prioridade crítica.** Score máximo, exploração remota sem autenticação (AV:N, PR:N) e exploit público amplamente conhecido. Se qualquer API Java do Banco Seguro usar Log4j2 vulnerável, a plataforma inteira pode ser tomada por RCE. É a CVE mais urgente do conjunto: deve ser corrigida imediatamente, com varredura de dependências em todo o código (SAST/SCA) para garantir que nenhuma versão vulnerável permaneça.

**CVE-2024-3094 (xz, 10.0) — Prioridade alta, preventiva.** O score 10.0 reflete o potencial de comprometimento total do SSH. No entanto, as versões afetadas (5.6.0/5.6.1) foram publicadas por pouco tempo e a maioria das distribuições já as removeu. A prioridade aqui é de processo: confirmar que nenhum servidor do Banco Seguro usa essas versões e reforçar a verificação de integridade de dependências no pipeline DevSecOps, pois o risco real é de cadeia de suprimentos, não de exposição direta.

**CVE-2024-21626 (runc, 8.6) — Prioridade média-alta.** O vetor exige acesso local (AV:L) e interação do usuário (UI:R), então não é explorável remotamente por si só — depende de o atacante já ter código em execução dentro de um container. Ainda assim, em um ambiente de containers na AWS, um escape dá acesso ao host e a toda a plataforma, quebrando o isolamento (defesa em profundidade). Deve ser corrigida na atualização do runtime de containers, priorizada após as CVEs de exploração remota.

> Achado adicional do scan: **CVE-2024-6387 (OpenSSH, 8.1)** — RCE remoto sem autenticação em sshd (glibc). Também de prioridade alta, com patch disponível em 9.8p1; deve ser tratada junto ao PostgreSQL na primeira janela de manutenção.

## 5. Análise complementar — Temporal e Environmental

O **CVSS Base** é o ponto de partida, não a decisão final. O **Temporal Score** ajusta o risco conforme a evolução da ameaça (exploit disponível, correção publicada, confiança no relato). O **Environmental Score** ajusta ao contexto do Banco Seguro (exposição real do ativo e criticidade para o negócio financeiro). O **Score Final** é o Environmental, que já incorpora ambos — é ele que deve orientar a priorização.

| CVE | CVSS Base | Temporal Score | Environmental Score | Score Final |
|---|---|---|---|---|
| CVE-2021-44228 (Log4j2) | 10.0 — Crítica | 9.6 — Crítica | 9.6 — Crítica | 9.6 — Crítica |
| CVE-2024-3094 (xz utils) | 10.0 — Crítica | 9.4 — Crítica | 9.0 — Crítica | 9.0 — Crítica |
| CVE-2024-21626 (runc) | 8.6 — Alta | 7.8 — Alta | 7.8 — Alta | 7.8 — Alta |
| CVE-2025-1094 (PostgreSQL) | 8.1 — Alta | 7.6 — Alta | 7.0 — Alta | 7.0 — Alta |
| CVE-2025-23419 (nginx) | 4.3 — Média | 3.9 — Baixa | 3.9 — Baixa | 3.9 — Baixa |

O que explica cada variação: o Log4Shell mantém 9.6 (exploit massivo, E:H, e fix oficial); o xz cai para 9.0 (versões maliciosas já removidas pelas distribuições e SSH restrito à rede interna, MAV:A); o runc mantém 7.8 (escape exige acesso local, mas quebraria o isolamento na AWS); o PostgreSQL cai para 7.0 (banco não exposto à internet, MAV:A, e patch oficial), mas segue sendo o ativo mais crítico do negócio — o julgamento qualitativo pode mantê-lo à frente na fila; o nginx cai para 3.9 (impacto limitado e privilégio prévio), apesar de estar na borda. Para reproduzir, use a calculadora CVSS v3.1 do NVD com as premissas: setor financeiro (CIA altos), PostgreSQL/SSH internos (MAV:A), APIs/nginx expostos (MAV:N), runc local (MAV:L).

## 6. Conexão com o portfólio

Os ativos críticos do `01-cenario-e-ativos.md` (PostgreSQL, APIs REST, nginx, nuvem AWS, integrações externas) se materializam aqui como serviços concretos com CVEs reais. Os achados alimentam a matriz de riscos (`04-matriz-de-riscos.md`) e dialogam com o pipeline DevSecOps (`07-plano-devsecops.md`): Semgrep e Gitleaks no commit, Trivy no build (origem dos achados Log4j2, runc e xz), OWASP ZAP no staging e nmap/OpenVAS na operação (origem dos achados nginx, PostgreSQL e OpenSSH).