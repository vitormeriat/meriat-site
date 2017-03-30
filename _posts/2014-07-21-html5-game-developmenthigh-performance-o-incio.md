---
layout: post
title: HTML5 Game Development–High Performance o início
date: 2014-07-21 16:18:29.000000000 -03:00
type: post
published: true
status: publish
categories:
- Game Development
- HTML5
- JavaScript

---
<p align="justify">Falando em games, existe um elemento que provavelmente seja mais importante que uma boa ideia e gráficos extraordinários: a fluidez e continuidade. Não tem nada pior que um jogo cheio de pausas e lags. Estudos recentes de usabilidade mostram um grande nível de frustração dos usuários em jogos onde há delay aparente. Mesmo um jogo realista e com uma ótima arte vai ser tornar chato e desinteressante se for lento e sem &quot;fluidez&quot;.</p>
<blockquote><p align="justify">Levando isso em consideração é importante ter em mente que mesmo aquela super ideia, arte ou conceito pode se perder se não for bem&#160; implementada. </p>
</blockquote>
<p align="justify">Dito isto, é fundamental para o desenvolvimento de games que você se preocupe com a performance, e já que estamos falando de games em HTML5 e JavaScript, precisamos entender como o JavaScript funciona, o que gera a falta de performance e as possíveis técnicas a serem utilizadas a fim de garantir games mais performáticos e com ótima fluidez.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/07/capa1.png"><img title="capa"  alt="capa" src="http://blob.vitormeriat.com.br/images/2014/07/capa.png" width="700" height="303" /></a></p>
<p align="justify">O que você consegue fazer em 16 milissegundos? Quando falamos de games essa pode ser a diferença entre o sucesso e fracasso. Nesta série sobre High Performance vou abordar alguns dos assuntos fundamentais para construção de games com HTML5 &amp; JavaScript. Como este é um assunto longo, vou dividir os temas para abordar com mais detalhes e testes práticos referentes a performance. </p>
<p align="justify">Agenda deste artigo:</p>
<ul>
<li>
<div align="justify">FPS</div>
</li>
<li>
<div align="justify">Gestão de memória em JavaScript</div>
</li>
<li>
<div align="justify">Garbage Collected (Coleta de lixo)</div>
</li>
<li>
<div align="justify">Memory Leak (Vazamento de memória)</div>
</li>
</ul>
<p><!--more-->
<p align="justify">&#160;</p>
<h2 align="justify">FPS &amp; Frame Rate (taxa de quadros)</h2>
<p align="justify">Vale lembrar que animações são feitas quadro a quadro, ou seja, uma série de imagens que são passadas em uma determinada velocidade a fim de gerar a impressão de movimento, graças a ilusão de óptica conhecida como <strong>Fenômeno Phi</strong>. Enfim, o interessante é ficar claro que animações são feitas quadro a quadro.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/07/animacao.png"><img title="animacao"  alt="animacao" src="http://blob.vitormeriat.com.br/images/2014/07/animacao.png" width="700" height="491" /></a></p>
<p align="justify">Uma boa jogabilidade afirma que o game deve ser capaz de proporcionar ao jogador, ver as animações e conseguir reagir adequadamente. </p>
<p align="justify">A grosso modo <strong>FPS</strong> é a quantidade de vezes em que a tela é desenhada em um segundo. O usual para um jogo é que esta taxa esteja entre <strong>30</strong> e <strong>60 FPS</strong>. Isso significa que se seu game estiver rodando a 60 FPS você terá apenas 16ms para realizar todo a lógica e atualizar a tela.</p>
<p align="justify">O importante aqui é criar seu jogo dentro de uma taxa de quadros constante a fim de gerar esta experiência contínua ao usuário. Até porque sua expectativa é obter as repostas dos comandos de forma imediata, em <strong>“tempo real”</strong>.&#160; Logo, o <u>objetivo</u> é manter o frame rate sempre constante. </p>
<p align="justify">Quando falamos de performance, estamos nos preocupando com a perda de quadros(frames) que ocorre quando temos lags, pausas indevidas e lentidão na execução do jogo. </p>
<p align="justify"><a href="http://jsfiddle.net/vitormeriat/H4GT4/" target="_blank">VEJA ESTE EXEMPLO NO JSFIDDLE.</a></p>
<p align="justify">O exemplo acima deixa claro a diferença entre animações iguais exibidas em taxas de <strong>15</strong>, <strong>30</strong> e <strong>60 FPS</strong>. Perceba que, no primeiro, o movimento existe, mas é pouco fluido e parece deixar rastros. Já a animação no segundo quadro é bem melhor, com uma boa fluidez. O último roda com uma taxa de 60 FPS e, praticamente, não deixa rastros no caminho da figura.</p>
<p align="justify">E o que pode causar essas percas de quadro??? Os próximos tópicos vão nos ajudar a elucidar esta questão…</p>
<p align="justify">&#160;</p>
<h2>Gestão de memória no JavaScript</h2>
<p align="justify">Em JavaScript tudo é objeto. Logo, são os objetos que ocupam memória. Quando um objeto é criado, o JavaScript automaticamente aloca uma quantidade adequada de memória para ele. A partir desse ponto existe um mecanismo responsável por continuamente avaliar se o objeto é válido, e quando não for mais é descartado e seu espaço de memória fica disponível para ser reutilizado.</p>
<p align="justify">Um objeto é considerado válido enquanto houver uma referência a ele (vou explicar isso em detalhes). A partir do momento em que a memória não for mais referenciada fica candidata a ser reaproveitada.</p>
<p align="justify">Considere o jogo abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/07/manyobjects.png"><img title="manyobjects"  alt="manyobjects" src="http://blob.vitormeriat.com.br/images/2014/07/manyobjects.png" width="700" height="451" /></a></p>
<p align="justify">Cada elemento é um objeto que vai efetivamente ocupar espaço de memória. Considere ainda que seu game vai rodar em vários tipos de dispositivos como mobile. </p>
<p align="justify">A gestão de memória é um ponto sensível quando falamos de games com JavaScript porque afetam diretamente a execução do jogo. Como já falado existe um mecanismo próprio para realizar esta gestão, o famoso Garbage Collected. </p>
<p align="justify">&#160;</p>
<h2 align="justify">Garbage Collected</h2>
<p align="justify">O problema mais comum de desempenho é referente a alocação de memória. Isso ocorre em muito dado a falta de preocupação dos desenvolvedores sobre este tema.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/07/heart-polish.png"><img title="heart-polish" style="background-image:none;float:left;padding-top:0;padding-left:0;margin:0 30px 0 0;display:inline;padding-right:0;border-width:0;"   alt="heart-polish" src="http://blob.vitormeriat.com.br/images/2014/07/heart-polish.png" width="220" align="left" height="216" /></a></p>
<p align="justify">JavaScript é um linguagem com Garbage Collected (coleta de lixo). Em ciência da computação, coleta de lixo é uma forma de gerenciamento automático de memória.</p>
<p align="justify">É justamente por isso que muitos programadores acabam tendo a <u>falsa</u> impressão que não é preciso se preocupar com a memória, é só ir criando os objetos conforme a necessidade e outorgar ao <strong>GC</strong> toda responsabilidade. </p>
<p align="justify">O fato é que o <strong>GC</strong> é muito mais importante do que imaginamos. Ele é praticamente o coração do seu game/aplicação. Efetivamente o <strong>GC</strong> é responsável por:</p>
<ul>
<li>
<div align="justify">Alocar memória para novos objetos</div>
</li>
<li>
<div align="justify">Identificar os objetos que devem ser coletados (descartados)</div>
</li>
<li>
<div align="justify">Recuperar a memória dos objetos coletados</div>
</li>
</ul>
<h3 align="justify">A vantagem</h3>
<p align="justify">Libera o programador de ter que lidar com a gestão de memória. Linguagens de baixo nível como <strong>C/C++</strong> tem primitivas como <strong>malloc()</strong> e <strong>free()</strong> para a gestão de memória. Em JavaScript não precisamos alocar e desalocar memória diretamente.</p>
<h3 align="justify">E tem Desvantagem?</h3>
<p align="justify">A primeira coisa a se falar sobre a coleta de lixo é que ela consome recursos computacionais quando acionada. O mais interessante é que o <strong>GC</strong> é acionado pelo JavaScript Runtime que decide quando o mesmo deve fazer a coleta. Neste momento sua execução é prioritária então seu processamento é interrompido durante o tempo necessário para completar a coleta. </p>
<p align="justify">Não há como forçar a coleta de lixo. A coleta pode ocorrer em qualquer momento da execução do seu código.</p>
<p align="justify">&#160;</p>
<h2 align="justify">Então a culpa é do GC?</h2>
<p align="justify">Muitos jogos em HTML5 &amp; Javascript, tem como grande obstáculo para uma experiência contínua e suave as famosas pausas geradas pela coleta de lixo <strong>(GC)</strong>. Esse processo pode ser demorado especialmente em um celular, o que pode gerar a perda de frames.</p>
<p align="justify">Imagine que seu jogo está rodando a <strong>60 FPS</strong>, o que te dá 16 milissegundos para toda a lógica e renderização de um quadro. Mesmo usando uma taxa menor como <strong>30 FPS</strong>, você terá 32ms para fazer tudo. Dependendo do navegador e do número de objetos que você esteja usando, o processo de coleta de lixo pode demorar de <strong>20ms</strong> a <strong>200ms</strong>. Quanto maior a limpeza maior será o tempo, ou seja, o <strong>GC</strong> vai gastar mais tempo na coleta do que o disponível para um frame, o que resulta em uma pausa visível, ou em situações ainda piores, uma experiência de jogo constantemente falha.</p>
<p align="justify">Respondendo a pergunta: NÃO!!! A culpa não é só do <strong>GC</strong>… Vamos ver que para games mais performáticos o ideal é você mesmo <strong><u>“cuidar”</u></strong> do gerenciamento de memória para evitar pagar um imposto muito alto com o <strong>GC</strong>. </p>
<p align="justify">&#160;</p>
<h2 align="justify">JavaScript internals</h2>
<p align="justify">Em uma linguagem com coleta de lixo, todo objeto que não for referenciado será coletado. Sendo assim enquanto o objeto estiver referenciado o JavaScript runtime vai deixa-lo intocado.</p>
<blockquote><p align="justify">Em JavaScript o gerenciamento de memória é um conceito de acessibilidade.</p>
</blockquote>
<p align="justify">Levando em consideração o que já falamos sobre o escopo, se definirmos objetos no escopo global, enquanto deixarmos o browser aberto estes objetos estão referenciados. Objetos do escopo global só são destruídos quando se atualiza ou fecha o browser. Observere a imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/memory-organization.png"><img title="memory organization"  alt="memory organization" src="http://blob.vitormeriat.com.br/images/2014/07/memory-organization.png" width="700" height="330" /></a></p>
<p align="justify">Ela representa o esquema da memória baseada no encadeamento dos objetos. A cadeia de referência dos objetos se inicia com o <strong>Window Object</strong> que é o <strong>escopo global</strong>. O <strong>GC</strong> vai iniciar dai a busca de todos os objetos que não estiverem nessa raiz, como é o caso dos objetos 10 e 11.</p>
<p align="justify">Mesmo não podendo forçar a coleta de lixo, você pode forçar uma variável a ser coletada quando o <strong>GC </strong>for executado. É só excluir as referências do mesmo. Abaixo segue a representação de uma coleta. A figura abaixo representa uma cadeia de memória.</p>
<h2 align="justify"></h2>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/lcm1.png"><img title="LCM1"  alt="LCM1" src="http://blob.vitormeriat.com.br/images/2014/07/lcm1.png" width="700" height="508" /></a></p>
<p align="justify">Para que um objeto seja candidato a coleta de lixo é necessário não possuir referências com o Root Node. Na figura abaixo estamos destruindo a referência de um objeto root. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/lcm2.png"><img title="LCM2"  alt="LCM2" src="http://blob.vitormeriat.com.br/images/2014/07/lcm2.png" width="700" height="508" /></a></p>
<p align="justify">Com isso, todos os objetos que estiverem abaixo na herança serão também candidatos a coleta. No exemplo abaixo ao destruir a referência do objeto pai, os filhos se tornam candidatos com exceção do último objeto a direita que tem uma referência direta ao root.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/lcm3.png"><img title="LCM3"  alt="LCM3" src="http://blob.vitormeriat.com.br/images/2014/07/lcm3.png" width="700" height="508" /></a></p>
<p align="justify">Após a coleta de lixo os objetos restantes serão apenas os que tinham referência ao root. Neste momento teremos a liberação da memória.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/lcm4.png"><img title="LCM4"  alt="LCM4" src="http://blob.vitormeriat.com.br/images/2014/07/lcm4.png" width="700" height="508" /></a></p>
<h2 align="justify">Vazamento de memória</h2>
<p align="justify">Mesmo assim ainda é possível termos problemas em relação a gestão de memória. Estes são conhecidos como <strong>vazamento de memória. </strong>Vazamento de memória ocorre quando uma porção de memória, alocada para uma determinada operação, não é liberada mesmo não sendo mais necessária. </p>
<p align="justify">Existem muitas maneiras em que você pode reter objetos indesejados na memória. É bem verdade que os browsers tem investido e melhorado no tratamento de coleta de lixo, porém este ainda vai ser um ponto em que vamos ter de nos preocupar quando falamos de games e desempenho.</p>
<p>&#160;</p>
<p align="justify">Esta foi a primeira parte do artigo, apenas com a parte “teórica” a fim de equalizar o conhecimento. Nas próximas partes vou traduzir todo este conteúdo em código e apresentar algumas técnicas para evitar os vazamentos de memória bem como diminuir o trabalho do GC, focando na programação defensiva em relação a&#160; performance.</p>
<p>&#160;</p>
<h2>Bons estudos e até a próxima pessoal&#160; ;)</h2>
