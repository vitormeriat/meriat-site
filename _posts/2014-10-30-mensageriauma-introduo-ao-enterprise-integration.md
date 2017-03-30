---
layout: post
title: Mensageria–Uma introdução ao Enterprise Integration
date: 2014-10-30
categories:
  - Enterprise Integration
  - SOA
image: "http://blob.vitormeriat.com.br/images/2014/10/capa2.png"
---

<p><a href="http://blob.vitormeriat.com.br/images/2014/10/capa2.png"><img alt="capa" src="http://blob.vitormeriat.com.br/images/2014/10/capa.png" width="465" align="left" height="372" /></a></p>
<p align="justify">Primeiro vale notar qual a necessidade da mensageria. Hoje muito se fala em sistemas distribuídos, escaláveis, cloud computing e etc. O que nos leva a perceber que a cada dia temos mais sistemas e serviços sendo utilizados em massa, e que logicamente estes sistemas raramente são construídas de forma isolada.</p>
<p align="justify">O que temos visto é que a prática de mercado aponta para uma pluralidade de sistemas, o que por sua vez aponta para uma pluralidade de plataformas e linguagens. Neste post vamos iniciar os estudos sobre as técnicas de integração de sistemas (Enterprise Integration Patterns), iniciando pela mensageria.</p>
<p><!--more--><br />
<h2><strong>Um pouco de história</strong></h2>
<p align="justify">A ideia surge em 1983, quando o indiano Vivek Ranadivé, após seu MBA no MIT, teve a ideia de criar um barramento de software à semelhança do que acontece no barramento de comunicação entre a placa mãe e as demais placas de um PC. Para realizar sua ideia ele criou a empresa Teknekron e começou a desenvolver sua ideia com o TIB (<strong>The Information Bus</strong>). Em 1985 seu primeiro cliente foi a Goldman Sachs. O conceito teve ótima adoção nas empresas do mercado financeiro, o que levou a expansão do conceito para os demais mercados.
<p align="justify">O famoso TIP da Teknekron trabalhava no conceito <strong>publish-subscribe</strong> (<strong>PubSub</strong>), onde uma aplicação disponibiliza dados a serem consumidos por outras que subscrevem para ter acesso. O modelo foi um sucesso. Na época todo mundo usava COBOL mas as aplicações poderiam tratar os dados de forma diferente. Quem fazia o meio de campo era o tal TIB (<strong>The Information Bus</strong>).
<p align="justify">As empresas financeiras em geral usavam máquinas IBM para processar o espetacular software da Teknekron. A IBM não ganhava nada porém seus técnicos não ficaram só assistindo. Por volta de 1990 começaram a desenvolver algo do gênero, até que em 1993, lançaram o <strong>IBM MQseries</strong> (hoje Websphere MQ). Em 1997 foi a vez da Microsoft entrar neste mercado lançando a primeira versão do <strong>MSMQ</strong> (Microsoft Message Queue).
<p align="justify">O conceito <strong>PubSub</strong> hoje em dia é largamente utilizado por aplicações populares como <strong>Facebook</strong> e <strong>Twitter</strong>. Porém antigamente era coisa de rico. Os servidores <strong>MQs</strong> semelhantes ao TIB, foram durante muitos anos usados quase que exclusivamente por grandes empresas. Um dos principais motivos pela não popularização, foi o modelo vendor lock-in usado pelas empresas que comercializavam os <strong>MQs</strong>. A elas não interessava permitir interoperabilidade entre diferentes produtos e até dificultavam ao máximo uma eventual troca de fornecedor de <strong>MQ</strong>.
<p align="justify">Os próprios clientes reclamavam disso porque era comum ter que fazer um TIBCO MQ conversar com um IBM MQseries e era um verdadeiro parto... felizmente as coisas mudaram.&nbsp;
<p>&nbsp;</p>
<h2>Introdução</h2>
<p align="justify">Hoje porém é consenso que, a integração entre estas múltiplas aplicações é uma necessidade constante. O que precisa ser notado é que para se integrar um simples sistema temos de enfrentar alguns desafios:</p>
<ul>
<li>Redes não são 100% confiáveis;  </li>
<li>Redes são lentas ;  </li>
<li>Aplicações podem usar diferentes linguagens, operar em plataformas diferentes e tratar os dados de acordo com suas próprias necessidades;  </li>
<li>Mudanças são inevitáveis. Uma solução de integração deve minimizar dependências entre aplicações. O acoplamento entre elas deve ser tão baixo que mudanças em uma aplicação não implique em mudanças nas demais.</li>
</ul>
<p align="justify">O que se vê ao longo do amadurecimento das tecnologias de informação, foram diversas tentativas de vencer (ou amenizar) os desafios já citados por meio de algumas abordagens de comunicação entre aplicações distintas:</p>
<ol>
<li>
<div align="justify"><strong>Comunicação por transferência de arquivo</strong> – Quando uma determinada aplicação grava um arquivo em um lugar acordado e a outra lê e apaga após ler. O formato dos dados geralmente era um outro acordo; </div>
</li>
<li>
<div align="justify"><strong>Comunicação via armazenamento</strong> - Compartilhamento de uma base de dados; </div>
</li>
<li>
<div align="justify"><strong>Comunicação via RPC, Remote Procedure Call</strong> – Quando uma aplicação expõe as funcionalidades necessárias de modo a possibilitar o acesso remoto. Este tipo de comunicação é real time e síncrono, logo quem solicita algo ao serviço deve esperar a resposta; </div>
</li>
<li>
<div align="justify"><strong>Comunicação via Mensagens (ou mensageria)</strong> – Neste tipo de comunicação uma aplicação envia uma mensagem para um canal de acesso comum. Neste caso as demais aplicações vão efetuar a leitura quando quiserem, mediante contrato para determinação do canal e formato, bem como alguns detalhes que veremos mais detalhadamente. Geralmente este tipo de comunicação é assíncrona;</div>
</li>
</ol>
<p>&nbsp;</p>
<h2>Com tantas opções, porque falar só sobre mensageria? </h2>
<p align="justify">Vale notar que ao longo do tempo diversas técnicas foram implementadas, porém a mensageria acabou se tornando o padrão neste caso. Entre os vários motivos que veremos mais detalhadamente, a interoperabilidade, evolução dos protocolos e o consumo assíncrono são de longe as características que elevaram o status da mensageria em relação a integração de sistemas.</p>
<p>&nbsp;</p>
<h2>Então, o que é mensageria?</h2>
<p align="justify">Vamos considerar o seguinte cenário para a abstração: Uma chamada telefônica é uma forma de comunicação <strong>síncrona</strong> porque os dois lados precisam estar disponíveis ao mesmo tempo. </p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/10/fig1.png"><img alt="FIG1" src="http://blob.vitormeriat.com.br/images/2014/10/fig1.png" /></a></p>
<p align="justify">Já se um dos lados liga e deixa um recado de voz, esta mensagem pode ser ouvida e respondida conforme a disponibilidade do outro lado. Neste caso dizemos que houve uma comunicação <strong>assíncrona</strong>.</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/10/fig2.png"><img alt="FIG2" src="http://blob.vitormeriat.com.br/images/2014/10/fig2.png" /></a></p>
<blockquote><p align="left">Mensageria é uma tecnologia que permite comunicação de alta velocidade e de forma assíncrona entre sistemas diferentes com mensagens entregues de forma garantida.</p>
</blockquote>
<p align="justify">Os canais, também conhecidos como filas de mensagens (<strong>MQ = message queuing</strong>), são caminhos lógicos que conectam os sistemas. Eles se comportam como se fossem uma coleção de mensagens compartilhadas entre múltiplos computadores que podem ser acessados concorrentemente por múltiplas aplicações.</p>
<p align="justify">Quem envia a mensagem (escreve no canal) é o <strong>sender</strong> ou <strong>producer</strong> e o que recebe (lê o canal) é o <strong>receiver</strong> ou <strong>consumer</strong>. </p>
<blockquote><p>A mensagem em si é simplesmente algum tipo de dado.</p>
</blockquote>
<p align="justify">Normalmente a mensagem contém um cabeçalho (<strong>header</strong>) e o corpo propriamente dito (<strong>body</strong>). O header contém os <strong>metadados</strong> sobre a mensagem. O corpo contém os dados trocados e é ignorado pelo sistema de mensageria. No linguajar DEV, podemos dizer que a mensagem é o corpo.</p>
<p align="justify">&nbsp;</p>
<h2>O que é um sistema de mensageria?</h2>
<p align="justify">É o tal canal. Normalmente é um software que gerencia e coordena as mensagens enviadas e recebidas com a responsabilidade de não perder nenhuma. Em caso de falha, deve ser capaz de tentar novamente até conseguir (ou ocorrer uma intervenção externa). Conhecido em inglês por <strong>messaging system</strong> ou <strong>message-oriented middleware</strong> (MOM).</p>
<p>Entre os mais conhecidos e utilizados modelos de <strong>MOMs </strong>temos o <strong>MSMQ</strong> (Message Queuing), <strong>JMS</strong> (Java Message Service) e <strong>MQSeries</strong> (IBM WebSphere MQ). Estes veremos com mais detalhes em postagens futuras.</p>
<p>Uma mensagem é transmitida em 5 passos:</p>
<ol>
<li><strong>CREATE</strong> – o sender cria a mensagem e a preenche com dados;  </li>
<li><strong>SEND</strong> – o sender adiciona a mensagem ao canal;  </li>
<li><strong>DELIVER</strong> – o sistema de mensageria move a mensagem do computador do sender deixando disponível ao computador do receiver;  </li>
<li><strong>RECEIVE</strong> – o receiver lê a mensagem no canal;  </li>
<li><strong>PROCESS</strong> – o receiver extrai os dados da mensagem.</li>
</ol>
<p>Tudo de acordo com a figura abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/fig3.png"><img alt="FIG3" src="http://blob.vitormeriat.com.br/images/2014/10/fig3.png" /></a></p>
<p>Dois tipos importantes de envio de mensagens:</p>
<ol>
<li>
<div align="justify"><strong>Send and forget (ou fire and forget)</strong> – O sender cria e envia a mensagem em questão. Completado o envio, o sender assume outras tarefas confiando que o sistema de mensageria&nbsp; em algum momento entregará a mensagem ao receiver. </div>
</li>
<li>
<div align="justify"><strong>Store and forward</strong> - Ao enviar, o sender armazena em seu computador a mensagem (na memória ou no disco). O sistema de mensageria igualmente grava a mensagem no computador do receiver. Trocas de mensagens usando o processo Store-and-forward podem ser repetidas quantas vezes forem necessárias sem risco de existir em duplicata no receiver.</div>
</li>
</ol>
<p align="justify">&nbsp;</p>
<p align="justify">No próximo post vamos ver sobre os protocolos de mensageria mais conhecidos e praticados no mercado hoje.</p>
<p align="justify">&nbsp;</p>
<h2>Referências</h2>
<ul>
<li><a href="http://www.eaipatterns.com/Introduction.html" target="_blank">Gregor Hohpe - Enterprise Application Integration</a>  </li>
<li><font size="3"><font style="font-weight:normal;"><a href="http://pt.wikipedia.org/wiki/Message_Oriented_Middleware" target="_blank">Message Oriented Middleware</a></font></font>  </li>
<li><a title="http://www.eaipatterns.com/Introduction.html" href="http://www.eaipatterns.com/Introduction.html">http://www.eaipatterns.com/Introduction.html</a></li>
</ul>