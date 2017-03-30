---
layout: post
title: Programando seu Arduino com Visual Studio
date: 2015-07-12
categories:
  - Arduino
  - IoT
image-full: "http://blob.vitormeriat.com.br/images/2015/07/vs-e-arduino.png"
---
<p align="justify">Recentemente fui questionado sobre opções para se trabalhar com o <strong>Arduino</strong> no Visual Studio. Como acho esse um tema interessante (um tanto pelo interesse do público em <strong>IoT</strong>, um tanto por ser da comunidade Microsoft), resolvi condesar aqui as minhas dicas de como utilizar o <strong>Visual Studio</strong> para programar um Arduino.
<p style="background-color: #e5e204;"><img alt="vs e arduino" src="http://blob.vitormeriat.com.br/images/2015/07/vs-e-arduino.png" width="100%" />
<p align="justify">Temos aqui duas estratégias distintas: <strong>Node.js</strong> e o <strong>Arduino for Microsoft Visual Studio</strong>. Ambas utilizam a mesma base para a comunicação com o Arduino, sendo assim o primeiro passo é falar sobre o protocolo firmata. </p>
<p><!--more--><br />
<h1>Firmata</h1>
<p align="justify">Firmata é um protocolo genérico que te permite a comunicação de um computador hospedeiro e um microcontrolador via software.</p>
<p align="justify">Basicamente, estamos falando de um firmware que estabelece um protocolo de comunicação via software, do seu computador para o Arduino. O objetivo é permitir que você consiga controlar todas as portas analógicas e digitais do seu Arduino, com o mesmo conectado no seu computador. Dito isso vamos as opções:</p>
<p>&nbsp;<br />
<h1>Node.js</h1>
<p align="justify">A primeira opção é utilizar Node.js. Para isso, será necessário ter o Arduino Software (IDE), que é baixado diretamtne do site do Arduino, clicando <a href="https://www.arduino.cc/en/Main/Software" target="_blank">AQUI</a>!</p>
<p align="justify">Assim que você realizar a instalação da IDE, conecte seu arduino e acesse o código de exemplo do Firmata que está disponível em <strong>Examples</strong> &gt; <strong>Firmata</strong> &gt; <strong>StandartFirmata</strong>, como na imagem abaixo:</p>
<p><img title="firmata" alt="firmata" src="http://blob.vitormeriat.com.br/images/2015/07/firmata.png" width="100%" /></p>
<p align="justify">Assim que o <strong>Sketch</strong> carregar, basta fazer o Upload para o Arduino e pronto! Seu Arduino já está preparado para ser uma extenção do seu computador. Basta agora criar um novo projeto no Visual Studio utilizando o templeta do Node.js. Para isso é necessário ter instalado o <a href="https://nodejstools.codeplex.com/" target="_blank">Node.js Tools for Visual Studio</a>.</p>
<p>&nbsp;<br />
<h1>Arduino for Microsoft Visual Studio</h1>
<p align="justify">Este é um plugin pago. Por isto mesmo nunca havia me interessado em o utilizar, porém o que está disponível na versão free é o mesmo que conseguimos fazem com a IDE oficial do Arduino, porém com as facilidades que a <strong>IDE do Visual Studio</strong> nos traz.</p>
<p align="justify"><img title="visualstudio" alt="visualstudio" src="http://blob.vitormeriat.com.br/images/2015/07/visualstudio.png" width="100%" /></p>
<p align="justify">Se você ainda não tiver o <strong>Visual Studio</strong> instalado, indico o uso do Visual <a href="https://www.visualstudio.com/products/visual-studio-community-vs" target="_blank">Studio 2013 Community Edition</a>, que é uma <strong>IDE</strong> muito completa e grátis.</p>
<p align="justify">Para baixar o plugin, basta acessar a página do <a href="http://www.visualmicro.com/" target="_blank">Visual Micro</a> e fazer o download. Todas as instruções de instalação e uso das duas opções estão no vídeo baixo:</p>
<p align="center">&nbsp;<iframe height="506" src="https://www.youtube.com/embed/PGMgV3cE1VM?rel=0" frame  width="900" allowfullscreen></iframe></p>

<h1>Referências</h1>
<ul>
<li><a href="http://firmata.org/wiki/Main_Page">http://firmata.org/wiki/Main_Page</a> </li>
<li><a href="https://www.arduino.cc/">https://www.arduino.cc/</a></li>
<li><a title="https://nodejstools.codeplex.com/" href="https://nodejstools.codeplex.com/">https://nodejstools.codeplex.com/</a></li>
<li><a title="https://www.visualstudio.com/products/visual-studio-community-vs" href="https://www.visualstudio.com/products/visual-studio-community-vs">https://www.visualstudio.com/products/visual-studio-community-vs</a></li>
<li><a title="http://www.visualmicro.com/" href="http://www.visualmicro.com/">http://www.visualmicro.com/</a></li>
</ul>
<p>&nbsp;</p>
<h3>Bons estudos e até a próxima pessoal&nbsp; ;)</h3>