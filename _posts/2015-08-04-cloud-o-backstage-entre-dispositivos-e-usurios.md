---
layout: post
title: CLOUD - O BackStage entre Dispositivos e Usuários
date: 2015-08-04
categories:
  - Amazon Web Service
  - Arduino
  - Big Data
  - Cloud Computing
  - IoT
  - Microsoft Azure
  - Microsoft Azure Storage
  - NoSQL
---
<p align="justify">Olá pessoal… novamente tive a grande honra de participar do <strong><a href="http://www.iotweekend.com.br/" target="_blank">IoT Weekend</a></strong>, desta vez na edição <strong>Brasília</strong> (minha terra natal)<strong>. </strong>Foi um evento maravilhoso, com um público muito atento, palestrantes extremamente qualificados e grandes cases de sucesso, entre <strong>IoT</strong> e <strong>Cloud Computing</strong>.</p>
<p align="justify">Como prometido segue o material da minha apresentação, <strong>Cloud Computing, o BackStage entre dispositivos e usuários. </strong>Nesta apresentação, utilizando um exemplo prático, vimos sobre fundamentos de Cloud Computing, utilização protocolos como <strong>AMQP</strong> e <strong>MQTT</strong>, <strong>Big Data</strong>, <strong>Stream Analytics</strong> e <strong>Machine Learning</strong>.</p>
<p style="background-color: #646767;"><img src="http://blob.vitormeriat.com.br/images/2015/08/capaiotweekendbsb.png" alt="capaiotweekendbsb" width="100%" /></p>

<p>&nbsp;</p>

<p><img style="background-image: none; float: left; padding-top: 0px; padding-left: 0px; margin: 0px 40px 0px 0px; display: inline; padding-right: 0px; border: 0px;" title="iotweekend" src="http://blob.vitormeriat.com.br/images/2015/08/iotweekend.jpg" alt="iotweekend" width="470" height="522" align="left" /></p>
<p align="justify">Um dispositivo de <strong>Internet das Coisas</strong> necessariamente tem que enviar e receber comandos e mensagens e muitas das vezes milhares de vezes em um determinado período de tempo curto. Uma coleira de cachorro inteligente por exemplo pode definir uma cerca virtual e quando o animal ultrapassar o perímetro definido ele começa a enviar o seu novo  posicionamento e com isso seu dono pode além de o encontrar facilmente, conhecer seus hábitos e muitas vezes tornar a vida do animal mais divertida e melhor. Este é um dos exemplos onde temos a geração de centenas de dados por dia e que se utilizados e tratados de forma adequada podem gerar uma informação de extrema valia e qualidade. Em um dispositivo como este também precisamos enviar comandos visando modificar o comportamento do dispositivo e também interagir com o animal. Tudo isso é orquestrado pelos serviços na nuvem, de forma escalável e segura.</p>
<p align="justify">E foi baseado nessa premissa que montei um exemplo básico: Um simples sensor <strong>PIR</strong> <strong>(Passive Infrared)</strong>, enviando dados para o <a href="https://azure.microsoft.com/pt-br/documentation/articles/storage-dotnet-how-to-use-queues/" target="_blank"><strong>Azure Queue Storage</strong></a>, <a href="https://azure.microsoft.com/en-us/documentation/articles/event-hubs-csharp-ephcs-getstarted/" target="_blank"><strong>Azure Event Hubs</strong></a> e um <a href="http://www.cloudmqtt.com/" target="_blank"><strong>Broker SaaS MQTT na Amazon Web Services</strong></a>. Os dados gerados são gravados em um <strong>NoSQL</strong>, que é utilizado como base para o <strong>Machine Learning</strong>. Nesta apresentação, foi utilizado o <a href="http://azure.microsoft.com/en-us/services/machine-learning/" target="_blank"><strong>Azure Machine Learning</strong></a> e o <a href="http://www.ibm.com/smarterplanet/us/en/ibmwatson/" target="_blank"><strong>IBM Watson</strong></a>.</p>
<p align="justify">
<p><iframe style="height: 670px; width: 1000px;" src="//pt.slideshare.net/slideshow/embed_code/key/4UO8NyHjNsvsWe" width="998" height="150" frame  marginwidth="0" marginheight="0" scrolling="no"> </iframe></p>
<p>&nbsp;</p>
<p align="justify">Em breve vou estar postando um vídeo do protótipo e da implementação, bem como dos serviços utilizados.</p>
<p>&nbsp;</p>
<h2><span style="color: #666666; font-size: x-large;">Bons estudos e até a próxima pessoal  ;)</span></h2>