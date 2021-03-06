---
layout: post
title: Filosofia no JavaScript - Funções são declaração ou expressão?
date: 2014-10-24
categories:
  - JavaScript
image: "http://blob.vitormeriat.com.br/images/2014/10/capa1.png"
---
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/capa1.png"><img title="Capa" alt="Capa" src="http://blob.vitormeriat.com.br/images/2014/10/capa.png" /></a></p>
<p align="justify">Primeiro, de maneira simples e clara a resposta da pergunta acima é: <strong>Tanto faz…</strong> Funções em <strong>Javascript</strong> funcionam tanto como <strong>Declaração</strong> ou <strong>Expressão</strong>. O que nos leva a segunda pergunta: Então para que este post se é algo tão simples? Assim como na filosofia alguns dos temas mais complexos se escondem na simplicidade (não que este seja o caso).</p>
<p align="justify">O certo porém, é que uma <strong>função</strong> em Javascript pode ser utilizada de maneiras diferentes, como nos seguintes casos:</p>
<ul>
<li>
<div align="justify"><strong>Expressões</strong> - Expression </div>
</li>
<li>
<div align="justify"><strong>Passar valores</strong> - Passed as value </div>
</li>
<li>
<div align="justify"><strong>Retornar valores</strong> - Returned as value </div>
</li>
<li>
<div align="justify"><strong>Declarações</strong> - Statement </div>
</li>
</ul>
<p align="justify">Contudo é bom observar alguns aspectos, já que dependendo do uso as funções podem sofrer limitações ou adquirir novos comportamentos. </p>
<p><!--more-->
<p>Observe a função abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod01.png"><img title="COD01" alt="COD01" src="http://blob.vitormeriat.com.br/images/2014/10/cod01.png" /></a></p>
<p align="justify">O mesmo código pode ser escrito atribuindo a função como expressão (retorno) de uma variável. Exatamente como no código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod02.png"><img title="COD02" alt="COD02" src="http://blob.vitormeriat.com.br/images/2014/10/cod02.png" /></a></p>
<p align="justify">OK... O código é o mesmo. Não mudou nada, correto? Não…</p>
<p align="justify">Uma função como instrução sempre é “hospedada” no escopo onde foi definida. Logo, não é desnecessário definir a função antes do uso. Você pode simplesmente comprovar isso no exemplo abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod03.png"><img title="COD03" alt="COD03" src="http://blob.vitormeriat.com.br/images/2014/10/cod03.png" /></a></p>
<p align="justify">Notem que estamos chamando a função antes de sua definição. Dado o seu escopo este código está correto e o seu resultado será o esperado. Agora vamos tentar o mesmo utilizando a função como expressão. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod04.png"><img title="COD04" alt="COD04" src="http://blob.vitormeriat.com.br/images/2014/10/cod04.png" /></a></p>
<p><font color="#ff0000"><strong>Que lindo!!! minhaFuncao() é undefined!!! Throw exception in your face :|</strong></font></p>
<p align="justify">Mesmo que “<em>geralmente</em>” tratem os “<em>tipos</em>” de função como sendo a mesma coisa, na prática são diferentes em relação a sua execução e objetivo. A maior utilidade (ou mais comum) para uma função como expressão é o uso em estruturas de decisão. Podemos fazer isso trabalhando com a palavra reservada <strong>return</strong>. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod05.png"><img title="COD05" alt="COD05" src="http://blob.vitormeriat.com.br/images/2014/10/cod05.png" /></a></p>
<p>Notem quem ele imprime os dois valores, tanto o da função quanto o do IF. Agora basta trocar o valor do retorno para 0 e não vamos mais entrar no IF, ou seja, apenas a primeira sentença será impressa. <strong>[EXEMPLO 6 no código fonte]</strong></p>
<p>Também é possível usar outra abordagem, considerar a função como um Valor. Tendo isso em mente podemos simplesmente atribuir nossa função como uma propriedade de um objeto. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod07.png"><img title="COD07" alt="COD07" src="http://blob.vitormeriat.com.br/images/2014/10/cod07.png" /></a></p>
<p>Outra maneira seria passar nossa função como argumento de outra função:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/cod08.png"><img title="COD08" alt="COD08" src="http://blob.vitormeriat.com.br/images/2014/10/cod08.png" /></a></p>
<p>Sei que não existe nada de inovador nisso, porém sempre é bom ver as coisas sob um novo angulo, e tentar sempre que possível entender aquilo que estamos programando.</p>
<p>&nbsp;</p>
<h4><font color="#808000">Bons estudos e até a próxima pessoal&nbsp; ;)</font></h4>
