# Previsão do Preço de Energia

#### Aluno: [Matheus Rangel Cardoso](https://github.com/MatheusRangelCardoso).
#### Orientadores: [Leonardo Forero Mendonza](https://github.com/leofome8) e [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](TCC_Energia.ipynb).

---

### Resumo

O trabalho de conclusão de curso tem como objetivo construir um modelo capaz de prever qual será o preço da energia na próxima hora.

O modelo utiliza como base de dados:

1. Dados históricos do consumo de energia da Espanha;
2. Dados históricos de características climáticas presentes em cinco cidades da Espanha: **Valencia, Madrid, Bilbao, Barcelona e Seville**.

É realizado um pré-processamento nas duas bases de dados para a verificação de registros nulos e registros duplicados. Não foi realizada uma análise profunda para a verificação de *outliers*. Logo, variáveis com "suspeitas de *outliers*" não foram consideradas para a criação do modelo. Após a realização do pré-processamento foi realizado um "*merge*" entre as duas bases de dados, possibilitando assim o cruzamento de informações entre o consumo de energia e os dados climáticos para a construção do modelo.

Após o ajuste da base de dados, são criados três modelos utilizando a mesma arquitetura de rede neural:

1. LSTM (*Long Short Time Memory*): Com 100 neurônios. Camada responsável por "aprender" a dependência temporal de longa duração na série;
2. *Dropout*: Camada para ajudar na capacidade de generalização da rede, prevenindo o *overffiting* do modelo. Esta camada de *dropout* possui 20% de chance de ativação, isto é, durante a realziação do treinamento, o *output* de um neorônio terá 20% de chance do seu valor ser substituido por "0". Desta maneira, um neurônio não vai ficar "especializado" durante o treinaemnto ajudando assim a combater o *overfitting* do modelo;
3. *Flatten*: Responsável por vetorizar o resultado da rede neural. Essa camada foi adicionada para que o *output* seja exibido em um *array* (possibilitando a manipulação dos dados do *output* de uma maneira mais otimizada);
4. *Dense*: A camada *dense* é responsável por resolver o problema de forma não linear. Essa camada é responsável por passar o resultado produzido por um neurônio em uma função não linear, possibilitando assim a resolução de problemas complexos e não lineares. Essa camada foi configurada com 100 neurônios e possui a função de ativação "relu".

    ![image](https://user-images.githubusercontent.com/39468750/115156371-46303f80-a05a-11eb-8f5e-e39c00ec2c72.png)

    Para a função relu, se o valor produzido por um neurônio for negativo, ele será automaticamente 0, caso for positivo, ele será transformado e considerado;

5. *Dropout*: Com 10% de chance de ativação;
6. *Dense*: Com uma função de ativação linear possuindo um único neurônio.

    **Otimizador**: Adam. O otimizador é um algorítimo usado para modificar os atributos de uma rede neural a cada época de treinamento com o intutio de reduzir o erro produzido pela rede neural a cada época. 

    Exemplo: a cada época de treinamento, a rede passa por um ajuste nos pesos de seus neurônios para que no próximo treinamento o erro seja cada vez menor, e esse ajuste nos pesos é realizado por conta do otimizador.


A única diferença entre cada modelo é o **número de variáveis utilizadas como *input*** para realizar a previsão do consumo de energia:

- Modelo 1: Possui 16 variáveis;
- Modelo 2: Possui 10 variáveis;
- Modelo 3: Apresenta apenas o janelamento de uma única variável ("*price day ahead*") cinco horas atrás, possuindo assim 6 variáveis.

O intuito da criação de três modelos com diferentes variáveis de *input* é verificar se o modelo construído pela rede neural é capaz de realizar previsões assertivas com a redução da complexidade do modelo, isto é, verificar se a medida que as variáveis de *input* são retiradas do modelo, a rede neural é capaz de melhorar suas previsões ou não.

Os três modelos são avliados utilizando duas métricas de avaliação:

- *Root-mean-square deviation* (RMSE);
- *Mean absolute percentage error* (MAPE).

Após a avaliação dos modelos, constatou-se que o último modelo (**modelo 3**), utilizando o janelamento da variável "*price day ahead*" cinco horas para trás apresentou um melhor resultado do que os outros dois modelos anteriores. Desta maneira, a realização do janelamento da variável "*price day ahead*" foi suficiente para a criação de uma rede neural capaz de realizar a previsão do preço do consumo de energia.

---

Matrícula: 191.671.027

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
