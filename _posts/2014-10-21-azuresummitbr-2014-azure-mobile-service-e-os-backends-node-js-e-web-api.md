---
layout: post
title: "#AzureSummitBR 2014 – Azure Mobile Service e os backends Node.JS e Web API"
date: 2014-10-21
categories:
  - Cloud Computing
  - Comunidade
  - Microsoft Azure
  - Mobile
  - Palestras

---
<p align="justify">Primeiro gostaria de agradecer a todos os que participaram desta palestra,&nbsp; e por todos&nbsp; os feedbacks. Como o prometido vou estar disponibilizando a DEMO principal, as referências e um vídeo de como criar o seu serviço e consumir o Jogo da Forca.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/10/03.jpg"><img title="03" alt="03" src="http://blob.vitormeriat.com.br/images/2014/10/03.jpg" /></a></p>
<p align="justify">O <a href="http://www.azuresummitbrasil.com.br/2014/" target="_blank">#AzureSummitBrasil</a> é o maior evento de Microsoft Azure do Brasil, organizado pela <a href="http://www.brsolucoesintegradas.com.br/" target="_blank">BR Soluções Integradas</a> e este ano rodou sua segunda edição. Para os que ainda não conheciam o evento, sugiro apenas que entre no site e leia a grade de palestras… é um evento realmente imperdível!!! </p>
<p>[youtube https://www.youtube.com/watch?v=17qUJ2jqxVk]
<p align="justify">&nbsp;</p>
<p align="justify">Em relação a minha palestra, a primeira demo foi o jogo <strong><u>TicTacToe MAMS</u></strong>, que é um jogo da velha com o <strong>backend</strong> no <strong>Microsoft Azure Mobile Service</strong> com <strong>Node.js</strong>. Basicamente você informa o nome do jogador, faz a sua jogada e o vencedor recebe uma pontuação randômica, que se for maior que a maior pontuação atual, envia uma notificação aos usuários indicando o novo campeão.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/capa.png"><img title="capa" alt="capa" src="http://blob.vitormeriat.com.br/images/2014/10/capa.png" /></a></p>
<p align="justify">A segunda demo foi o<u> <strong>Jogo da Forca MAMS</strong></u>. Este exemplo utilizou o <strong>backend .NET Web API</strong>, que faz basicamente o mesmo que o jogo anterior. Neste caso também demonstrei como forçar a utilização da autorização <strong>(IDENTITY)</strong>, e algumas possibilidades de utilização para armazenamento de dados, testes locais e publicações.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/capture.png"><img title="Capture" alt="Capture" src="http://blob.vitormeriat.com.br/images/2014/10/capture.png" /></a></p>
<p><!--more-->
<p align="justify">A última demo foi a criação de um <strong>SCHEDULER</strong> que utilizando a API do Twitter, fez a busca da hashtag oficial do evento (#azuresummitbr) e por fim fez o sorteio de valores únicos de um dos nomes da lista para um brinde especial.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/10/sorteio.png"><img title="sorteio" alt="sorteio" src="http://blob.vitormeriat.com.br/images/2014/10/sorteio.png" /></a></p>
<p align="justify">Em relação a palestra, o vídeo já está sendo editado e em breve será disponibilizado no canal do evento. Aqui neste post vou apenas colocar as demos cruas e alguns passos para que os que já trabalham com o <strong>MAMS</strong> possam rodar as APPs. </p>
<p align="justify">Já para aqueles que ainda não conheciam (ou conhecem) o MAMS, <u>vou estar gravando um vídeo</u> com os passos mais detalhadamente para uma inicialização ao serviço.</p>
<p>&nbsp;</p>
<h2>As&nbsp; Demos</h2>
<p>Primeiro faça o download do código fonte <a href="http://1drv.ms/1CQFrXp" target="_blank"><font size="4"><strong>clicando aqui!</strong></font></a></p>
<p align="justify">Agora estou levando em conta que você já tem uma subscription ativa do Microsoft Azure. Caso contrário<strong> </strong><a href="http://azure.microsoft.com/pt-br/" target="_blank"><strong>acesse esse link</strong></a>. Agora é só seguir os passos do vídeo e as referências logo abaixo para criar o seu Azure Mobile Service.</p>
<p>[youtube https://www.youtube.com/watch?v=2ZmR8-BFS6o]
<p>&nbsp;</p>
<p align="justify">Para os que sentiram falta do exemplo em Node.js, dado o número de dúvidas que surgiram decidi gravar um vídeo (ou série) sobre o assunto com mais detalhes. Sendo assim pretendo utilizar o jogo do TicTacToe para estas explicações. Também criar alguns exemplos com o <a href="http://xamarin.com/" target="_blank">Xamarin</a> dado o interesse da galera!!!&nbsp; <img class="wlEmoticon wlEmoticon-openmouthedsmile" style="border-style:none;" alt="Open-mouthed smile" src="http://blob.vitormeriat.com.br/images/wlemoticon-openmouthedsmile.png" /></p>
<h2 align="justify">Referências</h2>
<p align="justify"><a href="http://azure.microsoft.com/pt-br/documentation/articles/mobile-services-windows-store-javascript-get-started-users/" target="_blank">Introdução à autenticação nos Serviços Móveis</a></p>
<p align="justify"><a name="introduo-s-notificaes-por-push-nos-servios-mveis"></a><a href="http://azure.microsoft.com/pt-br/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-get-started-push/" target="_blank">Introdução às notificações por push nos Serviços Móveis</a></p>
<p align="justify">&nbsp;</p>
<p>Abaixo segue o PPT da apresentação que está disponível para download.</p>
<p>[slideshare id=40148994&w=700&h=395&style=margin-bottom: 5px; max-width: 100%; border-top: #ccc 1px solid; border-right: #ccc 1px solid; border-bottom: #ccc 1px solid; border-left: #ccc 1px solid&sc=no]
<div style="margin-bottom:5px;"><strong><a title="Azure Summit BR 2014 - Mobile Services - Adicione Servi&ccedil;os para suas Aplica&ccedil;&otilde;es Mobile" href="https://pt.slideshare.net/VitorMeriat/azure-summit-br-2014-mobile-services-adicione-servios-para-suas-aplicaes-mobile" target="_blank">#AzureSummitBR 2014 - Microsoft Azure Mobile Services</a> </strong></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h4><font color="#9bbb59">Bons estudos e até a próxima pessoal&nbsp; ;)</font></h4>