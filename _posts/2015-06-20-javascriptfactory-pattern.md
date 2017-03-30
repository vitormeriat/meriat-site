---
layout: post
title: JavaScript–Factory Pattern
date: 2015-06-20
categories:
  - Desing Patterns
  - JavaScript
---

<p align="justify">Criar objetos é a especialidade do <strong>Factory Pattern</strong>. A grande vantagem desse pattern é que ele reduz a duplicação das tarefas de inicialização em objetos similares, além de permitir abstrair construções que podem ser complexas.
<p align="justify">Normalmente o método responsável por inicializar os objetos é um método estático, que no contexto do <strong>JavaScript</strong> pode ser adaptado para um método adicionado diretamente à função construtora. </p>
<pre><code class="javascript">
function Usuario(attrs) {
    for (var nome in attrs) {
    this[nome] = attrs[nome];
    }
}

Usuario.build = function (attrs) {
    return new Usuario(attrs);
};
</code></pre>
<p><!--more-->
<p align="justify">O <strong>Factory Pattern</strong> pode ser uma boa alternativa para evitar que funções construtoras não sejam chamadas sem a palavra-chave <strong>new</strong>. Para inicializar um novo usuário, podemos chamar a <strong>Factory Usuario.build</strong>. </p>
<pre><code class="javascript">
var user = Usuario.build({
    nome: "Vitor Meriat",
    email: "vitormeriat@hotmail.com"
});
</code></pre>
<p align="justify">Ele também pode ser uma boa alternativa para normalizar parâmetros antes da instanciação; lembre-se que no <strong>JavaScript</strong> não existe sobrecarga de métodos. Imagine que você queira simplificar a instanciação de um <strong>novo objeto Usuario;</strong> caso um objeto seja passado como argumento, ele é utilizado. Se dois parâmetros forem passados, um objeto contendo o nome e e-mail deve ser definido antes. </p>
<pre><code class="javascript">
Usuario.build = function (attrs) {
    if (arguments.length === 2) {
    attrs = {
    nome: arguments[0],
    email: arguments[1]
    };
    }
    return new Usuario(attrs);
};
</code></pre>
<p align="justify">O <strong>Factory Pattern</strong> é uma forma excelente de <strong>reduzir/remover</strong> complexidades na criação de objetos. Os exemplos deste artigo são simples, claro, mas não se deixe enganar. <strong>Factories</strong> podem ser extremamante complexos e tudo vai depender de quão complexo é a definição de seus objetos, podendo conter inclusive toda a parte de configuração.</p>
<p>&nbsp;</p>
<h2>Bom estudo e até a próxima!!!</h2></p>
