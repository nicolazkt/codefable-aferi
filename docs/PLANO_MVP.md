# Plano do MVP e requisitos — 06/11/2026

## 1. Problema
Hoje, dados de laboratórios de fabricantes de intertravados podem ficar dispersos entre fichas, planilhas e laudos. O Aferi deve reduzir retrabalho, erros de transcrição e dificuldade para localizar o histórico por produto/lote, sem obrigar a fábrica a reproduzir digitalmente cada etapa da norma.

## 2. Público e proposta
Usuários iniciais: responsável pela qualidade, operador de laboratório e gestor. Projeto preparado para ser instalado em empresas diferentes, mas **primeiro MVP = uma empresa por instalação**. Isso evita um SaaS multi-tenant antes de validarmos o uso real.

## 3. Jornada principal (PAVER)
`Cadastrar produto → registrar lote → registrar ensaio → lançar forças em tf → visualizar MPa por CP e fpk → avaliar → gerar laudo → consultar histórico`.

Uma nova idade de ensaio (por exemplo 24 h, 7 d ou 28 d) pode ser registrada sobre o mesmo lote. Não gerar automaticamente três ensaios se a fábrica não trabalhar assim.

## 4. Requisitos essenciais
| ID | Prioridade | Comportamento |
|---|---|---|
| RF-01 | MVP | Configurar dados básicos da empresa (nome, logo, dados do laudo) e usuários com acesso |
| RF-02 | MVP | Cadastrar produtos: modelo/código, categoria, classe normativa quando aplicável, dimensões nominais, metas internas, padrão de unidade |
| RF-03 | MVP | Cadastrar lotes: produto, lote, fabricação, máquina/linha (opcional), quantidade/área produzida (quando informada), observações |
| RF-04 | MVP | Criar ensaio de compressão PAVER por lote e idade, com data, amostra/CPs, força por peça, inspeção simples e notas |
| RF-05 | MVP | Aceitar **tf como unidade padrão de lançamento**, mostrar MPa automaticamente por peça sem conversões manuais intermediárias; preservar força e unidade originais |
| RF-06 | MVP | Calcular média e resistência característica estimada (`fpk,est`) com fórmula e parâmetros da edição normativa aplicável |
| RF-07 | MVP | Exibir resultado técnico, meta interna e **estado normativo separados**; sinalizar amostragem insuficiente, dados faltantes e procedimento diferente |
| RF-08 | MVP | Gerar laudo imprimível/exportável em PDF com identificação do lote, CPs, unidades, resultados, referência normativa, observações e responsável |
| RF-09 | MVP | Listar/pesquisar por período, produto, lote, idade e situação; mostrar indicadores básicos de ensaios e resistência |
| RF-10 | MVP | Permitir correção dos lançamentos com justificativa e trilha simples de alterações; não perder o valor original |
| RF-11 | MVP | Login e permissões básicas (administrador e laboratório); isolamento de dados por instalação |
| RF-12 | MVP | Exportar dados em formato aberto (CSV/JSON) e manter migrações versionadas do banco |
| RF-13 | Próximo | Importação CSV, caso a operação piloto realmente precise, sem integração automática PPCP na primeira entrega |
| RF-14 | Próximo | Reutilizar a jornada no módulo BLOCO e depois PLACA com calculadoras específicas |

**Requisitos não funcionais:** interface utilizável no computador do laboratório; operação ágil; validação de entrada e mensagens claras; cálculo determinístico; ausência de segredos no navegador/repositório; logs mínimos; layout de laudo adequado a A4.

## 5. Regras de experiência
- Não criar campos obrigatórios só porque aparecem na norma. Pedir apenas o necessário para **registrar**; exigir evidências adicionais apenas para **avaliar como normativo**.
- Permitir quantidade de corpos de prova diferente da amostragem prescrita, mas **não permitir afirmar conformidade normativa com dados insuficientes**.
- Unidades visíveis ao operador: tf (preferencial), kN ou N; cálculos usam N internamente. Nunca exigir digitar tf, depois kgf e depois N.
- Classificação de laudo tem fonte explícita: **norma / meta interna / não avaliado**. A condição interna não é sinônimo de atendimento à ABNT.
- Validação de formulário bloqueia erros físicos e técnicos básicos (valor negativo, força ausente para calcular, dimensões impossíveis), mas avisos de procedimento geram pendência, não desaparecimento do dado.
- Não presumir que ensaio de 24 h ou 7 d comprova o requisito de 28 d. São acompanhamento interno, salvo circunstância normativa específica documentada.
- O relatório não pode afirmar resultado definitivo sem idade, amostragem e critérios pertinentes.

## 6. Telas mínimas
1. **Painel:** totais simples, últimos lotes, alertas e evolução básica.
2. **Produtos:** listagem e formulário de especificação.
3. **Lotes:** listagem, detalhe e ensaios associados.
4. **Lançamento de ensaio:** grade de CPs (tf → MPa em tempo real), média, fpk, notas e inspeção.
5. **Laudo:** prévia e impressão/exportação.
6. **Configurações:** dados da empresa, metas internas e usuários.

Sem telas separadas para cada parâmetro normativo. Preferir abas/seções contextuais.

## 7. Três marcos de entrega
**Marco A — Planejamento e base (atual):** documentação aprovada; projeto Next.js; banco e migrações; autenticação básica; cadastro de produto/lote.

**Marco B — Paver funcional:** entrada de ensaio, calculadora testada, resultado interno/normativo distinto, histórico, laudo PDF e indicadores essenciais. **Este é o primeiro produto utilizável.**

**Marco C — Expansão modular:** bloco (compressão pela área bruta, regras/validação próprias); placa (tração na flexão). Somente depois considerar importação PPCP, automações ou indicadores mais complexos.

Não abrir múltiplas frentes antes de fechar o marco B.

## 8. Critérios objetivos para dizer que PAVER está pronto
- Um operador cadastra produto e lote, lança 6 CPs em tf e vê MPa individual e fpk corretamente.
- Amostra com menos CPs que o requisito pertinente permanece salva, com aviso e **sem selo de conformidade ABNT**.
- A diferença entre 24 h, 7 d e 28 d aparece claramente.
- Laudo identifica lote, produto, amostra, idade, dados originais, cálculos, método/edição e conclusão com seu escopo.
- Corrigir um valor exige justificativa e gera registro do que foi alterado.
- Um segundo usuário consegue consultar um lote e emitir novamente o laudo.
- Testes automatizados cobrem conversão de unidades, fator p, fpk/ψ, estados normativos e casos limites.
- Exportação dos registros funciona, garantindo que os dados não ficam presos a um serviço.

## 9. Não fazer no primeiro MVP
Sem microserviços, configuração universal de formulários, editor de normas, BI avançado, integrações com prensa/ERP/PPCP, apps nativos, múltiplas empresas na mesma instalação, geração de ensaios automática com regras complexas, nem um sistema inteiro de gestão da produção.

## 10. Questões abertas mínimas
- O piloto será conduzido com qual fluxo real de laboratório e quais campos são indispensáveis para a equipe?
- O acesso inicial será apenas interno ou também de clientes externos para consultar laudos? **Padrão proposto: apenas interno.**
- Aprovar a instalação separada por empresa no início, em vez de SaaS multiempresa.
