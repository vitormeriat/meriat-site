---
layout: post
title: Conversão de ASCII para Binário e Binário para ASCII
date: 2011-05-05
categories:
    - C#
---

Em 1962, J.C.R. Licklider começou a fazer algumas anotações sobre sua idéia de Rede Intergalática, onde todas as pessoas do mundo estariam conectadas e poderiam acessar programas e dados de qualquer lugar do universo. Em Outubro deste ano, Lick, foi nomeado chefe do programa de pesquisas sobre computadores na <strong>ARPA</strong> (a avó da Internet), o qual ele batizou como <strong>IPTO</strong> (Information Processing Techniques Office - Escritório das Técnicas de Processamento de Informação).

Para criar uma rede de computadores são necessárias máquinas compatíveis e, o mais importante, um alfabeto comum que todas as máquinas pudessem entender. Como um alfabeto deste tipo não existia, constitui-se um comitê para estudar o assunto. O resultado foi o primeiro padrão universal para computadores, chamado de <strong>A</strong>merican <strong>S</strong>tandard <strong>C</strong>ode for <strong>I</strong>nformation <strong>I</strong>nterchange (Código Padrão Americano para a Troca de Informações), o <strong>ASCII</strong>.

> <strong>ASCII</strong>, é uma forma especial de código binário que é largamente utilizado em microprocessadores e equipamentos de comunicação de dados.

O <b>sistema binário</b> ou base 2, é um sistema de numeração posicional em que todas as quantidades se representam com base em dois números, com o que se dispõe das cifras: 0 e 1. O sistema de números binários (de base 2) representa valores usando dois símbolos, os números 0 e 1, que são chamados pelo computador de bits. Quando arranjados em grupo de 8 bits (1 byte), são gerados 256 valores (0 – 255). Através de uma tabela ASCII, estes valores são então interpretados em caracteres, podendo ser dessa forma armazenados e entendidos por nós. Outros sistemas são usados, como o hexadecimal, de base 16, e o octal, de base 8. Simples questão de matemática.

<p><a href="http://blob.vitormeriat.com.br/images/2011/05/011.png"><img alt="01" src="http://blob.vitormeriat.com.br/images/2011/05/01.png" /></a></p>

Este código é uma brincadeira que fiz e estou disponibilizando para que todos possam estudar e procurar melhores implementações(quem o fizer, favor compartilhar).
Vamos dar uma olhada nos métodos:
<p><a href="http://blob.vitormeriat.com.br/images/2011/05/021.png"><img alt="02" src="http://blob.vitormeriat.com.br/images/2011/05/02.png" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/05/031.png"><img alt="03" src="http://blob.vitormeriat.com.br/images/2011/05/03.png" /></a></p>
<p><a href="http://cid-bd055aa47a388023.office.live.com/self.aspx/.Public/ASCII.rar" target="_blank">Código Fonte do Artigo.</a></p>
