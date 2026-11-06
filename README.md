# CodeFable Aferi

Sistema modular de gestão laboratorial e controle de qualidade para fabricantes de artefatos de concreto: peças/pavers, blocos e placas.

**Estado em 06/11/2026:** planejamento inicial. O repositório foi iniciado com documentação; a aplicação ainda não foi implementada.

## Objetivo
Centralizar cadastro de produtos e lotes, registro de inspeções e ensaios, cálculo de resultados, análise de conformidade, emissão de laudos e indicadores básicos de qualidade. Referência técnica nas ABNT NBR 9781-1/-2:2026 e ABNT NBR 6136-1/-2:2026.

## Princípio de produto
**Normativo nos cálculos e transparente nos desvios; flexível na operação.**

As regras normativas devem estar identificadas e versionadas, mas não devem impedir o registro de ensaios internos ou com amostragem diferente. Um ensaio não elegível para avaliação normativa **não pode ser apresentado como conforme à ABNT**. Diferenciar:
- Resultado medido/calculado;
- Meta interna definida pela empresa;
- Avaliação normativa, quando aplicável;
- Situação do lote e pendências de evidência.

## Ordem de execução
1. **Paver/peça:** fluxo completo mínimo — produto → lote → ensaio de compressão → resultado/fpk → laudo → consulta.
2. **Bloco:** reutilizar fluxo, incluir cálculo pela área bruta e regras da NBR 6136.
3. **Placa:** reutilizar fluxo, incluir ensaio de tração na flexão e regras aplicáveis.

Uma única aplicação modular, sem microserviços ou mecanismo genérico de normas.

## Fonte de contexto
- [Plano do MVP e requisitos](docs/PLANO_MVP.md)
- [Decisões de arquitetura e portabilidade](docs/ARQUITETURA.md)
- [Matriz normativa e tratamento de desvios](docs/MATRIZ_NORMATIVA.md)
- [Decisões, contexto e pendências](docs/DECISOES_CONTEXTO.md)
- [Instruções para agentes e contribuidores](AGENTS.md)

**Regra de continuidade:** após cada alteração importante, atualizar os documentos afetados e registrar decisões novas em `docs/DECISOES_CONTEXTO.md`. O estado do GitHub é a referência compartilhada, não o histórico de um chat.

## Normas e direitos autorais
Os quatro PDFs de normas foram fornecidos como anexos no contexto de trabalho do projeto, mas **não são redistribuídos neste repositório público**. A matriz registra normas, edições e referências às seções para consulta em cópias licenciadas. Não copiar páginas, tabelas completas ou arquivos integrais da ABNT para o GitHub sem autorização adequada.

## Fora de escopo por ora
ERP/PPCP, controle estatístico avançado, IA de previsão, automação da prensa, aplicativo móvel nativo, multiempresa SaaS, sistema completo de auditorias e dezenas de telas de cadastro.

Este repositório não promete certificação, acreditação de laboratório ou garantia automática de conformidade legal.
