---
layout: page
title: TDC 2014 Porto Alegre
date: 2014-10-19 05:33
author: jorgemaia
comments: true
categories: [.NET, ADO.NET, ASP, ASP.NET, Bar Code, Beacons, BLE, EF, Entyty Framework, Eventos, Internet das Coisas, IOT, IOT, LINQ2SQL, M2MQTT, MQTT, NFC, ORM, QRCODE, RFID, RSMB, TDC, tdc2014]
---
Nos dias 15 e 16 de outubro, estive em Porto Alegre para participar do The Developers Conference, um evento que agrupa diversas comunidades de desenvolvimento de software em um ambiente perfeitamente criado para troca de experiências e repasse de conhecimento. Quem nunca foi a um TDC, recomendo que fique atento ao <a href="http://www.thedevelopersconference.com.br" target="_blank">site</a> deles e faça sua inscrição no próximo, sem falta.

Participei em três trilhas, e recebi um excelente feedback de perguntas, conversas de corredores e interações durante as palestras que ministrei. Uma experiência que foi extremamente proveitosa!
<table border="0" width="400" cellspacing="0" cellpadding="2">
<tbody>
<tr>
<td valign="top" width="200"><a href="http://www.jorgemaia.com.br/wp-content/uploads/2014/10/WP_20141017_006-1.jpg"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="WP_20141017_006 1" src="http://www.jorgemaia.com.br/wp-content/uploads/2014/10/WP_20141017_006-1_thumb.jpg" alt="WP_20141017_006 1" width="277" height="331" border="0" /></a></td>
<td valign="top" width="200">
<table border="0" width="199" cellspacing="0" cellpadding="2">
<tbody>
<tr>
<td valign="top" width="199"><a href="http://www.jorgemaia.com.br/wp-content/uploads/2014/10/WP_20141016_004-1.jpg"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="WP_20141016_004 1" src="http://www.jorgemaia.com.br/wp-content/uploads/2014/10/WP_20141016_004-1_thumb.jpg" alt="WP_20141016_004 1" width="260" height="155" border="0" /></a></td>
</tr>
<tr>
<td valign="top" width="199"><a href="http://www.jorgemaia.com.br/wp-content/uploads/2014/10/WP_20141017_004-1.jpg"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="WP_20141017_004 1" src="http://www.jorgemaia.com.br/wp-content/uploads/2014/10/WP_20141017_004-1_thumb.jpg" alt="WP_20141017_004 1" width="260" height="155" border="0" /></a></td>
</tr>
</tbody>
</table>
</td>
</tr>
</tbody>
</table>
A Primeira trilha em que falei foi a de <a href="http://www.thedevelopersconference.com.br/tdc/2014/portoalegre/trilha-mobile" target="_blank">Mobile</a>,  coordenada pela @morvanabonin e pelo @jacksonfdam, um dia repleto de sessões extremamente interessantes. Apresentei no início da tarde sobre<strong> Near Field Communication</strong>, com o título: <strong>NFC – Uma nova Possibilidade</strong>, para as aplicações móveis,   demonstrei o que é possível se fazer com a tecnologia e aproveitei para fazer um comparativo entre <strong>RFID</strong>, <strong>BLE</strong> e  <strong>QRCode</strong>, como sempre passando a mensagem de que tecnologia deve ser usada somente para atender a um único objetivo, o de retornar valor para o cliente. Enquanto eu falava sobre tudo isso e também sobre pagamentos com <strong>NFC</strong> a <strong>Apple</strong> anunciava os parceiros e lojas que aceitarão sua solução de pagamentos. A sessão foi gravada e estará disponível em breve no <a href="http://www.infoq.com" target="_blank">InfoQ</a>. Prometi um vídeo sobre a criação de uma aplicação em <strong>Windows Phone</strong> e em <strong>Android</strong> para demonstrar o uso de uma tag, vou fazer em breve e colocarei em meu canal do <a href="http://www.youtube.com/user/jorgeSMaia" target="_blank">YouTube</a>.

<iframe src="//www.slideshare.net/slideshow/embed_code/40447075" width="476" height="400" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>

Fim do dia 15, foi hora de <strong>Internet das Coisas</strong>, trilha coordenada pelo @vsenger, nome mais que conhecido e reconhecido no munto #IoT no Brasil, e pela @desisant, e agora eu vim para falar sobre a comunicação dos dispositivos e apresentei sobre o tema : <strong>Comunicação entre dispositivos IoT e nuvem para aplicações inteligentes – Do Zero ao Produto</strong>. Quase uma hora e demonstrei como controlar um protótipo de sinal de trânsito a partir de qualquer cliente que possa emitir mensagens para um broker de <strong>MQTT</strong>. Para esta apresentação, utilizei um <strong>netduino</strong> e uma <strong>Worker Role</strong> no Azure para a camada de Broker rodando o <strong>RSMB</strong> da <strong>IBM</strong>, para o controle pelos usuários os mesmos o fizeram por meio de um WebSite armazenado também no <strong>Azure</strong>.

Desde usabilidade e definições de projeto, fizemos uma discussão extremamente rica sobre mensageria e limitação de banda, tamanho de mensagens emitidas pelo hardware e no final todos tiveram a possibilidade de controlar o sinal da forma que desejassem. Esta apresentação foi realmente muito proveitosa, pois o público era de alto nível e tivemos uma troca de experiências sensacional!

<iframe src="//www.slideshare.net/slideshow/embed_code/40447052" width="476" height="400" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>

No meu segundo dia de evento (dia 16) era hora de .<a href="http://www.thedevelopersconference.com.br/tdc/2014/portoalegre/trilha-dot-net">NET</a>, sob o comando do @andrecarlucci e do @cristianmathias, nesta seção falei sobre <strong>ORM</strong>, de onde viemos, passamos pelo bom e velho Visual <strong>Basic 6</strong> e <strong>ASP</strong> com seus <strong>Recordsets</strong> conectados, passando pelo início do <strong>ADO.NET</strong> com os <strong>Datasets</strong> tipados e suas tabelas e readers, <strong>ORM</strong>, <strong>LINQ2SQL</strong>, <strong>Entity Framework</strong> e culminamos na discussão de adoções de código no banco de dados com <strong>Stored Procedures</strong>, <strong>CTEs</strong>, <strong>Views</strong> e funções de <strong>TSQL</strong>. Uma discussão muito boa e de altíssimo nível.

<iframe src="//www.slideshare.net/slideshow/embed_code/40447086" width="476" height="400" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>

Me diverti bastante, fiz novos amigos e encontrei vários outros! Que venha o TDC 2015.
