

# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

Desafio de projeto "Previsão de Estoque Inteligente na AWS com SageMaker Canvas. Este Lab feito na DIO tem como objetivo aprender a usar o SageMaker Canvas para criar previsões de estoque baseadas em Machine Learning (ML). 


## 🎯 Objetivos Deste Desafio de Projeto (Lab)

Construir um modelo que possa prever a quantidade de produtos em estoque usando Machine Learning, para isso vamos passar por quatro etapas.

![image](https://github.com/digitalinnovationone/lab-aws-sagemaker-canvas-estoque/assets/730492/72f5c21f-5562-491e-aa42-2885a3184650)


### 1. Escolha do dataset

O dataset escolhido contém quatro colunas: ID_PRODUTO, DATA(31/12/23 - 08/02/2024), FLAG_PROMOCAO e QUANTIDADE_ESTOQUE

### 2. Construção/Treinamento

Para Construir o modelo é necessário importar o dataset para o SageMaker Canvas, configurar qual será a coluna analisada, para esse projeto foi a QUANTIDADE_ESTOQUE e indicar a coluna com identificador unico(ID_PRODUTO).

Após indicar quais são essas colunas é recomendado ver as sugestões que o SageMaker Canvas irá te fornecer.

Quando tudo estiver configurado começa a fase de treinamento, existe duas formas de treinar o seu modelo, uma mais rapida porém menos precisa e outra mais demorada mas que na maioria das vezes retorna um resultado mais preciso.

### 3. Análise

Após o treinamento precisamos analisar os valores obtidos em cada métrica utilizada:

- Avg. wQL(Average Weighted Quantile Loss): É usada para medir a precisão do modelo em um quantil especifico atribuindo pesos diferentes para cada quantil, isso é util para realização das previsões de estoque.

- MAPE(Mean Absolute Percentage Error): Usado para calcular a média do erro percentual absoluto entre a previsão e o valor real, quanto menor for esse valor mais preciso será o modelo.

- WAPE(Weighted Absolute Percentage Error): É usado para medir o desvio geral entre os valores previstos e os valores observados, ou seja, ele compara a soma dos valores observados com a soma dos valores previstos e calcula o erro entre esses valores, assim como no MAPE quanto menor o valor desse erro mais preciso é o modelo.

- RMSE(Root Mean Square Error): É uma metrica que amplifica o impacto dos valores outliers(valores muito discrepantes com relação aos outros), é muito relevante quando apenas algumas previsões erradas tem um alto custo.

- MASE(Mean Absolute Scaled Error): Realiza a divisão entre o erro absoluto médio de um modelo por um fator de escala ou modelo sem treinamento. É uma métrica muito usada para dados ciclicos ou sazonais.


#### 3.1 Análise do modelo treinado
![image](https://github.com/lobodavi/lab-aws-sagemaker-canvas-estoque/blob/main/metricas.png)

- O valor de Avg. wQL foi de 0.288 o que é um desempenho satisfatório mas ainda existe como melhorar esse valor.

- O valor apresentado para o MAPE foi de 0.933 ou 93,3 % o que é bastante alto, existe algumas hipoteses do porque isso aconteceu sendo uma delas a escolha pelo treinamento rápido o que pode ter gerado uma dificuldade significativa para o modelo.

- O WAPE do modelo foi 0.482 o que é razoável para esse primeiro momento mas assim como as outras métricas analisadas anteriormente pode melhorar para as versões futuras.

- O valor de RMSE foi de 21.072 o que indica que os erros de previsão estão altos ainda o que pode ser problematico dependendo do total do estoque. 

- O modelo obteve 0.662 de MASE o que indica que ele está melhor que um modelo sem treinamento mas pode ser melhorado bastante ainda.

Para melhorar a precisão do modelo podemos realizar a revisão do dataset com relação a qualidade dos dados, a possível inclusão de novas variáveis, buscar uma maneira de capturar o padrão de dados. 

Realizando esses procedimentos é esperado que os erros diminuam e as previsões sejam mais precisas.

### 4. Previsões

![image](https://github.com/lobodavi/lab-aws-sagemaker-canvas-estoque/blob/main/previsao.png)

De acordo com o modelo a previsão de estoque para um determinado produto com demanda histórica de 36 unidades seria suprida 90% (P90) das vezes mantendo 86 unidades em estoque, na média seria necessário 40 unidades e o minimo é de 22 unidades, assim garantindo que o produto não faltaria na prateleira.


