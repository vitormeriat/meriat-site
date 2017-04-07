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


Embora os [Mythbusters](https://www.youtube.com/watch?v=JVgkvaDHmto) em seu programa tenham provado completamente que era possível Jack e Rose ter sobrevivido utilizando a porta flutuante, o interesse aqui é medir a chance real de sobrevivência dos passageiros a bordo do Titanic em 14 de abril de 1912.

A história do Titanic é muito conhecida, tendo originado diversos livros, filmes, HQs e afins. É válido lembrar que a história narrada de forma célebre por James Cameron em seu filme de 1997, ilustra perfeitamente o motivo deste desafio. Vamos começar com uma breve perspectiva sobre o tema: Em Abril de 1912 o Titanic zarpou rumo a New York com 2224 passageiros, dos quais estima-se que apenas 710 tenham sobrevivido.

É aqui que entra nosso desafio: Desenvolver um padrão simples para identificar o perfil dos sobreviventes deste desastre.

> Nota: Muitos dos barcos salva-vidas não estavam com a sua capacidade máxima de pessoas a bordo. Se estivessem, seria possível salvar 53,4% dos passageiros, mas apenas 31,6% deles sobreviveram.

Neste caso não temos complicação com elementos aleatórios de sorte. A maioria dos sobreviventes eram mulheres, crianças e pessoas da alta sociedade.

# Start

A lista de sobreviventes e não sobreviventes já foi transformada em dois datasets, **train.csv** e **test.csv**. Existe apenas uma diferença entre os dois arquivos, a lista de status de sobrevivência que está presente apenas nos dados de **treino**. Nos dados de teste este valor precisa ser deduzido.

Neste desafio vamos utilizar os dados do site Kaggle para desenvolver três modelos (regressão logística, árvore de probabilidade condicional e florestas aleatórias), a fim de prever as taxas de sobrevivência para os passageiros do Titanic.

<p align="center"><img src="http://blob.vitormeriat.com.br/images/2017/03/18/decision-tree.jpg"></p>

O conjunto de teste conta com 418 passageiros e o conjunto de treinamento é composto por 891 passageiros. O conjunto de dados é composto por:

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


# Passo 1
O colapso do "Titanic" está associada com a regra não escrita do salvamento no mar: "mulheres e crianças primeiro".

Nesta tarefa, os competidores precisam analisar a probabilidade de sobrevivência das diferentes categorias de passageiros.

Para determinar se o passageiro sobreviveu ao "Titanic", vamos usar uma árvore de decisão. Uma árvore de decisão é gerada automaticamente com base no parâmetro de entrada. A imagem abaixo mostra um exemplo de uma árvore de decisão é criada.

<p align="center"><img src="http://blob.vitormeriat.com.br/images/2017/03/18/decision-tree02.jpg"></p>

# O repositório
Você pode olhar o código completo acessando o mesmo no repositório **Meriat Machine Learning Notes** no meu Github.

[Titanic: Machine Learning from Disaster](https://github.com/vitormeriat/meriat-ml-notes/blob/master/Titanic%20-%20Machine%20Learning%20from%20Disaster.ipynb)

<div style="margin-bottom: 5em;"></div>

### Até a próxima pessoal ;)
