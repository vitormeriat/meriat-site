---
layout: post
title: 'Enumerator, foreach e o erro “InvalidOperationException: Collection Was Modified”'
date: 2012-02-23
categories:
  - C#
---

<p align="justify">Vamos abordar o cenário mais comum: Você possui uma coleção que pode ser uma lista de string, int ou como neste caso uma coleção de uma classe qualquer. Sua coleção tem diversos itens adicionados e você necessita retirar os itens conforme uma determinada lógica de negócio. Observe o código abaixo:</p>
<<<<<<< HEAD
<p><!--more-->
<p><a href="http://blob.vitormeriat.com.br/images/2012/02/listagem-1.png"><img alt="Listagem 1" src="http://blob.vitormeriat.com.br/images/2012/02/listagem-1.png"/></a></p>
<p>&#160;</p>
=======

<p><a href="http://blob.vitormeriat.com.br/images/2012/02/listagem-1.png"><img alt="Listagem 1" src="http://blob.vitormeriat.com.br/images/2012/02/listagem-1.png" /></a></p>

>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<h2>O motivo</h2>
<p align="justify">Você utiliza um <strong>loop foreach</strong> para percorrer cada item da coleção. Assim que sua regra é atendida por um dos itens da coleção, chamamos o método <strong>Remove() </strong>que tenta modificar a coleção durante o laço <strong>foreach</strong>.</p>

<h2>O erro</h2>
<p align="justify">A mensagem retornada no <strong>InvalidOperationException</strong> é bem clara: A coleção foi modifica e a enumeração não pode ser executada.</p>
<p align="justify">O primeiro passo para entender o erro é saber como funciona a forma básica de um <strong>foreach</strong>. O loop <strong>foreach</strong> foi criado para proporcionar uma forma elegante e simples de varrer todos os elementos de uma determinada coleção. Um <strong>foreach</strong> não utiliza índices inteiros em suas iterações, em vez disso, ele usa um mecanismo que retorna cada elemento em ordem. Este mecanismo é chamado de <strong>enumerator</strong>. Ele foi criado para evitar os erros comuns causados pelo manuseio incorreto de índices. </p>
<blockquote><p align="justify">Um <strong>enumerator</strong> é um cursor somente leitura (<strong>read-only</strong>), sequencial (<strong>forward-only</strong>) em uma sequencia de valores. Ele implementa <strong>IEnumerator</strong> ou <strong>IEnumerator&lt;T&gt;.</strong></p>
</blockquote>
<p align="justify">O <strong>foreach</strong> consulta o <strong>enumerator</strong> da coleção e solicita o próximo elemento lista. Em nosso exemplo, quando removemos um item tornamos o <strong>enumerator</strong> inválido já que o mesmo aponta para o estado atual do loop. O <strong>enumerator</strong> guarda uma cópia do layout da coleção. Não é possível para o <strong>foreach</strong> em tempo de execução (<strong>runtime</strong>) saber que o item foi removido. Logo, quando alteramos a coleção dentro de um loop <strong>foreach</strong>, o <strong>enumerator</strong> se perde… </p>
<p align="justify">Sendo assim, toda vez que retiramos um item durante a iteração com a lista, ocorrerá o erro assim que o laço “pegar” o próximo item.</p>

<h2>A solução</h2>
<p align="justify">Existem várias estratégias para isto, a maioria envolve trabalhar com listas auxiliares e é exatamente isto que quero evitar. </p>
<p align="justify">Levando em consideração aquilo que já sabemos sobre o funcionamento do <strong>foreach</strong>, podemos solucionar o problema de satisfatória apenas substituindo a linha do <strong>foreach</strong> pela sintaxe abaixo:</p>
<<<<<<< HEAD
<p><a href="http://blob.vitormeriat.com.br/images/2012/02/listagem-2.png"><img alt="Listagem 2" src="http://blob.vitormeriat.com.br/images/2012/02/listagem-2.png"/></a></p>
<p align="justify">O que ocorre é que para cada iteração trabalhamos com uma nova cópia da lista, o que evita o erro de coleção modificada…</p>
<p>O código fonte do exemplo pode ser baixado <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21227">aqui!</a></p>
<p>&#160;</p>
=======
<p><a href="http://blob.vitormeriat.com.br/images/2012/02/listagem-2.png"><img alt="Listagem 2" src="http://blob.vitormeriat.com.br/images/2012/02/listagem-2.png" /></a></p>
<p align="justify">O que ocorre é que para cada iteração trabalhamos com uma nova cópia da lista, o que evita o erro de coleção modificada…</p>
<p>O código fonte do exemplo pode ser baixado <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21227">aqui!</a></p>

>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<h4><strong>Um ótimo feriado a todos.</strong></h4>