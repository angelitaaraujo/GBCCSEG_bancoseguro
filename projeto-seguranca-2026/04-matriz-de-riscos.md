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

Lembre-se que, utilizando uma matriz 3x3, o maior valor de nível será 9, neste caso o nível de risco será

| Faixa | Nível |
| --- | --- |
|  1  | Baixo |
|2 e 3| Médio |
|4 e 6| Alto  |
|  9  | Crítico |

> Atenção, sugestão usar este modelo no seu projeto, preenchendo a planilha disponível em [AQUI](https://ifcedubr-my.sharepoint.com/:x:/g/personal/angelita_araujo_ifc_edu_br/IQAR2iUfihiDR7spR15Jc8R0ASEwju2n8VKmE8XeBxT2zZ4)

Se você usar uma matriz 5 x 5, dependendo do seu nível de maturidade, pode usar a seguinte tabela

| Faixa | Nível |
|---|---|
| 1–4 | Baixo |
| 5–9 | Médio |
| 10–14 | Alto |
| 15–25 | Crítico |

**Tratamento (ISO 27005):** Mitigar (aplicar controles), Transferir (compartilhar o risco — seguro/terceiros), Aceitar (risco residual assumido) ou Evitar (eliminar o processo).



