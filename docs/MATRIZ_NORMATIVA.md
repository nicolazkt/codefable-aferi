# Matriz normativa inicial — versão 06/11/2026

> Resumo técnico de planejamento, **não substitui as normas originais**. Referências de página abaixo correspondem às páginas físicas dos PDFs fornecidos, que incluem capa e prefácio. Para decisões de conformidade e implementação, consultar o dispositivo completo na cópia licenciada. Não reproduzir PDFs integralmente em repositório público.

## Inventário dos anexos de referência
| Arquivo fornecido | Edição | Tema | Módulo |
|---|---|---|---|
| `Normas BR 9781-1.pdf` | ABNT NBR 9781-1:2026 | Requisitos de peças e placas para pavimentação intertravada | Paver, placa |
| `Normas BR 9781-2.pdf` | ABNT NBR 9781-2:2026 | Métodos de ensaio para pavimentação intertravada | Paver, placa |
| `Normas BR 6136-1.pdf` | ABNT NBR 6136-1:2026 | Requisitos de blocos vazados de concreto | Bloco |
| `Normas BR 6136-2.pdf` | ABNT NBR 6136-2:2026 | Métodos de ensaio para blocos vazados | Bloco |

## PAVER — prioridade 1
- A NBR **9781-1:2026, Seção 7 / Tabela 5 (PDF p. 14)** diferencia peças de concreto simples (mínimo característico **35 MPa**), peças permeáveis (**25 MPa**) e peças simples para abrasão intensa (**50 MPa**). A classificação depende de tipo e uso, não apenas do nome comercial.
- A NBR **9781-2:2026, Anexo C (PDF pp. 17–20)** descreve compressão axial em peças; o resultado individual usa a força máxima em N, área de carregamento da placa/dispositivo circular e fator de correção `p` pela espessura nominal. **Não usar a área total da peça**, nem a área bruta usada nos blocos.
- O dispositivo de ensaio nominal tem diâmetro **85 mm**, e a norma inclui requisitos da aparelhagem. Fator `p` deve vir da Tabela C.1 (por exemplo, 60 mm → 0,95; 80 mm → 1,00).
- A preparação do ensaio de compressão inclui saturação em água por **no mínimo 24 horas** antes do ensaio, conforme NBR 9781-2, Anexo C.5 (PDF p. 18). Registrar observação de procedimento no MVP; não exigir que o operador preencha um formulário gigantesco.
- A resistência característica estimada `fpk,est` usa as resistências individuais ordenadas, fórmula e limite inferior com o coeficiente **ψ** dependente de `n` (Anexo C.7, PDF p. 19). Não substituir por média nem por um desvio-padrão inventado.
- A NBR **9781-1:2026, Seções 19, 21, 23, 25 e 26 (PDF pp. 19–22)** trata de lote, requisitos, amostragem, idades e aceitação. Para avaliação normativa, a adequação da amostragem e dos demais critérios deve ser verificada. A tabela de amostragem varia com o tamanho do lote; não presumir sempre 6 CPs.
- A avaliação de 24 h e 7 d pode ser útil como controle interno, mas **não deve receber automaticamente a mesma conclusão de 28 d**. A regra de 80% da resistência para entrega antes de 28 dias depende da condição de controle e do momento pertinente (Seções 7 e 25); não converter em meta universal de qualquer ensaio precoce.

## BLOCO — prioridade 2
- NBR **6136-1:2026, Seções 4.3 e 7 / Tabelas 1 e 6 (PDF pp. 11 e 14)** traz classes por uso e resistência. A nomenclatura normativa A/B/C e subclasses B exige cuidado: um cadastro interno "estrutural 4,5 MPa" **não se torna automaticamente uma classe normativa 4,5**.
- NBR **6136-2:2026, Anexo B (PDF pp. 12–14)** define medições e área bruta pela largura × comprimento do bloco, sem descontar vazados.
- No Anexo C.7 (PDF p. 18), resistência individual do bloco = força em N / área bruta em mm². **Não usar fator de correção `p` do paver**.
- O cálculo da resistência característica estimada usa resultados ordenados e **ψ** por tamanho de amostra (Anexo C.8, PDF p. 19).
- Anexo C.9 (PDF p. 19) contém condicionantes de validação do ensaio ligadas à umidade relativa do bloco-testemunho. Resultado calculado não implica automaticamente ensaio válido ou lote aceito.
- NBR **6136-1:2026, Seções 16–20 (PDF pp. 17–19)** trata de amostras, idades e aceitação; consultar no desenvolvimento do módulo.

## PLACA — prioridade 3
- A NBR **9781-1:2026, Seção 8 / Tabela 6 (PDF pp. 14–15)** diferencia placas simples e permeáveis por **resistência característica à tração na flexão** (respectivamente **3,5 MPa** e **2,5 MPa**, conforme classes indicadas).
- A NBR **9781-2:2026, Anexo D (PDF a partir da p. 21)** apresenta método próprio de flexão e cálculo característico. **Não reutilizar a calculadora de compressão**.

## Outras inspeções e ensaios
- Paver: inspeção visual, dimensional, absorção de água e permeabilidade conforme classe/condição; requisitos e amostragem previstos na NBR 9781-1, Seções 5, 6, 9, 10, 21–23.
- Bloco: inspeção visual, dimensional, absorção e demais controles previstos na NBR 6136-1/-2.
- Essas rotinas podem entrar em versões incrementais, **mas um laudo somente de compressão deve se declarar "laudo de ensaio de compressão"**, não certificar o cumprimento de todos os requisitos do lote.

## Decisão obrigatória de modelagem
`resultado_medido`, `avaliacao_interna`, `avaliacao_normativa`, `validade_do_ensaio` e `aceitacao_do_lote` são conceitos distintos. Se faltam evidências para qualquer um deles, usar **"não avaliado / evidência insuficiente"**, nunca "aprovado" por omissão.

## Ponto de verificação antes do motor de conformidade
O texto fornecido da **NBR 9781-1:2026** contém referências à **NBR 9781-2:2025**, enquanto o documento fornecido da Parte 2 está identificado como edição **2026**. Verificar a relação entre as edições/referências normativas com a fonte oficial antes de afirmar validação integral. Não corrigir silenciosamente os documentos.

## Conversão de unidades — não é requisito de digitação
A UI aceita **tf** diretamente. Para cálculo, converter internamente:
`F(N) = força(tf) × 9.806,65`.
Manter o valor original e mostrar resultado em MPa automaticamente. O usuário não deve converter manualmente tf → kgf → N.
