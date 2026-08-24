# Cenário de Trabalho e Inventário de Ativos (descrição)

**Objetivo:** Escolher um ambiente (aplicação ou infraestrutura), descrevê-lo e listar o que precisa ser protegido, entendendo por que cada item importa para a continuidade do negócio.

## Etapa 1 — Criação do Cenário

Você deverá criar seu próprio cenário. Pode ser real ou fictício, e pode ser:

- Uma **aplicação** (ex: sistema web, aplicativo mobile, plataforma de streaming, sistema de gestão)
- Uma **infraestrutura** (ex: rede de uma empresa, ambiente de nuvem, laboratório de informática)

O cenário precisa ser simples, algo que você consiga descrever em poucas linhas. Evite ambientes muito complexos.

## Etapa 2 — Descrição do Cenário

Escreva uma narrativa curta **(3 a 5 linhas)** com:

- **Nome e missão** — ex: "MeuApp — aplicativo de delivery de marmitas"
- **Quem acessa** — clientes, entregadores, administradores? Parceiros?
- **Infraestrutura** — servidor na nuvem, banco de dados, dispositivo mobile? Quantos usuários?

**Exemplo:** "O MeuApp é um aplicativo de delivery onde clientes fazem pedidos, entregadores aceitam corridas e o dono gerencia os pedidos. A aplicação roda em servidores na nuvem (AWS), com banco de dados PostgreSQL. Cerca de 200 clientes e 30 entregadores usam o sistema diariamente."

## Etapa 3 — Identificação e Categorização dos Ativos

Liste os ativos — tudo que precisa ser protegido — em 4 categorias. Mínimo 2 itens por categoria.

| Categoria	| O que incluir |
|-----------|---------------|
| Informação (Dados) |	Dados de clientes, pedidos, senhas, registros financeiros
| Software |	Aplicativo, sistema operacional, banco e dados, bibliotecas
| Hardware	| Servidores, computadores, roteadores, tablets
| Pessoas	| Administradores, usuários, funcionários com acesso


## Etapa 4 — Valorização

Para uma categoria (escolha a mais crítica para o seu cenário), responda:

"Se esse ativo falhar ou for comprometido, o sistema consegue funcionar?"

**Exemplo:** "Se o banco de dados de pedidos for perdido, o aplicativo não consegue mostrar o cardápio nem registrar novos pedidos — o negócio para."

## Entrega esperada
| Item |	Formato |
|------|------------|
| Cenário criado (nome + descrição) |	Parágrafo de 3-5 linhas
| Tabela com ativos (mín. 2 por categoria) |	Lista ou tabela
| Justificativa de valor (1 categoria)	| 2-3 frases


