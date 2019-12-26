---
layout: post
title: Programando seu Arduino com Visual Studio
date: 2015-07-12
categories:
  - Arduino
  - IoT
image: "http://blob.vitormeriat.com.br/images/2015/07/vs-e-arduino.png"
---

Recentemente fui questionado sobre opções para se trabalhar com o <strong>Arduino</strong> no Visual Studio. Como acho esse um tema interessante (um tanto pelo interesse do público em <strong>IoT</strong>, um tanto por ser da comunidade Microsoft), resolvi condesar aqui as minhas dicas de como utilizar o <strong>Visual Studio</strong> para programar um Arduino.

<div align="center" class="image-content" style="background-color: #e5e204;">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/vs-e-arduino.png">
</div>

Temos aqui duas estratégias distintas: <strong>Node.js</strong> e o <strong>Arduino for Microsoft Visual Studio</strong>. Ambas utilizam a mesma base para a comunicação com o Arduino, sendo assim o primeiro passo é falar sobre o protocolo firmata. 

# Firmata

Firmata é um protocolo genérico que te permite a comunicação de um computador hospedeiro e um microcontrolador via software.

Basicamente, estamos falando de um firmware que estabelece um protocolo de comunicação via software, do seu computador para o Arduino. O objetivo é permitir que você consiga controlar todas as portas analógicas e digitais do seu Arduino, com o mesmo conectado no seu computador. Dito isso vamos as opções:

# Node.js

A primeira opção é utilizar Node.js. Para isso, será necessário ter o Arduino Software (IDE), que é baixado diretamtne do site do Arduino, clicando 
<a href="https://www.arduino.cc/en/Main/Software" target="_blank">AQUI</a>!

Assim que você realizar a instalação da IDE, conecte seu arduino e acesse o código de exemplo do Firmata que está disponível em <strong>Examples</strong> &gt; <strong>Firmata</strong> &gt; <strong>StandartFirmata</strong>, como na imagem abaixo:

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/firmata.png">
</div>

Assim que o <strong>Sketch</strong> carregar, basta fazer o Upload para o Arduino e pronto! Seu Arduino já está preparado para ser uma extenção do seu computador. Basta agora criar um novo projeto no Visual Studio utilizando o templeta do Node.js. Para isso é necessário ter instalado o <a href="https://nodejstools.codeplex.com/" target="_blank">Node.js Tools for Visual Studio</a>.
<p>&nbsp;<br />

# Arduino for Microsoft Visual Studio

Este é um plugin pago. Por isto mesmo nunca havia me interessado em o utilizar, porém o que está disponível na versão free é o mesmo que conseguimos fazem com a IDE oficial do Arduino, porém com as facilidades que a <strong>IDE do Visual Studio</strong> nos traz.

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2015/07/visualstudio.png">
</div>

Se você ainda não tiver o <strong>Visual Studio</strong> instalado, indico o uso do Visual <a href="https://www.visualstudio.com/products/visual-studio-community-vs" target="_blank">Studio 2013 Community Edition</a>, que é uma <strong>IDE</strong> muito completa e grátis.

Para baixar o plugin, basta acessar a página do <a href="http://www.visualmicro.com/" target="_blank">Visual Micro</a> e fazer o download. Todas as instruções de instalação e uso das duas opções estão no vídeo baixo:

<div align="center" class="video-container">
  <iframe  src="https://www.youtube.com/embed/PGMgV3cE1VM?rel=0" allowfullscreen style="border: 0px;"></iframe>
</div>

# Referências
<ul>
<li><a href="http://firmata.org/wiki/Main_Page">http://firmata.org/wiki/Main_Page</a> </li>
<li><a href="https://www.arduino.cc/">https://www.arduino.cc/</a></li>
<li><a title="https://nodejstools.codeplex.com/" href="https://nodejstools.codeplex.com/">https://nodejstools.codeplex.com/</a></li>
<li><a title="https://www.visualstudio.com/products/visual-studio-community-vs" href="https://www.visualstudio.com/products/visual-studio-community-vs">https://www.visualstudio.com/products/visual-studio-community-vs</a></li>
<li><a title="http://www.visualmicro.com/" href="http://www.visualmicro.com/">http://www.visualmicro.com/</a></li>
</ul>
<p>&nbsp;</p>
<h3>Bons estudos e até a próxima pessoal&nbsp; ;)</h3>
