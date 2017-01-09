---
layout: page
title: Experiência de Prototipar um dispositivo IOT em NY
date: 2015-03-07 12:10
author: jorgemaia
comments: true
categories: [azure, BLE, C#, Eventos, IOT, IOT, Xamarin]
---
Fevereiro de muita diversão, tive o prazer de participar da prototipação de um dispositivo de Internet das Cosias para monitoramento de animais  com uso de GPS. Diversos desafios tais como comunicação, protocolo e bateria estiveram em alta todos os dias do desenvolvimento.

Vamos aos desafios:
<ol>
	<li>Bateria - Precisávamos de um dispositivo que tivesse uma longevidade haja vista a necessidade de não se carregar e também não se trocar bateria durante longos períodos de tempo. Quando pensamos em um dispositivo de rastreamento temos que ter em mente o problema da bateria e sua carga. Para isso adotamos dois modelos de comunicação sendo o primeiro com Bluetooth smart para controle de localização dentro da residência e outro com comunicação GSM para quando estivéssemos em áreas abertas.</li>
	<li>Comunicação (entenda-se protocolo) - Testei tanto apis de gerenciamento de dados na nuvem para dispositivos móveis quanto o bom e velho MQTT que venho falando a tempo. Quanto as APIs, testei a mobile services do Azure, que funcionou extremamente bem porem eu precisava de algo mais leve para o hardware pois quanto mais peso ou processamento, mais bateria e mais custo. Uma coisa interessante quando pensamos no hardware do dispositivo é que devemos ter em mente que quanto mais inteligente ele for mais caro ele fica, tanto para projetar e prototipar quanto para produzir, logo a inteligência ficou a cargo da nuvem.</li>
	<li>Um outro que não foi listado acima mas considero também importante é o cross plataform, quando queremos atingir a massa, bom mesmo seria desenvolver tudo em C#, e é claro que é possível, Xamarin é o seu nome!  Optei por desenvolver rapidamente em C# nativo para Windows Phone e em swift para fazer a app de IOS, próximos passos serão feitos em Xamarin, assim espero.</li>
</ol>
Foram quase 20 dias de muita ralação e muito conhecimento. Convido você a escutar alguns episódios deste período no <a href="http:/www.jorgecast.com.br" target="_blank">JorgeCast</a> e veja as informações do dia a dia, eventos que participei por lá e o quanto é fácil se fazer tecnologia com a infraestrutura (não só de telecom, mas de entrega, transporte...) necessária disponível.

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/04/10407723_10152830083862585_5865610731164393200_n.jpg"><img class="alignnone size-medium wp-image-166" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/04/10407723_10152830083862585_5865610731164393200_n-300x225.jpg" alt="10407723_10152830083862585_5865610731164393200_n" width="300" height="225" /></a> <a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/04/11017707_10152827532882585_7659797378455912579_n.jpg"><img class="alignnone size-medium wp-image-167" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/04/11017707_10152827532882585_7659797378455912579_n-300x225.jpg" alt="11017707_10152827532882585_7659797378455912579_n" width="300" height="225" /></a>
