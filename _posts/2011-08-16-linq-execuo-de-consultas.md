---
layout: post
title: 'LINQ: Execução de consultas'
date: 2011-08-16
categories:
    - LINQ
---

<p align="justify">Durante a escrita de um teste para uma nova funcionalidade no sistema, reparei que havia da minha parte um esforço desnecessário para bater determinados valores em um relatório. Não era possível, tinha que ter algo de errado, pois minha lógica estava (humildemente falando) perfeita.
<p align="justify">Fuça daqui, mexe ali e repentinamente os valores agora batem com toda a precisão matemática que era exigida. Inicio minha busca em prol de encontrar o erro e me deparo com algo interessante. Vamos fazer um teste para simular meu problema:
<p><a href="http://blob.vitormeriat.com.br/images/2011/08/011.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="01"   alt="01" src="http://blob.vitormeriat.com.br/images/2011/08/01.png" width="570" height="250" /></a>
<p align="justify"></p>
<p><!--more-->
<p align="justify">Tenho minha fonte de dados que neste caso é uma lista de inteiros. Note que tenho três itens adicionados a lista. Neste momento crio minha consulta LINQ para retornar apenas os itens maiores que 2. Pelo estado da lista, o correto era inferir que o único item maior que 2 é 3, logo somente um item vai ser retornado.
<p align="justify">Então logo após a criação da consulta adiciono mais um item a lista. No momento da exibição do resultado o que vai ser retornado? Apenas o<strong> 3</strong> ou <strong>3 | 4</strong> ?
<p align="center">?
<p align="center">?
<p align="center">?
<p align="center">?
<p align="center">O resultado retornado foi precisamente <strong>3 | 4 |</strong>.
<p>&nbsp; Vamos fazer uma breve investigação sobre o ocorrido analisando a imagem abaixo:
<p><a href="http://blob.vitormeriat.com.br/images/2011/08/021.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;margin:10px 0 20px;" title="02"   alt="02" src="http://blob.vitormeriat.com.br/images/2011/08/02.png" width="570" height="788" /></a>
<ol>
<li>No primeiro quadrante temos a lista preenchida com 3 itens no momento da criação da consulta.  </li>
<li>No segundo quadrante a consulta já existe e aponta para a fonte de dados contendo 3 itens.  </li>
<li>No terceiro quadrante adicionamos um item a fonte de dados. No momento da exibição da consulta ela aponta para a fonte de dados agora contendo 4 itens.</li>
</ol>
<p>&nbsp;<br />
<h2>Em consulta...</h2>
<p>As operações de consulta LINQ seguem a seguinte lógica:
<ol>
<li>É obtida a fonte de dados;  </li>
<li>A consulta é criada;  </li>
<li>A consulta é executada.</li>
</ol>
<p align="justify">A consulta especifica quais informações recuperar a partir da(s) fonte(s) de dados indicadas. A consulta também pode especificar como as informações devem ser classificadas, agrupadas e como serão retornadas. Uma consulta é armazenada em uma variável de consulta e inicializada com uma expressão de consulta.
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/03.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="03"   alt="03" src="http://blob.vitormeriat.com.br/images/2011/08/03.png" width="570" height="288" /></a>
<p align="justify">Parece-me bem lógico que uma consulta LINQ seja feita sobre uma fonte de dados, um DataSet, XML, coleção de objetos e etc. O que não tinha ficado muito claro era a separação entre criação e execução da consulta.
<p>&nbsp;<br />
<h2>Execução da consulta</h2>
<p align="justify">Uma função importante da maioria dos operadores de consulta é a capacidade de executarem não quando construídos, mas quando enumerados. Isto significa que a consulta é executada no momento que o método <strong>MoveNext()</strong> de <strong>IEnumerator</strong> é chamado.
<p align="justify">Quando imprimimos o resultado do código da figura 1 percebemos que o número 4 está presente. Mesmo sendo inserido após a criação da consulta, ele está garantido no resultado porque somente na execução do <strong>foreach</strong> temos uma chamada a <strong>MoveNext()</strong> no enumerador da consulta.
<p align="justify">É importante destacar que no LINQ, a variável de <b>consulta</b> não pratica nenhuma ação e não retorna nenhum dado. Ela apenas armazena as informações que são necessárias para produzir os resultados quando a consulta realmente for executada.
<p align="justify">Com isso temos duas maneiras de executar as consultas LINQ: Execução tardia ou imediata.
<p>&nbsp;<br />
<h2>Execução Tardia (Lazy Loading )</h2>
<p align="justify">Basicamente a execução tardia atrasa a execução da consulta até o ultimo momento possível já que o LINQ atrasa a execução das queries até sua real necessidade. Este recurso é muito importante porque “separa” a construção da consulta de sua execução. Isto possibilita que você construa uma consulta em muitos passos e possibilita as consultas de LINQ to SQL.
<p align="justify">Com isso você pode trafegar uma consulta entre camadas e incrementa-la de acordo com regras de negócio e outras necessidades.
<p align="justify">Execução tardia também tem suas desvantagens. Sempre que uma consulta for enumerada ela sofre uma reavaliação tendo como base o estado atual da fonte de dados. Isto pode ser desvantajoso nos seguintes cenários:
<ul>
<li>
<div align="justify">Quando você quer guardar os resultados em um ponto determinado; </div>
</li>
<li>
<div align="justify">Quando temos uma consulta computacionalmente intensa, acessou remoto ou nas nuvens e queremos evitar o acesso desnecessário.</div>
</li>
</ul>
<p align="justify">Para estes casos a melhor opção é trabalhar com a execução imediata.
<p>&nbsp;<br />
<h2>Execução Imediata</h2>
<p align="justify">Como vimos anteriormente a maioria dos operadores de consulta proporcionam execução tardia, com exceção de:
<ul>
<li>
<div align="justify">Operadores que retornam um único elemento ou valor escalar como First, Count, Max ou Average; </div>
</li>
<li>
<div align="justify">Operadores de conversão: ToArray, ToList, ToDictionary, ToLookUp.</div>
</li>
</ul>
<p align="justify">Estes operadores realizam uma execução imediata da consulta pois seus mecanismos não dão suporte a execução tardia. Se repararmos a execução do método Count, é possível perceber que ele retorna apenas um simples inteiro que não é enumerado e portando não chama MoveNext.
<p align="justify">A consulta abaixo é executada imediatamente e retorna o resultado tendo como base a lista no momento da criação da consulta. O número 4 foi desprezado.
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/04.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="04"   alt="04" src="http://blob.vitormeriat.com.br/images/2011/08/04.png" width="570" height="314" /></a>
<p align="justify">Na execução tardia de consultas, a definição de consulta é armazenada em uma variável de consulta para posterior execução. Na execução imediata, a consulta é executada no momento da sua definição. Execução é disparada quando você aplica um método que requer acesso aos elementos individuais do resultado da consulta.
<p align="justify">&nbsp;<br />
<h2 align="justify">Finalizando </h2>
<p align="justify">Vamos analisar mais um exemplo:
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/051.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="05"   alt="05" src="http://blob.vitormeriat.com.br/images/2011/08/05.png" width="570" height="316" /></a>
<p align="justify">Somente utilizar um ToList ou Count não garante que sua consulta será executada de forma imediata, pois deve-se atentar em como faze-lo. Devemos utilizar os operadores no momento exato da criação da consulta ou então ele será um lazy loading de qualquer forma.
<p align="justify">Como é possível notar, o que separa a execução tardia da execução imediata são apenas detalhes. Detalhes que fazem muita diferença em determinadas situações como no meu caso, sendo assim meu concelho é: Procure sempre investigar os recursos que a linguagem te oferece pois, muito provavelmente eles irão salvar seu dia…
<p align="justify">Você pode baixar o código fonte deste artigo <a href="https://skydrive.live.com/?sc=documents&amp;cid=bd055aa47a388023#!/?cid=bd055aa47a388023&amp;sc=documents&amp;uc=1&amp;id=BD055AA47A388023%21220" target="_blank">aqui!</a><br />
<hr />
<h3>Um grande abraço e ótimo estudo!</h3>