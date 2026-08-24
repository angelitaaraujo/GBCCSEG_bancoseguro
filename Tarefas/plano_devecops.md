# Atualizar o plano DevSecOps
Abra o arquivo `07-plano-devsecops.md` no seu repositório e complete a tabela abaixo com as ferramentas que fariam sentido no seu cenário:

## 1. Ferramentas de Análise de Vulnerabilidades
| Etapa do pipeline | Ferramenta | Para quê |	Frequência |
|-------------------|------------|----------|----
| Commit | 	? | 	? | 	?
| Build | 	? | 	? | 	?
| Staging |	? |	? |	?
| Produção/Operação | 	? | 	? | 	?

Lembre-se das ferramentas que vimos na teoria e praticaram na room:
- SAST: Semgrep (código-fonte)
- SCA: Trivy (dependências)
- Secrets scanning: Gitleaks (credenciais no código)
- DAST: OWASP ZAP / Nikto (aplicação em execução)
- Scan de rede: nmap (serviços e versões)
- Gestão: OpenVAS (plataforma completa)

Preencha com qual ferramenta vocês usariam em cada etapa e por quê.

## 2. Cruzar serviços com CVEs

No arquivo `02-analise-de-vulnerabilidades.md`, adicione:

Ferramenta de Scan Selecionada
- Ferramenta: nmap / Nikto / OpenVAS - escolha a mais adequada ao seu cenário
- Justificativa: por que esta ferramenta faz sentido no meu cenário - 2 a 3 linhas

### Serviços Identificados (simulados para o meu cenário)
| Serviço | Versão | CVE encontrada | CVSS | Prioridade
|-----|-----|-----|-----|---
| (ex.: nginx) | (ex.: 1.10.3) | (ex.: CVE-2026-42945) | (ex.: 9.2) | (ex.: Crítica)
| ?|? | ? |	? |	?
| ?|? | ? |	? |	?

Para preencher esta tabela, pense: "quais serviços rodariam no meu cenário?" e busque CVEs reais no [NVD](nvd.nist.gov) para essas versões.

> Dica: você pode usar os serviços que encontraou na room como inspiração, mas adapte ao seu cenário. Se seu cenário é um hospital, pense em sistemas de prontuário eletrônico. Se é uma fintech, pense em APIs de pagamento.
