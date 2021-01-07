# Otimização da Abertura de Poços Produtores de Petróleo Utilizando Algorítmos Genéticos 

#### Aluno: [Luiz Fernando Giovanelli](https://github.com/Lfgiovan).
#### Orientadora: [Ana Carolina Abreu](https://github.com/acarolina1612).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](Otimização%20Modelo_RevB.xlsm).

---

### Resumo

O modelo tem por objetivo otimizar o cronograma de abertura dos poços produtores de petróleo, em relação ao originalmente planejado, de modo a atender a restrição da capacidade de processamento de óleo da unidade estacionária de produção (UEP). Com essa otimização do cronograma, temos a data de necessidade de abertura de cada poço produtor, insumo essencial para a determinação da estratégia de contratação dos dutos flexíveis que serão responsáveis por levar o óleo desde a cabeça do poço até a UEP.

#### Descrição do Modelo

- Quantidade de poços produtores: 24.
- Histórico de produção de 01/01/2025 até 01/12/2064 (40 anos).
- Capacidade máxima de tratamento de óleo da UEP (Coluna AA - “LIMITE”): 15.000,00 m3/d.
- Variável de decisão: Atraso – quantidade de meses que o poço pode atrasar (se Atraso > 0) ou que a abertura do poço pode adiantar (se Atraso < 0). Se Atraso for zero, significa que o poço será aberto na data planejada antes da otimização do cronograma.
- Limites da variável de decisão: As Linhas 2 e 4 apesentam os limites inferior e superior de cada variável de decisão. O limite inferior foi definido como a quantidade de meses necessários para antecipar a abertura do poço de modo que esta ocorra em 01/01/2025. O limite superior considera que o cada poço somente pode ser postergado até o mês 200.
- NP Atualizado: Soma da produção de todos os poços mês a mês, considerando o valor presente da produção com uma taxa de 0,8333% ao mês.
- Função objetivo: soma da coluna NP atualizado.
- Restrição: como o Solver do Excel possui um limite na quantidade de variáveis, não seria possível selecionar a Coluna LIMITE da Aba FPSO Otimizado. O objetivo da restrição é garantirmos que a soma da produção de todos os poços nunca ultrapasse o limite da capacidade máxima de tratamento de óleo da UEP (15.000,00 m3/d). Neste sentido, criamos uma célula chamada “Restrição - soma dos valores negativos de MARGEM deve ser zero”, através da qual somamos todos os itens negativos da coluna MARGEM (LIMITE – TOTAL). Por fim, a restrição passou a ser que esta célula deve ser zero.

#### Aba “FPSO Base”

- Recebe os dados estimados de produção dos poços P1 ao P24 nas colunas C até a Z.
- A Coluna A é um contador.
- A Coluna B contém as datas do intervalo onde foram simulados os dados de reservatório. Neste caso é o período de concessão da exploração do Campo de Petróleo.
- A Linha 1 contém os dados do contador, momento a partir do qual o poço é aberto.
- A Coluna AA contém os limites da capacidade de tratamento de óleo no FPSO. 

#### Aba “FPSO Otim”:

- Recebe os dados estimados de produção dos poços P1 ao P24 nas colunas C até a Z. A produção é puxada da Aba “FPSO Base”, porém considerando o resultado da variável de decisão “Atraso” (Linha 3, Coluna C a Z). As otimizações utilizaram o Solver Evolucionário do Excel, no arquivo `Otimização Modelo_RevA. xlsm`. Como parâmetros utilizados no Solver temos:
  - Convergência: 0,0001.
  - Taxa de mutação: 10%.
  - Tamanho da população: 200.
  - Tempo máximo sem aperfeiçoamento: 600s.

Inicialmente foram realizadas cinco otimizações (os resultados encontram-se na tabela das células AE9 até BE15), sempre utilizando como semente inicial o valor zero para o “Atraso” de cada um dos 24 poços. Dentre estes, utilizamos o resultado com o maior valor da função objetivo como semente (Semente 2) para as próximas cinco otimizações, as quais estão dispostas nas células AE17 até BE21.

Verificamos que não houve melhora na função objetivo para o segundo conjunto de otimizações. Desta forma, fizemos testes alterando o tamanho da população para 400 e mantendo-se constantes os demais parâmetros do solver evolucionário (conjunto 3 das otimizações), contudo melhores resultados não foram atingidos.

---

Matrícula: 192.190.067

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
