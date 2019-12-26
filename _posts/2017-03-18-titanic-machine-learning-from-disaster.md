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
image: "http://blob.vitormeriat.com.br/images/2017/03/18/capa.jpg"
---

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2017/03/18/capa.jpg">
</div>

O **Projeto Titanic** é uma competição de **Data Science** promovida pelo [Kaggle.com](kaggle.com). O objetivo deste desafio é deduzir os índices de sobrevivência dos passageiros do Titanic.

Meu objetivo aqui é resumir de forma simples este problema e como chegar a sua solução, aproveitando para introduzir alguns dos conceitos envolvido no tão falado **Machine Learning**. Não vou me aprofundar em nenunhum ponto, espero embreve fazê-lo com mais tempo e foco.

Este é um dos problemas iniciais favoritos dos estudantes de Data Science, e tem um dataset com a complexidade ideal para explorar alguns problemas que funcionam de pano de fundo para introduzir os conceitos de Machine Learning mais básicos.

## Agenda

* Introdução
* Os dados
* Descobrindo Padrões
* Exploratory Data Analysis
	* Missing Data
		* Embarked
		* Fare
		* Age
		* Name
	* Feature Engineering
		* Title
		* Cabin
		* Surname
		* Family Size
	* Data Transformation
	* Feature Selection 
	* Feature selection	 

## Introdução

Para quem assiste os [Mythbusters](https://www.youtube.com/watch?v=JVgkvaDHmto), sabe que em um de seus programas o assunto do Titanic foi mais do explorado. Não como iremos fazer aqui, já que o foco era provar que era possível Jack e Rose terem sobrevivido utilizando a porta flutuante.

<div class="especial-box yellow-box">
  <p>
  Nosso foco entretanto, é medir a chance real de sobrevivência dos passageiros a bordo do Titanic em 14 de abril de 1912.
  </p>
</div>

A história do Titanic é muito conhecida, tendo originado diversos livros, filmes, HQs e afins. É válido lembrar que a história narrada de forma célebre por James Cameron em seu filme de 1997, ilustra perfeitamente o motivo deste desafio. Vamos começar com uma breve perspectiva sobre o tema: Em Abril de 1912 o Titanic zarpou rumo a New York com `2224` passageiros, dos quais estima-se que apenas `710` tenham sobrevivido.

É aqui que entra nosso desafio: Desenvolver um padrão simples para identificar o perfil dos sobreviventes deste desastre.

> Nota: Muitos dos barcos salva-vidas não estavam com a sua capacidade máxima de pessoas a bordo. Se estivessem, seria possível salvar `53,4%` dos passageiros, mas apenas `31,6%` deles sobreviveram.

Neste caso não temos complicação com elementos aleatórios de sorte. A maioria dos sobreviventes eram mulheres, crianças e pessoas da alta sociedade.

## Os dados

A lista de sobreviventes e não sobreviventes foi transformada em dois datasets, **train.csv** e **test.csv**. Existe apenas uma diferença entre os dois arquivos, a lista de status de sobrevivência que está presente apenas nos dados de **treino**. Nos dados de teste este valor precisa ser deduzido.

<div class="especial-box yellow-box">
  <p>
  Todos os aprendizados começam com uma experiência e são um processo contínuo. Raramente tem um ponto final. Todos os aprendizados são apenas uma aproximação.
  </p>
</div>

Geralmente trabalhamos um experimento utilizando dois conjuntos de dados. Um de treino e um para o teste, tipicamente dividido em 80% ou 70% para treino e e restante para o teste. 

A aprendizagem acontece usando o `Conjunto A` e a validação acontece usando o `Conjunto B`. Uma vez que a aprendizagem é aperfeiçoada, aplicamos nosso modelo nos dados de teste. Vale lembrar que não temos o conhecimento do estado de sobrevivência do passageiro nos dados do teste. 

Neste desafio vamos utilizar os dados disponíveis no próprio site do Kaggle para desenvolver nosso modelo, a fim de prever as taxas de sobrevivência para os passageiros do Titanic.

O conjunto de teste conta com 418 passageiros e o conjunto de treinamento é composto por 891 passageiros. O dataset é composto por:

* `PassengerId`: Número de identificação do passageiro;
* `Survived`: Indica se o passageiro sobreviveu ao desastre. É atribuído o valor de 0 para aqueles que não sobreviveram, e 1 para quem sobreviveu;
* `Pclass`: Classe na qual o passageiro viajou. É informado 1 para primeira classe; 2 para segunda; e 3 para terceira;
* `Name`: Nome do passageiro;
* `Sex`: Sexo do passageiro;
* `Age`: Idade do passageiro em anos;
* `SibSp`: Quantidade de irmãos e cônjuges a bordo;
* `Parch`: Quantidade de pais e filhos a bordo;
* `Ticket`: Número da passagem;
* `Fare`: Preço da passagem;
* `Cabin`: Número da cabine do passageiro;
* `Embarked`: Indica o porto no qual o passageiro embarcou. Há apenas três valores possíveis: Cherbourg, Queenstown e Southampton, indicados pelas letras **C**, **Q** e **S**, respectivamente.

Como na maioria das competições Kaggle, você recebe dois conjuntos de dados:

* Um conjunto de treino completo com o resultado (outcome ou target variable), para um grupo de passageiros, bem como uma coleção de outros parâmetros, como sua idade, sexo, etc. Este é o conjunto de dados em que você deve treinar seu modelo preditivo.
* Um conjunto de teste, para o qual você deve prever a variável de destino agora desconhecida com base nos outros atributos de passageiros que são fornecidos para ambos os conjuntos de dados.

Este é um ótimo ponto de entrada para aprender machine learning com um conjunto de dados pequeno, gerenciável, interessante e com variáveis ​​de fácil compreensão.

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2017/03/18/ml-pattern.png">
</div>

# Descobrindo padrões

A tragédia do "Titanic" está associada com a regra não escrita do salvamento no mar: "mulheres e crianças primeiro".

Nesta tarefa, os competidores precisam analisar a probabilidade de sobrevivência das diferentes categorias de passageiros.

Vamos estipular o sexo dos passageiros e tripulantes. Este é um  dado importante, uma vez que o sexo do passageiro desempenha um papel crucial para determinar a sobrevivência do mesmo. Um simples count revela que temos 891 passageiros dos quais 65% são homens e 35% são mulheres.

<div align="center">
  <table class="table-fill">
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
  </table>
</div>

Se adicionarmos a taxa de sobrevivência a equação vamos ver que existe um padrão aqui.

<div align="center">
  <table class="table-fill">
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
  </table>
</div>

O seguinte pode ser observado a partir dos dados acima:

1. 62% (549/891) dos passageiros não sobreviveram  
2. 38% (342/891) sobreviveram

Dos 38% que sobreviveram, os passageiros do sexo feminino sobreviveram em maior número maior que os passageiros do sexo masculino.

1. De todos os passageiros do sexo feminino (233/314) 74% sobreviveram
2. De todos os passageiros do sexo masculino (109/577), apenas 19% sobreviveram

Podemos ilustrar este comportamento usando uma árvore de decisão. Cada nó determina o resultado final com base na maioria. Os votos do nó à direita representam o status de sobrevivência, já que a maioria nesta opção sobreviveu. Os votos do à esquerda representam o status de não sobrevivência, uma vez que a maioria não sobreviveu.

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2017/03/18/ml-pattern-all.png">
</div>

Este é nosso primeiro padrão. Par facilitar vamos conceituar algumas coisas: O dataset de treino é chamado de **labelled dataset**, onde a coluna <u>Survived</u> é chamda de "label" ou **response data**. Esta abordagem é chamada de aprendizagem supervisionada, onde aprendemos com os dados de treino e aplicamos este aprendizado nos dados de teste. O resultado desta abordagem é binária, portanto estamos aplicando uma técnica de classificação, utilizando duas classes, a saber, **survived** ou **not survived**.

Vamos nos referir ao conjunto de dados progressivamente ao longo deste post, começar a descobrir o conceito de aprendizagem da máquina e suas dimensões variadas. Como você pode observar a partir dos dados, os passageiros e seus atributos compõem os dados do Titanic.

<div class="especial-box yellow-box">
  <p>
    Um ponto importante sobre este tutorial: Não estou colocando todo o passo a passo da solução. Aqui não temos os passos para importação de dados e etc. Estou focando na solução técnica para a criação do modelo e resolução do problema. Para ver a solução completa que inclusive enviei para o Kaggle, você deve ver o código que está na sessão entitulada, <u><b>O repositório</b></u>
  </p>
</div>

<hr style="margin-bottom: 3em;" />

## Exploratory Data Analysis 

Em nossa fase de **análise exploratória de dados**, precisamos conhecer nossos dados e compreender sua qualidade para conseguir realizar nossa predição. 

Neste ponto vamos combinar os dados de teste de treino antes de realizar qualquer tipo de análise exploratória. Este propósito ficará mais claro em breve. Por hora vamos combinar os 2 conjuntos de dados, e para que isso seja possível precisamos criar uma coluna adicional no conjunto de teste chamado `Survived` e marcá-los todos com `-1`, a fim de que sejamos capazes de distinguir em um ponto posterior no tempo os dados de teste. Também há uma necessidade de reorganizar as colunas nos dados de treino para refletir o posicionamento dos dados de teste.

<pre style="font-size: 1.2em !important">
    <code class="python">
 testTitanicDS.is_copy = False
 testTitanicDS['Survived']=-1
 trainTitanicDS =  trainTitanicDS[['PassengerId','Pclass','Name','Sex','Age','SibSp','Parch','Ticket','Fare','Cabin','Embarked','Survived']]
 mergedTitanicDS = trainTitanicDS.append(testTitanicDS)
    </code>
</pre>

## Missing Data 

A falta de dados deve ser tratada antes de se aplicar qualquer algoritmo de aprendizado de máquina. Isso faz sentido já que se tivermos dados faltando em alguma linha, nosso resultado pode ser afetado. No código abaixo vamos procurar e exibir os dados de valores missing caso eles existam em nosso dataset.

<pre style="font-size: 1.2em !important">
    <code class="python">
 for col in mergedTitanicDS:
    if mergedTitanicDS[col].isnull().sum()>0:
        print("Missing Values in %s %d" % (col,(mergedTitanicDS[col].isnull().sum())))
    </code>
</pre>

Como resultado temos a seguinte saída:

```
***** output *****

Missing Values in Age 263
Missing Values in Fare 1
Missing Values in Cabin 1014
Missing Values in Embarked 2
```
Sendo assim já sabemos que existem muitos valores missing em nosso dataset. Uma vez que os identificamos o próximo passo é examinar para entender qual o motivo ou causa para esse comportamento. Em Machine Learning, os dados são essenciais, e como tal, devemos olhar com toda atenção.

Existem diversas técnicas para lidar como valores missing. Uma delas seria eliminar toda a linha e trabalhar somente com as linhas contendo dados completos. Em nosso caso vamos atacar cada um dos recursos em falta e definir qual estratégia usar. Vamos iniciar pelo mais simples.

#### Embarked

Podemos nota que existem apenas 2 valores missing para Embarked. Vamos observar sua distribuição:

<pre style="font-size: 1.2em !important">
    <code class="python">
 mergedTitanicDS['Embarked'].value_counts()
    </code>
</pre>

```
***** output *****

S    914
C    270
Q    123
Name: Embarked, dtype: int64
```

Bem vindo as variáveis categóricas. Temos pouca massa de manobra aqui. Uma estratégia consistente neste caso poderia ser substituir os valores missing pelo valor de `S`, já que o mesmo supera tanto `C` quanto `Q` em termos de númericos. Com esta abordagem estamos influenciando muito pouco no resultado final.

<pre style="font-size: 1.2em !important">
    <code class="python">
 mergedTitanicDS.is_copy = False
 mergedTitanicDS.loc[mergedTitanicDS['Embarked'].isnull(),'Embarked'] = 'S'
    </code>
</pre>

#### Fare

Há apenas um passageiro com dados missing sobre a tarifa. O passageiro em questão é senhor **"Storey, Mr. Thomas"**. Se olharmos para os dados do senhor Thomas, veremos que ele viajou na classe `Pclass 3`.

Neste caso podemos usar como estratégia, obter a média da tarifa paga pelos passageiros da classe **Pclass 3**.

<pre style="font-size: 1em !important">
    <code class="python">
  mergedTitanicDS_Merged.loc[
 	mergedTitanicDS_Merged['Fare'].isnull(),'Fare'] = 
 	mergedTitanicDS_Merged[mergedTitanicDS_Merged['Pclass'] == 3]['Fare'].mean()
    </code>
</pre>

<div class="especial-box yellow-box">  
  <p>
    <b style="font-size: 1.6em">Think outside the box</b><br>
    Esta é uma fase muito importante. Geralmente você vai se deparar com situações durante o tratamento de dados em que vai parecer impossível realziar um tratamento. Um exemplo disso em nosso projeto é a feature <u><b>AGE</b></u>
  </p>
</div>

#### Age

A idade é um ponto de dados contínuo. Há `263` valores missing, o que representa cerca de `19%` dos dados. Existem várias estratégias para substituição da idade, o mais simples é substituir por uma média, mediana ou moda.

A **armadilha** nesta estratégia é que todos os passageiros sem idade terão o mesmo valor estático, o que pode resultar em uma criança com a idade de um adulto, sendo assim, essa abordagem irá afetar diretamente no resultado final, tornando nossa privisão falha.

Como resolver este problema de forma satisfatória? Podemos começar olhando para o nosso dataset a fim de achar algo que nos ajude... 

#### Name

Opa... **Name** não possui valores missing, então o que está fazendo aqui? A questão é o que esse recurso tem a nos oferecer para resolver o problema das idades. Vamos lá...

Olhando para o este recurso veremos que juntamente com o nome temos os títulos. Os títulos nos dizem muito, já que podemos induzir se a pessoa é mais jovem ou mais madura com base neles. 

Vamos introduzir uma nova técnica para chegar nisso, chamamos essa técnica de **feature engineering**.


## Feature Engineering

A **engenharia de recurso** tenta aumentar a capacidade de previsão dos algoritmos de aprendizado criando recursos de dados brutos que facilitam o processo de aprendizado. Basicamente esse processo tenta criar outros recursos relevantes com base nos recursos brutos existentes nos dados e aumentar a capacidade de previsão do algoritmo de aprendizado.

Vamos continuar na análise dos nossos recursos agora aplicando um exemplo de feature engineering.

#### Title

Como vimos, temos junto aos nomes os **títulos de tratamento** para cada pessoa. Sendo assim podemos agregar a nossa estratégia de idade a indução da mesma com base no título.

Neste caso vamos extrair o título do nome e encontrar a média entre idade e o título informado, e depois substituir os **valores missing** pela média correspondente. Essa estratégia serve para ajudar a evitar substituir o valor missing de uma possível criança pela idade de um adulto. Assim diminuímos a margem de erro no tratamento de dados missing, e obtemos um resultado final eficiente.

Extrair e cruzar os dados de idade com os dados do título de treinamento é um exemplo de **Feature Engineering**, que visa tornar o conjunto de dados mais rico para o aprendizado.

Traduzindo isso em código, nossa primeira tarefa será criar uma coluna chamada **Title** e extrair o valor do título de tratamento para inserir o valor nela.

<pre style="font-size: 1.2em !important">
    <code class="python">
  mergedTitanicDS['Title'] = [nameStr[1].strip().split('.')[0] for nameStr in
  mergedTitanicDS['Name'].str.split(',')]
    </code>
</pre>

Para visualizar a importância desse novo recurso, vamos olhar a distribuição deste dado. No código abaixo geramos uu gráfico que exibe uma visão interessante da distribuição dos títulos distintos em nosso dataset. Alguns dos títulos refletem Realeza, como por exemplo Jonkheer, que é título de nobreza holandesa.

<pre style="font-size: 1.2em !important">
    <code class="python">
  mergedTitanicDS['Title'].value_counts().plot.bar()
    </code>
</pre>

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2017/03/18/feature engineering-title.png">
</div>

Sendo assim podemos analizar melhor nossa decisão. Como a grande maioria dos dados são representados pelo título `Mr`, e temos 18 títulos diferentes, sendo assim já sabemos de cara que seria um erro ter uma média generalizada.

Vamos traduzir isso para código. Abaixo temos os 4 passos para o nosso objetivo:

1. Agregamos a idade pelo título e aplicamos a média;
2. Como será gerada uma nova coluna, vamos renomeá-la para Title;
3. Realizamos o merge da nova coluna em nosso dataset;
4. Substituímos os valores missing pela média de cada título.

<pre style="font-size: 1.2em !important">
    <code class="python">
 # 1
 aggAgeByTitleDS = mergedTitanicDS[['Age','Title']].groupby(['Title']).mean().reset_index()

 # 2
 aggAgeByTitleDS.columns = ['Title','Mean_Age']

 # 3
 mergedTitanicDS_Merged = pd.merge(mergedTitanicDS, aggAgeByTitleDS,on="Title")

 # 4
 mergedTitanicDS_Merged.loc[mergedTitanicDS_Merged['Age'].isnull(),'Age']=mergedTitanicDS_Merged[mergedTitanicDS_Merged['Age'].isnull()]['Mean_Age']
    </code>
</pre>

#### Cabin

Vamos evoluir em nossa análise. A feature **cabin** parece ser o maior problema, ele é parece ser realmente complexo. Para começar ele represente mais de 70% dos dados missing em nosso dataset.

Não há muito o que os dados da cabine possam oferecer em relação ao nosso problema. Nada que revele uma predisposição a sobrevivência ou não, algo como a relação de proximidade com o assidente ou coisa do tipo. Como não temos informação adicional ou externa sobre este recurso, uma estratégia que podemos utilizar é criar um novo recurso indicando a existência ou não da cabine.

<pre style="font-size: 1.2em !important">
    <code class="python">
  mergedTitanicDS['IsCabinDataEmpty'] = 0
  mergedTitanicDS.loc[mergedTitanicDS['Cabin'].isnull(),'IsCabinDataEmpty'] = 1
    </code>
</pre>

#### Surname

Outro dado que podemos extrair e que será de extrema importância é o sobrenome do passageiro. Com este dado em mãos podemos realizar uma combinação posterior para inferir as famílias que estavam no Titanic. Podemos resolver isso com apenas uma linha de código.

<pre style="font-size: 1.2em !important">
    <code class="python">
  mergedTitanicDS_Merged['Surname'] = [nameStr[0].strip() for 
  nameStr in mergedTitanicDS_Merged['Name'].str.split(',')]
    </code>
</pre>

Agora, qual a importância dessa ação? Aqui vai mais uma dica: Procure avaliar cada nova `feature` possível. Isso é de suma importância, já que posteriormente conseguimos avaliar se existe ou não alguma relação deste novo recurso e nossa meta.

Agora já temos o sobrenome, mas isso pode acabar sendo outra armadilha, uma vez que é possível termos passageiros com o mesmo sobrenome e que não sejam da mesma família. Para isso vamos tentar melhorar nossa combinação de dados...

#### Family Size

Algo que pode nos ajudar nesse sentido é descobrir o tamanho da família. Udsando as features `SibSp` que representa a quantidade de irmãos e cônjuges, e `Parch` que representa a quantidade de pais e filhos, podemos inferir nosso **Family Size**.

<pre style="font-size: 1.2em !important">
    <code class="python">
  mergedTitanicDS_Merged['FamilySize'] = 
  mergedTitanicDS_Merged['SibSp'] + mergedTitanicDS_Merged['Parch'] + 1
    </code>
</pre>

## Data Transformation

Antes de prosseguirmos, vamos avalidar todos os recursos que criamos e o que já tinhamos a nossa disposição:

<pre style="font-size: 1.4em !important">
    <code class="python">
  mergedTitanicDS_Merged.dtypes
    </code>
</pre>

O resultado será o seguinte:

```
  PassengerId           int64
  Pclass                int64
  Name                 object
  Sex                  object
  Age                 float64
  SibSp                 int64
  Parch                 int64
  Ticket               object
  Fare                float64
  Cabin                object
  Embarked             object
  Survived              int64
  IsCabinDataEmpty      int64
  Title                object
  Mean_Age            float64
  Surname              object
  FamilySize            int64
```

Observe os campos cujo o tipo são `object`:

* Name
* Sex
* Ticket
* Cabin
* Embarked
* Title

Para realizarmos nosso algorítimo de forma satisfatória, precisamos "adequar" nossos dados. A priori já sabemos que para trabalhar com estatística consideramos dois tipos de dados: **numérico** ou **categórico**. 

> **Nota**: Uma descrição detalhada pode ser encontrada em meu post [Variáveis, Estatística e Macnhine Learning](http://www.vitormeriat.com.br/2017/04/20/variables-in-statistic/).

Sendo assim vamos aplicar alguma transformação para estes dados a fim de torná-los compativeis que nosso algorítimo.

#### Sex, Embarked and Title

Temos apenas dois tipos possíveis para sexo: Masculino e Feminino. Esta é uma tranformação simples, já que se trata de uma opção binária. Seguindo esta linha vamos `codificar` essa feature para que consigamos realizar uma representação onde para cara linha tenhamos uma coluna `male` e `female` onde necessáriamente um será positivo (1) e o outro negativo (0).

<pre style="font-size: 1.4em !important">
    <code class="python">
  pd.get_dummies(mergedTitanicDS_Merged['Sex'])
    </code>
</pre>

Teremos como resultado a seguinte saída:

FIG sex

O mesmo conseito pode ser aplicado para **Embarked** e **Title**:

FIG embarked

FIG title

Utilizando o **Pandas** vamos realizar a transformação dos dados categóricos em tipos que possam ser expressos de forma númerica. Logo após fazemos o merge das novas informações em nosso **DataFrame**.

<pre style="font-size: 1.2em">
    <code class="python">
  mergedTitanicDS_Merged = pd.concat([mergedTitanicDS_Merged,
  pd.get_dummies(mergedTitanicDS_Merged['Embarked'])],axis = 1)
 
  mergedTitanicDS_Merged = pd.concat([mergedTitanicDS_Merged,
  pd.get_dummies(mergedTitanicDS_Merged['Sex'])],axis = 1)
 	
  mergedTitanicDS_Merged = pd.concat([mergedTitanicDS_Merged,
  pd.get_dummies(mergedTitanicDS_Merged['Title'])],axis = 1)
    </code>
</pre>

Agora uma coisa pode parecer parecer estranha neste processo. Estamos incluindo um grande número de recursos, o que geralmente é bom para nos dar mais massa de manobra na exploração de relações com nosso alvo. O efeito colateral é que também pode trazer confusão se não for algo bem elaborado.

> **Nota**: Variáveis categóricas são conhecidas por ocultar e mascarar muitas informações interessantes em um conjunto de dados. É crucial aprender os métodos de lidar com essas variáveis.

## Feature Selection

A seleção de recursos também é chamada seleção de variáveis (variable selection) ​​ou seleção de atributos (attribute selection). Esta técnica se resume em saber selecionar quis os atributos em seus dados são realmente relevantes para a modelagem preditiva que você está construindo.

Sendo assim, vamos analisar o que temos de atributos, e ver se precisamos ou não de todos eles para a construção do nosso modelo.


<hr style="margin-bottom: 4em; margin-top: 6em;" />

# O repositório

Você pode olhar o código completo acessando o mesmo no repositório **Meriat Machine Learning Notes** no meu Github.

[Titanic: Machine Learning from Disaster](https://github.com/vitormeriat/meriat-ml-notes/blob/master/Titanic%20-%20Machine%20Learning%20from%20Disaster.ipynb)

<div style="margin-bottom: 5em;"></div>

# Referências
* [Titanic: Machine Learning from Disaster](https://www.kaggle.com/c/titanic)
* [Titanic: Getting Started With R](http://trevorstephens.com/kaggle-titanic-tutorial/getting-started-with-r/)
