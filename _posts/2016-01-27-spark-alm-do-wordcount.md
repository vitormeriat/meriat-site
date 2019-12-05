---
layout: post
title: Spark além do WordCount
date: 2016-01-27
categories:
   - Big Data
   - Spark
image: "http://blob.vitormeriat.com.br/images/2016/01/spark-capa.jpg"
---
<p style="background-color: #000000" align="center"><a href="http://blob.vitormeriat.com.br/images/2016/01/spark-capa.jpg"><img title="spark-capa" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto"   alt="spark-capa" src="http://blob.vitormeriat.com.br/images/2016/01/spark-capa.jpg" width="819" height="518" /></a></p>

Não é enganação, vou fazer o famoso exemplo do **WordCount**, porém vou tentar ir além do que apenas mostrar o código ou dizer Spark torna esta tarefa mais simples que utilizar Hadoop/MapReduce. A exemplo do post <a href="http://www.vitormeriat.com.br/spark-resilient-distributed-datasets/">Spark – Resilient Distributed Datasets</a>, vou focar na base e estrutura básica da ferramenta para se conseguir o desempenho esperado ao utilizar o Spark.

## Spark e o MapReduce
Resumindo toda a brincadeira, o Spark estende o <a href="https://en.wikipedia.org/wiki/MapReduce">MapReduce</a> de modo a evitar mover os dados durante o processamento se utilizando de recursos como armazenamento em memória e processamento em tempo real (ou quase isso). Só a utilização destas artimanhas já é capaz de proporcionar um desempenho várias vezes melhor que outras tecnologias de Big Data.

Os resultados intermediários são retidos em memória ao invéz de serem escritos em disco. Isso é traduzido em desempenho, principalmente quando se precisa processar o mesmo conjuntos de dados muitas vezes.

É importante saber que o Spark funciona tanto em memória quanto em disco, e sendo assim executa as operações em disco quando os dados não cabem mais na memória, logo podemos utilizar o Spark para o processamento de conjuntos de dados maiores que a memória agregada de um cluster.

Praticamente como tudo na vida de TI, cabe ao técnico analizar os dados e casos de uso para avaliar os requisitos de memória necessários. Só assim será possível conseguir o desempenho esperado ao se utilizar o Spark.

## Spark Framework Ecosystem
Fora a API do Spark, existem bibliotecas adicionais que fazem parte do seu ecossistema e fornecem capacidades adicionais para as áreas de análise de Big Data e aprendizado de máquina.

<a href="http://blob.vitormeriat.com.br/images/2016/01/spark-stack.png"><img title="spark-stack" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto"   alt="spark-stack" src="http://blob.vitormeriat.com.br/images/2016/01/spark-stack.png" width="633" height="298" /></a>
<div style="height: 50px;"></div>

#### <a href="https://spark.apache.org/sql/">Spark SQL</a>
Fornece a capacidade de expor os conjuntos de dados Spark através de uma API JDBC. Isso permite executar consultas no estilo SQL sobre esses dados usando ferramentas tradicionais de BI e de visualização. Além disso, também permite que os usuários usem ETL para extrair seus dados em diferentes formatos (como JSON, Parquet, ou um banco de dados), transformá-los e expô-los para consultas ad-hoc;

#### <a href="https://spark.apache.org/streaming/">Spark Streaming</a>
Pode ser usado para processar dados de streaming em tempo real baseado na computação de microbatch. Para isso é utilizado o DStream que é basicamente uma série de RDD para processar os dados em tempo real;

#### <a href="https://spark.apache.org/mllib/">MLlib</a>
É a biblioteca de aprendizado de máquina do Spark, que consiste em algoritmos de aprendizagem, incluindo a classificação, regressão, clustering, filtragem colaborativa e redução de dimensionalidade;

#### <a href="https://spark.apache.org/graphx/">GraphX</a>
É uma nova API do Spark para grafos e computação paralela. Em alto nível, o GraphX ​​estende o Spark RDD para grafos. Para apoiar a computação de grafos, o GraphX ​​expõe um conjunto de operadores fundamentais (por exemplo, subgrafos e vértices adjacentes), bem como uma variante optimizada do Pregel. Além disso, o GraphX ​​inclui uma crescente coleção de algoritmos para simplificar tarefas de análise de grafos.
<div style="height: 50px;"></div>

O Spark é escrito na linguagem <a href="http://www.scala-lang.org/">Scala</a>, executa em uma máquina virtual Java e atualmente suporta as seguintes linguagens:
* <a href="http://www.scala-lang.org/">Scala</a>
* Java
* <a href="https://www.python.org/">Python</a>
* <a href="http://clojure.org/">Clojure</a>
* <a href="https://www.r-project.org/">R</a>
<div style="height: 50px;"></div>

## Instalação
Basicamente você pode testar o Spark utlizando uma instalação em sua máquina para execução stand-alone, utilizar alguma máquina virtual (VM) pronta, como as disponibilizadas pela Cloudera, Hortonworks, MapR ou ainda, utilizando o Spark como serviço em Cloud Computing no Azure ou AWS.

Basicamente para este exemplo vamos apens executar o mesmo localmente. O processo é simples, basta instalar o <a href="http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html">JDK</a> e realizar o download da última versão do <a href="https://spark.apache.org/downloads.html">Spark</a>.

O importante aqui é que após o download, você deve descompactar a pasta do Spark em alguma pasta, de preferência no C: da sua máquina. No meu caso eu estou usando o seguinte caminho: **C:bigdataspark**
<div style="height: 50px;"></div>

## Execução
Para verificar a instalação o Spark, navegue até o diretório e execute o shell do Spark utilizando os comandos a seguir. Isto é para Windows. Se estiver usando Linux ou Mac OS, edite os comandos para trabalhar em seu sistema operacional.
<pre style="font-size: 1.6em !important">
    <code class="javascript">
    cd c:bigdataspark
    binspark-shell
    </code>
</pre>

Se o Spark foi instalado corretamente, será apresentado as seguintes mensagens na saída no console.

<img title="spark-tela" alt="spark-tela" src="http://blob.vitormeriat.com.br/images/2016/01/spark-tela.jpg" width="100%" />

Para validar, rode o seguinte comando:
<pre style="font-size: 1.6em !important"><code class="javascript">sc.version</code></pre>

Ele deve voltar algo como String = 1.4.1, ou seja, a versão do Spark que estamos usando.
<div style="height: 50px;"></div>

## Mão na massa

Como já foi demonstrado, estamos utilizando o Spark via **Shell**. O Spark Shell está disponível em **Scala** e **Python**. Para acessá-los, execute respectivamente os comandos **spark-shell.cmd** e **pyspark.cmd**. Para este exemplo vou estar utilizando Scala.

Agora notem nas mensagens da inicialização do Spark a seguinte mensagem: **Spark context available as sc.** Ela indica que podemos interagir com o cluster Spark, o contexto é como se fosse a ponte entre um programa e o cluster.

O primeiro passo será carregar o arquivo **Crimes_-_2015.txt**. É um arquivo público com a base dos crimes cometidos em Chigago no ano de 2015. O link vai estar nas resferências. É um arquivo bem pequeno com apenas 260 mil registros. Ótimo para um teste.

O objeto de contexto possui várias métodos para que um arquivo possa ser carregado e utilizado pelo Spark, no nosso caso utilizaremos o método **textFile** que recebe como parâmetro obrigatório o caminho do arquivo ou arquivos, podemos utilizar wildcards, caminho de um diretório, caminho para arquivos locais, arquivos em um HDFS, S3.

Além de **Text Files** o Spark permite que os **RDDs** possam ser criados a partir de <a href="http://hadoop.apache.org/common/docs/current/api/org/apache/hadoop/mapred/SequenceFileInputFormat.html">Sequence Files</a> e qualquer outro <a href="http://hadoop.apache.org/docs/stable/api/org/apache/hadoop/mapred/InputFormat.html">InputFormat</a> do Hadoop.

Mas o que é um RDD? A maioria dos processamentos realizados em sistemas, sejam eles comerciais ou de pesquisas avançadas fazem uso de coleções de objetos, sejam esses simples ou complexos, se formos pensar em algo muito utilizado em Big Data que é a estatística, vamos perceber que no fim serão realizadas as quatro operações básicas da matemática combinadas de formas diferentes para chegar a um resultado, desse modo podemos definir os **RDDs** de forma simples como sendo coleções de objetos que nos permitem realizar uma série de operações (não apenas matemáticas) em seu conteúdo.

Até aí nada de novo, qualquer linguagem de programação possui de uma forma ou de outra o conceito de coleções, mas agora pense em coleções com Terabytes de conteúdo, como podemos distribuir o processamento de forma confiável, com tolerância a falhas e em paralelo? Pois bem, nesse ponto entra o **RDD** que é uma coleção com todas essas características te liberando para pensar nas suas implementações ao invés desses detalhes tão importantes e difíceis de implementar.

Agora vamos carregar nosso arquivo utilizando o método **textFile**. Por padrão o **textFile** irá carregar cada linha do arquivo como sendo um registro.

<pre style="font-size: 1.6em !important">
    <code class="javascript">
    val full = sc.textFile("C:/bigdata/bases/Crimes_-2015.txt")
    </code>
</pre>

O método **textFile** aceita dois parâmetros, o caminho do arquivo e o número de **Partitions**.**Partitions**? O que são as **Partitions**? Vamos executar dois comandos:

<pre style="font-size: 1.6em !important">
    <code class="javascript">
    full.partitions
    full.partitions.length
    </code>
</pre>

Podemos ver que para o arquivo que carregamos foram geradas **70 Partitions** que na verdade é o **Dataset** completo dividido em partes menores, no nosso exemplo estamos usando **HadoopPartition**, sendo assim cada **Partition** estará limitada ao tamanho de um bloco **HDFS** cujo padrão é 64MB, não é assunto para esse post mas o número de **Partitions** tem influência direta no comportamento do **Spark** principalmente em relação a performance e movimentação de dados no cluster. Como mencionei há um parâmetro opcional que é o número de **Partitions**, caso você especifique o número menor que o necessário baseado no cálculo padrão o parâmetro será desprezado.

Agora, antes de executarmos o WordCount vamos entender o que ocorre internamente quando executamos um programa Spark. Primeiramente é importante saber que para um **RDD** temos dois tipos de operações:

* Transformations: São as operações que criam um novo **Dataset** a partir de um existente, no nosso caso temos três transformações (**flatMap**, **map** e **reduceByKey**)
* Actions: São as operações que retornam um valor processado, no nosso caso seria o **collect** que retorna todos os elementos do **Dataset** em formato de array.
<div style="height: 50px;"></div>

### Passo 1:
Nesse momento serão identificadas as necessidades de processamento, no nosso exemplo teremos a seguinte sequência:
* HadoopRDD
* flatMap()
* map()
* reduceByKey()
* collect()
<div style="height: 20px;"></div>

### Passo 2:
Nesse momento serão identificados os estágios (**Stages**) para o processamento, os **Stages** são definidos de acordo com a necessidade de movimentação de dados na execução das **transformations** e **actions**, no nosso exemplo teremos 2 estágios, o primeiro contemplando a criação do RDD, **flatMap**, **map** e **reduceByKey** e um outro estágio exclusivamente para o **collect**.
<div style="height: 20px;"></div>

### Passo 3:
Agora que temos os estágio definidos é o momento de dividir os estágios em **Tasks** e submetê-las para processamento, uma **Task** é a combinação dos dados e computação sobre esses dados (**transformations** e **actions**) a idéia é que somente após todas as **<em>Tasks</em>** estejam concluídas o próximo estágio seja iniciado.
<div style="height: 20px;"></div>

Agora que já sabemos o básico dos detalhes internos do **Spark** vamos executar o programa que contará as palavras.

<pre style="font-size: 1.6em !important">
<code class="javascript">
val counts = full.flatMap(line =&gt; line.split(" "))
 .map(word =&gt; (word, 1))
 .reduceByKey(_+_)
 .collect()
</code></pre>

Após a execução o **collect** nos retorna parte do resultado como podemos ver abaixo:

<img title="spark-result" alt="spark-result" src="http://blob.vitormeriat.com.br/images/2016/01/spark-result.jpg" width="100%" />

O retorno nos mostra uma estrutura de mapa contendo como **Key** a palavra cujo o valor é a quantidade de vezes que a palavra aparece no arquivo.

A imagem abaixo mostra a UI do **Spark** exibindo os dados de execução dos 2 estágios:

<img title="spark-ui" alt="spark-ui" src="http://blob.vitormeriat.com.br/images/2016/01/spark-ui.jpg" width="100%"/>

Ao invés de utilizar o **collect** poderíamos utilizar o **saveAsTextFile** e teríamos todo o conteúdo em arquivo.

<div style="height: 50px;"></div>

## Referências
* Download: <a href="http://spark.incubator.apache.org/downloads.html"> http://spark.incubator.apache.org/downloads.html</a>
* Quick Start:<a href="http://spark.incubator.apache.org/docs/latest/quick-start.html"> http://spark.incubator.apache.org/docs/latest/quick-start.html</a>
* DataSet: <a title="https://data.cityofchicago.org/Public-Safety/Crimes-2015/vwwp-7yr9" href="https://data.cityofchicago.org/Public-Safety/Crimes-2015/vwwp-7yr9">https://data.cityofchicago.org/Public-Safety/Crimes-2015/vwwp-7yr9</a>
* <a title="http://spark.apache.org/examples.html" href="http://spark.apache.org/examples.html">http://spark.apache.org/examples.html</a>

## Citação
Neste post realizei citações ao post do master Isaías que pode ser lido <a href="https://isaiasbarroso.wordpress.com/2014/08/22/wordcount-em-spark/">clicando aqui!</a>
