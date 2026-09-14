# Mapa de Conformidade — Banco Digital Seguro (BDS)

**Organização:** Banco Seguro (cliente da AngelCorp)\
**Versão:** 1.0\
**Data:** 12/09/2026\
**Responsável:** AngelCorp — área de Segurança Cibernética\
**Aprovação:** Diretoria do Banco Seguro\
**Revisão:** anual ou após mudança normativa relevante

---

## 1. Objetivo

Mapear as obrigações legais e regulatórias aplicáveis ao Banco Seguro e relacionar cada uma aos controles técnicos e organizacionais que comprovam a conformidade — conectando as diretrizes da política de segurança (05) aos padrões já estudados (ISO 27001/27002, NIST CSF e CIS Controls).

## 2. Escopo

Aplica-se a todos os sistemas e ativos do Banco Seguro descritos no `01-cenario-e-ativos.md`:

- Aplicativo mobile e internet banking
- APIs REST (autenticação, PIX, cartões)
- Core bancário e banco de dados PostgreSQL
- Infraestrutura em nuvem AWS (VPC, WAF, load balancer)
- Integrações externas (SPI/PIX, bandeiras de cartão, fornecedores)

## 3. Legislações e padrões aplicáveis

| Legislação/Padrão | Tipo | Por que se aplica ao BDS |
| --- | --- | --- |
| LGPD (Lei 13.709/2018) | Obrigatório | Trata dados pessoais de ~500 mil clientes (cadastro, chaves PIX, transações) |
| Marco Civil da Internet (Lei 12.965/2014) | Obrigatório | Opera app mobile e internet banking; guarda registros de conexão e acesso |
| Código Civil (Lei 10.406/2002) | Obrigatório | Responsabilidade civil por danos a clientes (arts. 186 e 927) |
| Lei 12.737/2012 + Lei 14.155/2021 | Obrigatório | Crimes cibernéticos; preservação de evidências na resposta a incidentes |
| Res. CMN 4.893/2021 + BCB 85/2021 (+ BCB 538/2025) | Obrigatório | Instituição financeira autorizada; política de segurança cibernética e reporte ao BC |
| PCI-DSS v4.0 | Obrigatório (contratual) | Processa dados de cartões de crédito e débito (bandeiras) |
| ISO 27001/27002 | Voluntário | Base do SGSI e dos controles de segurança da informação |
| NIST CSF | Voluntário | Estrutura de cibersegurança (Identify, Protect, Detect, Respond, Recover) |
| CIS Controls v8 | Voluntário | Controles priorizados que sustentam as diretrizes da política (05) |
| GDPR (UE 2016/679) | Condicional | Aplicável apenas se houver clientes na União Europeia — não é o caso atual |

## 4. Mapa de conformidade

| Requisito | Legislação/Padrão | Controle | Evidência | Status | Prioridade |
| --- | --- | --- | --- | --- | --- |
| Tratamento de dados pessoais com base legal | LGPD (arts. 6º e 7º) | Bases legais documentadas, privacy by default | RIPD + registro de operações (ROPA) | Parcial | Alta |
| Direitos dos titulares atendidos (acesso, correção, exclusão) | LGPD (art. 18) | Canal do titular + encarregado nomeado (art. 41) | Canal de atendimento com prazos de resposta | Parcial | Alta |
| Notificação de incidentes com risco a titulares | LGPD (art. 48) | Plano de resposta a incidentes (08) | Procedimento de notificação à ANPD em até 72h | Parcial | Alta |
| Segurança de dados de cartões | PCI-DSS v4.0 | Segmentação de rede, criptografia, testes trimestrais | Relatório de conformidade do ambiente de cartões | Não conforme | Alta |
| Política de segurança cibernética e resposta a incidentes | Res. CMN 4.893/2021 + BCB 85/2021 (+ BCB 538/2025) | Política de segurança (05), plano de resposta (08) | Política aprovada pela diretoria; reporte ao BC | Conforme | Alta |
| Guarda de registros de conexão e acesso | Marco Civil (arts. 13 e 15) | Retenção de logs: conexão 1 ano, aplicações 6 meses | Política de retenção + logs centralizados | Parcial | Média |
| Responsabilidade civil por danos a clientes | Código Civil (arts. 186 e 927) | Contratos/SLA com fornecedores, cláusulas de segurança | Contrato AngelCorp com SLA e responsabilidades | Conforme | Média |
| Preservação de evidências em incidentes | Lei 12.737/2012 + Lei 14.155/2021 | Logs imutáveis, cadeia de custódia | Trilhas de auditoria (CIS 8/13) | Parcial | Média |
| Sistema de gestão de segurança da informação | ISO 27001/27002 | SGSI com controles do Anexo A | Política, procedimentos e auditorias internas | Parcial | Média |
| Estrutura de cibersegurança | NIST CSF | Funções Identify/Protect/Detect/Respond/Recover | Mapeamento dos controles por função CSF | Parcial | Média |
| Controles priorizados de segurança | CIS Controls v8 | 18 controles essenciais (inventário, hardening, monitoramento) | Inventário de ativos, hardening, alertas | Parcial | Alta |

## 5. Rastreabilidade com a política (05) e os riscos (04)

Cada linha do mapa responde a uma diretriz da política de segurança (05) e a um risco da matriz (04):

- **Vazamento de dados pessoais (risco crítico, 04)** → linhas 1–3 do mapa → diretrizes 4.3 (classificação e tratamento da informação) e 4.7 (resposta a incidentes) da política.
- **Indisponibilidade do PIX/plataforma (risco crítico, 04)** → linha 5 do mapa → diretriz 4.8 (backup e continuidade) e reporte ao Banco Central.
- **Comprometimento de logs (risco alto, 04)** → linhas 6 e 8 do mapa → diretriz 4.7 e controle CIS 8/13 (monitoramento e logs).
- **Cadeia de suprimentos (risco alto, 04)** → linha 12 (CIS 15 — gerenciamento de fornecedores) → diretriz 4.6 (terceiros e fornecedores), lição do incidente PIX de 2025.

## 6. Lacunas e plano de ação

| Lacuna | Ação | Prazo | Responsável |
| --- | --- | --- | --- |
| Ambiente de cartões ainda não segmentado (PCI-DSS) | Segmentar rede, criptografar PAN, iniciar testes trimestrais | 90 dias | AngelCorp + equipe de infraestrutura |
| RIPD/ROPA desatualizados | Concluir inventário de tratamento de dados | 60 dias | DPO do BDS |
| Retenção de logs de aplicação abaixo do prazo legal | Ajustar política de retenção para 6 meses (Marco Civil) | 30 dias | AngelCorp |
| Procedimento de notificação à ANPD não testado | Integrar notificação ao plano de resposta (08) e simular | 60 dias | AngelCorp + DPO |

## 7. Responsabilidades

- **AngelCorp:** implementar, monitorar e auditar os controles do mapa.
- **DPO do Banco Seguro:** responder à ANPD e conduzir o RIPD/ROPA.
- **Diretoria do Banco Seguro:** aprovar o mapa e garantir recursos para as ações.
- **Colaboradores e fornecedores:** cumprir as diretrizes da política (05) que sustentam cada linha do mapa.

## 8. Revisão

Este mapa será revisado anualmente ou sempre que ocorrer mudança normativa relevante (LGPD, PCI-DSS, Banco Central), incidente significativo ou alteração de escopo dos ativos do BDS.