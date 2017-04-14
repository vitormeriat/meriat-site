---
layout: post
title: Animações em ASCII
date: 2013-01-16 
categories:
	- C#
image: "http://blob.vitormeriat.com.br/images/2013/01/1.png"
---
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2013/01/1.png"><img alt="1" src="http://blob.vitormeriat.com.br/images/2013/01/1.png" /></a></p>

<p align="justify"><b>ASCII</b> (acrônimo para <i><strong>A</strong>merican <strong>S</strong>tandard <strong>C</strong>ode for <strong>I</strong>nformation <strong>I</strong>nterchange)</i>, referido em português como &quot;Código Padrão Americano para o Intercâmbio de Informação&quot;. o Padrão <strong>ASCII</strong> tem extrema utilidade e isso já é bem sabido por nós programadores, no entanto, vou me ater a funcionalidade que mais me diverte: Animações em <strong>ASCII</strong>. <img class="wlEmoticon wlEmoticon-smile" style="border-style:none;" alt="Alegre" src="http://blob.vitormeriat.com.br/images/wlemoticon-smile.png" /></p>
<p><!--more-->
<p align="justify">Vou apenas indicar alguns locais onde buscar referências e postar minha brincadeirinha… </p>
<p align="justify">Primeiro gostaria de justificar que tive um problema com internet, não estava em casa e sem um livro ou guitarra por perto então aproveitei para fazer alguma coisa interessante e divertida aproveitando minha parca bateria do note. Isso foi para a galera meus colegas <strong>“Developos”</strong> que não acreditaram que eu estava fazendo isso…</p>
<p align="justify">Bem, primeiro vai a primeira animação que vi e me incentivou a brincar com isso. É a famosa animação em <strong>ASCII</strong> baseado no <a href="http://www.asciimation.co.nz/" target="_blank">Episode IV - A NEW HOPE.</a></p>
<p align="justify">Um lugar bacana para procurar personagens e inspiração para animações é no site <strong>ASCII Arte </strong>que pode ser acessado neste endereço: <a title="http://www.asciiarte.com/" href="http://www.asciiarte.com/">http://www.asciiarte.com/</a></p>
<p align="justify">O que eu fiz primeiro foi montar um framework para me auxiliar no desenho e animação. O primeiro ponto e determinar a quantidade de linhas e caracteres para formar um <strong>stage</strong> onde os cenários e personagens serão exibidos. Depois de alguns testes cheguei a conclusão que era melhor montar o <strong>stage</strong> com<strong> 25 linhas</strong> e<strong> 72 caracteres</strong>.</p>
<p>O segundo passo foi criar uma classe Filme como os seguintes métodos:</p>
<ul>
<ul>
<li><strong>SubstituirLinha:</strong> Subistitui a linha do cenário principal pela linha indicada</li>
<li><strong>Exibir:</strong> Aplica um tempo determinado antes de limpar o console e exibir as linhas</li>
<li><strong>Legenda:</strong> Insere a legenda ao cenário atual</li>
<li><strong>CenarioPrincipal:</strong> Cria o cenário principal com o desenho da cidade</li>
<li><strong>CenarioVazio:</strong> Cria o cenário com as linhas vazias</li>
</ul>
</ul>

O terceiro e último foi montar as animações. O exemplo pode ser visto no <strong>código fonte</strong> disponibilizado no fim do post.


## Dicas

Monte um roteiro. Desenhe seus personagens, se possível aconcelho usar o <strong>Notepad++ </strong>pelos recusos de seleção e contagem de caracteres que facilitam o trabalho. Depois é só ficar de olho no tempo de troca para a animação ficar com cara de filme.

Abaixo segue alguns prints da minha animação:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2013/01/11.png"><img alt="1" src="http://blob.vitormeriat.com.br/images/2013/01/1.png" /></a></p>

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2013/01/2.png"><img alt="2" src="http://blob.vitormeriat.com.br/images/2013/01/2.png" /></a></p>

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2013/01/3.png"><img alt="3" src="http://blob.vitormeriat.com.br/images/2013/01/3.png"/></a></p>

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2013/01/4.png"><img alt="4" src="http://blob.vitormeriat.com.br/images/2013/01/4.png" /></a></p>

<p>O <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%211413" target="_blank">código fonte pode ser baixado aqui!</a></p>
