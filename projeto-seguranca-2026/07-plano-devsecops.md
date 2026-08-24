# Plano DevSecOps — Banco Digital Seguro (BDS)

> Plano que consolida a tarefa de DevSecOps e conversa com o `02-analise-de-vulnerabilidades.md`: as ferramentas escolhidas aqui são as mesmas que deram origem aos achados da análise de vulnerabilidades (Trivy, nmap) e alimentam a matriz de riscos (`04-matriz-de-riscos.md`).

## 1. Visão geral

O Banco Seguro adota **security by design**: a segurança está presente em todas as etapas, do código à operação. O plano DevSecOps da AngelCorp cobre dois escopos:

- **Desenvolvimento**: pipeline de CI/CD com análise estática (SAST), varredura de dependências (SCA), detecção de segredos e testes dinâmicos (DAST).
- **Operações**: hardening de infraestrutura na AWS, segmentação de rede, scans contínuos de vulnerabilidades e monitoramento.

O objetivo é **detectar o mais cedo possível e corrigir antes da produção**: quanto mais à esquerda no pipeline, mais barato e seguro é o processo.

## 2. Ferramentas de Análise de Vulnerabilidades

| Etapa do pipeline | Ferramenta | Para quê | Frequência |
|---|---|---|---|
| Commit | Semgrep (SAST) + Gitleaks (secrets) | Análise estática do código-fonte para detectar SQLi, XSS e quebras de autenticação antes do merge; Gitleaks bloqueia credenciais e chaves vazadas no repositório | A cada commit / Pull Request |
| Build | Trivy (SCA) | Varredura de dependências e imagens de container por CVEs conhecidas (ex.: Log4j, xz) antes de gerar os artefatos | A cada build |
| Staging | OWASP ZAP (DAST) + Nikto | Testes dinâmicos na aplicação em execução (SQLi, XSS, configuração do servidor web) em ambiente controlado, antes de produção | A cada deploy em staging e diariamente |
| Produção/Operação | OpenVAS (gestão) + nmap (rede) | Scans agendados de vulnerabilidades na plataforma completa e mapeamento contínuo dos serviços expostos na borda (AWS) | Semanal e a cada mudança de rede |

## 3. Justificativa das escolhas

- **Semgrep (Commit)**: análise estática leve e rápida, adequada para rodar a cada PR sem atrasar o fluxo; cobre as classes do OWASP Top 10 no código das APIs.
- **Gitleaks (Commit)**: evita que credenciais, chaves de API e tokens (ex.: chaves AWS, credenciais do SPI) cheguem ao repositório — proteção essencial para as integrações externas.
- **Trivy (Build)**: varre dependências e imagens de container; foi a origem dos achados Log4j2 (CVE-2021-44228), xz (CVE-2024-3094) e runc (CVE-2024-21626) documentados no 02.
- **OWASP ZAP + Nikto (Staging)**: testes dinâmicos na aplicação em execução, em ambiente controlado, replicando o cenário de um atacante contra as APIs e o internet banking antes de ir a produção.
- **OpenVAS + nmap (Produção)**: gestão completa de vulnerabilidades com scans agendados; o nmap mapeia os serviços expostos (nginx, PostgreSQL, OpenSSH) que originaram os achados do 02.

## 4. Operações (escopo de infraestrutura)

- **Hardening AWS**: VPC com sub-redes segmentadas (pública para o load balancer/WAF, privada para aplicação e banco), security groups com princípio do menor privilégio.
- **Gerenciamento de patches**: janela de atualização mensal para SO e serviços; correção imediata para CVEs com exploit público (ex.: Log4Shell).
- **Monitoramento contínuo**: logs centralizados e alertas; trilhas de auditoria para alimentar a resposta a incidentes (`08-plano-resposta-incidentes.md`).
- **Verificação de integridade**: conferência de assinaturas e hashes de dependências no pipeline — reforço importante após o incidente real de cadeia de suprimentos contra a própria ferramenta Trivy (mar/2026, grupo TeamPCP).

## 5. Conexão com o portfólio

- Os ativos do `01-cenario-e-ativos.md` definem os alvos do pipeline (APIs, PostgreSQL, nginx, AWS).
- Os achados do `02-analise-de-vulnerabilidades.md` mostram onde cada ferramenta atua (Trivy → dependências; nmap → serviços de rede).
- As prioridades de remediação alimentam a matriz de riscos (`04-matriz-de-riscos.md`).