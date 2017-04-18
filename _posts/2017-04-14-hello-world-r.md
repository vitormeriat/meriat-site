---
layout: post
title: "Hello World R - Da base à Regressão Linear"
date: 2017-04-14
categories:
    - R
    - Data Science
description: "Esta é minha primeira impressão utilizando a linguagem R, usada por programadores e cientistas de dados com ênfase em computação estatísticas. Para começar com o pé direito, nada como implementar uma regressão linear para iniciar."
image: "https://meriatblob.blob.core.windows.net/images/2017/04/14/capa-logo-r.png"
---

<p align="center"><img src="https://meriatblob.blob.core.windows.net/images/2017/04/14/capa-logo-r.png" class="absolute-bg"></p>

A linguagem R é um projeto GNU de software livre. O **R** derivou de uma linguagem chamada **S** (de "statistics"), criada na **Bell Laboratories** nos anos 70. Esta é uma linguagem usada por programadores e cientistas de dados para computação estatística.

R foi desenvolvida por estatísticos para estatística, dado seu foco na resolução de problemas matemáticos, ele possui um estrutura simples o que facilita a implementação e traz ganhos na otimização no tempo de desenvolvimento. Você pode obter todas as referncias na documentação oficial em [rdocumentation.org](https://www.rdocumentation.org/), fora que é possível contar com um riquíssimo ecossistema de pacotes para diferentes áreas de aplicação.

<hr/>

Para começar vamos criar um exemplo de regressão linear, uma espécie de **"Hello World"** da computação estatística. Então, mãos a obra...

## Regressão Linear

A regressão linear é uma técnica estatística usada para descrever a relação entre uma variável numérica (na estatística, chamada de variável dependente) e uma ou mais variáveis explicativas (chamadas de variáveis independentes) que podem ser numéricas ou categóricas. Quando há apenas uma única variável explicativa/de previsão, a técnica é chamada de regressão linear simples. Quando houver duas ou mais variáveis independentes, a técnica é chamada de regressão linear múltipla.

Para iniciar vamos começar importando o arquivo de texto que será utilizado no exemplo.

<pre style="font-size: 1.6em !important">
    <code class="r">
  data <- read.table("sementes.txt", header=TRUE, sep=",")
    </code>
</pre>

No trecho de código acima estamos utilizando a importação de um **TXT** como DataSet. Na operação que estamos utilizando, podemos observar que a linguagem **R** usa parâmetros nomeados. O parâmetro de cabeçalho informa se a primeira linha é de cabeçalho ou não. O parâmetro **sep** (separador) indica como os valores em cada linha são separados. Por exemplo, (\t) indica valores delimitados por tabulação, e (" ") indica valores delimitados por espaço.

> O R diferencia maiúsculas de minúsculas e você geralmente pode usar o operador (<-) para atribuir valores, ou o operador (=). Essa escolha é uma questão de preferência pessoal, já que ambos exercem a mesma função. Tipicamente, a boa prática aponta para o uso do operador (<-) na atribuição de objetos e (=) para atribuição de valores de parâmetro.

Para se trabalhar com o **CSV**, formato mais comun nestes casos, seria tão simples quanto passar o caminho do arquivo.

<pre style="font-size: 1.6em !important">
    <code class="r">
  data <- read.csv("sementes.csv")
    </code>
</pre>

Vamos olhar a estrutura de nosso arquivo. Se trata de uma listagem de sementes classificada por cor, comprimento, largura e índice de nutrientes. Nosso objetivo aqui é prever os valores da coluna nutrientes com base nos dados anteriores da semente.

Uma vez que temos nosso arquivo carregado, podemos utilizar alguns comandos a fim de vizualizar o nosso conjunto de dados.

<pre style="font-size: 1.6em !important">
    <code class="r">
  # Exibe o shape dos dados
  dim(data)

  # Concatena duas strings
  paste("Linhas: ", dim(data)[1], sep=" ")
  paste("Colunas: ", dim(data)[2], sep=" ")

  # Exibe o dados
  print(data)
    </code>
</pre>

A primeira função exibe a estrutura básica dos dados, retornando a quantidade de linhas e colunas do dataset. Notem que estou utilizando a função **paste()** para concatenar duas strings. Aqui podemos ver que o resultado pode ser lido como um **array**, onde tenho na posição 1 o primeiro item, e na posição 2 o segundo item. Depois apenas nomeio qual é a coluna e qual é a linha. A próxima função irá exibir os dados como extraído do arquivo. Usamos a função **print()** para exibir qualquer saída para o nosso programa.

Nossa saída seria algo como o que se segue abaixo:

<pre style="font-size: 1.2em !important">
    <code class="r">
  8 4

  'Linhas:  8'
  'Colunas:  4'

     Color Length Width Nutrients
  1   blue    5.4   1.8       0.9
  2   blue    4.8   1.5       0.7
  3   blue    4.9   1.6       0.8
  4 yellow    5.0   1.9       0.4
  5 yellow    5.2   1.5       0.3
  6 yellow    4.7   1.9       0.4
  7  green    3.7   2.2       1.4
  8  green    4.2   1.9       1.2
    </code>
</pre>

> Observe que a saída acima exibe os índices do __array de dados, começando em 1__. Este é um ponto importante a se notar, já que na maioria das linguagens estamos acostumados com os índices de __base 0__, como em C# ou Python.

Agora vamos executar a análise da função de __Modelo Linear__. Para isso execute os comandos abaixo:

<pre style="font-size: 1.4em !important">
    <code class="r">
  model <- lm(data$Nutrients ~ (data$Color + data$Length + data$Width))

  summary(model)
    </code>
</pre>

Neste trecho de código temos a variável __model__ que é o resultado da nossa análise de regressão linear. Aqui estamos usando a função __lm()__ **(linear model)**, na qual temos a __variável dependente__ a ser prevista (data$Nutrients), e as variáveis independentes, a saber: __data$Color, data$Length, data$Width__.

O próximo commando **(summary(model))**, vai exibir o resultádo básico formatado da análise que foi armazenda no objeto model. Teremos a seguinte saída para o código acima:

<pre style="font-size: 1.2em !important">
    <code class="r">
  Call:
  lm(formula = data$Nutrients ~ (data$Color + data$Length + data$Width))

  Residuals:
          1         2         3         4         5         6         7         8
   0.009418 -0.030030  0.020611 -0.028320  0.044164 -0.015844  0.042596 -0.042596

  Coefficients:
                   Estimate Std. Error t value Pr(>|t|)   
  (Intercept)      -0.14758    0.48286  -0.306  0.77986   
  data$Colorgreen   0.35672    0.09990   3.571  0.03754 *
  data$Coloryellow -0.49083    0.04507 -10.891  0.00166 **
  data$Length       0.04159    0.07876   0.528  0.63406   
  data$Width        0.45200    0.11973   3.775  0.03255 *
  ---
  Signif. codes:  0 ‘\***\’ 0.001 ‘\**\’ 0.01 ‘\*\’ 0.05 ‘.’ 0.1 ‘ ’ 1

  Residual standard error: 0.05179 on 3 degrees of freedom
  Multiple R-squared:  0.9927,	Adjusted R-squared:  0.9829
  F-statistic: 101.6 on 4 and 3 DF,  p-value: 0.00156
    </code>
</pre>

Olhando para o nosso conjunto de dados responda a seguinte pergunta: Qual seria o valor de <u>Nutrientes</u> para uma determinada semente se a <u>cor</u> da mesma fosse <u>yellow</u> e suas <u>largura</u> e <u>altura</u> fossem <u>1.9</u> e <u>4.7</u> respectivamente?

E ai? Já sabe a resposta?

Olhando para o nosso dataset é fácil de responder esta pergunta. Estamos falando do item <u>[6]</u> de nossa lista. Sendo assim sabemos que o valor de nutrientes será <u>0.4</u>.

Agora queremos <u>prever</u> este valor usando nosso modelo. Como faremos isso?

Vamos olhar para o resultado da análse que fizemos anteriormente. Em Coefficients vamos utilizar apenas a primeira e segunda colunas. Temos aqui nossas variáveis independetes e suas estimativas.

> Vale notar que temos uma constante chamada (Intercept), não associada a qualquer variável.

Quando você tem variáveis explicativas categóricas, um dos valores é descartado. Em nosso caso o valor escolhido foi o blue.

Para fazer uma previsão usando o modelo, é necessário calcular a soma linear dos valores das estimativas multiplicados pelos valores correspondentes em relação as variáveis independentes. Em nosso caso a equação seria:

<pre style="font-size: 1.2em !important">
    <code class="r">
  -0.14758 + (0.35672 * 0) + (-0.49083 * 1) + (0.04159 * 4.7) + (0.45200 * 1.9)
    </code>
</pre>

Vamos entender como chegar neste resultado. Com base nos quadro abaixo fica mais simples compreender:

| NA | yellow | green | Length | Width |
|------:|------:|------:|------:|------:|
| -0.14758 | 0.35672 | -0.49083 | 0.04159 | 0.45200 |

<div style="margin-bottom: 5em;"></div>

Primeiro listamos os valores da coluna Estimate. Depois para cada valor, multiplicamos a variável correspondente. No caso do primeiro valor estamos falando da constante Intercept, logo não existe valor a ser multiplicado. Para o segundo valor, temos como resultado <u>(0.35672 * 0)</u>. É o sugundo valor multiplicado por 0, já que nossa previsão não inclui a variável green. Multiplicamos o valor de data$Length, 0.04159 por 4.7 e temos (0.04159 * 4.7). A mesma lógica para data$Width e temos (0.45200 * 1.9).

O resultado será 0.415863, um valor muito próximo de 0.40, que é o valor real descrito no arquivo.

Na saída acima temos uma sessão, iniciada com <u>Residual standard error</u>. Aqui temos a relação entre as variáveis independentes e a variável dependente.

<pre style="font-size: 1.2em !important">
    <code class="r">
  Residual standard error: 0.05179 on 3 degrees of freedom
  Multiple R-squared:  0.9927,	Adjusted R-squared:  0.9829
  F-statistic: 101.6 on 4 and 3 DF,  p-value: 0.00156
    </code>
</pre>

O valor de <u>Multiple R-squared (0,9927)</u> é a porcentagem de variação na variável dependente explicada pela combinação linear das variáveis independentes. Neste caso os valores de R-squared são valores entre 0 e 1, onde os valores mais altos significam um modelo de previsão melhor. Em nosso caso, R-squared tem um valor extremamente alto, indicando que Color, Length e Width podem prever o resultado com boa precisão. F-statistic, Adjusted R-squared e p-value são outras medidas de ajuste do modelo.

## Impressões
No geral minha primeira impressão da linguagem <u><b>R</b></u> foi muito boa. Achei uma sintaxe limpa, fácil e bem direcionada ao seu propósito. Já tinha em mente que esta seria uma linguagem orientada a estatística computacional, mas esperava algo mais rebuscado, diferente da facilidade de compreensão que tive.

## Conclusão
Minha ideia aqui não era fazer um comparativo, ou muito menos explicar os principais comandos da linguagem. A documentação por si só já é eficaz, e ainda existe uma infinidade de materiais sobre este tema. Preferi aqui fazer uma analise da minha impressão ao implementar uma técnica básica como a regressão linear.

## Referências
* [rdocumentation.org](https://www.rdocumentation.org/)
* [Linear Regression](https://en.wikipedia.org/wiki/Linear_regression)


<style type="text/css">
table {
	color:#333333;
	border-width: 1px;
	border-collapse: collapse;
}
table th {
	border-width: 1px;
	padding: 12px;
	border-style: solid;
	background-color: #dedede;
}
table td {
	border-width: 1px;
	padding: 8px;
	border-style: solid;
	background-color: #ffffff;
}
</style>
