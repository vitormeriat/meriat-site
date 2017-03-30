---
layout: post
title: Spark - Resilient Distributed Datasets
date: 2015-08-29
categories:
  - Big Data
  - Spark
---

<p align="justify"><a href="http://spark.apache.org/"><strong><font size="4">Spark</font></strong></a> é uma estrutura de processamento paralelo, um sistema <strong>Open Source</strong> para computação em <a href="http://pt.wikipedia.org/wiki/Cluster"><strong>cluster</strong></a> cujo objetivo é possibilitar que a análise de dados seja a mais rápida possível. <strong>Spark</strong> foi pensado com base na crescente necessidade de análise de grandes volumes de dados no menor tempo possível. Seu mecanismo de processamento foi desenvolvido com foco em velocidade e facilidade de uso, visando sempre uma análise sofisticada.
<p style="background-color: #0e324a">
    <img width="100%" alt="spark-bigdata" src="http://blob.vitormeriat.com.br/images/2015/08/spark-bigdata.jpg" />
</p>

<p align="justify">Estou falando de um projeto <strong>Apache</strong> anunciado como <u>“lightning fast cluster computing”</u>, que te permite (segundo o Apache) executar programas <strong>100 vezes</strong> mais rápidos em memória e <strong>10 vezes</strong> mais rápidos em disco, quando comparado ao Hadoop, por exemplo.
<p>Em 2014, no durante toda a bateria de testes do <a href="https://databricks.com/blog/2014/10/10/spark-petabyte-sort.html" target="_blank"><strong>Daytona GraySort contest</strong></a>, Spark se mostrou <strong><font size="4">3x</font></strong> mais rápido que o Hadoop e foi considerado a solução <strong>open source</strong> mais rápida no processamento de um <strong>petabyte</strong>.
<p>Outra vantagem é em relação a codificação. Observe o exemplo abaixo:

<pre><code class="javascript">
sparkContext.textFile("hdfs://...")
    .flatMap(line =&gt; line.split(" "))
    .map(word =&gt; (word, 1)).reduceByKey(_ + _)
    .saveAsTextFile("hdfs://...")
</code></pre>

<p align="justify">Este é um exemplo simples de um <strong>Word Count</strong>, o <strong>Hello World</strong> em big data. Este código de <strong>MapReduce</strong> escrito em <strong>Java</strong> seria feito com cerca de 50 linhas, enquanto no Spark podemos utilizar <strong>Scala</strong> para uma codificação bem mais simplificada. </p>
<p align="justify">Spark também é compatível com Hadoop, sendo assim qualquer sistema de armazenamento suportado por <strong>Hadoop</strong> (<strong><u>HDFS</u>, <u>Hive</u>, <u>HBase</u>, <u>Cassandra,</u> <u>S3</u>, <u>SequenceFiles</u></strong>) poderá ser utilizado como fonte de dados para o Spark. </p>
<p align="justify">As primeiras aplicações práticas para o Spark foram no sentido de estender o modelo MapReduce para um melhor suporte a aplicações analíticas como Algoritmos <em><strong>iterativos</strong> </em>(<a href="http://pt.wikipedia.org/wiki/Aprendizagem_de_m%C3%A1quina">Learning machines</a> e <a href="https://pt.wikipedia.org/wiki/Teoria_dos_grafos" target="_blank">grafos</a>), bem como em ferramentas para mineração de dados <strong>interativas</strong> (<a href="http://www.r-project.org/">R</a>, Excel, Python). </p>

<h2>Por que Spark?</h2>

<p align="justify">A maioria da soluções envolvendo modelo de programação em cluster como por exemplo, o <strong>Hadoop,</strong> são baseados em um fluxo de dados acíclico onde os registros são carregados de um meio de armazenamento estável (sistema de arquivos distribuído, banco de dados, etc), submetidos a um <strong>DAG</strong> <strong>(Directed Acyclic Graph)</strong> de operadores deterministicos, e escritos de volta em um meio de armazenamento estável. Observe a imagem abaixo, que representa um <strong>DAG</strong>, onde as atividades estão interligadas por ciclos que não estão em uma sequência seguindo uma mesma direção.</p>
<p align="justify">
    <img width="100%" alt="Directed_acyclic_graph" src="http://blob.vitormeriat.com.br/images/2015/08/Directed_acyclic_graph.png" />
</p>
<p align="justify">A imagem abaixo exibe um fluxo de dados acíclico com um modelo tradicional <strong>MapReduce</strong>. Ela demonstra a leitura dos dados de um meio estável, o processamento utilizando MapReduce em paralelo e a escrita do resultado em um meio estável. Para aplicações que precisam ler conjuntos de dados repetidas vezes e utilizar funções de agregação (<strong>count</strong>, <strong>min</strong>, <strong>max</strong>, <strong>avg</strong>) esse modelo não é tão eficiente pois precisa ler os dados do disco a cada query, para quem esta acostumado a realizar análise de dados principalmente utilizando Hadoop provavelmente conhece o <a href="http://hive.apache.org/">Apache Hive</a> cuja a função é fornecer um sistema de <strong>Data Warehouse</strong> para Hadoop.</p>
<p style="background-color: #0c3f67">
  <img width="100%" alt="map-reduce-end" src="http://blob.vitormeriat.com.br/images/2015/08/map-reduce-end.png" />
</p>
<p align="justify">Nesse ponto o Spark desponta como uma solução mais viável pois uma vez os dados em memória a manipulação das informações se torna muito mais rápida, em alguns estudos Spark se mostra <u><strong>30 vezes</strong></u> mais eficiente que <strong>Hive/Hadoop</strong>. </p>

<h2>Como o Spark consegue isso?</h2>
<p align="justify">Uma primeira vista é sobre o Spark Core, a engine que permite o processamento distribuído em grande escala. Sua responsábilidade é a gestão de memória, recuperação de falhas, distribuição e monitormanto dos jobs em um cluster e integração com os sistemas de armazenamento. Esse é o cara respnosável por orquestrar todo o desempenho que o Spark pode alcançar.</p>
<p align="justify">E qual o segredo de todo este desempenho? Está no chamado <strong>RDDs</strong> ou <strong>Resilient Distributed Datasets</strong>, que mantêm as características essenciais do MapReduce (<strong>Tolerância a falhas</strong>, <strong>transparência de localização de dados</strong> e <strong>escalabilidade</strong>).</p>
<p align="justify">Spark introduziu o conceito de RDD, que formalmente é uma coleção de objetos <strong>somente leitura</strong>, particionados em um conjunto de nodos do cluster, podendo somente&nbsp; ser criado através de funções determinísticas (<strong>map</strong>, <strong>filter</strong>, <strong>join</strong>, <strong>groupBy</strong>) executadas em outros RDDs ou meios de armazenamentos estáveis como o Hadoop Filesystem. Basicamente RDDs suportam dois tipos de operações: <strong>Transformations</strong> (map, filter, join, union, etc) e <strong>Actions</strong> (reduce, count, first, etc).</p>
<p align="justify">RDDs são representados no Spark por objetos, transformações são executadas invocando métodos nesses objetos. Aplicações em Spark são conhecidas como <strong><em>Drivers </em></strong><em></em>e esses drivers implementam as operações que são executadas tanto no modo <strong><em>single- node cluster</em></strong> ou <strong><em>multi-node cluster</em></strong>. Um Driver pode executar dois tipos de operações em um conjunto de dados: Um ação e uma transformação. Um ação executa um processamento em um conjunto de dados e retorna um valor para o Driver, uma transformação cria um novo conjunto de dados a partir de um conjunto de dados existente. </p>
<p>&nbsp;<br />

<h2>Referências</h2>
<ul>
  <li><a href="http://spark.apache.org/docs/latest/programming-guide.html" target="_blank">Spark Programming Guide</a></li>
  <li><a href="http://www.datanami.com/2014/03/06/apache_spark_3_real-world_use_cases/" target="_blank">Apache Spark: 3 Real-World Use Cases</a></li>
  <li><a href="https://databricks.com/blog/2014/10/10/spark-petabyte-sort.html" target="_blank">Spark the fastest open source engine for sorting a petabyte</a></li>
</ul>
