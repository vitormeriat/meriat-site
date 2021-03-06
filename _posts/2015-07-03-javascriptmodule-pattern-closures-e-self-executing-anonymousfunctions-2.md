---
layout: post
title: JavaScript–Module Pattern, Closures e Self-Executing AnonymousFunctions
date: 2015-07-03
categories:
  - Desing Patterns
  - JavaScript
image: "http://blob.vitormeriat.com.br/images/2015/07/capaJSMP.png"
---

<div align="center" class="image-content" style="background-color: #D5D5D1;">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/capaJSMP.png">
</div>

Quem trabalha com JavaScript conhece bem a problemática em relação ao escopo e criação de variáveis. Uma das grandes preocupações dos desenvolvedores JavaScript é evitar o uso indiscriminado de variáveis globais, o que pode levar a erros terríveis e de difícil rastreabilidade.

Como <strong>"AINDA"</strong> não temos uma sintaxe de módulos do próprio JavaScript, o padrão é a utilização de módulos para garantir um escopo de variáveis fechado, além de simular a privacidade de atributos e funções.
Este pattern pode envolver uma combinação de técnicas como closures e funções auto-executáveis. A sintaxe é bastante característica e pode ser encontrada facilmente em diversas bibliotecas, como no caso do <a href="https://dev.windows.com/en-us/develop/winjs" target="_blank">WinJS</a>.

<pre><code class="javascript" style="font-size: 1.6em !important;">
(function () {
    // Seu código aqui!!!
})();

</code></pre>

## Clousures

Uma clousure define um determinado escopo de execução. Vamos ao exemplo:

<pre><code class="javascript">
function init() {
    console.log('Escopo Global');
}

(function () {
    function init() {
    console.log('Escopo Global');
    }

    init(); // Escopo Local

    window.init(); // Escopo Global
}());
</code></pre>

<div align="center" class="image-content" style="background-color: #B09D8B;">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/fig1.png">
</div>

<p align="justify">Notem que aqui eu declarei 2 funções com o mesmo nome: init. Porém cada uma em um escopo. Uma está lá no escopo global window, e a outra é local dentro da clousure. Por existirem em escopos diferentes uma função não interfere na outra e pode coexistir em um mesmo código.</p>

<p align="justify">Tudo o que for declarado no escopo window é acessível de qualquer lugar, já que o escopo window é o root. O que for declarado dentro da clousure só é acessível de dentro dela, e se não for usado nenhum <strong>padrão de revelação</strong> só é acessível lá.</p>

<p align="justify">Se olharmos para o resultado do código veremos que primeiro foi executado a função do <strong>Escopo Local</strong> e depois a do <strong>Escopo Global</strong> sem erros.</p>
<p align="justify">Agora vamos ao código abaixo:</p>

<pre><code class="javascript">
(function () {
    var namespaceUm = {
    init: function () {
    console.log('Namespace Um');
    }
    };

    // NamespaceUm
    namespaceUm.init();
}());
// ReferenceError: namespaceUm is not defined
namespaceUm.init();
</code></pre>

<div align="center" class="image-content" style="background-color: #B09D8B;">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/fig2.png">
</div>

<p align="justify">Aqui vemos uma função declarada dentro de uma clousure e comprovamos como a mesma é inacessível fora deste contexto. No primeiro momento é executado a função que exibe o valor correto, e no segundo momento tento executar a função de fora do escopo da clousure o que gera o erro de objetjo undefined.</p>

<p align="justify">Isso é importante para entendermos como podemos criar <strong>módulos independentes</strong> e simulando a visibilidade privada tão difundida na OOP.</p>

## Módulos e Namespaces

<p align="justify">No JavaScript tudo é objeto, isso inclui as funções. Sendo assim podemos atribuir uma função a uma variável. Quando pensamos na criação de um módulo ou namespace (você pode encontrar estes dois termos na literatura padrão), nós simplesmente pulamos esta atribuição, e de cara, já realizamos a execução da função assim que ela for definida.</p>

<p align="justify">Esta sintaxe é chamada de <strong>função anônima</strong> (<strong><em>Anonymous Functions</em></strong>). O porém da história é que não podemos executar uma função anônima, já que esta não é uma sintaxe válida. Sendo assim para realizar a<strong> auto-execução</strong> (<strong><em>Self Executing</em></strong>) da função, o correto é englobar tudo dentro de parênteses.</p>

<pre><code class="javascript" style="font-size: 1.6em !important;">

// Declarando uma função anônima que se auto executa
(function () {

})();

</code></pre>

<p>Como o JavaScript ainda não possui módulos nativamente (embora isso provavelmente entre na versão <a href="http://wiki.ecmascript.org/doku.php?id=harmony:specification_drafts" target="_blank">ECMAScript 6</a>, também chamada de Harmony), este pattern é muito utilizado para simular a criação de módulos.</p>


> O que é uma função anônima? Fácil. É uma função sem um nome. NEXT!


<p align="justify">Isso só é possível por causa do escopo local de variáveis de uma função, que permite isolar tudo o que é feito dentro deste tipo de função. Como variáveis definidas em uma função tem escopo local, podemos usar o <strong>Module Pattern</strong> para simular privacidade de atributos.</p>

<p align="justify">E por que isso é importante? Vamos a um exemplo prático. Observe o código abaixo:</p>

<pre><code class="javascript">
var Pontos = {
    contador: 0,
    incrementar: function (){
    return this.contador += 1;
    },
    imprimir: function (){
    console.log(this.contador);
    }
};

Pontos.incrementar();
Pontos.incrementar();
Pontos.incrementar();
Pontos.imprimir(); // returns 3
Pontos.contador = 500;
Pontos.imprimir(); // returns 500

</code></pre>

<div align="center" class="image-content" style="background-color: #B09D8B;">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/fig3.png">
</div>

<p align="justify">Temos uma função <strong>Pontos</strong> com um atributo contador responsável por guardar um valor que é importante em nosso regra. O ideal é que este valor só seja alterado pela utilização do método <strong>incrementar</strong>, porém como vemos no exemplo este tipo de implementação torna muito fácil a quebra do <strong>encapsulamento</strong>, dando total acesso a manipulação do atributo <strong>Pontos.contador</strong> de forma direta.</p>
<p align="justify">Para resolver este problema vamos criar uma variável local para armazenar o <strong>contador</strong> e o expor em uma interface pública que retorna esse valor.  Vamos ao código:</p>
<pre><code class="javascript">
var Pontos = (function () {
    var contador = 0;
    return {
    contador: function () {
    return contador;
    },
    incrementar: function () {
    return contador += 1;
    },
    imprimir: function () {
    console.log(contador);
    }
    };
})();

Pontos.incrementar();
Pontos.incrementar();
Pontos.imprimir(); // returns 2
Pontos.contador = 500;
Pontos.imprimir(); // returns 2

</code></pre>

<div align="center" class="image-content" style="background-color: #B09D8B;">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/fig4.png">
</div>

<p align="justify">Note que ambas as funções referenciam a variável <strong>contador</strong>, que agora não é mais acessível de forma direta, ou de fora do escopo da<strong> função auto executável</strong>. Mesmo que alguém tente alterar o valor da variável <strong>contador</strong> de fora do escopo, o valor continua o mesmo, só sendo alterado pelo método <strong>incrementar</strong>.</p>

<p align="justify">Dessa forma, podemos encapsular todo o comportamento, sem termos que nos preocupar com modificações feitas sem ser pela função <strong>Pontos.incrementar()</strong>, exatamente como o esperado.</p>

<p align="justify">Agora vamos para um exemplo do dia a dia. Observe o seguinte código e teste o seu resultado:</p>

<p><iframe src="//jsfiddle.net/vitormeriat/qz63s6o2/2/embedded/" width="100%" height="400" frame  allowfullscreen="allowfullscreen"></iframe></p>


<p align="justify">Em breve trago outros exemplos de implementações do modelo <strong>Self-Executing Anonymous Functions</strong> no <strong>JavaScript</strong>.</p>
<p>&nbsp;</p>

<h2>Referência</h2>

<p><a href="http://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript" target="_blank">Learning JavaScript Design Patterns</a></p>


<h3><span style="color: #ffc000;">Bons estudos e até a próxima pessoal  ;)</span></h3>
