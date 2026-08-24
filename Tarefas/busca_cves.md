# Busca de CVEs
_Nessa aula trabalhamos os conceitos relacionados às CVEs, agora vamos buscar vulnerabilidades ligadas ao projeto_ 

## 1. Buscar 5 CVEs reais para o seu cenário 

Acesse o NVD: [nvd.nist.gov](nvd.nist.gov)

Na barra de busca, procure por serviços ou produtos que poderiam existir no seu cenário de projeto. Por exemplo:
- Se seu cenário é um hospital: busque por "healthcare", "medical device", "EHR", "PACS"
- Se seu cenário é uma fintech: busque por "banking", "payment", "fintech", "PostgreSQL", "nginx"
- Se seu cenário é uma empresa de e-commerce: busque por "web application", "Apache", "MySQL", "WordPress"

Escolham 5 CVEs que fariam sentido no seu cenário. Para cada uma, preencham:

```
CVE: CVE-XXXX-XXXXX
Produto: [nome do produto/serviço afetado]
CVSS Base Score: [X.X]
Vetor CVSS: [AV:.../AC:.../PR:.../UI:.../S:.../C:.../I:.../A:...]
Descrição (1 frase): [o que a vulnerabilidade permite]
Conexão com meu cenário (1 frase): [por que esta CVE afetaria meu cenário]
```

## 2. Justificar a prioridade de remediação

Para cada uma das 5 CVEs, escrevam 1 parágrafo (3-5 linhas) justificando a prioridade de remediação considerando o contexto do seu cenário. Lembre-se:
- O CVSS Base Score é o ponto de partida, não a decisão final
- Considere: o ativo está exposto à internet? É crítico para o negócio? Há exploit público?
- Uma CVE com CVSS 7.5 em um serviço exposto pode ser mais urgente que uma CVSS 9.8 em um servidor interno segregado



# CVEs para o Banco Seguro
_Aqui listamos as 5 CVEs para o nosso estudo de caso_

## CVE 1 — Banco de dados
- **CVE:** CVE-2025-1094
- **Produto:** PostgreSQL (libpq/psql)
- **CVSS Base Score:** 8.1 (High)
- **Vetor CVSS:** AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H
- **Descrição:** Falha na neutralização de aspas nas funções de escape do libpq (PQescapeLiteral, PQescapeIdentifier, etc.) permite injeção de SQL em certos padrões de uso.
- **Conexão com o cenário:** O Banco Seguro usa PostgreSQL como banco central de contas e saldos; qualquer aplicação ou ferramenta que monte consultas usando essas funções de escape poderia ter o banco comprometido por SQL injection.


## CVE 2 — Proxy / TLS
- **CVE:** CVE-2025-23419
- **Produto:** nginx (TLS session resumption)
- **CVSS Base Score:** 4.3 (Medium)
- **Vetor CVSS:** AV:N/AC:L/PR:L/UI:N/S:U/C:L/I:N/A:N
- **Descrição:** Com servidores virtuais compartilhando IP e porta em TLS 1.3, um atacante pode usar retomada de sessão para burlar a autenticação por certificado de cliente (mTLS).
- **Conexão com o cenário:** O nginx do Banco Seguro atua como proxy/reverse proxy na borda; burlar a autenticação por certificado permitiria a um atacante se passar por uma integração autorizada (como parceiros do SPI/PIX).

## CVE 3 — APIs Java
- **CVE:** CVE-2021-44228 (Log4Shell)
- **Produto:** Apache Log4j2
- **CVSS Base Score:** 10.0 (Critical)
- **Vetor CVSS:** AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
- **Descrição:** Injeção via JNDI no Log4j2 permite execução remota de código (RCE) sem autenticação por meio de mensagens de log manipuladas.
- **Conexão com o cenário:** As APIs REST e o core bancário do Banco Seguro, se desenvolvidos em Java com Log4j2, ficariam expostos a RCE total na camada de aplicação.

## CVE 4 — Cadeia de suprimentos (DevSecOps)
- **CVE:** CVE-2024-3094
- **Produto:** xz utils / liblzma
- **CVSS Base Score:** 10.0 (Critical)
- **Vetor CVSS:** AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
- **Descrição:** Backdoor inserido nas versões 5.6.0 e 5.6.1 do xz intercepta a autenticação do sshd, permitindo acesso não autorizado aos servidores.
- **Conexão com o cenário:** Como backdoor de cadeia de suprimentos, afeta a infraestrutura Linux e o pipeline CI/CD do Banco Seguro, podendo comprometer o acesso SSH aos servidores em nuvem (AWS).

## CVE 5 — Nuvem / containers
- **CVE:** CVE-2024-21626
- **Produto:** runc
- **CVSS Base Score:** 8.6 (High)
- **Vetor CVSS:** AV:L/AC:L/PR:N/UI:R/S:C/C:H/I:H/A:H
- **Descrição:** Vazamento de file descriptors no runc permite que um processo de container escape para o filesystem do host.
- **Conexão com o cenário:** O Banco Seguro roda serviços em containers na AWS (ECS/EKS); um escape de container poderia dar ao atacante acesso ao host e, daí, a outros serviços da plataforma.

## 2. Justificativa de prioridade de remediação
- **CVE-2025-1094 (PostgreSQL, 8.1):** Prioridade **alta**. Embora o CVSS seja 8.1 e o vetor exija complexidade de ataque alta (AC:H), o PostgreSQL é o ativo mais crítico do Banco Seguro — se comprometido, o negócio para. Além disso, a CVE já foi explorada em ataques reais (BeyondTrust, Tesouro dos EUA), o que indica risco real de exploração. Como o banco pode estar exposto via APIs internas, a correção deve ser imediata, atualizando para as versões corrigidas (17.3+, 16.7+, 15.11+).
- **CVE-2025-23419 (nginx, 4.3):** Prioridade **média**, apesar do score baixo. O CVSS é 4.3 porque exige privilégio prévio (PR:L) e impacto limitado (C:L). Porém, o nginx está na borda da rede, exposto à internet, e a falha afeta justamente o **mTLS** que protege as integrações com parceiros (SPI/PIX). Como a exploração depende de um atacante já autenticado, a urgência é menor que a do banco, mas a correção deve entrar no próximo ciclo de manutenção, pois o impacto reputacional de uma integração falsa é alto.
- **CVE-2021-44228 (Log4Shell, 10.0):** Prioridade **crítica**. Score máximo, exploração remota sem autenticação (AV:N, PR:N) e **exploit público amplamente conhecido**. Se qualquer API Java do Banco Seguro usar Log4j2 vulnerável, a plataforma inteira pode ser tomada por RCE. É a CVE mais urgente do conjunto: deve ser corrigida imediatamente, com varredura de dependências em todo o código (SAST/SCA) para garantir que nenhuma versão vulnerável permaneça.
- **CVE-2024-3094 (xz, 10.0):** Prioridade **alta**, mas com nuance. O score 10.0 reflete o potencial de comprometimento total do SSH. No entanto, as versões afetadas (5.6.0/5.6.1) foram publicadas por pouco tempo e a maioria das distribuições já as removeu. A prioridade aqui é **preventiva e de processo**: confirmar que nenhum servidor do Banco Seguro usa essas versões e reforçar a verificação de integridade de dependências no pipeline DevSecOps, pois o risco real é de cadeia de suprimentos, não de exposição direta.
- **CVE-2024-21626 (runc, 8.6):** Prioridade **média-alta**. O vetor exige acesso local (AV:L) e interação do usuário (UI:R), então não é explorável remotamente por si só — depende de o atacante já ter código em execução dentro de um container. Ainda assim, em um ambiente de containers na AWS, um escape dá acesso ao host e a toda a plataforma, quebrando o isolamento (defesa em profundidade). Deve ser corrigida na atualização do runtime de containers, priorizada após as CVEs de exploração remota.

## Resumo e análise (não é um entregável solicitado)
| CVE | CVSS Base |	Temporal Score |	Environmental Score	| Score Final |
|---|---|----|---|---
| CVE-2021-44228 (Log4j2) |	10.0 — Crítica	|9.6 — Crítica	|9.6 — Crítica	|9.6 — Crítica
|CVE-2024-3094 (xz utils)	|10.0 — Crítica	|9.4 — Crítica	|9.0 — Crítica	|9.0 — Crítica
|CVE-2024-21626 (runc)	|8.6 — Alta	|7.8 — Alta	|7.8 — Alta	|7.8 — Alta
|CVE-2025-1094 (PostgreSQL)	|8.1 — Alta	|7.6 — Alta	|7.0 — Alta	|7.0 — Alta
|CVE-2025-23419 (nginx)	|4.3 — Média	|3.9 — Baixa	|3.9 — Baixa	|3.9 — Baixa


- CVE-2021-44228 (Log4Shell) 
    - Base 10.0 
    - Temporal 9.6 
    - Environmental 9.6
    - Vetor temporal: `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H/E:H/RL:O/RC:C`. O temporal reduz pouco (10.0 → 9.6) porque o exploit é **maduro e massivo** (E:H) — dezenas de PoCs e exploração ativa desde dez/2021 —, mas há **fix oficial** (RL:O, Log4j 2.17.1+). 
    - O ambiental mantém 9.6: as APIs Java do internet banking estão **expostas à internet** (MAV:N) e o impacto é RCE total. Continua crítica.
- CVE-2024-3094 (xz utils) 
    - Base 10.0
    - Temporal 9.4 
    - Environmental 9.0
    - Vetor temporal: `.../E:F/RL:O/RC:C`. O backdoor era **funcional** (E:F) nas versões 5.6.0/5.6.1, mas as distribuições **removeram oficialmente** as versões maliciosas (RL:O). 
    - O ambiental cai para 9.0 porque o SSH dos servidores na AWS **não está exposto à internet** (MAV:A — acesso restrito a rede interna/VPN). Continua crítica, mas a mitigação de rede reduz a urgência relativa.
- CVE-2024-21626 (runc) 
    - Base 8.6 
    - Temporal 7.8 
    - Environmental 7.8**
    - Vetor temporal: `.../E:P/RL:O/RC:C`. Há **PoC público** (E:P, "Leaky Vessels") e **fix oficial** (RL:O, runc 1.1.12). 
    - O ambiental mantém 7.8: apesar de exigir **acesso local** (MAV:L, não explorável remotamente), um escape de container na AWS comprometeria o host e toda a plataforma — por isso não cai mais.
- CVE-2025-1094 (PostgreSQL) 
    - Base 8.1
    - Temporal 7.6
    - Environmental 7.0**
    - Vetor temporal: `.../E:F/RL:O/RC:C`. O exploit é **funcional** (E:F — foi explorada em ataques reais a BeyondTrust e ao Tesouro dos EUA em 2025) e há **fix oficial** (RL:O, PostgreSQL 17.3+/16.7+/15.11+). 
    - O ambiental cai para 7.0: o banco de dados **não está exposto à internet** (MAV:A, rede interna) e o patch já existe. 
    - **Atenção:** o score caiu, mas o PostgreSQL continua sendo o ativo mais crítico do negócio — o julgamento qualitativo pode mantê-lo à frente do runc na fila de remediação.
- CVE-2025-23419 (nginx) 
    - Base 4.3
    - Temporal 3.9
    - Environmental 3.9
    - Vetor temporal: `.../E:P/RL:O/RC:C`. Há **PoC/análises públicas** (E:P) e **fix oficial** (RL:O, nginx 1.27.4+/1.26.3+). 
    - O ambiental não muda: o nginx **já é exposto à internet** no vetor base (AV:N), então o ambiente não altera nada. O que mantém o score baixo é o **impacto limitado** (apenas leitura de baixa confidencialidade, sem integridade/disponibilidade) e a exigência de privilégio prévio (PR:L).
