---
layout: post
title: JavaScript–Singleton Pattern
date: 2015-06-16
categories:
  - Desing Patterns
  - JavaScript
---
<p align="justify">O <strong>Singleton Pattern</strong> diz que você pode ter apenas uma única instância de uma classe (ou, no caso do <strong>JavaScript</strong>, função construtora). Isso significa que uma vez que a classe for instanciada, você deve sempre retornar esta mesma instância em chamadas subsequentes.</p>
<p align="justify">Um exemplo clássico deste pattern é usar um único objeto como namespace de sua aplicação, como podemos ver no exemplo abaixo:</p>
<pre><code class="javascript" style="font-size: 22pt !important;">
var MinhaApp = {};
</code></pre>
<p align="justify">Pelo fato de termos definido a variável como um objeto, não podemos instanciar novos objetos à partir dele (embora possamos criar novos objetos usando este como base com a função <strong>Object.create</strong>, por exemplo). </p>
<p align="justify">Esse pattern também pode ser aplicado às funções construtoras. A maneira mais simples é utilizar Singleton com <strong>Immediately-Invoked Function Expression</strong> (<strong>IIFE</strong>) ou, como dizemos mais comumente, funções auto-executáveis. </p>
<pre><code class="javascript">
function MinhaApp() {
    if (!MinhaApp.instance) {
    MinhaApp.instance = this;
    }
    return MinhaApp.instance;
}
</code></pre>

<p align="justify">Essa função construtora irá garantir que você sempre receba a mesma instância como resultado. Isso só é possível porque funções construtoras utilizam o retorno como resultado da instanciação. Na prática, você poderia retornar qualquer tipo de objeto, como arrays ou strings. </p>
<pre><code class="javascript">
var instance = new MinhaApp();
console.log(instance === new MinhaApp()); // result = true
</code></pre>
<p align="justify">Você pode perceber que o resultado é sempre o mesmo, independente de quantas vezes instanciarmos a função <strong>MinhaApp</strong>. </p>
<p align="justify">O grande problema dessa implementação é que alguém pode manipular a instância armazenada em <strong>MinhaApp.instance</strong>, embora seja pouco provável. Uma alternativa seria utilizar o conceito de closure para simular a privacidade do atributo. </p>
<pre><code class="javascript">
function MinhaApp() {
    var instance;

    MinhaApp = function () {
    return instance;
    };

    instance = this;
}
</code></pre>
<p><p align="justify">Essa é uma implementação bastante curiosa. A função <strong>MinhaApp</strong> possui uma implementação que redefine a própria função <strong>MinhaApp</strong> para retornar apenas a instância. </p>
<p align="justify">Alternativamente você poderia utilizar o Module Pattern, mas acho que fica um pouco mais complexo que a implementação anterior. </p>
<pre><code class="javascript">
var MinhaApp;

(function () {
    var instance;

    MinhaApp = function () {
    if (instance) {
    return instance;
    }

    instance = this;
    };
})();

</code></pre>

<h2>Bons estudos e até a próxima galera!</h2>
