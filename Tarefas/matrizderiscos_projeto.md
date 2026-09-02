# Matriz de Riscos — [NOME DO SEU CENÁRIO]

**Objetivo:** Criar a escala de probabilidade e a escala de impacto do seu cenário e montar uma matriz de riscos 3x3, transformando as ameaças que você modelou no `03-modelagem-de-ameacas.md` em riscos priorizados.

## Introdução — Da ameaça ao risco

Na aula anterior você identificou as ameaças do seu cenário (STRIDE) e as vulnerabilidades reais (CVEs) que poderiam explorá-las. Mas nem toda ameaça merece a mesma atenção: algumas são raras e causam pouco dano; outras são frequentes e podem derrubar o negócio. A **matriz de riscos** organiza essa percepção: cruzando **probabilidade** (chance de acontecer) com **impacto** (dano se acontecer), ela transforma opinião em prioridade — e prioridade em decisão de negócio.

## Etapa 1 — Escala de Probabilidade

Defina a escala de probabilidade do seu cenário: a frequência esperada de ocorrência de cada ameaça. Use 3 níveis:

| Nível | Probabilidade | Descrição sugerida |
|---|---|---|
| 1 | Baixa | Rara — ocorre em situações excepcionais (ex.: menos de uma vez por ano) |
| 2 | Média | Possível — pode ocorrer em circunstâncias normais (ex.: algumas vezes por ano) |
| 3 | Alta | Frequente — esperada no dia a dia da operação (ex.: mensalmente ou mais) |

> As descrições acima são um ponto de partida. Adapte os exemplos de frequência à realidade do seu cenário — o que é "frequente" para uma loja virtual pode não ser para um hospital.

## Etapa 2 — Escala de Impacto

Defina a escala de impacto: o dano ao negócio caso a ameaça se concretize, considerando confidencialidade, integridade e disponibilidade (CIA) dos seus ativos. Use 3 níveis:

| Nível | Impacto | Descrição sugerida |
|---|---|---|
| 1 | Baixo | Dano pequeno e recuperável — sem impacto relevante na operação |
| 2 | Médio | Dano relevante — indisponibilidade parcial, custos moderados, retrabalho |
| 3 | Alto | Dano grave — indisponibilidade prolongada, perda de dados, dano reputacional ou regulatório |

## Etapa 3 — Matriz 3x3

Cruzando as duas escalas, monte a matriz de riscos. O **nível de risco = Probabilidade × Impacto**:

| Probabilidade \ Impacto | Impacto 1 (Baixo) | Impacto 2 (Médio) | Impacto 3 (Alto) |
|---|---|---|---|
| Probabilidade 3 (Alta) | 3 | 6 | 9 |
| Probabilidade 2 (Média) | 2 | 4 | 6 |
| Probabilidade 1 (Baixa) | 1 | 2 | 3 |

Com a matriz 3x3, o maior nível possível é 9. Classifique os resultados:

| Faixa | Nível |
|---|---|
| 1 | Baixo |
| 2 | Médio |
| 3 – 4 | Alto |
| 6 e 9 | Crítico |

## Etapa 4 — Preenchendo a matriz com as suas ameaças

Volte ao seu `03-modelagem-de-ameacas.md` (ameaças STRIDE) e ao `02-analise-de-vulnerabilidades.md` (CVEs). Para cada ameaça:

1. Atribua a **probabilidade** (Etapa 1) e o **impacto** (Etapa 2), justificando brevemente cada escolha.
2. Calcule o **nível de risco** (Probabilidade × Impacto) e classifique-o.
3. Proponha o **tratamento** do risco, conforme a ISO 27005: **Mitigar** (aplicar controles), **Transferir** (compartilhar — seguro/terceiros), **Aceitar** (assumir o risco residual) ou **Evitar** (eliminar o processo).

| Ameaça (STRIDE) | Vulnerabilidade | Probabilidade | Impacto | Nível de risco | Tratamento |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

**Exemplo (Banco Seguro):** Elevation of Privilege — CVE-2024-6387 (regreSSHion) no SSH de administração → Probabilidade: Média (2) | Impacto: Alto (3) | Nível: 6 (Crítico) | Tratamento: Mitigar (patch OpenSSH 9.8p1, segmentação de rede, MFA).

Preencha **no mínimo 5 ameaças** do seu cenário, procurando cobrir níveis diferentes de risco — é isso que mostra que a sua matriz está funcionando.

## Entrega esperada

| Item | Formato |
|---|---|
| Escala de probabilidade | Tabela com 3 níveis e descrições adaptadas ao cenário |
| Escala de impacto | Tabela com 3 níveis e descrições adaptadas ao cenário |
| Matriz 3x3 | Tabela com os níveis de risco e a classificação |
| Riscos preenchidos | Tabela com mínimo 5 ameaças, nível de risco e tratamento |
| Commit | Mensagem descritiva (ex.: "matriz de riscos: escalas de probabilidade e impacto preenchidas") |

> Dica: preencha o arquivo `04-matriz-de-riscos.md` do seu repositório seguindo este roteiro. Se quiser mais granularidade, você pode evoluir para uma matriz 5x5 no futuro — mas neste semestre vamos trabalhar com a 3x3.