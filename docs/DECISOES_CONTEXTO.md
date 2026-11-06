# Decisões, contexto e pendências

## Contexto estável (06/11/2026)
- Produto: CodeFable Aferi, sistema para laboratórios e qualidade de fabricantes de artefatos de concreto.
- Problema a evitar: versão anterior rígida, enorme, com excesso de regras obrigatórias e bugs.
- Expectativa: normas como referência técnica principal, mas operação flexível, rápida e adaptável.
- Sequência solicitada: **Paver → Bloco → Placa**, sempre entregando um fluxo utilizável antes de ampliar escopo.
- Forma de trabalho: híbrida — planejamento/alterações pequenas via ChatGPT+GitHub; implementação com agente no VS Code quando houver edição/teste local extensivo.
- GitHub é a base de contexto compartilhada; não depender de memória de chat.
- **Implantação confirmada:** uma empresa por instalação, com instância de aplicação e banco de dados próprios; sem multi-tenant compartilhado no MVP.
- Banco e hospedagem ainda não foram formalmente decididos. Cloudflare citada como possibilidade para teste online, não exigência de produção.
- Os PDFs das normas estão anexados ao contexto de trabalho; não colocá-los num GitHub público sem licença de redistribuição.
- Nenhum dado operacional real, imagem de cliente, conta, token ou conexão privada deve ser colocado no repositório público.

## Registro de decisões

| ID | Data | Estado | Decisão | Razão |
|---|---|---|---|---|
| D-001 | 2026-11-06 | Confirmada pelo briefing | Ordem Paver → Bloco → Placa | MVP rápido, modular |
| D-002 | 2026-11-06 | Confirmada pelo briefing | Regras normativas sem formulário universal rígido | Aderir à fábrica e preservar rastreabilidade |
| D-003 | 2026-11-06 | Confirmada pelo briefing | GitHub como memória de projeto e trabalho híbrido com VS Code | Reduz perda de contexto |
| D-004 | 2026-11-06 | Proposta | Aplicação Next.js/React/TypeScript monolítica em Node.js | Menos infra e menor manutenção |
| D-005 | 2026-11-06 | Proposta | PostgreSQL + migrações Drizzle; Neon opcional para testes | Portabilidade entre provedores PostgreSQL |
| D-006 | 2026-11-06 | **Confirmada pelo usuário** | Uma empresa por instalação, com aplicação e banco independentes; sem SaaS multi-tenant no MVP | Simplicidade, isolamento e portabilidade |
| D-007 | 2026-11-06 | Proposta | Diferenciar controle interno de avaliação normativa | Impedir laudo que declare conformidade sem evidência |
| D-008 | 2026-11-06 | Proposta | Cloudflare somente após MVP local validado | Evitar acoplar domínio a plataforma de deploy |
| D-009 | 2026-11-06 | Proposta | Entrada de força em tf, cálculo interno em N | Aderência ao fluxo real do laboratório |

## Pendências que realmente mudam o produto
1. Confirmar se o primeiro piloto terá **somente usuários internos** (proposta) ou acesso externo de clientes aos laudos.
2. Na implementação do Paver, validar uma ficha e um laudo reais (com dados anonimizados) para confirmar os campos mínimos e o leiaute.
3. Verificar a referência cruzada 9781-1:2026 → 9781-2:2025 mencionada no texto do documento, antes de afirmar cobertura normativa integral.

## Consequências da D-006
- Cada cliente terá configuração de empresa, usuários, dados e credenciais do banco exclusivos daquela implantação.
- Migrações do schema serão compartilhadas no código; instalação e restauração de backup serão independentes.
- Um mesmo projeto/versão poderá ser implantado várias vezes sem introduzir `tenant_id` ou selector de empresas no produto.
- Uma futura oferta SaaS compartilhada exigirá nova decisão de arquitetura e segurança; não antecipá-la no MVP.

## Próxima tarefa executável
**Marco A:** inicializar aplicação Next.js/TypeScript; definir schema mínimo e seed fictício; montar cadastro de produto/lote. Somente depois começar o ensaio de paver. Nada foi implementado ainda.

## Como atualizar este arquivo
Ao encerrar uma tarefa, registrar o que foi feito, o que ficou pendente e qualquer decisão relevante. Sempre separar **confirmado pelo usuário**, **proposto** e **implementado/testado**. Não registrar hipóteses como resultados comprovados.
