---
layout: post
title: JavaScript Development Insights–Escopo e Criação de Classes
date: 2014-07-02 13:32:00.000000000 -03:00
type: post
published: true
status: publish
categories:
- JavaScript

---
<p align="justify">Antes de continuar a série “<strong>HTML5 Game Development</strong>” vou falar de alguns temas chave quando estamos escrevendo código para games e <strong>APPs</strong> com <strong>JavaScript</strong>. Antes de construir uma casa temos de fazer o fundamento, pelo menos se queremos algo com qualidade e durabilidade. Sendo assim é fundamental dominar alguns pontos da linguagem. <img class="wlEmoticon wlEmoticon-winkingsmile" style="border-style:none;" alt="Smiley piscando" src="http://blob.vitormeriat.com.br/images/2014/07/wlemoticon-winkingsmile.png" /> </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/capa.png"><img title="capa"  alt="capa" src="http://blob.vitormeriat.com.br/images/2014/07/capa.png" width="700" height="384" /></a></p>
<p align="justify">O código acima “<u>parece</u>” totalmente despretensioso e simples porém as duas linhas acima <strong>NÃO</strong> tem o mesmo efeito. O <strong>Script A</strong> e o <strong>Script B</strong> escondem uma diferença fundamental para o tema em questão. O simples fato de utilizar ou não a palavra chave <strong><u>var</u></strong>, pode alterar drasticamente o sentido e função do código.</p>
<p><!--more-->
<p align="justify">JavaScript é uma linguagem orientada a objetos muito flexível quando se trata de sintaxe, mesmos assim é importante lembrar que não há classes em JavaScript. Com um conhecimento melhor da linguagem podemos simular classes, mas, em geral, JavaScript é <strong>class-less language</strong>. Tudo em JavaScript é um objeto. E quando se trata de <strong>herança</strong>, os objetos herdam de objetos e não classes a partir de classes. </p>
<blockquote><p align="justify">Para facilitar o estudo, você pode baixar todos os scripts utilizados neste post <a href="http://1drv.ms/1qQnHrd" target="_blank">clicando aqui!!!</a></p>
</blockquote>
<p align="justify">&#160;</p>
<h2 align="justify">Revisando</h2>
<p align="justify">Como falei anteriormente, podemos dizer que existem duas formas para se criar um objeto: Usando <strong>object literal</strong> ou <strong>constructor function</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo0.png"><img title="codigo0"  alt="codigo0" src="http://blob.vitormeriat.com.br/images/2014/07/codigo0.png" width="700" height="746" /></a></p>
<p align="justify">Embora os métodos dos objetos sejam iguais, eles são diferentes (???). Um <strong>object literal</strong> cria um objeto que pode ser imediatamente utilizado sem primeiro ser &quot;<strong>instanciado</strong>&quot; com a palavra-chave <strong>new</strong>. Neste ponto um object literal também é conhecido como <strong>static</strong>. O porém da história e que objetos statics não podem implementar herança e encapsulamento no JavaScript.</p>
<p align="justify">Já utilizado a <strong>function constructor</strong> podemos implementar orientação a objetos, simulando o comportamento de uma classe.</p>
<p align="justify"><em>UPDATE: Para quem já leu minha referência ao object&#160; literal como singleton, estou atualizando para static. Correção sugerida pelo Júlio Ködel, já que por definição em Singleton podemos implementar herança.</em></p>
<p>&#160;</p>
<h2>Escopo </h2>
<p align="justify">O primeiro passo é entender sobre o <strong>Escopo</strong>. Em JavaScript escopo é o contexto em que uma entidade, seja ela variável, função ou objeto é acessível ou visível a outras entidades.</p>
<p align="justify">Temos alguns tipos de escopo porém vou abordar de uma maneira simplificada apenas tratando tudo como Escopo Global ou Escopo Local.</p>
<h3>Escopo Global</h3>
<p align="justify">O Escopo global é o mais alto nível de contexto e é definido pelo <a href="http://www.w3schools.com/jsref/obj_window.asp" target="_blank">Window Object</a>. Tudo se inicia no escopo global e qualquer entidade definida no escopo global pode ser acessada em qualquer parte do código.</p>
<h3>Escopo Local</h3>
<p align="justify">O escopo local é toda entidade definida fora do contexto global <em>(Sério???)</em>. Uma entidade de escopo corrente ou local, só é acessível dentro de seu próprio escopo e não pode ser acessado em&#160; outro escopo, incluindo o escopo global. Vamos a um exemplo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo01.png"><img title="codigo01"  alt="codigo01" src="http://blob.vitormeriat.com.br/images/2014/07/codigo01.png" width="700" height="493" /></a></p>
<p align="justify">No código acima criamos uma variável e uma função de escopo global. Já em nossa função estamos criando uma variável de escopo local. Ao executar nossa função de escopo global conseguimos exibir os resultado corretamente por que é possível acessar o valor da variável global e local. Agora se tentarmos exibir os valores das duas variáveis no contexto global veremos que o resultado para a variável local será <strong>ReferenceError: local is not defined</strong>. </p>
<p align="justify">O <strong>escopo atual </strong>pode ser acessado usando o objeto <strong><u>this</u></strong>. Este objeto aponta para o escopo que está sendo utilizado no momento. Se estivermos no <strong>escopo global</strong> o objeto <strong>this</strong> vai apontar para o <strong>Window object</strong>. Já se estivermos em um <strong>escopo local</strong>, <strong>this</strong> vai apontar para o <strong>Current</strong> <strong>Object</strong>. Vamos ao exemplo abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo02.png"><img title="codigo02"  alt="codigo02" src="http://blob.vitormeriat.com.br/images/2014/07/codigo02.png" width="700" height="413" /></a></p>
<p align="justify">O escopo dentro de um objeto ou função é algo um pouco mais complexo, pois depende da definição do mesmo. Vamos voltar a introdução deste post…</p>
<p align="justify">Para declarar a entidade você pode usar as palavras chave <strong><u>var</u></strong> ou <strong><u>this</u></strong>. Quando criamos uma entidade usando o <strong>var</strong>, ela se torna uma entidade de <strong>escopo local</strong>. Já entidades declaradas utilizando o <strong>this</strong> se tornam uma propriedade do objeto no <strong>escopo atual</strong>. Isso significa que a entidade pode ser acessada fora do <strong>escopo corrente. </strong>Vamos ao exemplo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo03.png"><img title="codigo03"  alt="codigo03" src="http://blob.vitormeriat.com.br/images/2014/07/codigo03.png" width="700" height="630" /></a></p>
<p align="justify">Neste exemplo temos uma função Triangulo que exibe a altura do mesmo baseado na sua área. Note que <strong>_altura</strong> é declarado utilizando <strong>var</strong>. Para as demais propriedades estamos utilizando <strong>this</strong>. Neste caso ao acessar diretamente nossas entidades, vemos que a declaração <strong>this</strong> expos as mesmas fora do <strong>escopo corrente</strong>. Já a declaração de <strong>_altura</strong> utilizando <strong>var</strong> só é acessível dentro do <strong>escopo local</strong>.</p>
<p align="justify">É fundamental entender o funcionamento do escopo para a correta implementação da orientação a objeto e criação de entidades públicas e privadas. </p>
<p>&#160;</p>
<h2>Criando Classes!?!</h2>
<p align="justify">Como Já falei anteriormente JavaScript <strong>não é</strong> uma linguagem baseada em classes e sim <strong>orientada a protótipos</strong>. Não temos classes em JavaScript porém com o conhecimento que já temos sobre o funcionamento do escopo de uma entidade e criação dos objetos, é possível discutir em como implementar classes no JavaScript.</p>
<p align="justify">Já vimos que o dependendo da declaração do objeto suas entidades podem estar no escopo global (públicas e acessíveis fora do objeto), ou local (privadas e acessíveis apenas no objeto).&#160; Vejamos o exemplo abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo04.png"><img title="codigo04"  alt="codigo04" src="http://blob.vitormeriat.com.br/images/2014/07/codigo04.png" width="700" height="837" /></a></p>
<p align="justify">Estamos definindo um polígono qualquer e queremos saber sua área e perímetro. Como implementamos nossa função <strong>exibirArea</strong> apenas no escopo local do objeto, ao tentar chamar no escopo global obtemos um erro. Já a função <strong>exibirPerimetro</strong> é acessível no escopo global como uma simples propriedade do objeto <strong>Poligono</strong>.</p>
<p align="justify">Funções com construtor seguem o mesmo princípio, só que neste caso os parâmetros são de escopo local. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo05.png"><img title="codigo05"  alt="codigo05" src="http://blob.vitormeriat.com.br/images/2014/07/codigo05.png" width="700" height="578" /></a></p>
<p align="justify">Vale fazer uma parênteses neste ponto para lembrar que em JavaScript quando não informamos o valor de um parâmetro para um função com construtor, ele vai por padrão atribuir um “<strong>value of undefined</strong>”. Uma forma de tratar isso é definir em sua função um retorno padrão caso o parâmetro não seja informado.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo06.png"><img title="codigo06"  alt="codigo06" src="http://blob.vitormeriat.com.br/images/2014/07/codigo06.png" width="700" height="478" /></a></p>
<p align="justify">Ao contrário das linguagens baseadas em classes, em JavaScript não temos sobrecarga (<strong>overloading</strong>) de funções. Não adianta alterar a quantidade de parâmetros. Se você criar duas entidades com o mesmo nome no mesmo escopo a última entidade vai sobrescrever a primeira. Vamos tirar a prova:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo07.png"><img title="codigo07"  alt="codigo07" src="http://blob.vitormeriat.com.br/images/2014/07/codigo07.png" width="700" height="621" /></a></p>
<p align="justify">Por outro lado é possível ter uma função com o número variável de argumentos.&#160; Como exemplo de funções com argumentos múltiplos podemos citar <strong>Math.max()</strong> e <strong>Math.min()</strong>. Como pode isso??? Em JavaScript podemos utilizar o objeto <strong>arguments</strong> que é basicamente uma matriz de todos os argumentos passados para a função.</p>
<p align="justify">Notem que eu o objeto arguments é &quot;<u>basicamente</u>&quot; uma matriz, porém existem algumas considerações necessárias que pretendo decorrer no próximo post. Independente disto este é um poderoso recurso para resolver nosso problema.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo08.png"><img title="codigo08"  alt="codigo08" src="http://blob.vitormeriat.com.br/images/2014/07/codigo08.png" width="700" height="660" /></a></p>
<p>&#160;</p>
<h2>Adicionando novas propriedades</h2>
<p align="justify">Neste ponto vamos dizer que já sabemos como criar nossa função com construtor derivando de um objeto. Agora imagina que em dado ponto é necessário adicionar uma nova &quot;<u>propriedade</u>&quot; ao objeto. Em JavaScript temos a facilidade de realizar alterações nos objetos em <strong>tempo de execução</strong>. Sendo assim novas entidades adicionadas serão entendidas como propriedades do objeto, sendo acessadas como entidades declaradas no objeto utilizando a palavra-chave this. Vejamos o exemplo abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo09.png"><img title="codigo09"  alt="codigo09" src="http://blob.vitormeriat.com.br/images/2014/07/codigo09.png" width="700" height="498" /></a></p>
<p align="justify">Agora existe um porém. Tenha em mente que ao criar novas entidades utilizando este mecanismo, elas não serão refletidas nos outros objetos que derivam da mesma função. Vamos a prova:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/07/codigo10.png"><img title="codigo10"  alt="codigo10" src="http://blob.vitormeriat.com.br/images/2014/07/codigo10.png" width="700" height="628" /></a></p>
<p align="justify">A melhor maneira para tratar isso é com a utilização do Prototype como escrevi <a href="http://vitormeriat.com.br/2014/06/23/html5-game-developmentprincpios-da-programao-javascript-com-prototype/" target="_blank">neste post!!!</a></p>
<p>&#160;</p>
<h2>Conclusão</h2>
<p align="justify">Como vimos é possível imitar o comportamento das classes usando funções com construtor. Sendo assim podemos usar os princípios da Orientação como encapsulamento para criar entidades públicas e privadas.</p>
<p align="justify">&#160;</p>
<h2>Bons estudos e até a próxima pessoal&#160; ;)</h2>
