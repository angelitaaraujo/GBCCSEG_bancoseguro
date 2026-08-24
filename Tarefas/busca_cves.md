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
