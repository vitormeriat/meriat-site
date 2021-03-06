---
layout: post
title: HTML5 Game Development–Princípios da programação JavaScript com Prototype
date: 2014-06-23
categories:
- Game Development
- HTML5
- JavaScript
---

Olá pessoal. Saindo um pouco do habitual hoje vou falar sobre desenvolvimento de games com <strong>JavaScript</strong> e <strong>HTML5</strong>. Minha ideia é abordar alguns assuntos que&#160; acho pertinentes sobre o desenvolvimento de games com HTML5 e JavaScript. Estou levando em conta que você já conhece pelo menos o básico de HTML5 e JavaScript portanto vou logo para o lado mais denso da brincadeira.

Entre os vários assuntos associados a este tema vou iniciar esta mini-série falando sobre este recurso poderoso que é o <strong>Prototype</strong>. Um dos motivos que me levaram a isso se dá ao fato deste ser o meu primeiro objeto de estudo quando decidi me aprofundar no JavaScript. Parte disso se da pelo fato da grande utilização deste padrão. Já quando falamos em desenvolver games com JavaScript, geralmente vamos ter um grande número de objetos, métodos e arquivos scripts. Manter esta estrutura de forma organizada e coesa é na maioria dos casos um desafio.

<p align="center"><img title="capa1" src="http://blob.vitormeriat.com.br/images/2014/06/capa11.png" /></p>

<p align="justify">Sendo assim é importante entender como otimizar a criação dos objetos de certa forma que seja possível diminuir a quantidade de código e risco nas alterações futuras.</p>
<p><!--more-->
<p>Para facilitar, vou disponibilizar o código fonte dos exemplos que pode ser <a href="http://1drv.ms/1j7kiil" target="_blank">baixado aqui!!!</a>. </p>
<p align="justify">Este é um assunto que causa certa estranheza para os iniciantes em <strong>JavaScript</strong>, principalmente se já desenvolvem em alguma linguagem <strong>Orientada a Objetos</strong>. O primeiro passo é lembrar que o JavaScript <strong>não é</strong> uma linguagem baseada em classes e sim <strong>orientada a protótipos</strong>. Isso significa que (de maneira resumida) o JavaScript não usa classes para definir objetos e sim objetos para criar outros objetos. </p>

Ficou um pouco confuso? Não tem problema, vou tentar esclarecer isso no decorrer deste post.

## Iniciando a conversa

As linguagens como <strong>C#</strong>, <strong>C++</strong> e <strong>Java</strong> são baseadas em classes. Como resultado desta abordagem tradicional, para criarmos um objeto é necessário primeiro criar uma classe que defina as propriedades e métodos deste objeto.&#160; Neste contexto a classe é utilizada como um modelo para ser definir e conhecer como criar o referido objeto.

Uma vez que a classe foi criada é só a utilizar para a se obter novas instâncias. Criar uma instância é uma maneira elegante de se dizer que você criou um objeto da classe utilizando o famoso <strong>NEW</strong>.

No JavaScript não temos classes, apenas objetos e os tipos primitivos de dados. Isso justamente por que o JavaScript utiliza o modelo <a href="http://en.wikipedia.org/wiki/Prototype-based_programming" target="_blank">Prototype-based programming</a>. Para simplificar vamos dizer que tudo em JavaScript é um objeto… tudo, até mesmo funções!!! 

<h2>Então como criar meus objetos?</h2>
<p align="justify">Em JavaScript temos<strong> “basicamente”</strong> duas maneiras de se criar objetos: Usando um <strong><u>object literal</u></strong> ou <strong><u>constructor function</u></strong>.</p>

<p align="justify">Já estou preparando um post específico sobre este assunto então vou apenas ilustrar estas duas maneiras de criar objetos como no código abaixo:</p>

<p><a href="http://blob.vitormeriat.com.br/images/2014/06/003.png"><img title="003"  alt="003" src="http://blob.vitormeriat.com.br/images/2014/06/003.png" width="700" height="768" /></a></p>

<p align="justify">Existe uma série de assuntos a se considerar sobre estas abordagens. No entanto vamos abordar a criação de objetos com função de construtor, que é o mais utilizado por ser <strong>”essencialmente”</strong> uma classe.</p>

<p align="justify">Observe o código abaixo:</p>

<p align="center"><img title="04"  alt="04" src="http://blob.vitormeriat.com.br/images/2014/06/041.png" /></p>

<p align="justify">Note que primeiro criamos nossa “função construtora de objeto”. Com ela definida podemos utilizar o bom e velho <strong>NEW</strong> para obter um novo objeto que é uma cópia do objeto <strong>“pai”</strong>, trazendo suas propriedades e métodos. </p>
<p align="justify">Porém reparem que estou utilizando uma função <strong><u>toString()</u></strong> que não está definido no objeto inicial. Isso porque qualquer objeto em JavaScript pode utilizar esta função para retornar uma string de si mesmo. Agora como isso é possível se JavaScript <u>não é</u> uma linguagem orientada a classe? <u>A resposta é: Através do <strong>PROTOTYPE</strong>!!!</u></p>
<p align="justify"><u></u></p>
<p align="justify"><u></u></p>
<h2>O que é esse tal de PROTOTYPE?</h2>
<p align="justify">Todo objeto em JavaScript possui uma propriedade implícita chamada [Prototype]. Esta propriedade nada mais é que um ponteiro que guarda a referência ao objeto que vai ser executado via delegation caso a propriedade ou método não seja encontrada no objeto corrente.</p>
<p align="justify">Sendo assim quando você pede a um objeto determinado “recurso”, o JavaScript vai primeiro procurar no objeto corrente. Caso não encontre o próximo passo é olhar para a propriedade [Prototype] e procurar o “recurso” no objeto referenciado. Se não encontrar no objeto referenciado ele repete o mesmo ciclo até que a propriedade [Prototype] seja nulo.</p>
<p align="justify">Isso é chamado de prototype chain (cadeia de protótipos). Um prototype pode ser acessado utilizando o <strong>Object.isPrototypeOf()</strong>. Outra forma muito utilizada é acessar a propriedade [Prototype] com <strong>__proto__</strong>.</p>
<p align="justify">Vamos voltar ao exemplo do objeto Pessoa utilizando a função toString(). Neste caso o JavaScript procura a função toString() no objeto Pessoa e não acha. Vai para a propriedade Prototype que aponta para outro objeto. Neste objeto ele realiza o mesmo processo procurando a função e não acha, então, vai novamente para propriedade Prototype que aponta para outro objeto realiza a busca, acha a função e a executa.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/005.png"><img title="005"  alt="005" src="http://blob.vitormeriat.com.br/images/2014/06/005.png" width="700" height="140" /></a></p>
<p align="justify">É simples validar isso apenas utilizando a função <strong>hasOwnProperty()</strong> que retorna um true ou false indicando se o objeto tem ou não a propriedade indicada.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/006.png"><img title="006"  alt="006" src="http://blob.vitormeriat.com.br/images/2014/06/006.png" width="700" height="461" /></a></p>
<p>&#160;</p>
<h2>E a aplicação prática?</h2>
<p align="justify">Já vimos que de maneira simples podemos pensar no Prototype como uma maneira de criar heranças frouxas onde é possível adicionar novas características evitando uma declaração global.</p>
<p align="justify">A ideia neste exemplo é criar uma função para calcular o XP de um usuário do game. Baseado no nível e na pontuação temos os pontos de experiência. Pois bem, o mais comum é trabalhar essa estrutura de maneira simples como segue o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/007.png"><img title="007"  alt="007" src="http://blob.vitormeriat.com.br/images/2014/06/007.png" width="700" height="692" /></a></p>
<p>Sem pensar muito é possível encontrar algumas falhas nessa abordagem</p>
<ul>
<li>Fica complexo manter a medida que a função cresce </li>
<li>Fica mais difícil debugar </li>
<li>Torna os testes mais difíceis </li>
<li>Torna as alterações mais complexas e com mais tendência a falha </li>
</ul>
<p align="justify">Não quero me deter nisso já que pretendo retomar este assunto em outro post. Agora vamos pensar neste mesmo código sobre a <u>perspectiva do Prototype</u>. Abaixo temos a criação do nosso objeto sem nenhuma implementação. Logo abaixo temos a referência ao nosso <strong>Script1</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/009.png"><img title="009"  alt="009" src="http://blob.vitormeriat.com.br/images/2014/06/009.png" width="700" height="274" /></a></p>
<p align="justify">O <strong>Script1</strong> é responsável pela implementação inicial. Neste caso estou fazendo a mesma lógica do código inicial.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/008.png"><img title="008"  alt="008" src="http://blob.vitormeriat.com.br/images/2014/06/008.png" width="700" height="722" /></a></p>
<p align="justify">Agora voltamos ao que falei no início. Dificilmente você vai construir sua aplicação ou game utilizando um só script. Então vamos continuar nossa implementação… agora surgiu a necessidade de em dado momento alterar o calculo do <strong>XP</strong>. </p>
<p align="justify">De maneira muito simples apenas chamamos nosso <strong><u>objeto.prototype</u></strong> e a propriedade a ser alterada (neste caso o método <strong>calcularExperience</strong>), podemos realizar a alteração desejada, refletindo apenas no momento da necessidade. O resto ficou inalterado e pode ser utilizado normalmente. Vamos ao nosso <strong>Script2</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/010.png"><img title="010"  alt="010" src="http://blob.vitormeriat.com.br/images/2014/06/010.png" width="700" height="526" /></a></p>
<p align="justify">Como é possível ver no output continuamos recebendo o mesmo valor para os cálculos anteriores e um novo resultado derivado da alteração que realizamos por último.</p>
<p align="justify">&#160;</p>
<h2 align="justify">Várias maneiras de implementação</h2>
<p align="justify">Outra coisa bacana é como podemos trabalhar o protótipos dentro do JavaScript. Vamos observar o exemplo abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/06/011.png"><img title="011"  alt="011" src="http://blob.vitormeriat.com.br/images/2014/06/011.png" width="700" height="758" /></a></p>
<p align="justify">Primeiro criamos um objeto <strong>Monstro</strong> com apenas uma propriedade chamada <strong>vidas</strong>. Logo depois crio um objeto <strong>monstro1</strong> usando Monstro como protótipo. Agora <strong>monstro1</strong> também tem a propriedade <strong>vidas</strong>. </p>
<p align="justify">Já em <strong>monstro2</strong> estamos utilizando o <strong>Object.create()</strong>. Note que de maneira simples estamos setando o número de vidas e criando uma nova propriedade chamada <strong>força</strong>.</p>
<p align="justify">Em <strong>monstro3</strong> utilizamos o próprio <strong>Object.create()</strong> para a criação de propriedade extras. Neste caso criando a propriedade poder.</p>
<p align="justify">Podemos criar a mesma estrutura sem utilizar o Object.create(). </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/06/012.png"><img title="012"  alt="012" src="http://blob.vitormeriat.com.br/images/2014/06/012.png" width="700" height="748" /></a></p>
<p align="justify">Neste caso estamos criando nosso protótipo <strong>(personagemPrototype) </strong>e logo após uma função <strong>(personagem)</strong>&#160; para forçar a <strong>“inicialização”</strong> para as novas chamadas ao protótipo. Não é a maneira mais simples mas traz o mesmo resultado.</p>
<p align="justify">O que é possível perceber nestes exemplos é a facilidade na criação e orientação de novos objetos utilizando prototipagem sem o compromisso de um único <strong>“jeito”</strong> para a implementação. Vale anotar que dependendo da sua abordagem o entendimento o entendimento futuro pode se tornar bastante complexo.&#160;&#160; </p>
<p align="justify">&#160;</p>
<p align="justify">O que pode ter passado desapercebido, é que através do prototype podemos criar novas características para as &quot;classes&quot; já definidas pelo próprio JavaScript. Como exemplo, vamos colocar um novo método na &quot;classe&quot; String do JavaScript.</p>
<p align="justify">Apenas para fins didáticos vamos incluir a função <strong>parseInt()</strong> a fim de converter uma String em Inteiro de uma maneira simplificada utilizando prototype:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/001.png"><img title="001"  alt="001" src="http://blob.vitormeriat.com.br/images/2014/06/001.png" width="700" height="410" /></a></p>
<p align="justify">Agora podemos chamar o parseInt() direto de uma String em vez de chamar a função e passar uma string a ser convertida [<strong>parseInt(&quot;950&quot;);</strong>]</p>
<p align="justify">&#160;</p>
<h2 align="justify">Conclusão</h2>
<p align="justify">Como vimos o&#160; prototype nos permite adicionar características e comportamentos para as <strong>&quot;classes&quot;</strong>, após sua definição, sendo assim podemos reutilizar toda a definição de uma<strong> “classe”</strong> em outra.</p>
<p>&#160;</p>
<h2><font color="#f79646">Bons estudos e até a próxima pessoal&#160; ;)</font></h2>
