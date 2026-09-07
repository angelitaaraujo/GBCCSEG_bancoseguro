# 05 — Política de Segurança da Informação

**Organização:** Banco Seguro (cliente da AngelCorp)

**Versão:** 1.0

**Data:** 08/09/2026

**Responsável:** AngelCorp — área de Segurança Cibernética

**Aprovação:** Diretoria do Banco Seguro

**Revisão:** anual ou após incidente relevante

---

## 1. Objetivo

Estabelecer as diretrizes de segurança da informação do Banco Seguro,
protegendo a confidencialidade, a integridade e a disponibilidade das
informações da instituição e de seus aproximadamente 500 mil clientes,
em conformidade com a LGPD, o PCI-DSS e as regulações do Banco Central.

## 2. Escopo

Esta política aplica-se a todos os colaboradores, estagiários, prestadores
de serviço e fornecedores do Banco Seguro, bem como a todos os sistemas e
ativos, incluindo:

- Aplicativo mobile e internet banking
- APIs REST (autenticação, PIX, cartões)
- Core bancário e banco de dados PostgreSQL
- Infraestrutura em nuvem AWS (VPC, WAF, load balancer)
- Integrações externas (SPI/PIX, bandeiras de cartão, fornecedores)

## 3. Princípios (lentes de projeto)

- **Security by design:** segurança considerada desde a concepção de
  produtos e serviços.
- **Privacy by default:** privacidade como padrão no tratamento de dados.
- **Menor privilégio:** acesso mínimo necessário para a função.
- **Zero Trust:** nenhum acesso é confiável por padrão, mesmo interno.
- **Defesa em profundidade:** múltiplas camadas de proteção.

## 4. Diretrizes

### 4.1 Controle de acesso e autenticação

- Acesso pelo menor privilégio, com revisão trimestral de acessos.
- MFA obrigatório para acessos administrativos, transacionais e remotos.
- Contas de serviço com credenciais rotacionadas e sem uso humano direto.
- Acessos de ex-colaboradores revogados em até 24h após o desligamento.

### 4.2 Senhas

- Senhas com no mínimo 12 caracteres, sem reuso entre sistemas.
- Uso de gerenciador corporativo de senhas.
- Proibido compartilhar credenciais ou anotá-las em locais não seguros.

### 4.3 Classificação e tratamento da informação

- Informações classificadas em: pública, interna, confidencial e restrita.
- Dados classificados como confidencial ou restrita devem ser
  criptografados em repouso e em trânsito.
- Dados pessoais de clientes tratados conforme a LGPD, com registro das
  operações de tratamento.

### 4.4 Uso aceitável

- Recursos corporativos destinados exclusivamente a atividades
  profissionais.
- Proibido armazenar dados de clientes em dispositivos pessoais ou
  serviços não aprovados.

### 4.5 Desenvolvimento seguro (DevSecOps)

- SAST e análise de dependências obrigatórios no pipeline (ex.: Semgrep,
  Gitleaks, Trivy).
- DAST antes de liberações em produção (ex.: OWASP ZAP).
- Revisão de código com foco em segurança e gestão de vulnerabilidades
  (CVE) com prazos definidos por severidade.

### 4.6 Terceiros e fornecedores

- Fornecedores com acesso a dados sensíveis devem cumprir os mesmos
  controles internos.
- Acessos de terceiros limitados, monitorados e revisados a cada 6 meses.
- Termo de confidencialidade obrigatório (lição do incidente PIX de 2025).

### 4.7 Resposta a incidentes

- Incidentes de alto impacto comunicados à equipe de segurança em até 1h.
- Notificação à ANPD em até 72h quando houver risco a titulares (LGPD).
- Registro e análise pós-incidente com plano de ação corretiva.

### 4.8 Backup e continuidade

- Backups criptografados, testados mensalmente e armazenados em região
  separada.
- RTO e RPO definidos e documentados para os sistemas críticos.
- Plano de continuidade de negócios revisado anualmente.

## 5. Rastreabilidade (diretriz × controle CIS × evidência)

| Diretriz | Controle CIS | Evidência auditável |
|---|---|---|
| Menor privilégio + MFA obrigatório | CIS 5/6 | Log de autenticação |
| Classificação da informação (4 níveis) | CIS 3 | Inventário de dados + política de classificação |
| Senhas fortes, sem reuso, gerenciador | CIS 5/6 | Relatório de conformidade de senhas |
| Desenvolvimento seguro (SAST/DAST, dependências) | CIS 16 | Relatórios SAST/DAST no pipeline |
| Terceiros: acesso mínimo, monitorado, revisado | CIS 15 | Revisão semestral de acessos registrada |
| Resposta a incidentes (1h / 72h ANPD) | CIS 17 | Registro de incidentes + tempos de resposta |
| Backup criptografado e testado | CIS 11 | Relatório mensal de teste de restore |
| Monitoramento e logs centralizados | CIS 8/13 | Alertas e trilhas de auditoria |

## 6. Responsabilidades

- **AngelCorp:** implementar, monitorar e auditar os controles.
- **Gestores do Banco Seguro:** aprovar acessos e garantir o cumprimento
  das diretrizes em suas áreas.
- **Colaboradores e terceiros:** cumprir esta política e reportar
  desvios ou suspeitas de incidentes.

## 7. Descumprimento

O descumprimento desta política sujeita o infrator a medidas
administrativas, disciplinares e legais, conforme a gravidade, sem
prejuízo das sanções previstas na LGPD e na regulação bancária.

## 8. Revisão

Esta política será revisada anualmente ou sempre que ocorrer incidente
relevante, mudança significativa de infraestrutura ou alteração
normativa (LGPD, PCI-DSS, Banco Central).
