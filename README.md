# Trabalho de Conclusão de Curso - Previsão do Preço de Energia.

#### Aluno: [Matheus Rangel Cardoso](https://github.com/MatheusRangelCardoso)
#### Orientadores: [Leonardo Mendonza](https://github.com/leofome8) e [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/MatheusRangelCardoso/tcc-bi-master-2019.1).


---

### Resumo

Trabalho de conclusão de curso com o objetivo de construir um modelo capaz de prever qual será o preço da energia na próxima hora.
<br>
O modelo utiliza como base de dados:
<br>
<br>
1 - Dados históricos do consumo de energia da Espanha
<br>
2 - Dados históricos de características climáticas presentes em cinco cidades da Espanha: **Valencia, Madrid, Bilbao, Barcelona e Seville.**
<br>
<br>
É realizado um pré processamento nas duas bases de dados para a verificação de registros nulos e registros duplicados. Não foi realizada uma análise profunda para a verificação de outliers. Desta maneira, variáveis com "suspeitas de outliers" não foram consideradas para a criação do modelo. Após a realização do pré processamento, é realizado um **"merge"** entre as duas bases de dados, possibilitando assim o cruzamento de informações entre o consumo de energia e os dados climátiocs para a construção do modelo.
<br>
<br>
Após o ajuste da base de dados, são criados três modelos utilizando a mesma arquitetura de rede neural:
<br>
<br>
**1 camada LSTM (Long Short Time Memory)** -  Com 100 neurônios. Camada responsável por "aprender" a dependência temporal de longa duração na série.
<br>
<br>
**2 camada Dropout** - Camada para ajudar na capacidade de generalização da rede, previnindo o ***overffiting** do modelo. Esta camada de dropout possui 20% de chance de ativação, isto é, durante a realziação do treinamento, o output de um neorônio terá 20% de chance do seu valor ser substituido por "0". Desta maneira, um neorônio não vai ficar "especializado" durante o treinaemnto ajudando assim a combater o overfitting do modelo.
<br>
<br>
**3 camada Flattern** - Responsável por vetorizar o resultado da rede neural. Esta camada foi adicionada para que o output seja exibido em um array (possibilitando a manipulação dos dados do output de uma maenira mais otimizada)
<br>
<br>
**4 camada dense** - A camada dense é responsável por resolver o problema de forma não linear. Essa camada é responsável por passar o resultado produzido por um neurônio em uma função não linear, possibilitando assim a resolução de problemas complexos e não lineares. Essa camada foi configurada com 100 neurônios e possui a função de ativação "relu".
<br>
![image](https://user-images.githubusercontent.com/39468750/115156371-46303f80-a05a-11eb-8f5e-e39c00ec2c72.png)
<br>
Para a função relu, se o valor produzido por um neurônio for negativo, ele será automaticamente 0, caso for positivo, ele será transformado e considerado.
<br>
<br>
**5 camada dropout** - Com 10% de chance de ativação
<br>
<br>
**6 camada dense** - Com uma função de ativação linear possuindo um único neurônio.
<br>
<br>
**Otimizador** - Adam.
<br>
O otimizador é um algorítimo usado para modificar os atributos de uma rede neural a cada época de treinamento com o intutio de reduzir o erro produzido pela rede neural a cada época. 
<br>
*Exemplo: a cada época de treinamento, a rede passa por um ajuste nos pesos de seus neurônios para que no próximo treinamento o erro seja cada vez menor, e este ajuste nos pesos é realizado por conta do otimizador.*
<br>
<br>
A única **diferença** entre cada modelo é o **número de variáveis utilizadas como input** para realizar a previsão do consumo de energia:
<br>
**Modelo 1** - Possui 16 variáveis, 
<br>
**Modelo 2** - Possui 10 variáveis 
<br>
**Modelo 3** - Apresenta apenas o janelamento de uma única variável (**"price day ahead"**) cinco horas atrás, possuindo assim 6 variáveis.
<br>
<br>
O intuito da criação de três modelos com diferentes variáveis de input é verificar se o modelo construído pela rede neural é capaz de realizar previsões assertivas com a redução da complexidade do modelo, isto é, verificar se a medida que as variáveis de input são retiradas do modelo, a rede neural é capaz de melhorar suas previsões ou não.
<br>
<br>
Os três modelos são avliados utilizando duas métricas de avaliação:
<br>
**Root-mean-square deviation (RMSE)**
<br>
**Mean absolute percentage error (MAPE)**
<br>
<br>
Por fim, após a valiação dos modelos, constata-se que o último modelo (**Modelo 3**), utilizando o janelamento da variável **"price day ahead"** cinco horas para traz apresnetou um melhor resultado do que os outros dois modelos anteriores. Desta maneira, a realização do janelamento da variável **"price day ahead"** foi suficiente para a criação de uma rede neural capaz de realizar a previsão do preço do consumo de energia.

---

Matrícula: 191.671.027

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
