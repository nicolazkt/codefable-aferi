# Arquitetura proposta — simples e portátil

**Estado:** arquitetura técnica proposta; **modelo de implantação independente por empresa confirmado pelo usuário em 06/11/2026**. Tecnologias de apoio exatas serão fixadas no Marco A. Evitar dependências desnecessárias.

## Stack
- **Next.js (App Router) + React + TypeScript**, aplicação web full-stack única; APIs/ações de servidor dentro do próprio projeto. **Node.js** como alvo primário de execução.
- Componentes de interface simples e responsivos; Tailwind CSS se facilitar a execução, sem impor kit visual complexo.
- **PostgreSQL** como modelo de banco (padrão amplamente portável). **Neon** é candidato para ambiente de desenvolvimento/teste, não dependência conceitual da aplicação.
- **Drizzle ORM** + migrações versionadas como proposta para schema explícito e controle de SQL. Separar acesso ao banco dos serviços de domínio.
- Validação de entradas com schemas TypeScript/Zod, se escolhida na implementação.
- Testes unitários da matemática e smoke test dos principais fluxos; não montar infraestrutura pesada de testes E2E.

## Portabilidade
`Navegador → Next.js/Node → serviços de domínio → repositórios de dados → PostgreSQL`

As calculadoras normativas são funções puras em TypeScript, não consultas SQL nem regras espalhadas nas telas.

**Decisão confirmada: uma instalação por empresa.** Cada implantação terá aplicação, variáveis de ambiente, usuários, banco e backup próprios. Uma tabela de configuração da empresa é suficiente; não introduzir `tenant_id` em dezenas de consultas nem seletor de empresas. Reutilizar o **mesmo código e migrações** em todas as instalações. Migração entre provedores se dará por backup/restore do PostgreSQL e reconfiguração da conexão, não por migração entre tenants.

Modelo de implantação (exemplo, sem dados reais):
```text
Empresa A → Aferi (instância A) → PostgreSQL A
Empresa B → Aferi (instância B) → PostgreSQL B
```

A infraestrutura de cada empresa pode variar, mas a separação lógica e operacional dos dados deve permanecer. Exportação em formatos abertos e estratégia de backup fazem parte da portabilidade.

Deploy inicial: execução local/Node. Avaliar demonstração na Cloudflare Workers somente quando o fluxo estiver funcional. O adaptador Cloudflare é uma decisão de **infraestrutura**, não deve governar a modelagem ou a matemática. Documentação oficial consultada em 06/11/2026 recomenda `vinext` para novos projetos Next em Workers; essa recomendação pode mudar:
- https://developers.cloudflare.com/workers/framework-guides/web-apps/nextjs/
- https://nextjs.org/docs/app/getting-started/deploying

Neon utiliza PostgreSQL e conexão padrão; usar variáveis de ambiente, não credenciais no código:
- https://neon.com/docs/get-started/connect-neon

## Organização inicial do código (a implementar)
```text
src/
  app/                   # telas, rotas e API do Next.js
  components/            # elementos reutilizáveis
  features/
    produtos/
    lotes/
    ensaios/
    laudos/
    indicadores/
  domain/
    common/              # unidades, tipos e estados
    paver/               # cálculos e critérios NBR 9781
    bloco/               # implementação futura NBR 6136
    placa/               # implementação futura NBR 9781
  db/                    # schema, migrações, queries
  lib/                   # autenticação, logger, utilidades
tests/
```

**Proibido por padrão:** um "motor universal de normas" parametrizável com dezenas de regras arbitrárias. Criar implementações pequenas por família de produto e abstrair somente duplicações verificadas.

## Entidades mínimas
- `organization_settings`: cabeçalho e identidade da instalação.
- `users`: credenciais/identidade e papel.
- `products`: código, nome, família, dimensão nominal, classe aplicável, critério interno versionado.
- `lots`: identificação externa, produto, fabricação, máquina/linha opcional e quantidade.
- `tests`: lote, método/tipo, idade, data, referência normativa, status e observações.
- `specimens`: CP, valor de força, unidade original, características/medidas e resultado calculado.
- `reports`: referência ao ensaio e versão/snapshot dos resultados publicados.
- `audit_events`: autor, data, campo alterado e motivo.

É uma proposta lógica — o banco físico será modelado com o mínimo de tabelas necessário. Não salvar somente o resultado arredondado: preservar força original, valores intermediários necessários e versão do cálculo.

## Conformidade e estados
Três camadas independentes:
1. **Medição:** o que foi efetivamente informado e calculado.
2. **Controle interno:** comparação com a meta operacional configurada para o produto/idade.
3. **Avaliação normativa:** conforme / não conforme / não avaliado, com base na edição e nos requisitos documentados.

Para afirmação de conformidade, checar amostragem, idade, procedimento e requisitos aplicáveis. Quando a evidência é insuficiente, registrar pendências; não inferir aprovação. "Ensaio válido" e "lote aceito" são coisas diferentes.

## Segurança e qualidade
- Sessões e autenticação por biblioteca mantida; não implementar criptografia ou login próprio.
- Segredos via variáveis de ambiente; dados de empresas reais não entram no GitHub público.
- Correções dos resultados registradas, com motivo, antes de gerar nova versão de laudo.
- Backups e restauração são independentes para cada implantação, com rotina e retenção definidos na implantação; exportação deve existir no MVP.
- Não misturar credenciais, logs, arquivos ou armazenamento entre instalações; a equipe de suporte deve acessar somente a instância autorizada.
- Conclusão técnica deve ser rastreável até amostra, produto, regra e data.

## Separação de responsabilidades
- **ChatGPT com GitHub:** planejamento, documentação, revisão de mudanças pequenas, manutenção de contexto.
- **Agente no VS Code:** implementação multi-arquivo, execução local, testes, ajustes de UI e migrações.
- **Regra:** não pedir a dois agentes para editar simultaneamente a mesma área. Inspecionar estado atual do repositório antes de cada tarefa.
