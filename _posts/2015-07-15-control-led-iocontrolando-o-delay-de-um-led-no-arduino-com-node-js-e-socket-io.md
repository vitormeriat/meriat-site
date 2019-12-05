---
layout: post
title: Control LED IO–Controlando o delay de um LED no Arduino com Node.js e Socket.io
date: 2015-07-15
categories:
  - Arduino
  - IoT
  - Node.js
  - Socket.io
image: "http://blob.vitormeriat.com.br/images/2015/07/capa-control-led-io.png"
---
<p align="justify"><img src="http://blob.vitormeriat.com.br/images/2015/07/capa-control-led-io.png" alt="capa control led io" width="100%" /></p>
<p align="justify"><strong>Primeiro acenda um LED, depois domine o mundo!</strong> Seguindo esta premissa estou disponibilizando meu primeiro projeto/estudo em <strong>Node.js</strong> no <strong>Arduino</strong>. Trata-se de um simples <strong>blink</strong> utilizando Node.js, <strong>Socket.io</strong>, <strong>Firmata </strong>e <strong>Johnny-five</strong> no <strong>Visual Studio</strong>. Abaixo segue o vídeo de demonstração:</p>
<p><iframe src="https://www.youtube.com/embed/S2ewQMYJR5I?rel=0" width="100%" height="563" frame  allowfullscreen="allowfullscreen"></iframe><!--more--></p>
<p align="justify">O projeto é bem simples e tem o passo-a-passo já está descrito no Github.</p>
<p align="justify">Para mais detalhes e <strong>baixar o projeto</strong>, <a href="https://github.com/vitormeriat/Control-LED-IO" target="_blank">acesse o Repository da solução aqui</a>!</p>
<p>&nbsp;</p>
<h1>O código</h1>
<p>Em <strong><span style="font-size: large;">app.js</span></strong> temos:</p>
<pre><code class="javascript">
var express = require('express'),
    app = express(),
    server = require('http').Server(app),
    io = require('socket.io')(server),
    five = require("johnny-five");

app.disable('x-powered-by');

app.use(function (req, res, next) {
    res.setHeader('Access-Control-Allow-Origin', "http://" + req.headers.host + ':8000');
    res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS, PUT, PATCH, DELETE');
    res.setHeader('Access-Control-Allow-Headers', 'X-Requested-With,content-type');
    next();
});

app.use("/", express.static(__dirname + "/view"));

app.get('/', function (req, res) {
    res.sendfile(__dirname + '/view/index.html');
});

server.listen(3000, "127.0.0.1");

five.Board().on("ready", function () {

    var led = new five.Led(13).strobe(1000);

    io.on('connection', function (socket) {

    console.log('Iniciado!!!');

    socket.on('led', function (data) {
    console.log('Novo Delay LED: ' + data.delay);
    led.strobe(data.delay);
    });
    });
});
</code></pre>
<p>Já o script em nossa view <strong><span style="font-size: large;">index.html</span></strong></p>
<pre><code class="javascript">
var socket = io.connect("http://" + document.location.hostname + ":3000"), notif;
console.log('Iniciado!!!');

$('#ledSet').on('click', function () {
    var tmp = parseInt($('#ledDelay').val(), 10);
    socket.emit('led', { delay: tmp });
    console.log("LED Delay Configurado para: ", tmp);
});
</code></pre>
<h2>Próximos passos</h2>
<p align="justify">Minha ideia é aproveitar o trabalho que já realizei com <strong>backend</strong> e <strong>integrações</strong> de <strong>cloud</strong> e <strong>IoT</strong>, para montar um projeto com o mesmo código funcionando no <strong>Arduino</strong>, <strong>Intel Galileo2</strong>, <strong>Intel Edison</strong> e <strong>Raspeberry Pi</strong>. Tudo se comunicando com a nuvem via <strong>Microsoft Azure</strong> :D</p>

<p>&nbsp;</p>
<h2>Bons estudos e até a próxima pessoal  ;)</h2>
