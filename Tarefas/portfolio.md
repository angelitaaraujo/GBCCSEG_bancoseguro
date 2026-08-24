# Portfólio de Projeto — Configuração do Repositório no GitHub

Ao longo do semestre, você vai construir um portfólio de projeto de segurança completo, peça por peça. Para organizar e versionar tudo, vamos usar um repositório no GitHub.

Cada prática de cada aula vai adicionar conteúdo a um arquivo dentro deste repositório. Nada de atividades soltas — tudo converge para o projeto final.

## Passo 1 — Criar o repositório do projeto
1. Crie o seu repositorio com os seguintes dados:
- **Repository name:** projeto-seguranca-2026 (use exatamente este nome, com hiféns, sem espaços)
- **Description:** Portfólio de Segurança em Sistemas — Cenário: [NOME DO SEU CENÁRIO]
- **Visibility:** Private (mantenha privado durante o semestre — você pode tornar público no final do semestre, se quiser)
- **Add a README file:** marque esta opção
Add .gitignore: selecione o template "Node" (mesmo que não use Node, evita arquivos indesejados)
2. Envie nesta tarefa o link do repositório

## Passo 2 — Crie a estrutura de pastas e arquivos

O repositório precisa ter uma estrutura fixa. Crie os seguintes arquivos:

### 2.1 — Criar o arquivo principal do cenário

#### Cenário.
 - Nome do arquivo: `01-cenario-e-ativos.md`
 - Conteúdo
```md 
# Cenário de Projeto — [NOME DO SEU CENÁRIO]

## Descrição do Cenário

[Descreva brevemente o seu cenário: qual organização, qual setor, qual sistema, quantos usuários, quais serviços. 1 parágrafo.]

## Ativos

| Ativo | Tipo | Criticidade | Descrição |
|-------|------|-------------|-----------|
| (ex.: Servidor web) | Infraestrutura | Alta | Hospeda o portal de atendimento |
| ? | ? | ? | ? |

## Valor dos Ativos

[Por que estes ativos são importantes para a organização? O que acontece se forem comprometidos?]
```

#### Análise de Vulnerabilidades
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.

- Arquivo: `02-analise-de-vulnerabilidades.md`
```md

# Análise de Vulnerabilidades — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida na aula de Análise de Vulnerabilidades.]
```

#### Modelagem de Ameaças
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.

- Arquivo: `03-modelagem-de-ameacas.md`

```md
# Modelagem de Ameaças — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida na aula de Modelagem de Ameaças.]
```

#### Matriz de Riscos
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.
-  Arquivo: `04-matriz-de-riscos.md`

```md
# Matriz de Riscos — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida na aula de Gerenciamento de Riscos.]
```

#### Política de Segurança
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.
- Arquivo: `05-politica-de-seguranca.md`

```md
# Política de Segurança — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida na aula de Políticas de Segurança.]
```

#### Política de Segurança
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.
- Arquivo: `06-mapa-de-conformidade.md`

```md
# Mapa de Conformidade — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida na aula de Padrões e Conformidade.]
``` 
#### Plano DevSecOps — [NOME DO SEU CENÁRIO]
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.
- Arquivo: `07-plano-devsecops.md`

```md
# Plano DevSecOps — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida ao longo das aulas de DevSecOps.]
```

#### Plano de Resposta a Incidentes
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.
- Arquivo: `08-plano-resposta-incidentes.md`

```md
# Plano de Resposta a Incidentes — [NOME DO SEU CENÁRIO]

[Esta seção será preenchida na aula de Resposta a Incidentes.]
```
#### Relatório Final
Apenas crie o arquivo com um título e a estrutura básica. Vamos preencher ao longo das aulas.
- Arquivo: `09-relatorio-final.md`

```md
# Relatório Final — [NOME DO SEU CENÁRIO]

[Esta seção será consolidada nas últimas aulas do semestre.]
```

### 2.3 — Compartilhar com a professora
Compartilhar com `angelitaaraujo`

#### Estrutura final do repositório

Ao terminar, seu repositório deve ter esta estrutura:

```md
projeto-seguranca-2026/
├── README.md
├── 01-cenario-e-ativos.md
├── 02-analise-de-vulnerabilidades.md
├── 03-modelagem-de-ameacas.md
├── 04-matriz-de-riscos.md
├── 05-politica-de-seguranca.md
├── 06-mapa-de-conformidade.md
├── 07-plano-devsecops.md
├── 08-plano-resposta-incidentes.md
├── 09-relatorio-final.md
```

## Regras de uso do repositório
- Um repositório por aluno — não compartilhe com colegas (atividades individuais, exceto quando indicado)
- Mantenha privado até o final do semestre — você pode tornar público na entrega final, se quiser
- Faça commit a cada aula — não acumule conteúdo; commit pequeno e frequente é melhor que commit gigante no final
- Não apague arquivos — se precisar corrigir, edite e faça um novo commit (o Git mantém o histórico)
- Use mensagens de commit descritivas — ex.: "Aula 5: modelagem de ameaças com STRIDE" em vez de "update"

## Entrega desta configuração

- **O que entregar:** o link do seu repositório no GitHub
- **Como entregar:** submeta o link na atividade correspondente no Moodle (campo "Entrega de texto" ou "URL")

### Antes de entregar, confira:
- O repositório foi criado com o nome projeto-seguranca-2026
Todos os 9 arquivos .md foram criados (de 01-cenario-e-ativos.md até 09-relatorio-final.md)
- A pasta incidentes-da-semana/ foi criada com o README.md dentro
- O arquivo 01-cenario-e-ativos.md está preenchido com o seu cenário (descrição + tabela de ativos + valor dos ativos)
- O repositório está como Private e o link funciona