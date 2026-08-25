# Matriz de Riscos — Banco Digital Seguro (BDS)

> Matriz baseada na ISO 27005, consolidando as ameaças STRIDE do `03-modelagem-de-ameacas.md` e as vulnerabilidades (CVEs) do `02-analise-de-vulnerabilidades.md`. As opções de tratamento dialogam com o pipeline do `07-plano-devsecops.md`.

## 1. Metodologia

Escala qualitativa de **Probabilidade** (frequência esperada de ocorrência) e **Impacto** (dano ao negócio, considerando CIA e contexto regulatório do setor financeiro):

| Escala | Probabilidade | Impacto |
|---|---|---|
| 1 | Baixo | Baixo |
| 2 | Médio | Médio |
| 3 | Alto | Alto |

**Nível de risco = Probabilidade × Impacto**:

| Faixa | Nível |
|---|---|
| 1–4 | Baixo |
| 5–9 | Médio |
| 10–14 | Alto |
| 15–25 | Crítico |

**Tratamento (ISO 27005):** Mitigar (aplicar controles), Transferir (compartilhar o risco — seguro/terceiros), Aceitar (risco residual assumido) ou Evitar (eliminar o processo).

