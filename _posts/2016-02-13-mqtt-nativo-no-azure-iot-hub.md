---
layout: post
title: MQTT nativo no Azure IoT Hub
date: 2016-02-13
categories:
  - Azure IoT Suite
  - IoT
  - Microsoft Azure
  - MQTT
---

Estou utilizando o Microsoft Azure em projetos de IoT antes mesmo do lançamento do <a href="https://azure.microsoft.com/pt-br/services/iot-hub/" target="_blank"><strong>Azure IoT Hub</strong></a>. Desde então tenho aguardado um notícia que veio enfim, no dia 8 de fevereiro de 2016: O suporte nativo ao protocolo <a href="http://mqtt.org/" target="_blank"><strong>MQTT</strong></a> sem a necessidade do protocol gateway.

Embora essa fosse um solicitação recorrente, há de se parabenizar o esforço do time do <strong>Azure IoT</strong>. Pouco tempo após o <strong>MQTT</strong> ter sido aprovado como padrão <strong>ISO/IEC</strong> (a saber: <a title="http://www.iso.org/iso/catalogue_detail.htm?csnumber=69466" href="http://www.iso.org/iso/catalogue_detail.htm?csnumber=69466" target="_blank">#ISO20922</a>), somos agraciados com a notícia do suporte nativo no <strong>Azure IoT Hub</strong>.

Essa é uma notícia que agrega e muito ao serviço. Aqueles que já trabalham na área sabem o quanto é fundamental a questão da comunicação. Um projeto IoT depende desse fator, e para se ter um projeto robusto é necessário se pensar nos principais problemas como restrição de banda, restrição de plataforma etc. É ai que entra o MQTT. Já abordei isso por cima em alguns posts anteriores.

Devo fazer alguns posts sobre a experiência em utilizar o IoT Hub da Microsoft. Neles devo abordar detalhes do produto e a experiência de migrar um projeto já pronto, enviando dados para um broker na nuvem no modelo IaaS, para o serviço na plataforma Azure.

Utilizar o Azure IoT Hub com MQTT é tão simples quanto o esperado. Não há segredos nem customizações, apenas informe o protocolo a ser usado e sua string de conexão. Abaixo segue o exemplo em Node.js:

## Criar um device

<pre style="font-size: 16pt !important">
  <code class="javascript">
    var clientFromConnectionString =
    require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = '[IoT Hub device connection string]';
    var client = clientFromConnectionString(connectionString);
  </code>
</pre>

## Enviando dados

<pre style="font-size: 16pt !important">
  <code class="javascript">
  var msg = new Message('some data from my device');
  client.sendEvent(message, function (err) {
    if (err) console.log(err.toString());
  });
  </code>
</pre>

## Recebendo dados

<pre style="font-size: 16pt !important">
  <code class="javascript">
  client.receive(function (err, msg) {
  if (err) console.error(err);
    else console.log(msg);
  });
  </code>
</pre>

<hr style="margin-bottom: 5em; margin-top: 5em;" />

## Referências

<p><a href="https://azure.microsoft.com/en-us/blog/azure-iot-hub-ga-capability-overview/?wt.mc_id=WW_CE_IOT_OO_SCL_TW&amp;Ocid=C+E+Social+FY16_Social_TW_MicrosoftIoT_20160209_363303519" target="_blank">Azure IoT Hub general availability overview</a></p>
<p><a href="https://github.com/Azure/azure-iot-sdks/tree/master/node/device/transport/mqtt" target="_blank">Github - Azure IoT Device MQTT</a></p>

