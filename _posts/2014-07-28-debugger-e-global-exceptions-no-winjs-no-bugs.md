---
layout: post
title: Debugger e Global exceptions no WinJS – No Bugs
date: 2014-07-28 18:22:14.000000000 -03:00
type: post
published: true
status: publish
categories:
- JavaScript

---
<p>Quando estamos desenvolvendo uma aplicação é comum nos depararmos com diversos erros não tratados ao longo do caminho. Na maioria das linguagens isso é muito fácil de reconhecer através dos erros de compilação. Já no desenvolvimento de aplicações para a Windows Store com JavaScript (WinJS) não é algo tão simples assim…</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/capa2.png"><img title="CAPA" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="CAPA" src="http://blob.vitormeriat.com.br/images/2014/07/capa.png" width="700" height="633" /></a></p>
<p><!--more-->
<p align="justify">Neste post gostaria de abordar sobre exceções globais e modo <strong>debugger</strong>. Durante o desenvolvimento de uma APP acabei me deparando com algumas necessidades e particularidades em relação a construção de aplicações para <strong>Windows Store</strong> com JavaScript (<strong>WinJS</strong>).</p>
<p align="justify">A primeira coisa que me incomodou durante o processo de desenvolver uma APP com <strong>WinJS</strong> é o fato da aplicação ser encerrada, fechada e não exibir nenhuma mensagem referente ao erro. Este é o comportamento padrão quando estamos trabalhando com <strong>WinJS</strong>.</p>
<p align="justify">Em aplicações JavaScript e <strong>HTML</strong> para a Windows Store temos o mesmo comportamento de uma página da Web. Quando ocorre um erro em um objeto <strong>DOM</strong> <u>(Document Object Model)</u> em que é possível o tratamento do erro, é disparado um evento onerror. Os erros de JavaScript, percorrem o caminho da call stack (pilha de chamadas) até caírem em um bloco<strong> try/catch</strong> ou chegarem a camada do objeto Window, gerando assim o evento window.onerror.</p>
<p align="justify">Já o WinJS fornece o evento <strong>WinJS.Application.onerror</strong> onde é concentrado nossa linha de defesa mais básica contra erros gerados pela aplicação. É neste evento que conseguimos capturar todos os erros que chegam ao window.onerror.</p>
<p>&#160;</p>
<h2>Por que somos humanos…</h2>
<p align="justify">Vale lembrar que como seres humanos estamos suscetíveis as falhas. Se seu código nunca falhasse creio que você não estaria lendo este post, correto? Sendo assim é importante conseguir conhecer onde está ocorrendo o erro em nosso código, ainda mais em uma linguagem que não é fortemente tipada e favorece ainda mais a erros como é o caso do JavaScript. </p>
<p align="justify">Embora este encerramento este seja o comportamento padrão, é possível de maneira simples implementar o tratamento de erro global a fim de facilitar o desenvolvimento. </p>
<p>Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod01.png"><img title="COD01" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD01" src="http://blob.vitormeriat.com.br/images/2014/07/cod01.png" width="700" height="342" /></a></p>
<p align="justify">Neste caso estou utilizando a propriedade onerror do objeto Application do WinJS. É aqui que podemos capturar as ações que ocasionaram o erro, tratar as falhas, gravar logs e impedir o fechamento da aplicação. Podemos entender o onerror como um <strong>try/catch</strong> onde toda a aplicação está.</p>
<p align="justify">Como já mencionado aqui, outro ponto importante é que podemos obter detalhes do erro. Utilizando a propriedade detail temos acesso as informações mais específicas. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod02.png"><img title="COD02" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD02" src="http://blob.vitormeriat.com.br/images/2014/07/cod02.png" width="700" height="406" /></a></p>
<p align="justify">Uma dica dada pelo <a href="http://caioproiete.net/pt/" target="_blank">Caio Proiete</a>, e que particularmente tenho utilizado, é a criação de uma popup para exibir os erros e evitar o fechamento da aplicação. O lado prático é a facilidade de visualização da exceção, e poder examinar outros pontos da aplicação durante o erro já que a mesma não foi encerrada.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod03.png"><img title="COD03" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD03" src="http://blob.vitormeriat.com.br/images/2014/07/cod03.png" width="700" height="587" /></a></p>
<p align="justify">Um ponto importante é o retorno. Note que estou utilizando o return true. É este cara que impede o fechamento da aplicação. Neste exemplo, o manipulador de eventos de erro mostra uma mensagem informando ao usuário que ocorreu um erro e qual o erro. O manipulador de eventos retorna true para manter a caixa de diálogo de mensagem aberta até que o usuário a descarte. Retornar true também informa o processo <strong>WWAHost.exe</strong> que o erro foi tratado e que o mesmo pode seguir em execução.</p>
<p align="justify">Ainda sobre a dica de exibição no <strong>MessageDialog</strong>, eu gosto de concatenar a linha e caractere dos erros provenientes do <strong>window.onerror</strong>. É sempre bom examinar o erro mais de perto, até porque muitas vezes as mensagens não são nada significativas. Segue um exemplo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig01.png"><img title="FIG01" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="FIG01" src="http://blob.vitormeriat.com.br/images/2014/07/fig01.png" width="700" height="470" /></a></p>
<p>A mensagem abaixo provêm da seguinte linha de código:</p>
<p><font size="5"><strong>varr x = 4;</strong></font></p>
<p align="justify">Note que a mensagem não é clara. Alguém pode pensar que está faltando apenas o <strong>; </strong>quando na verdade o problema é outro.</p>
<p align="justify">Já para as exceções do Application eu utilizo toda a propriedade stack para ter uma visão do erro. Abaixo, segue um exemplo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig02.png"><img title="FIG02" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="FIG02" src="http://blob.vitormeriat.com.br/images/2014/07/fig02.png" width="700" height="554" /></a></p>
<p>Este erro é gerado pelo seguinte trecho de código:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod05.png"><img title="COD05" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD05" src="http://blob.vitormeriat.com.br/images/2014/07/cod05.png" width="700" height="171" /></a></p>
<p align="justify">Neste código estou chamando uma função processamento que não foi definida, retornando a stack erro que já vimos.</p>
<p>&#160;</p>
<h2>Debugger</h2>
<p align="justify">Sabe aquele código&#160; e mensagens de erro que só fazem sentido durante o desenvolvimento? Pois&#160; é… Outra utilidade que não poderia faltar é capacidade de saber quando a aplicação está em modo <strong>debugger</strong>, o famoso <strong>F5</strong>. Esta é uma parte interessante quando queremos definir que determinado seguimento de código deve ser executado apenas durante o <strong>debugging</strong> da aplicação.&#160; </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig03.png"><img title="FIG03" style="border-top:0;border-right:0;background-image:none;border-bottom:0;float:left;padding-top:0;padding-left:0;margin:0 20px 0 0;border-left:0;display:inline;padding-right:0;"   alt="FIG03" src="http://blob.vitormeriat.com.br/images/2014/07/fig03.png" width="518" align="left" height="238" /></a></p>
<p align="justify">Vale lembrar que <strong>JavaScript</strong> não é compilado, logo sua depuração não é &quot;<u>tradicional</u>&quot;. Quando estamos debuggando o <strong>WinJS</strong> para<strong> Windows Store</strong>, o<strong> Visual Studio</strong> anexa o depurador ao <strong>JavaScript</strong> da aplicação. Mesmo assim, trabalhar com o <strong>debugger</strong> é tão simples como apenas utilizar uma propriedade. É só chamar a propriedade <strong>debuggerEnabled</strong> do objeto <strong>Debug</strong>. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod06.png"><img title="COD06" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD06" src="http://blob.vitormeriat.com.br/images/2014/07/cod06.png" width="700" height="368" /></a></p>
<p>Observe o código executando:</p>
<p><strong>Com debugger ativado</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig05.png"><img title="FIG05" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="FIG05" src="http://blob.vitormeriat.com.br/images/2014/07/fig05.png" width="700" height="324" /></a></p>
<p><strong>Sem debugger</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig04.png"><img title="FIG04" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="FIG04" src="http://blob.vitormeriat.com.br/images/2014/07/fig04.png" width="700" height="330" /></a></p>
<p align="justify">Mesmo não estando acessível via Intellisense, o objeto <strong>Debug</strong> é global e intrínseco ao <strong>JavaScript</strong>. Também podemos utilizar o objeto Debug para escrever dicas e ajudar a monitorar determinados trechos de código ou valores quando em modo debugger.</p>
<pre>var contador = 42;
Debug.write(&quot;O valor em contador é &quot; + contador);</pre>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod07.png"><img title="COD07" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD07" src="http://blob.vitormeriat.com.br/images/2014/07/cod07.png" width="700" height="369" /></a></p>
<p align="justify">No exemplo acima utilizamos as funções <strong><u>write</u></strong> ou <strong><u>writeln</u></strong> para exibir uma string na janela de <strong>Output</strong> do <strong>Visual Studio</strong> apenas quando estivermos em modo <strong>debugger</strong>. Alguém lembra do <strong>alert</strong>…</p>
<p align="justify">Existe muito mais sobre o objeto Debug e como ele pode agregar no desenvolvimento das APPs. Para aprofundar no assunto não deixe de ler as referências no final do post.</p>
<p>&#160;</p>
<p>Outra possibilidade é a combinação destes dois mecanismos para a exibição de mensagens específicas ao usuário final e ao desenvolvedor quando em modo debugger.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/cod08.png"><img title="COD08" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD08" src="http://blob.vitormeriat.com.br/images/2014/07/cod08.png" width="700" height="529" /></a></p>
<p>Como resultado temos as seguintes saídas:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig07.png"><img title="FIG07" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="FIG07" src="http://blob.vitormeriat.com.br/images/2014/07/fig07.png" width="700" height="451" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/fig06.png"><img title="FIG06" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="FIG06" src="http://blob.vitormeriat.com.br/images/2014/07/fig06.png" width="700" height="451" /></a></p>
<p>&#160;</p>
<h2>Referências</h2>
<p><a href="http://msdn.microsoft.com/en-us/library/hh771032.aspx" target="_blank">Start a debugging session for Store Apps in Visual Studio (JavaScript)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/magazine/dn519922.aspx" target="_blank">Build More Efficient Windows Store Apps Using JavaScript: Error Handling</a></p>
<p>&#160;</p>
<h2><font color="#ffc000">Bons estudos e até a próxima pessoal&#160; ;)</font></h2>