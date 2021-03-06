---
layout: post
title: MQTT, protocolos, integrações e os cuidados com IoT
date: 2015-06-08
categories:
  - Cloud Computing
  - Enterprise Integration
  - IoT
image: "http://blob.vitormeriat.com.br/images/2015/06/capa1.png"
---

<strong>MQTT</strong> ou <strong><a href="http://mqtt.org/" target="_blank">Message Queuing Telemetry Transport</a></strong>, é um protocolo de conectividade para <strong>M2M </strong>(Machine-to-Machine)<strong> / IoT</strong> (Internet of Things), projetado para suportar o transporte de mensagens para dispositivos de pequena capacidade, baixo consumo de energia, baixa largura de banda, alta latência e disponibilidade variável.

Em resumo é um protocolo de mensagens de peso leve, que traz a capacidade de comunicação assíncrona em redes restritas, a dispositivos de recursos limitados. Ele se tornou um padrão <a href="https://www.oasis-open.org/" target="_blank">OASIS</a> em 07 de novembro de 2014, em sua versão <strong>3.1.1</strong>.

<div align="center" class="image-content" style="background-color: #59B2C2;">
  <img src="http://blob.vitormeriat.com.br/images/2015/06/capa1.png">
</div>

Recentemente me perguntaram (<a href="http://vitormeriat.com.br/2014/11/21/mensageria-e-os-protocoloschoose-your-poison/" target="_blank">por conta deste post</a>), sobre qual a necessidade de um protocolo como o MQTT. A verdade é que muito se dá ao desconhecimento do público em relação ao mundo da “<strong>Internet das Coisas</strong>”.

Este não é um post específico sobre MQTT, ou sua implementação. É sobre o gancho que este protocolo extremamente leve traz para o <strong>“pensar em IoT”</strong>.

Cada dia vemos novos modelos de placas com capacidades maiores, mais próximas de uma máquina usual, e repentinamente nos ocorre que é possível construir aplicações exatamente como fazemos para o mundo Web, ou construir serviços exatamente como fazemos nossas APIs.

O fato é que no mundo do IoT, os dispositivos que estão implantados nos relógios, tênis e outros diversos acessórios, não são placas com 2GB, USB 3.0 ou HDMI. Os dispositivos que estamos falando são componentes altamente minimalistas.

Para se manter em um mercado cada vez mais agressivo, é fundamental construir devices que façam o melhor proveito de seus componentes, a fim de serem mais precisos em suas finalidades e com um custo menor de manufatura.

Sendo assim, o que vemos na prática são diversos dispositivos com microprocessadores de 8-BITs e 192KB RAM. Quando olhamos para estas capacidades, fica claro que deve se existir uma preocupação enorme com protocolos, brokers e as aplicações que serão desenvolvidas para um projeto de IoT.

Nem todo dispositivo pode se dar ao luxo de 16MB de RAM, quem dirá 2GB. Então nestes termos olhar para o MQTT faz muito sentido. Aliás, estamos falando de um protocolo com apenas 2 bytes de Header. Em determinadas aplicações, até protocolos como o <strong>AMQP</strong> podem ser inviáveis dado o seu tamanho, ainda mais se houver necessidade de <strong>SSL</strong>.

MQTT pode ser ideal em determinadas aplicações móveis por causa de seu tamanho, onde temos pacotes de dados minimalistas e uma distribuição eficiente de informações para um ou muitos receptores (assinantes). Sem falar no transporte de mensagens que não se preocupa com o conteúdo a ser entregue.

Você ainda pode facilmente integrar com a nuvem a fim de abstrair sua infra, utilizando brokers já preparados para este cenário.

Mas não se engane. MQTT não é uma bala de prata. Para quem quer entrar no mundo do IoT é importante conhecer toda as questões envolvidas.

Já os <strong>early adopters</strong> de IoT vem de áreas como desenvolvimento de software e eletrônica, conectando dispositivos dentro desta rede mediante os diferentes protocolos disponíveis. Mas, para levar esse conceito ao nosso dia a dia é necessária uma camada de integração e protocolos que ofereçam suporte a todas as necessidades e complexidades técnicas. No final, para usuário é irrelevante se seu dispositivo “fala” via jSON, XML, SMS, COISAML…! Já para a implementação e desempenho este é um assunto totalmente relevante.

Outra coisa que vale notar é o fator segurança. Mais dispositivos conectados significa mais IPs disponíveis que por sua vez significa mais portas vulneráveis e maior risco de segurança. As políticas de segurança e de privacidade com certeza serão revistas neste novo contexto. O aumento de comunicação nesta rede incrementa o risco de distribuir informações de forma indevida, sem falar da possibilidade dos erros de comunicação entre dispositivos. O desenho de novos serviços ganha mais um desafio, agora voltado à privacidade de dados e, principalmente, nos meios que podemos utilizar para ganhar a confiança dos usuários.

Você encontra toda a e especificação do MQTT <a href="http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html" target="_blank">aqui!</a>

>Nos próximos posts, vou estar implementando algumas integrações entre Nuvem e IoT.