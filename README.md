# Projeto Segurança em Sistemas — Estudo de Caso: Banco Digital Seguro (BDS)

Repositório do portfólio da disciplina **Segurança em Sistemas** (Bacharelado em Ciência da Computação — IFC). Aqui é desenvolvido, ao longo do semestre, o estudo de caso **Banco Digital Seguro (BDS)** — também referenciado como "Banco Seguro" —, usado como exemplo vivo para aplicar cada conceito da disciplina: da análise de vulnerabilidades à resposta a incidentes.

## O Cenário

O **Banco Digital Seguro (BDS)** é uma instituição financeira digital com aproximadamente **500 mil clientes**, que oferece conta digital, cartões de crédito e débito, **PIX**, empréstimos e **investimentos** — incluindo transferências de grandes somas para fundos de investimento — por meio de um **aplicativo mobile** e do **internet banking**.

O BDS é o principal cliente da **AngelCorp**, uma empresa de segurança cibernética contratada para integrar segurança em todo o ciclo de vida do negócio: do desenvolvimento do aplicativo (pipeline DevSecOps) à operação da infraestrutura em nuvem, incluindo monitoramento contínuo, resposta a incidentes e conformidade regulatória.

Por movimentar valores expressivos e dados financeiros sensíveis, o BDS adota uma postura de **security by design**: cada camada do sistema — do código ao datacenter — é projetada com controles de segurança nativos, e não como um complemento posterior.

## Arquitetura do Sistema

- **Canais de acesso**: aplicativo mobile (Android/iOS) e internet banking web
- **APIs REST**: serviços de autenticação, PIX e cartões
- **Core bancário + banco de dados**: sistema central de processamento e PostgreSQL
- **Infraestrutura em nuvem (AWS)**: VPC, WAF, load balancer e segmentação de rede
- **Integrações externas**: Banco Central (SPI/PIX), bandeiras de cartão e fornecedores parceiros

## Postura de Segurança

O sistema adota, desde a concepção:

- **Autenticação multifator (MFA)**: senha + token gerado no celular e, em casos de maior risco, biometria facial
- **Criptografia de ponta a ponta**: dados cifrados em trânsito e em repouso com algoritmos como o **AES**
- **Integridade por hash**: uso de funções como **SHA-256** para garantir que valores não sejam alterados durante o processamento
- **Registros detalhados de logs**: todas as ações geram trilhas de auditoria de alta qualidade
- **Disponibilidade reforçada**: servidores redundantes e proteção contra ataques de negação de serviço (DoS/DDoS)

## A Segurança na Prática — Tríade CID

### Confidencialidade
O sistema garante que apenas o dono da conta e os gestores de fundo autorizados consigam visualizar o saldo e o histórico de investimentos do cliente. Se um atacante interceptar o tráfego, encontrará apenas dados cifrados, protegendo o sigilo das informações financeiras.

### Integridade
Ao realizar um aporte de R$ 50.000, o sistema utiliza funções de hash (como SHA-256) para garantir que o valor não seja alterado para R$ 5.000 ou R$ 500.000 durante o processamento ou enquanto os dados estão em repouso no banco de dados.

### Disponibilidade
O BDS utiliza servidores redundantes e proteção contra ataques de negação de serviço para assegurar que o cliente consiga acessar a plataforma e resgatar seus valores a qualquer momento — especialmente em períodos de alta volatilidade no mercado, quando a demanda por acesso aumenta.

## Atributos Complementares 

### Autenticidade
Para acessar a conta, o cliente deve fornecer sua senha, um token gerado no celular e, em alguns casos, biometria facial. Isso garante que a entidade que requisita o acesso é realmente quem alega ser.

### Legalidade
O BDS projetou a plataforma em total conformidade com a **Lei Geral de Proteção de Dados Pessoais (LGPD)**, garantindo a anonimização de dados sensíveis e o uso das informações apenas para fins contratuais e regulatórios. Como instituição financeira, também atende aos requisitos de **PCI-DSS** (dados de cartão) e às regulações do **Banco Central** (PIX, SPI).

### Auditabilidade
Todas as ações na plataforma — do login à confirmação de um investimento — geram logs de alta qualidade. Esses registros permitem que auditores identifiquem posteriormente quem acessou o quê e quais operações foram realizadas.

### Não-repúdio
Uma vez que o cliente autoriza uma transferência utilizando sua assinatura digital ou MFA, ele não pode negar a autoria da transação: o BDS possui evidências técnicas e digitais que vinculam, de forma inequívoca, a ação à sua identidade.

## Contexto Regulatório e de Ameaças

O cenário não é fictício em seus riscos: o setor financeiro brasileiro é alvo constante de ataques. Ataques ao **PIX via fornecedores legítimos** (2025), a suspensão do PIX no Banco do Nordeste após ataque hacker (jan/2026) e os recorrentes vazamentos de chaves PIX reportados pelo Banco Central mostram a relevância de cada tema deste portfólio. O BDS, por sua dependência de integrações externas e operação em nuvem, precisa se defender tanto no **desenvolvimento** (pipeline DevSecOps, SAST/DAST) quanto nas **operações** (hardening, segmentação, monitoramento).

## Estrutura do Portfólio

| # | Documento | Tema |
|---|-----------|------|
| 01 | cenario-e-ativos | Cenário, ativos e valorização |
| 02 | analise-de-vulnerabilidades | Vulnerabilidades (CWE, OWASP) |
| 03 | modelagem-de-ameacas | Modelagem de ameaças (STRIDE) |
| 04 | matriz-de-riscos | Gerenciamento de riscos (ISO 27005) |
| 05 | politica-de-seguranca | Política de segurança |
| 06 | mapa-de-conformidade | NIST, ISO 27000, CIS Controls |
| 07 | plano-devsecops | DevSecOps (desenvolvimento + operações) |
| 08 | plano-resposta-incidentes | Resposta a incidentes |
| 09 | relatorio-final | Relatório consolidado |