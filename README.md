# Trabalho de Conclusão de Curso - Previsão do Preço de Energia.

#### Aluno: [Matheus Rangel Cardoso](https://github.com/MatheusRangelCardoso)
#### Orientadores: [Leonardo Mendonza](https://github.com/leofome8) e [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/MatheusRangelCardoso/tcc-bi-master-2019.1).


---

### Resumo

Trabalho de conclusão de curso com o objetivo de constuir um modelo capaz de prever qual será o preço da energia na próxima hora.

O modelo utiliza como base de dados:

1 - Dados históricos do consumo de energia da Espanha
2 - Dados históricos de características climáticas presentes em cinco cidades da Espanha: Valencia, Madrid, Bilbao, Barcelona e Seville.

São criados três modelos utilizando a mesma arquitetura de rede neural (LSTM). A única diferença entre cada modelo é o número de variáveis 
utilizadas como input para realizar a previsão do consumo de energia.

O primeiro modelo possui 16 variáveis, o segundo modelo 10 variáveis e o terceiro modelo apresenta apenas o janelamento de uma única variável 
cinco horas atrás, possuindo assim seis variáveis.

O intuito da criação de três modelos com diferentes variáveis de input é verificar se o modelo construído pela rede neural é capaz de realizar 
previsões assertivas com a redução da complexidade do modelo, isto é, verificar se a medida que as variáveis de input são retiradas do modelo, 
a rede neural é capaz de melhorar suas previsões ou não.

---

Matrícula: 191.671.027

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
