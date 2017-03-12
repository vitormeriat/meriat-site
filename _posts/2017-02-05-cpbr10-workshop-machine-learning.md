---
layout: post
title: "Workshop de Machine Learning na CPBR10"
date: 2017-02-05
categories:
  - IA
  - Machine Learning
  - Jupyter Notebook
  - Python
description: Workshop de Machine Learning na Campus Party 2017, a CPBR10. Este ano tive a honra de mais uma vez palestrar na Campus Party. Na minha deixa pude demonstrar como iniciar um projeto de Machine Learning do zero utilizando como ferramentas o Jupyter Notebook, Python e o famoso dataset Pima Indians Diabetes Database.
image-full: "http://blob.vitormeriat.com.br/images/2017/02/05/campus-ia.jpg"
---
<div style="width: 100%; -ms-align-items: center; -webkit-align-items: center; align-items: center;">
    <img style="width: 100%;" src="http://blob.vitormeriat.com.br/images/2017/02/05/campus-ia.jpg" class="absolute-bg">
</div>

Este ano tive a honra de mais uma vez palestrar na Campus Party. Como de costume minha participação foi em conjunto com a comunidade CrazyTechGuys.

Nesta oportunidade dividi as ações com o mestre Jorge Maia, no workshop de [IoT e Machine Learning](http://campuse.ro/events/campus-party-brasil-2017/workshop/sensores-internet-das-coisas-e-inteligencia-artificial-de-perto-e-sem-mitos/). Nesta atividade trabalhamos além dos conceitos básicos de IoT e Machine Learning, novidade de mercado, protocolos, linguagens e plataformas.

Na minha deixa pude demonstrar como iniciar um projeto de Machine Learning do zero utilizando como ferramentas o Jupyter Notebook, Python e o famoso dataset Pima Indians Diabetes Database que é normalmente utilizando para tarefas de classificação e, é largamente utilizado para prever o início de diabetes com base em diagnósticos já realizados.

É possível encontrar diversos exemplos de utilização do dataset, bem como uma ampla gama de exemplos de diferentes explorações e tratamentos dos dados.

Neste workshop demonstrei como utilizar o Jupyter Notebook bem como os principais módulos para se trabalhar com Data Science e Python. Vimos os principais conceitos envolvidos nesta atividade e como aplicar em exercício prático.

# Resumindo

Quando falamos de ML, temos duas pricipais tecnicas para trabalhar:
* Aprendizagem supervisionada
* Aprendizagem Nao supervisionada

Quando falamos de aprendizagem supervisionada e não supervisionada, tendemos a pensar que a diferença está na predição com ou sem a supervisão humana, mas na realidade tudo está ligado aos dados.

Quando se trata de Aprendizagem supervisionada, cada linha possui diversos atributos, que serão os inputs e os possíveis outputs, ou seja, o valor que esperamos para o conjunto de atributos da linha.

Se usamos como exemplo determinar o valor de casas em uma determinada região, podemos pegar como atributos o tamanho, quantidade de quartos, área da casa, localidade e claro, o preço.

Logo após passamos esses dados em um algorítimo de ML, com todos os dados de entrada e os possíveis dados de saída, que neste caso será o valor da casa. O algorítimo determina a relação entre os atributos da casa e seu valor final.

Depois o resultante do algorítimo será um Modelo, que nada mais é que uma função matemática. Este Modelo será o cara que vai receber os novos dados e ser capaz de prever o preço final.

O modelo é capaz de prever o preço, pq ele aplica a função matemática que ele aprendeu durante o processo no novo conjunto de dados. A medida que temos novos dados, podemos melhorar nosso modelo e realizar o tão famoso aprendizado de máquina...

No processo de aprendizagem não supervisionada, o algorítimo busca em seu conjunto de dados, clusters, ou agrupamentos de dados com características semelhantes.

Sendo assim, o algorítimo identifica a partir dos dados de entrada grupos de dados que compartilhem as mesmas características. Neste caso, não precisamos apresentar os possíveis dados de saída.

Imagine um conjunto de gravações com pessoas falando. Podemos gerar um dataset com os atributos das vozes das pessoas como entonação, inflexção, altura e etc. Passamos estes dados em um algorítimo de aprendizagem não supervisionado.

O algorítimo analisa os dados e cria um modelo que classifica clusters de dados que compartilham os mesmos padrões de voz. Com isso o algorítimo será capaz de isolar uma única voz a partir dos dados aprendidos.


Podemos rezumir de forma simples da segunte maneira:

**Aprendizagem supervisionada**
* Previsão de valores
* Nossos dados de treino devem ter valores de entrada e saída, para que o mesmo possa aprender a partir dos novos dados de entrada, a gerar uma saída correta.

**Aprendizagem não supervisionada**
* Idendificação de grupos de dados
* Nossos dados precisam apenas possuir entradas

### Source
* [Github](https://github.com/vitormeriat/workshop-cpbr10)


### Dataset
* [UCI](https://archive.ics.uci.edu/ml/datasets/Pima+Indians+Diabetes)
* [Kaggle](https://www.kaggle.com/uciml/pima-indians-diabetes-database)
