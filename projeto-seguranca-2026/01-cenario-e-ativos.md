# Cenário de Projeto — Banco Digital Seguro (BDS)

## Descrição do Cenário

A **AngelCorp** é uma empresa de segurança cibernética que presta serviços de proteção para clientes corporativos. Seu principal cliente é o **Banco Seguro** — também chamado de **Banco Digital Seguro (BDS)** —, uma instituição financeira digital com cerca de **500 mil clientes**. O BDS oferece conta digital, cartões de crédito e débito, PIX, empréstimos e investimentos — incluindo transferências de grandes somas para fundos de investimento — por meio de um **aplicativo mobile** (Android/iOS) e do **internet banking web**. A AngelCorp é responsável por integrar segurança em todo o ciclo de vida do negócio: do desenvolvimento do aplicativo (pipeline DevSecOps) à operação da infraestrutura em nuvem (AWS), incluindo monitoramento contínuo, resposta a incidentes e conformidade regulatória (LGPD, PCI-DSS e regulações do Banco Central).

A plataforma adota **security by design**: autenticação multifator (senha + token gerado no celular + biometria facial em casos de maior risco), criptografia de ponta a ponta em trânsito e em repouso (AES), integridade de dados com funções de hash (SHA-256) e trilhas de auditoria completas para todas as operações.

## Ativos

| Ativo | Tipo | Criticidade | Descrição |
|-------|------|-------------|-----------|
| Aplicativo mobile (Android/iOS) | Software | Alta | Canal principal de acesso: consulta de saldo, transferências, PIX e investimentos |
| Internet banking web | Software | Alta | Canal web de acesso; operações de grande valor e gestão de investimentos |
| APIs REST (autenticação, PIX, cartões) | Software | Alta | Interface de integração entre canais, core bancário e parceiros |
| Core bancário | Software | Alta | Sistema central de processamento de transações, saldos e contas |
| Banco de dados PostgreSQL | Dados | Alta | Persistência de dados dos clientes, saldos, histórico de operações e logs |
| Nuvem AWS (VPC, WAF, load balancer) | Infraestrutura | Alta | Hospeda a plataforma; segmentação de rede, filtragem de tráfego e distribuição de carga |
| Integrações externas (SPI/PIX, bandeiras de cartão) | Serviço | Alta | Conexão com Banco Central, bandeiras e fornecedores parceiros |
| Sistema de logs e auditoria | Dados | Média | Registro de todas as ações para auditoria, detecção e resposta a incidentes |
| Dados pessoais e financeiros dos clientes | Dados | Alta | Dados sensíveis protegidos pela LGPD; principal alvo de ataques |
| Equipe de segurança (AngelCorp) | Pessoas/Processos | Alta | Time responsável por monitoramento, resposta a incidentes e gestão de vulnerabilidades |

## Valor dos Ativos

Todos os ativos do BDS sustentam a operação central do negócio: **movimentar dinheiro de forma segura, confiável e disponível**. Para uma instituição financeira, a perda de confiança vale mais do que a perda financeira imediata — um vazamento ou uma indisponibilidade prolongada pode afastar clientes, gerar sanções regulatórias (Banco Central, ANPD) e danos irreparáveis à reputação.

Se um ativo falhar ou for comprometido, o impacto depende de sua posição na cadeia:

- **Banco de dados PostgreSQL**: se for perdido ou corrompido, o sistema não consegue mostrar saldos, registrar transferências nem gerar extratos — **o negócio para**.
- **APIs REST**: se forem comprometidas, um atacante pode interceptar ou manipular operações de PIX e investimentos, desviando valores sem passar pelo core bancário.
- **Integrações externas (SPI/PIX)**: se houver falha ou exploração de credenciais de fornecedores, o BDS fica impossibilitado de liquidar PIX — exatamente o que ocorreu em ataques reais ao sistema brasileiro em 2025/2026.
- **Aplicativo mobile e internet banking**: se ficarem indisponíveis, o cliente não consegue acessar a conta nem resgatar valores — especialmente crítico em períodos de alta volatilidade do mercado.
- **Nuvem AWS (VPC, WAF, load balancer)**: se a segmentação ou a filtragem falharem, toda a plataforma fica exposta a ataques externos e movimentação lateral.
- **Sistema de logs e auditoria**: se for comprometido, a organização perde a capacidade de detectar, investigar e comprovar incidentes — comprometendo a auditabilidade e o não-repúdio das operações.
- **Dados pessoais e financeiros**: se vazarem, o BDS viola a LGPD, sofre sanções da ANPD e perde a confiança dos 500 mil clientes.

O valor desses ativos também se expressa na **tríade CIA**:

- **Confidencialidade**: apenas o dono da conta e os gestores de fundo autorizados podem visualizar saldo e histórico de investimentos; qualquer interceptação encontra apenas dados cifrados (AES).
- **Integridade**: um aporte de R$ 50.000 não pode ser alterado para R$ 5.000 ou R$ 500.000 durante o processamento ou em repouso no banco de dados — garantida por hashes (SHA-256).
- **Disponibilidade**: servidores redundantes e proteção contra negação de serviço garantem acesso e resgate a qualquer momento.

Por fim, o ativo mais valioso do BDS é intangível: **a confiança** (!!!). Cada controle implementado pela AngelCorp existe para proteger um único objetivo — que o cliente tenha certeza de que seu dinheiro e seus dados estão seguros.