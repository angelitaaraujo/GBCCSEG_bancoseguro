# Tarefa — Mapa de Conformidade (item 06 do portfólio)

## Contexto

Você já definiu o cenário (01), analisou vulnerabilidades (02), modelou ameaças (03), priorizou riscos (04) e escreveu a política de segurança (05). Agora vem a pergunta que fecha o ciclo: **quais leis e padrões se aplicam ao seu cenário — e como você prova que está cumprindo?**

As legislações (LGPD, Marco Civil, Código Civil, regulações setoriais) dizem **o que é obrigatório** e o que acontece se você não cumprir. Os padrões que já estudamos (ISO 27001/27002, NIST CSF e CIS Controls) dizem **como implementar**. O mapa de conformidade é exatamente o ponto onde os dois mundos se encontram: cada exigência legal mapeada para um controle e uma evidência.

> A boa notícia: você já fez o trabalho pesado. Sua política (05) já cita controles CIS e diretrizes específicas. O mapa organiza tudo isso por exigência legal — e mostra, com honestidade, o que já está conforme e o que ainda falta.

## O que entregar

Arquivo `projeto-seguranca-2026/06-mapa-de-conformidade.md` com:

1. **Legislações e padrões aplicáveis** — mínimo 3, com uma frase justificando por que cada uma se aplica ao seu cenário (setor, tipo de dado, tipo de serviço).
2. **Mapa de conformidade** — tabela com 5 a 8 linhas: 

| Requisito | Legislação/Padrão | Evidência | Status | Prioridade.
|------|------|------|-----|---- 
|.| | | | 
|


3. **Lacunas e plano de ação** — o que ainda não está conforme e o que fazer para chegar lá (com prazo).
4. **Conexão com o portfólio** — como o mapa conversa com a política (05) e com o plano DevSecOps (07).

## Requisitos

- Cada linha do mapa deve citar uma **legislação ou padrão real** (LGPD, Marco Civil, Código Civil, PCI-DSS, ISO 27001, NIST CSF, CIS Controls, regulação setorial do seu cenário). Não invente leis.
- **Status honesto**: Conforme, Parcial, Não conforme ou N.A. (não aplicável) — com justificativa.
- **Evidências concretas** e auditáveis (documento, log, relatório, contrato), não frases genéricas.
- O mapa deve conversar com os itens anteriores: mesmos ativos do 01, mesmos riscos do 04, mesmas diretrizes do 05.
- Se o seu cenário for de um setor regulado (saúde, finanças, educação), inclua a regulação específica.

## Como fazer

1. Abra sua política de segurança (05) e liste as diretrizes.
2. Identifique as legislações e padrões que se aplicam ao seu cenário (use o comparativo da aula como ponto de partida).
3. Monte a tabela do mapa: para cada requisito, defina a evidência, o status e a prioridade.
4. Liste as lacunas e proponha ações com prazo.
5. Revise com o checklist abaixo.

## Checklist

- [ ] Mínimo 3 legislações/padrões aplicáveis, com justificativa
- [ ] Tabela com 5 a 8 linhas (Requisito | Legislação/Padrão | Evidência | Status | Prioridade)
- [ ] Status honesto e justificado
- [ ] Evidências concretas e auditáveis
- [ ] Conversa com os itens 01, 04 e 05
- [ ] Lacunas com plano de ação e prazo
- [ ] Sem leis inventadas

## Conexão com o que vem

O mapa de conformidade alimenta o **Plano DevSecOps (item 07)**: cada lacuna vira um controle no pipeline ou na operação. E as obrigações de notificação (LGPD art. 48, Banco Central) serão detalhadas no **Plano de Resposta a Incidentes (item 08)**. Quanto mais rastreável o mapa, mais fácil será provar conformidade no relatório final (09).

---

*Consulte o exemplo completo do Banco Seguro em `projeto-seguranca-2026/06-mapa-de-conformidade.md`.*