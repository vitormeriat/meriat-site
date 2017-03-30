---
layout: post
title: Windows Azure - PING, ICMP e conectividade na nuvem.
date: 2014-02-17 14:07:20.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure

---
<p><a href="http://blob.vitormeriat.com.br/images/2014/02/capa.png"><img title="capa" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="capa" src="http://blob.vitormeriat.com.br/images/2014/02/capa.png" width="540" height="269" /></a></p>
<p align="justify">Bom o lance é o seguinte: Um determinado cliente estava passando por um problema de latência em uma das aplicações rodando em um ambiente IaaS, era uma simples VM no Windows Azure. Após um checklist alguém teve a brilhante ideia de realizar um PING no servidor e…</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/02/0001.png"><img title="0001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="0001" src="http://blob.vitormeriat.com.br/images/2014/02/0001.png" width="560" height="196" /></a></p>
<p>Não preciso dizer qual foi a reação do cliente ao ver o resultado… ligações desesperadas, conclusões precipitadas, e-mails urgentes e&#160; lá vamos nós…</p>
<p><!--more-->
<p align="justify">Em fim, mesmo o PING não sendo “100% confiável” isso ocorre por um motivo e neste post vamos entender o por que e algumas técnicas para testes de conectividade envolvendo VMs no Windows Azure.</p>
<p>&#160;</p>
<h2>O PING</h2>
<p align="justify"><strong>PING</strong> ou <strong>P</strong>acket <strong>I</strong>nterNet <strong>G</strong>rouper é utilizado para medir quantos milissegundos (<strong>ms</strong>) um pacote de informações leva para ir até um destino e voltar. De forma simples, quanto menor o valor que ele retornar, mais rápida é sua conexão.</p>
<p align="justify">Sendo assim o <strong>PING</strong> - (<strong>procurador de pacotes na internet</strong>, em tradução livre) e trata-se de uma ferramenta fundamental para verificar se um computador está funcionando e se as conexões de rede (<strong>TCP/IP</strong>) encontram-se intactas.</p>
<p align="justify">Esta ferramenta verifica a conectividade de nível IP com outro computador TCP/IP através do envio de mensagens de solicitação de eco de protocolo <strong>ICMP</strong> (echo 8). A confirmação das mensagens de resposta é exibida juntamente com o tempo de ida e volta.</p>
<p>&#160;</p>
<h2>O problema</h2>
<p align="justify">O erro acima ocorre devido uma <strong>“limitação”</strong>, na verdade, se trata de um dos requisitos de segurança do Windows Azure, mas este é outro ponto.&#160; </p>
<p align="justify">Você não vai conseguir fazer um PING fora da Nuvem <strong>(Cloud Services)</strong>, a menos que você esteja utilizando o <strong>Windows Azure Connect </strong>(que vão vamos abordar aqui).</p>
<p align="justify">Isso ocorre devido a limitação no Load Balance do Azure não permite o tráfego de protocolos diferentes ou não baseados em <strong>TCP</strong>. PING em endereços externos a VMs no Azure não funcionam pois não há suporte a entrada ou saída ICMP (<strong>Internet Control Message Protocol</strong>), para Internet pois o tráfego é via <strong>Load Balance</strong>. </p>
<p>&#160;</p>
<h2>A solução</h2>
<p align="justify">Você conseguiria fazer isso sem problemas entre uma VM do Azure e o ambiente On-Premise utilizando o <strong>Windows Azure Connet</strong> (<strong>point-to-point IPSec VPN tunnel</strong>) ou <strong>Virtual Network Gateway</strong> (<strong>site-to-site IPSec VPN tunnel</strong>). Este não é nosso cenário então vamos a dica:</p>
<p align="justify">Como uma alternativa para o ping com ICMP, você pode verificar a conectividade, tentando chegar a uma porta TCP específica com ferramentas como <strong>TCPing</strong>, PortQuery ou NMap. Você consegue um ponto de entrada para uma VM no Azure, desde que você tenha aberto um EndPoint para a porta que você está tentando alcançar. Já com o <strong>Azure Connect </strong>e o <strong>Virtual Network </strong>você não precisa de um <strong>EndPoint</strong> específico, porque você vai estar se comunicando através de um túnel VPN.</p>
<p align="justify">Entre as opções disponíveis minha dica é utilizar o <strong>Psping</strong>. Com ele é possível testar a conectividade em uma porta específica. Um exemplo, caso a porta no EndPoint do RDP de acesso seja a 50799, você poderia realizar o teste com a seguinte linha de comando: <strong><u>C:&gt;psping meriat.cloudapp.net:50799</u></strong></p>
<p align="justify">Estou assumindo que você só precisa trocar para o seu <strong>DNS NAME</strong> e portas. Se o seu caso for o mesmo do meu, e você estiver testando um site hospedado na sua VM, basta colocar seu <strong>DNS</strong> padrão seguido da porta 80. <strong><u>C:&gt;psping seusite.com.br:80</u></strong></p>
<p>Sendo assim, vamos tentar um <strong>PING</strong> na aplicação <strong>xxx.cloudapp.net</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/02/000000001.png"><img title="000000001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="000000001" src="http://blob.vitormeriat.com.br/images/2014/02/000000001.png" width="540" height="151" /></a></p>
<p>Agora utilizando o Psping e apontando para a porta 80 como o sugerido acima:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/02/000000002.png"><img title="000000002" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="000000002" src="http://blob.vitormeriat.com.br/images/2014/02/000000002.png" width="540" height="254" /></a></p>
<p>&#160;</p>
<p align="justify">Você ainda pode utilizar comandos para a execução e monitoramento em intervalos de tempo fora outras funcionalidades especiais que você pode ver no site oficial.</p>
<p align="justify">Até esta data o Psping estava na versão 2.01 e pode ser baixado entre as utilidades no site do Windows Sysinternals <a href="http://technet.microsoft.com/en-us/sysinternals/jj729731.aspx" target="_blank">CLICANDO AQUI!!!</a></p>
<p>&#160;</p>
<h1><font color="#4bacc6">Até mais e bom estudo a todos!</font></h1>