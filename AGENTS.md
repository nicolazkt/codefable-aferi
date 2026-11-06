# Instruções de execução — CodeFable Aferi

Leia antes de implementar qualquer alteração:
1. `README.md`
2. `docs/PLANO_MVP.md`
3. `docs/ARQUITETURA.md`
4. `docs/MATRIZ_NORMATIVA.md`
5. `docs/DECISOES_CONTEXTO.md`

## Ordem de prioridade
**Primeiro Paver funcional. Depois Bloco. Depois Placa.** Não iniciar módulos paralelos, dashboards avançados ou integração PPCP sem necessidade comprovada.

## Regras inegociáveis
- Registrar o dado laboratorial mesmo quando o procedimento não for normativo. **Não** rotular ensaio incompleto como conforme à ABNT.
- Separar: resultado medido, meta interna, avaliação normativa, validade do ensaio e aceitação do lote.
- Não transferir fórmulas de um módulo para outro: paver tem dispositivo de carregamento e fator p; bloco usa área bruta; placa usa flexão.
- Operador digita **tf**; a conversão para N ocorre no cálculo e a saída deve mostrar MPa. Preservar valores brutos e unidade original.
- Normas e versões são referenciadas em cada regra técnica e laudo. Consultar a cópia licenciada antes de implementar/calibrar equações e condições normativas.
- Evitar lógica normativa solta em componentes React. Domínio em funções puras tipadas, com testes unitários e exemplos conferidos.
- Sem microserviços, motor genérico de formulários ou abstração prematura. Priorizar interface simples, poucos campos e pouco código.
- Nunca commitar PDFs da ABNT, dados reais de fábricas, credenciais, chaves ou variáveis de ambiente.
- Mudanças que afetam cálculo/laudo exigem testes e revisão da matriz normativa.
- Não alterar deployment, banco de produção, domínio, credenciais ou infraestrutura sem autorização explícita.

## Prática de trabalho
Antes de codar: inspecionar repositório/branch, ler a decisão relacionada e declarar escopo mínimo. Depois: executar build/testes disponíveis, mostrar resultados, atualizar documentação pertinente e registrar a decisão. Evitar refatorações amplas ou testes E2E custosos sem evidência de necessidade.

**GitHub é o contexto durável.** Uma sessão nova de ChatGPT ou VS Code deve reconstruir o estado do projeto a partir dos arquivos e commits, e não presumir decisões esquecidas em conversas.
