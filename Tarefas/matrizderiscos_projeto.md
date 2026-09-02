# Matriz de Riscos — [NOME DO SEU CENÁRIO]

**Objetivo:** Modelar as ameaças do seu cenário (DFD + STRIDE) e transformá-las em uma matriz de riscos 3x3, com escalas de probabilidade e impacto próprias, para priorizar o que tratar primeiro.

## Introdução — Da ameaça ao risco

Nas aulas anteriores você definiu o cenário e os ativos (`01-cenario-e-ativos.md`) e buscou vulnerabilidades reais (CVEs) que poderiam afetá-los (`02-analise-de-vulnerabilidades.md`). Antes de priorizar riscos, porém, é preciso saber **quais ameaças existem** no seu cenário — e é isso que o DFD e o STRIDE revelam. Nesta tarefa você vai:

1. Desenhar o **DFD** do seu cenário (Etapa 1);
2. Aplicar o **STRIDE** sobre ele (Etapa 2);
3. Criar as **escalas de probabilidade e impacto** e montar a **matriz 3x3** (Etapas 3 a 5);
4. Preencher a matriz com as suas ameaças e propor o **tratamento** (Etapa 6).

> O arquivo `03-modelagem-de-ameacas.md` do seu repositório ainda está só com o cabeçalho — é ele que você vai preencher nas Etapas 1 e 2. A matriz vai no `04-matriz-de-riscos.md`.

## Etapa 1 — DFD (Diagrama de Fluxo de Dados)

Desenhe o DFD do seu cenário mostrando como os dados circulam:

- **Entidades externas** — quem interage com o sistema (clientes, usuários, parceiros, integrações);
- **Processos** — o que transforma os dados (autenticação, processamento de pedidos, pagamento);
- **Depósitos de dados** — onde os dados ficam armazenados (banco de dados, logs, filas);
- **Fluxos de dados** — as setas que conectam os elementos.

Marque também as **fronteiras de confiança** (trust boundaries): os pontos onde os dados cruzam de um ambiente confiável para outro (ex.: da internet para o servidor, do servidor para o banco).

> Formato livre: à mão (foto), em ferramenta online (draw.io, Excalidraw) ou descrito em texto. O importante é o diagrama existir e ficar no seu repositório (pasta `images/` ou link).

## Etapa 2 — STRIDE (modelagem de ameaças)

Com o DFD pronto, aplique o STRIDE. Para cada categoria, responda: **o que ameaça o meu cenário?** e **qual CVE (da sua busca de CVEs) se relaciona?**

| Categoria STRIDE | O que ameaça no meu cenário | CVE relacionada |
|---|---|---|
| Spoofing (falsificação) | | |
| Tampering (adulteração) | | |
| Repudiation (repúdio) | | |
| Information Disclosure (vazamento) | | |
| Denial of Service (indisponibilidade) | | |
| Elevation of Privilege (elevação) | | |

Preencha **no mínimo 4 categorias** que façam sentido para o seu cenário — nem todo cenário tem as seis.

> Nesta tarefa não é preciso o detalhamento por componente (elemento × categoria × CVE × mitigação). O foco é a visão por categoria, que alimenta a matriz de riscos.

## Etapa 3 — Escala de Probabilidade

Defina a escala de probabilidade do seu cenário: a frequência esperada de ocorrência de cada ameaça. Use 3 níveis:

| Nível | Probabilidade | Descrição sugerida |
|---|---|---|
| 1 | Baixa | Rara — ocorre em situações excepcionais (ex.: menos de uma vez por ano) |
| 2 | Média | Possível — pode ocorrer em circunstâncias normais (ex.: algumas vezes por ano) |
| 3 | Alta | Frequente — esperada no dia a dia da operação (ex.: mensalmente ou mais) |

> As descrições são um ponto de partida. Adapte as frequências à realidade do seu cenário — o que é "frequente" para uma loja virtual pode não ser para um hospital.

## Etapa 4 — Escala de Impacto

Defina a escala de impacto: o dano ao negócio caso a ameaça se concretize, considerando confidencialidade, integridade e disponibilidade (CIA) dos seus ativos. Use 3 níveis:

| Nível | Impacto | Descrição sugerida |
|---|---|---|
| 1 | Baixo | Dano pequeno e recuperável — sem impacto relevante na operação |
| 2 | Médio | Dano relevante — indisponibilidade parcial, custos moderados, retrabalho |
| 3 | Alto | Dano grave — indisponibilidade prolongada, perda de dados, dano reputacional ou regulatório |

## Etapa 5 — Matriz 3x3

Cruzando as duas escalas, monte a matriz. O **nível de risco = Probabilidade × Impacto**:

| Probabilidade \ Impacto | Impacto 1 (Baixo) | Impacto 2 (Médio) | Impacto 3 (Alto) |
|---|---|---|---|
| Probabilidade 3 (Alta) | 3 | 6 | 9 |
| Probabilidade 2 (Média) | 2 | 4 | 6 |
| Probabilidade 1 (Baixa) | 1 | 2 | 3 |

Com a matriz 3x3, o maior nível possível é 9. Classifique:

| Faixa | Nível |
|---|---|
| 1 | Baixo |
| 2 | Médio |
| 3 – 4 | Alto |
| 6 e 9 | Crítico |

## Etapa 6 — Preenchendo a matriz com as suas ameaças

Volte ao STRIDE da Etapa 2. Para cada ameaça:

1. Atribua a **probabilidade** (Etapa 3) e o **impacto** (Etapa 4), justificando brevemente;
2. Calcule o **nível de risco** (Probabilidade × Impacto) e classifique-o;
3. Proponha o **tratamento** (ISO 27005): **Mitigar** (aplicar controles), **Transferir** (compartilhar — seguro/terceiros), **Aceitar** (assumir o risco residual) ou **Evitar** (eliminar o processo).

| Ameaça (STRIDE) | Vulnerabilidade | Probabilidade | Impacto | Nível de risco | Tratamento |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

**Exemplo (Banco Seguro):** Elevation of Privilege — CVE-2024-6387 (regreSSHion) no SSH de administração → Probabilidade: Média (2) | Impacto: Alto (3) | Nível: 6 (Crítico) | Tratamento: Mitigar (patch OpenSSH 9.8p1, segmentação de rede, MFA).

Preencha **no mínimo 5 ameaças**, procurando cobrir níveis diferentes de risco — é isso que mostra que a matriz está funcionando.

## Entrega esperada

| Item | Formato |
|---|---|
| DFD | Diagrama com entidades, processos, depósitos e fronteiras de confiança |
| STRIDE | Tabela com no mínimo 4 categorias e CVEs relacionadas |
| Escala de probabilidade | Tabela com 3 níveis adaptados ao cenário |
| Escala de impacto | Tabela com 3 níveis adaptados ao cenário |
| Matriz 3x3 | Tabela com os níveis de risco e a classificação |
| Riscos preenchidos | Tabela com mínimo 5 ameaças, nível de risco e tratamento |
| Commit | Mensagem descritiva (ex.: "modelagem de ameaças e matriz de riscos preenchidas") |

> Dica: preencha o `03-modelagem-de-ameacas.md` (Etapas 1 e 2) e o `04-matriz-de-riscos.md` (Etapas 3 a 6) do seu repositório seguindo este roteiro. Se quiser mais granularidade no futuro, dá para evoluir para uma matriz 5x5 — mas neste semestre vamos de 3x3.