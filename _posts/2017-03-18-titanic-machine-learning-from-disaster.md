---
layout: post
title: "Kaggle Competition - Titanic: Machine Learning from Disaster"
date: 2017-03-18
categories:
    - IA
    - Machine Learning
    - Data Science
    - Deep Learning
    - Jupyter Notebook
    - Python
description: "Getting Started Prediction Competition. Start here! Predict survival on the Titanic and get familiar with ML basics"
image-full: "http://blob.vitormeriat.com.br/images/2017/03/18/capa.jpg"
---

<img style="width: 100%;" src="http://blob.vitormeriat.com.br/images/2017/03/18/capa.jpg" class="absolute-bg">

O **Projeto Titanic** é uma competição de **Data Science** promovida pelo [Kaggle.com](kaggle.com). O objetivo deste desafio é deduzir os índices de sobrevivência dos passageiros do Titanic.

<hr/>

Para quem assiste os [Mythbusters](https://www.youtube.com/watch?v=JVgkvaDHmto), sabe que em um de seus programas o assunto do Titanic foi mais do explorado. Não como iremos fazer aqui, já que o foco era provar que era possível Jack e Rose terem sobrevivido utilizando a porta flutuante.

> Nosso foco entretanto, é medir a chance real de sobrevivência dos passageiros a bordo do Titanic em 14 de abril de 1912.

A história do Titanic é muito conhecida, tendo originado diversos livros, filmes, HQs e afins. É válido lembrar que a história narrada de forma célebre por James Cameron em seu filme de 1997, ilustra perfeitamente o motivo deste desafio. Vamos começar com uma breve perspectiva sobre o tema: Em Abril de 1912 o Titanic zarpou rumo a New York com 2224 passageiros, dos quais estima-se que apenas 710 tenham sobrevivido.

É aqui que entra nosso desafio: Desenvolver um padrão simples para identificar o perfil dos sobreviventes deste desastre.

> Nota: Muitos dos barcos salva-vidas não estavam com a sua capacidade máxima de pessoas a bordo. Se estivessem, seria possível salvar 53,4% dos passageiros, mas apenas 31,6% deles sobreviveram.

Neste caso não temos complicação com elementos aleatórios de sorte. A maioria dos sobreviventes eram mulheres, crianças e pessoas da alta sociedade.

## Start

A lista de sobreviventes e não sobreviventes já foi transformada em dois datasets, **train.csv** e **test.csv**. Existe apenas uma diferença entre os dois arquivos, a lista de status de sobrevivência que está presente apenas nos dados de **treino**. Nos dados de teste este valor precisa ser deduzido.

Todos os aprendizados começam com uma experiência e são um processo contínuo. Raramente tem um ponto final. Todos os aprendizados são apenas uma aproximação. O conjunto de dados de treino é tipicamente amostrado em 2 unidades, a amostra maior representando aproximadamente 80% dos dados, e uma 2ª amostra com o resto do dados. 

A aprendizagem acontece usando o Conjunto A e a validação acontece usando o conjunto B. Podemos validar como já sabemos os resultados reais de quem Sobreviveu e quem não fez no Conjunto B e depois compará-lo com os resultados previstos. Uma vez que a aprendizagem é aperfeiçoada no Set A e Set B, o conjunto final de padrões é aplicado nos dados do teste. Apenas um rápido lembrete de que não temos o conhecimento do estado de sobrevivência do passageiro nos dados do teste. No contexto de Kaggle, o resultado da aplicação do padrão nos dados de teste é carregado para o ambiente Kaggle, o que nos permite conhecer o sucesso do modelo que desenvolvemos. Kaggle sabe os resultados dos dados de teste, portanto, é capaz de validar contra o nosso arquivo de resultados submetidos. Aqui está uma visão geral do processo de aprendizagem da máquina genérica.

Neste desafio vamos utilizar os dados do site Kaggle para desenvolver três modelos (regressão logística, árvore de probabilidade condicional e florestas aleatórias), a fim de prever as taxas de sobrevivência para os passageiros do Titanic.

<p align="center"><img src="http://blob.vitormeriat.com.br/images/2017/03/18/decision-tree.jpg"></p>

O conjunto de teste conta com 418 passageiros e o conjunto de treinamento é composto por 891 passageiros. O dataset é composto por:

* Class
* Name
* Sex
* Age
* Sibling/Spouse
* Parents/Children
* Ticket (*)
* Fare
* Cabin (*)
* Port of Embarkment.

Como na maioria das competições Kaggle, você recebe dois conjuntos de dados:

* Um conjunto de treino completo com o resultado (outcome ou target variable), para um grupo de passageiros, bem como uma coleção de outros parâmetros, como sua idade, sexo, etc. Este é o conjunto de dados em que você deve treinar seu modelo preditivo.
* Um conjunto de teste, para o qual você deve prever a variável de destino agora desconhecida com base nos outros atributos de passageiros que são fornecidos para ambos os conjuntos de dados.

Este é um ótimo ponto de entrada para aprender machine learning com um conjunto de dados pequeno, gerenciável, interessante e com variáveis ​​de fácil compreensão.

<p align="center"><img src="http://blob.vitormeriat.com.br/images/2017/03/18/ml-pattern.png"></p>


# Passo 1

A tragédia do "Titanic" está associada com a regra não escrita do salvamento no mar: "mulheres e crianças primeiro".

Nesta tarefa, os competidores precisam analisar a probabilidade de sobrevivência das diferentes categorias de passageiros.

Vamos estipular o sexo dos passageiros e tripulantes. Este é um  dado importante, uma vez que o sexo do passageiro desempenha um papel crucial para determinar a sobrevivência do mesmo. Um simples count revela que temos 891 passageiros dos quais 65% são homens e 35% são mulheres.

<table class="table-fill">
  <tbody>
    <tr>
      <th>Gender</th>
      <th>Count of Passengers</th>
      <th> % </th>
    </tr>
    <tr>
      <td>female</td>
      <td>314</td>
      <td>35%</td>
    </tr>
    <tr>
      <td>male</td>
      <td>577</td>
      <td>65%</td>
    </tr>
  </tbody>
</table>

Se adicionarmos a taxa de sobrevivência a equação vamos ver que existe um padrão aqui.

<table class="table-fill">
  <tbody>
    <tr>
      <th>Count of Passengers</th>
      <th>Survived Status</th>
      <th> </th>
      <th> </th>
    </tr>
    <tr>
      <td style="background: #63dd69; color: white;">Gender</td>
      <td style="background: #63dd69; color: white;">Not Survived</td>
      <td style="background: #63dd69; color: white;">Survived</td>
      <td style="background: #63dd69; color: white;">Total</td>
    </tr>
    <tr>
      <td>female</td>
      <td>81</td>
      <td>233</td>
      <td>314</td>
    </tr>
    <tr>
      <td>male</td>
      <td>468</td>
      <td>109</td>
      <td>577</td>
    </tr>
    <tr>
      <td style="background: #777777; color: white;">Total</td>
      <td style="background: #777777; color: white;">549</td>
      <td style="background: #777777; color: white;">342</td>
      <td style="background: #777777; color: white;">891</td>
    </tr>
  </tbody>
</table>

O seguinte pode ser observado a partir dos dados acima:

1. 62% (549/891) dos passageiros não sobreviveram  
2. 38% (342/891) sobreviveram

Dos 38% que sobreviveram, os passageiros do sexo feminino sobreviveram em maior número maior que os passageiros machos

1. De todos os passageiros do sexo feminino (233/314) 74% sobreviveram
2. De todos os passageiros do sexo masculino (109/577), apenas 19% sobreviveram

Podemos ilustrar este comportamento usando uma árvore de decisão. Cada nó determina o resultado final com base na maioria. Os votos do nó à direita representam o status de sobrevivência, já que a maioria nesta opção sobreviveu. Os votos do à esquerda representam o status de não sobrevivência, uma vez que a maioria não sobreviveu.

<p align="center"><img src="http://blob.vitormeriat.com.br/images/2017/03/18/ml-pattern-all.png"></p>

Este é nosso primeiro padrão. Par facilitar vamos conceituar algumas coisas: O dataset de treino é chamado de **labelled dataset**, onde a coluna <u>Survived</u> é chamda de "label" ou **response data**. Esta abordagem é chamada de aprendizagem supervisionada, onde aprendemos com os dados de treino e aplicamos este aprendizado nos dados de teste. O resultado desta abordagem é binária, portanto estamos aplicando uma técnica de classificação, utilizando duas classes, a saber, **survived** ou **not survived**.

Vamos nos referir ao conjunto de dados progressivamente ao longo deste post, começar a descobrir o conceito de aprendizagem da máquina e suas dimensões variadas. Como você pode observar a partir dos dados, os passageiros e seus atributos compõem os dados do Titanic.

# Análise exploratória de dados 

Em nossa fase de **Exploratory Data Analysis**, precisamos conhecer nossos dados e compreender sua qualidade para conseguir realizar nossa predição. 

Neste ponto vamos combinar os dados de teste de treino antes de realizar qualquer tipo de análise exploratória. Este propósito ficará mais claro em breve. Por hora vamos combinar os 2 conjuntos de dados, e para que isso seja possível precisamos criar uma coluna adicional no conjunto de teste chamado 'sobreviveu' e marcá-los todos com -1, a fim de que sejamos capazes de distinguir em um ponto posterior no tempo os dados de teste. Também há uma necessidade de reorganizar as colunas nos dados de treino para refletir o posicionamento dos dados de teste.



# O repositório

Você pode olhar o código completo acessando o mesmo no repositório **Meriat Machine Learning Notes** no meu Github.

[Titanic: Machine Learning from Disaster](https://github.com/vitormeriat/meriat-ml-notes/blob/master/Titanic%20-%20Machine%20Learning%20from%20Disaster.ipynb)

<div style="margin-bottom: 5em;"></div>

### Até a próxima pessoal ;)
