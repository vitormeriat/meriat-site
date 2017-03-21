---
layout: post
title: Mensageria e os Protocolos–Choose your poison
date: 2014-11-21
categories:
  - Enterprise Integration
  - SOA
image: "http://blob.vitormeriat.com.br/images/2014/11/capa.png"
---
<p align="justify">Uma das questões mais interessantes da mensageria são os protocolos. Na arquitetura de software é fundamental entender a diferença entre os protocolos de mensagens e qual deve ser utilizado em cada tipo de aplicação.</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/capa.png"><img  alt="capa" src="http://blob.vitormeriat.com.br/images/2014/11/capa.png" /></a></p>
<p align="justify">Hoje com a multiplicidade de sistemas e plataformas, os arquitetos de software tem optado pela utilização do famoso <a href="http://www.eaipatterns.com/MessageBroker.html" target="_blank">Message Broker</a> (que vou abordar em um próximo post). Porém escolher um middleware de mensagens também implica em entender as diferenças sutis entre os protocolos de transporte, o que pode ser uma tarefa difícil.</p>
<p align="justify">Neste post vou apresentar os principais e mais utilizados protocolos de mensagem da atualidade.</p>
<p><!--more-->
<p>&nbsp;</p>
<h2>AMQP - Advanced Message Queuing Protocol</h2>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/amqp.png"><img alt="amqp" src="http://blob.vitormeriat.com.br/images/2014/11/amqp.png" /></a></p>
<p align="justify">O <a href="http://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol">AMQP</a> é um protocolo binário com diversas features tais como: multicanal, negociável, assíncrono, seguro, portável, neutro e eficiente. Ele se divide em duas camadas: </p>
<ul>
<p align="justify">– Camada funcional que define um conjunto de comandos ou métodos que fazem trabalho útil em benefício da aplicação permitindo suportar diversos estilos de trocas de mensagens. </p>
<p align="justify">– Camada de transporte – cobre o conteúdo relativo ao meio de transporte, coisas do tipo multiplexação de canais, pacote de dados (framing), encoding do conteúdo, heart-beating, representação dos dados e tratamento de erro.</p>
</ul>
<p align="justify">Os métodos citados na camada funcional são operações do tipo métodos HTTP e não tem nada em comum com os métodos das linguagens orientadas a objetos. São agrupados logicamente em classes de funcionalidade.
<p align="justify">Para quem quer saber mais, nada como consultar diretamente as especificações. Para isso é só acessar o <a href="http://www.amqp.org/confluence/download/attachments/720900/amqp0-9-1.pdf?version=1&amp;modificationDate=1227508523000">AMQP 0-9-1 Specification (PDF)</a> e ler direto na fonte.
<p>&nbsp;</p>
<h2>MQTT - Message Queue Telemetry Transport</h2>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/mqttorg.png"><img title="mqttorg" alt="mqttorg" src="http://blob.vitormeriat.com.br/images/2014/11/mqttorg.png" /></a>
<p align="justify">Inicialmente desenvolvido pela Pervasive Computing Team da IBM, o MQTT ao longo dos últimos anos, foi movido para a comunidade de open source, e o que se viu foi um crescimento significativo na popularidade e utilização deste protocolo.
<p align="justify">Os padrões de design e objetivos do MQTT são mais simples que o AMQP. Sendo assim é mais fácil fornecer o publish-and-subscribe messaging (sem se utilizar o mecanismo de fila, apesar do nome). O MQTT foi projetado especificamente para dispositivos com recursos limitados e baixa largura de banda, alta latência de rede (como linhas dial-up e links de satélite, por exemplo), o que o torna ideal para ser usado em sistemas embarcados.
<p>Os pontos fortes da MQTT são a simplicidade (apenas cinco métodos na API), a carga útil do pacote binário compacto (sem propriedades de mensagem, cabeçalhos compactados, muito menos detalhados do que algo como HTTP), e faz um bom ajuste para cenários simples impulso de mensagens como temperatura atualizações, tickers de preços de ações, feeds de pressão de óleo ou notificações móveis. É também muito útil para conectar máquinas em conjunto, como conectar um <a href="http://www.arduino.cc/">Arduino</a> dispositivo <a href="http://blog.m2m.io/post/30048662088/a-simple-example-arduino-mqtt-m2m-io">para um serviço web com MQTT</a> .
<p>&nbsp;</p>
<h2>MSMQ - Microsoft Message Queuing</h2>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/msmq.png"><img title="MSMQ" alt="MSMQ" src="http://blob.vitormeriat.com.br/images/2014/11/msmq.png" /></a></p>
<p align="justify">Microsoft Message Queuing (MSMQ) foi desenvolvido pela Microsoft (sério?) e está disponível desde 1997 em todas as plataformas do Windows (tem que ser instalado como componente do Windows), e sua versão mais atual é a 6.3.</p>
<p align="justify">O MSMQ está disponível em quase todas as máquinas Windows a partir do Windows 2000 (embora não o home edition Win2000). Com o Windows XP e Server 2003, a Microsoft introduziu MSMQ 3.0 e Service Pack 2 trouxe MSMQ para a versão 3.1, com um conjunto de recursos enterprise-ready.</p>
<p align="justify">O MSMQ fornece integração com o Active Directory, suporta operações nativas, bem como transações distribuídas utilizando o distributed transaction coordinator integration. As mensagens são gravadas em disco na máquina local, o que leva a necessidade de se implementar um armazenamento distribuído e redundante para evitar a perca de mensagens em caso de falha de disco.</p>
<p align="justify">Outro problema é a baixa interoperabilidade nativa do MSMQ, já que ele é executado em sistemas operacionais Windows. É razoavelmente rápido quando utilizado com código gerenciado (disponível no framework .NET) e ainda mais rápido quando combinado com código não gerenciado. Escalabilidade e alta disponibilidade podem ser alcançados com a construção de um cluster MSMQ (ou usar o NServiceBus ou ainda migrar para o Azure Service Bus). A administração de MSMQ é bastante fácil. Ele pode ser instalado, gerenciado e configurado com o PowerShell, no Microsoft Management Console (MMC) ou com ferramentas de terceiros.</p>
<p align="justify">Durante o tempo em que a Divisão de Sistemas Conectados à Microsoft estava desenvolvendo Indigo (agora conhecido como WCF), a intenção era substituir MSMQ com algo novo, porém o esforço para substituir MSMQ foi abandonado e MSMQ foi integrado ao WCF.
<p>&nbsp;<br />
<h2>JMS - <strong>Java Message Service</strong></h2>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/jsm.png"><img alt="JSM" src="http://blob.vitormeriat.com.br/images/2014/11/jsm.png" /></a>
<p align="justify">Em 2001 nasceu o <a href="http://docs.oracle.com/javaee/6/tutorial/doc/bncdq.html">JMS</a> (Java Message Service) tentando resolver os problemas de interoperabilidade e de vendor lock-in por meio de uma <a href="http://docs.oracle.com/javaee/6/tutorial/doc/bnceh.html">API Java comum</a> que escondesse as peculiaridades de cada fornecedor. Na verdade, resolveu apenas para a plataforma Java. Em um ambiente puramente Java normalmente é possível trocar de message broker apenas alterando configurações em um arquivo externo, como um <a href="http://docs.oracle.com/javase/jndi/tutorial/beyond/env/source.html">jndi.properties</a> por exemplo.
<p align="justify">As melhores referências para aprender a usar JMS diretamente estão nos capítulos 3 e 4 do livro <a href="http://www.amazon.com/Messaging-Charles-River-Media-Programming/dp/1584504188">Java Messaging</a> de autoria do colunista <a href="http://drdobbs.com/jvm/200001958">Eric Bruno</a> da <a href="http://drdobbs.com/?itc=ddj-header-navbar-home">revista Dr.Dobb’s</a>.
<p>&nbsp;</p>
<h2>STOMP - Simple/Streaming Text Oriented Messaging Protocol</h2>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/protocol.png"><img alt="Protocol" src="http://blob.vitormeriat.com.br/images/2014/11/protocol.png" /></a>
<p align="justify">STOMP (Streaming de texto simples / Orientada Messaging Protocol) é um protocolo baseado em texto, o que o torna mais análogo ao HTTP em termos de como ele olha debaixo do capô. Assim como o AMQP, o STOMP fornece um cabeçalho e corpo para a mensagem. Os princípios de design aqui eram para criar algo simples, e amplamente interoperável. Por exemplo, é possível conectar-se usando algo tão simples como um cliente telnet.
<p align="justify">STOMP é simples e leve, com uma vasta gama de <a href="http://stomp.github.com/implementations.html">suporte a linguagens</a>. Um dos exemplos mais interessantes é com RabbitMQ Web Stomp, que lhe permite <a href="http://www.rabbitmq.com/blog/2012/05/14/introducing-rabbitmq-web-stomp/">expor mensagens em um navegador através websockets</a> .
<p>&nbsp;</p>
<h2>RabbitMQ – O protocolo poliglota</h2>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/11/rabbitmq.png"><img alt="rabbitmq" src="http://blob.vitormeriat.com.br/images/2014/11/rabbitmq.png" /></a></p>
<p align="justify">O <a href="http://www.rabbitmq.com/" target="_blank">RabbitMQ</a> é uma implementação open source baseada em AMQP onde é possível se beneficiar de outros sistemas&nbsp; como OTP (Open Telecommunication Platform), que é utilizado pelas empresas de telecomunicação para gestão de exchanges para chamadas de voz, VoIP e agora vídeo.</p>
<p align="justify">O RabbitMQ é uma implementação open source baseada em AMQP, porém ao invés de criar uma nova infra-estrutura de mensagens, a equipe do RabbitMQ construiu uma camada em Erlang em cima de OTP (Open Telecommunication Platform). Toda a API é fornecida para que os desenvolvedores se conectam a ele sobre o protocolo AMQP. Isto combina a robustez e escalabilidade de uma plataforma comprovada com a flexibilidade do modelo de mensagens AMQP.</p>
<p align="justify">John O'Hara, Presidente do <a href="http://www.amqp.org/" target="_blank">AMQP Working Group</a> disse: "Um padrão forte precisa de uma variedade de interoperabilidade e implementações, e eu estou satisfeito em acolher o RabbitMQ na família. A visão do AMQP Working Group é por meio da padronização AMQP, permitindo que as empresas reduzam seus custos de integração utilizando processamento de transações simples e robusta entre as empresas no mundo todo."</p>
<p>&nbsp;</p>
<h2>Conclusão</h2>
<p align="justify">A ideia neste post é de apenas apresentar os protocolos de transporte mais utilizados. Vale notar que deixei de fora diversos protocolos já que hoje os mais utilizados são os que privilegiam a interoperabilidade. Nessa brincadeira temos como intruso o MSMQ que ainda é extremamente utilizado devido o grande legado de utilização do Windows como SO.</p>
<p>&nbsp;</p>
<h2>Referências</h2>
<p><a title="http://mqtt.org/" href="http://mqtt.org/">MQTT.org</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/ms711472.aspx" target="_blank">Message Queuing (MSMQ)</a></p>
<p><a href="http://www.rabbitmq.com/documentation.html" target="_blank">RabbitMQ</a></p>
<p><a href="http://stomp.github.io/" target="_blank">Stomp</a></p>
