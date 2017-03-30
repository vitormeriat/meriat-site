---
layout: post
title: Columm Store x Row Store e o In-Memory
date: 2015-07-17
categories:
  - Big Data
  - NoSQL
image-full: "http://blob.vitormeriat.com.br/images/2015/07/Untitled-8.png"
---
<p align="justify"><strong>IoT</strong>, <strong>Mobile</strong>, <strong>Big Data</strong>, <strong>Stream Analytics</strong> e por ai vai. Cada vez temos mais referências da necessidade dos chamados <strong>NoSQLs</strong>. A verdade é que o cenário de armazenamento de dados clássico tem se tornado inviável em alguns cenários. Para aqueles de nós que já estão vendo este futuro hoje, vale entender as bases deste novo mundo cheio de diferenças em relação ao nosso tradicional modelo relacional de armazenamento de dados.</p>
<p align="justify">Com a crescente necessidade de análise de grandes volumes de dados no menor tempo possível, bancos de dados baseados em uso intensivo de memória <strong>RAM</strong> (In-Memory) estão cotados como sendo a solução mais viável. A principal diferença entre os bancos de dados<strong> In-Memory</strong> e os “<u>tradicionais/clássicos</u>” já conhecidos, está na forma de armazenamento dos dados, <strong><em>Column Store vs Row Store. </em></strong>Vamos considerar uma tabela organizada nos dois modelos:</p>
<p>&nbsp;</p>
<h2><strong>Row Store</strong></h2>
<p><img src="http://blob.vitormeriat.com.br/images/2015/07/Untitled-1.png" alt="Untitled-1" width="100%" /></p>
<p>&nbsp;</p>

<h2><strong>Column Store</strong></h2>
<p><img src="http://blob.vitormeriat.com.br/images/2015/07/Untitled-5.png" alt="Untitled-5" width="100%" /></p>
<p><!--more--></p>
<p align="justify">Ao invés de cada registro da tabela ficar armazenado em uma linha, o registro passa a ser armazenado em colunas separadas. Essa forma de armazenamento tem algumas vantagens, como exemplo a capacidade de compressão dos dados, se formos analisar a compressão de um banco onde os registros são armazenados em linha, encontraremos em uma mesma linha diferentes tipos (<strong>domínios</strong>) o que torna o processo mais complicado, já no banco orientado a colunas, cada coluna irá conter o mesmo tipo (<strong>domínio</strong>) de dado. De acordo com algumas pesquisas o nível de compressão alcançado  em bancos orientados a colunas chega a ser de <strong>60%</strong> a <strong>70%</strong>  mais eficiente que nos bancos orientados a linhas.</p>
<p align="justify">Para o caso de armazenamento dos dados em colunas é necessário que haja um relacionamento entre as colunas para identificar que a mesma pertence a um registro específico, para resolver esse problema a estratégia de incluir um ID virtual é normalmente adotada, nesse caso a representação do armazenamento em colunas ficaria como a imagem abaixo:</p>
<p><img src="http://blob.vitormeriat.com.br/images/2015/07/Untitled-8.png" alt="Untitled-8" width="100%" /></p>
<p>Vamos a seguinte query:</p>
<pre style="font-size: 22pt !important;"><code class="sql">
SELECT AVG(PESSOA_IDADE) FROM PESSOA
</code></pre>
<p align="justify">Em um banco de dados orientado a linhas, esta consulta irá recuperar todas as linhas, carregando todos os campos para executar a operação e retornar a média de idade, já no banco de dados orientado a colunas apenas a coluna <strong>PESSOA_IDADE</strong> será levada em consideração, o que neste caso vai consumir menos recursos.</p>
<p align="justify">Vale lembrar que um <strong>SELECT * FROM PESSOA</strong>, possivelmente não terá vantagem alguma já que todas as colunas precisarão ser lidas.</p>
<p align="justify">As principais técnicas aplicadas a banco de dados em coluna são particionamento, indexação, compressão e uma série de estratégias para realização dos <strong>JOINS</strong>.</p>
<p align="justify">A utilização de armazenamento em colunas torna-se viável com a utilização de arquiteturas de hardware modernas com grande número de processadores e grandes quantidades de memória. Os tipos de sistemas mais indicados para uso de armazenamento em colunas são os sistemas que precisam ler e realizar operações de consultas em grandes volumes de dados (<a href="http://pt.wikipedia.org/wiki/OLAP">OLAP</a>), para sistemas do tipo <a href="http://pt.wikipedia.org/wiki/OLTP">OLTP</a> as operações de escrita podem não ser tão vantajosas.</p>
<p align="justify">Alguns fornecedores permitem que uma tabela seja definida como <strong>Column Store</strong> ou <strong>Row Store</strong> dentro do mesmo banco de dados. Mesmo com as implicações desta abordagem, o grande desafio dos fabricantes hoje é desenvolver as melhores soluções que consigam extrair o máximo do hardware e abstrair as complexidades para os usuários.</p>
<p align="justify">Para quem se interessar pelo assunto, deixo alguns links com boas informações sobre <strong>Column Store</strong>.</p>
<p>&nbsp;</p>
<h1>Referências</h1>
<ul>
<li><a href="http://cs-www.cs.yale.edu/homes/dna/talks/Column_Store_Tutorial_VLDB09.pdf">Column-Oriented Database Systems</a></li>
<li><a href="http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf"><em>Column</em>–<em>Stores</em> vs. Row-Stores: How Different Are They Really?</a></li>
<li><a href="http://en.wikipedia.org/wiki/Column-oriented_DBMS">Column Oriented DBMS</a></li>
</ul>
<p>&nbsp;</p>
<h2><span style="color: #ffc000;">Bons estudos e até a próxima pessoal  ;)</span></h2>