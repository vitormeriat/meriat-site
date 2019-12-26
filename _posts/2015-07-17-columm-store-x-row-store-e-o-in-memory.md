---
layout: post
title: Columm Store x Row Store e o In-Memory
date: 2015-07-17
categories:
  - Big Data
  - NoSQL
image: "http://blob.vitormeriat.com.br/images/2015/07/Untitled-8.png"
---

**IoT**, **Mobile**, **Big Data**, **Stream Analytics** e por ai vai. Cada vez temos mais referências da necessidade dos chamados **NoSQLs**. A verdade é que o cenário de armazenamento de dados clássico tem se tornado inviável em alguns cenários. Para aqueles de nós que já estão vendo este futuro hoje, vale entender as bases deste novo mundo cheio de diferenças em relação ao nosso tradicional modelo relacional de armazenamento de dados.</p>

Com a crescente necessidade de análise de grandes volumes de dados no menor tempo possível, bancos de dados baseados em uso intensivo de memória **RAM** (In-Memory) estão cotados como sendo a solução mais viável. A principal diferença entre os bancos de dados** In-Memory** e os “<u>tradicionais/clássicos</u>” já conhecidos, está na forma de armazenamento dos dados, **<em>Column Store vs Row Store. </em>**Vamos considerar uma tabela organizada nos dois modelos:

## Row Store

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/Untitled-1.png">
</div>

## Column Store

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/Untitled-5.png">
</div>

Ao invés de cada registro da tabela ficar armazenado em uma linha, o registro passa a ser armazenado em colunas separadas. Essa forma de armazenamento tem algumas vantagens, como exemplo a capacidade de compressão dos dados, se formos analisar a compressão de um banco onde os registros são armazenados em linha, encontraremos em uma mesma linha diferentes tipos (domínios) o que torna o processo mais complicado, já no banco orientado a colunas, cada coluna irá conter o mesmo tipo (domínio) de dado. De acordo com algumas pesquisas o nível de compressão alcançado  em bancos orientados a colunas chega a ser de **60%** a **70%**  mais eficiente que nos bancos orientados a linhas.

Para o caso de armazenamento dos dados em colunas é necessário que haja um relacionamento entre as colunas para identificar que a mesma pertence a um registro específico, para resolver esse problema a estratégia de incluir um ID virtual é normalmente adotada, nesse caso a representação do armazenamento em colunas ficaria como a imagem abaixo:

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/Untitled-8.png">
</div>

Vamos a seguinte query:

<pre style="font-size: 1.2em !important">
    <code class="sql">
  SELECT AVG(PESSOA_IDADE) FROM PESSOA
    </code>
</pre>

Em um banco de dados orientado a linhas, esta consulta irá recuperar todas as linhas, carregando todos os campos para executar a operação e retornar a média de idade, já no banco de dados orientado a colunas apenas a coluna **PESSOA_IDADE** será levada em consideração, o que neste caso vai consumir menos recursos.

Vale lembrar que um **SELECT * FROM PESSOA**, possivelmente não terá vantagem alguma já que todas as colunas precisarão ser lidas.

As principais técnicas aplicadas a banco de dados em coluna são particionamento, indexação, compressão e uma série de estratégias para realização dos **JOINS**.

A utilização de armazenamento em colunas torna-se viável com a utilização de arquiteturas de hardware modernas com grande número de processadores e grandes quantidades de memória. Os tipos de sistemas mais indicados para uso de armazenamento em colunas são os sistemas que precisam ler e realizar operações de consultas em grandes volumes de dados (<a href="http://pt.wikipedia.org/wiki/OLAP">OLAP</a>), para sistemas do tipo <a href="http://pt.wikipedia.org/wiki/OLTP">OLTP</a> as operações de escrita podem não ser tão vantajosas.

Alguns fornecedores permitem que uma tabela seja definida como **Column Store** ou **Row Store** dentro do mesmo banco de dados. Mesmo com as implicações desta abordagem, o grande desafio dos fabricantes hoje é desenvolver as melhores soluções que consigam extrair o máximo do hardware e abstrair as complexidades para os usuários.

Para quem se interessar pelo assunto, deixo alguns links com boas informações sobre **Column Store**.

## Referências

<ul>
<li><a href="http://cs-www.cs.yale.edu/homes/dna/talks/Column_Store_Tutorial_VLDB09.pdf">Column-Oriented Database Systems</a></li>
<li><a href="http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf"><em>Column</em>–<em>Stores</em> vs. Row-Stores: How Different Are They Really?</a></li>
<li><a href="http://en.wikipedia.org/wiki/Column-oriented_DBMS">Column Oriented DBMS</a></li>
</ul>