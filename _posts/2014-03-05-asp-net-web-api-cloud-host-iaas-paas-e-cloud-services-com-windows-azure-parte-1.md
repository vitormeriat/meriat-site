---
layout: post
title: ASP.NET Web API - Cloud-Host, IaaS, PaaS e Cloud Services com Windows Azure.
  Parte 1
date: 2014-03-05 19:49:06.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure
- Services
- WebAPI

---
<p align="justify">Nos posts anteriores já tivemos a oportunidade de conhecer o ASP.NET Web API, seu poder, arquitetura e possibilidades. Agora chegou a hora de brincar um pouco e levar os nossos serviços ao cenário distribuído da Cloud Computing com Windows Azure. Neste post vamos dar uma olhada nos cenários, possibilidades e como implantar WebAPI no Windows Azure.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/03/capa.png"><u><font color="#444444"></font></u><img title="capa"   alt="capa" src="http://blob.vitormeriat.com.br/images/2014/03/capa.png" width="540" height="342" /></a></p>
<p><!--more-->
<p>Antes de continuar, para este post vou considerar que você já tem experiência com Windows Azure, já possui uma conta e já tem acesso ao portal de gestão do <strong>Azure</strong>. Estou considerando que você já tem conhecimento sobre <strong>ASP.NET Web API</strong> e já leu os três artigos anteriores sobre como consumir<strong> Web API</strong> em domínios diferentes utilizando <strong>CORS</strong>, <strong>AJAX</strong> e <strong>JSONP</strong>. Caso contrário, sugiro primeiro a leitura dos links abaixo antes de continuar:</p>
<ul>
<ul>
<li><a href="http://vitormeriat.com.br/2013/09/20/asp-net-web-api-criando-e-consumindo-dados-parte-1/" target="_blank">ASP.NET Web API – Criando e consumindo dados [Parte 1]</a> </li>
<li><a href="http://vitormeriat.com.br/2013/09/23/asp-net-web-api-criando-e-consumindo-dados-parte-2/" target="_blank">ASP.NET Web API – Criando e consumindo dados [Parte 2]</a> </li>
<li><a href="http://vitormeriat.com.br/2013/10/18/asp-net-web-api-criando-um-crud-e-consumindo-em-um-domnio-diferente-cors-ajax-e-jsonp-parte-1/" target="_blank">ASP.NET Web API – Criando um CRUD e consumindo em um domínio diferente. CORS, AJAX e JSONP [Parte 1]</a> </li>
<li><a href="http://vitormeriat.com.br/2013/10/24/asp-net-web-api-criando-um-crud-e-consumindo-em-um-domnio-diferente-cors-ajax-e-jsonp-parte-2/" target="_blank">ASP.NET Web API – Criando um CRUD e consumindo em um domínio diferente. CORS, AJAX e JSONP [Parte 2]</a> </li>
<li><a href="http://vitormeriat.com.br/2013/10/30/asp-net-web-api-criando-um-crud-e-consumindo-em-um-domnio-diferente-cors-ajax-e-jsonp-parte-3/" target="_blank">ASP.NET Web API – Criando um CRUD e consumindo em um domínio diferente. CORS, AJAX e JSONP [Parte 3]</a> </li>
</ul>
</ul>
<p align="justify">Basicamente, falar de <strong>Cloud-Host</strong> com <strong>WebAPI</strong>, é falar em hospedar nosso serviço na nuvem. Neste caso no <strong>Windows Azure</strong>.</p>
<p align="justify">O primeiro ponto é perceber existem diversas maneiras de hospedar um serviço no Windows Azure. Podemos utilizar um modelo <strong>Web-Hosting</strong> ou <strong>Self-Hosting</strong> bem como hospedar um ambiente <strong>IaaS</strong>, <strong>PaaS</strong> ou <strong>SaaS</strong>. Enfim, não vou abordar todos os cenários pois o importante é entender os conceitos antes de prosseguir. Para isso, segue uma pequena referência:</p>
<ul>
<ul>
<li><strong>Web-Hosting</strong> – Estilo de hospedagem utilizando o IIS. </li>
<li><strong>Self-Hosting</strong> – Hospedagem que utiliza de um processo Windows diferente do IIS. </li>
<li><strong>Cloud-Hosting</strong> – Estilo de hospedagem utilizando o Windows Azure. </li>
<li><strong>IaaS</strong> – Infraestrutura como serviço. </li>
<li><strong>SaaS</strong> – Software como serviço. </li>
<li><strong>PaaS</strong> – Plataforma como serviço. </li>
</ul>
</ul>
<p align="justify">&#160; <br />Apenas para exemplificar, poderiamos hospedar nosso serviço utilizando um modelo <strong>Self-Hosting</strong> com um <strong>Worker-Role</strong> em um <strong>Cloud Service</strong> ou rodando um aplicativo console dentro de uma <strong>VM</strong> do <strong>Windows Azure</strong>. É possível apenas criar nossa WebAPI utilizando o template base do Visual Studio e publicar diretamente para um Cloud Service ou utilizar uma estrutura <strong>SaaS</strong> com <strong>Azure Web Sites</strong>.</p>
<p align="justify">O importante neste ponto é conhecer o que cada modelo pode te proporcionar. Lembre-se, estamos falando de nuvem, logo a premissa que impera aqui é: &quot;<strong>Pague pelo que usar</strong>&quot;. Sendo assim procure enteder sua necessidade para montar a melhor solução possível.</p>
<p align="justify">O que vamos fazer noste post é prover nosso serviço, hospendando ele nos seguinte cenários:</p>
<ul>
<li>
<div align="justify">SaaS – Utilizando um Template Web API hospedado no Azure Web Sites, modelo Web-Hosting</div>
</li>
<li>
<div align="justify">IaaS – Utilizando um Console Aplication rodando em uma VM no Cloud Service, modelo Self-Hosting</div>
</li>
</ul>
<p align="justify">&#160;</p>
<p align="justify">Para acompanhar os exemplos você precisa baixar os dois projetos que utlizamos no post “ASP.NET Web API – Criando um CRUD e consumindo em um domínio diferente. CORS, AJAX e JSONP [Parte 3]” <a href="https://skydrive.live.com/?cid=BD055AA47A388023&amp;id=BD055AA47A388023!3718" target="_blank">CLICANDO AQUI!</a></p>
<p align="justify">&#160;</p>
<h2 align="justify">Cloud-Host com SaaS</h2>
<p align="justify">Acesse o portal de gestão do <strong>Windows Azure </strong>e clique na aba Web Sites. Ao em Web Sites, clique no <strong>+ NEW </strong>que fica no canto inferior esquerdo. Selecione a opção <strong>WEB SITE</strong>, <strong>QUICK CREATE</strong> e informe a <strong>URL</strong> e a <strong>região</strong> do site a ser criado. No meu exemplo estou utilizando <strong>WebApiServerSaaS</strong> (como já estou utilizando e são <strong>URIs </strong>então escolha uma diferente ok?).</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/01.png"><img title="01"  alt="01" src="http://blob.vitormeriat.com.br/images/2014/03/01.png" width="560" height="301" /></a></p>
<p align="justify">Clique em <strong>CREATE WEB SITE</strong> e pronto. Seu Web Site no Windows Azure utilizando <strong>SaaS</strong> está pronto e rodando. </p>
<p align="justify">Clique no Web Site recém criado e na aba <strong>DASHBOARD</strong> selecione a opção <strong>“Download the publish profile”</strong>. Com isso você vai realizar o download de um arquivo <strong>.PublishSettings</strong> que nada mais é que um <strong>XML </strong>contendo as informações do site e da conexão para utilizar o recurso <strong>“Publish Web”</strong> do Visual Studio.</p>
<p align="justify">Já no <strong>Visual Studio</strong>, clique com o botão direito sobre o projeto <strong>CloudHostingMunicipios</strong> e selecione a opção <strong>Publish…</strong></p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/02.png"><img title="02"  alt="02" src="http://blob.vitormeriat.com.br/images/2014/03/02.png" width="560" height="614" /></a></p>
<p align="justify">Na tela que se segue, selecione a aba <strong>Profile</strong> importe o arquivo <strong>.PublishSettings. </strong>Na aba <strong>Preview</strong> clique em <strong>Star Preview</strong>, apenas para visualizar se todos os arqvuivos necessários está sendo enviados, teste a conexão e pode clicar em <strong>Publish</strong>. Neste momento nosso serviço <strong>WebAPI</strong> está sendo publicado na estrutura <strong>SaaS</strong> do <strong>WebSites</strong> Azure.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/03.png"><img title="03"  alt="03" src="http://blob.vitormeriat.com.br/images/2014/03/03.png" width="560" height="443" /></a></p>
<p align="justify">Após publicado o site será aberto no seu browser. Bom, meu serviço está publicado em <a href="http://webapiservercors.azurewebsites.net/">http://webapiservercors.azurewebsites.net/</a> e ficou com a seguinte cara:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/04.png"><img title="04"  alt="04" src="http://blob.vitormeriat.com.br/images/2014/03/04.png" width="560" height="508" /></a></p>
<p align="justify">Fiz algumas adaptações de layout na tela principal porque vou deixar este exemplo rodando para que o pessoal possa testar.</p>
<p align="justify">Com já realizamos todo o tratamento em nosso serviço para que o mesmo possa trabalhar com domínios diferentes, basta apenas alterar em nosso <strong>Web API HTML Client</strong> trocando nas <strong>URLs</strong> o valor de <a title="http://localhost:56601/" href="http://localhost:56601/">http://localhost:56601/</a> por <a title="http://webapiserversaas.azurewebsites.net" href="http://webapiserversaas.azurewebsites.net/">http://webapiserversaas.azurewebsites.net/</a>. Como exemplo, o código script da<strong> index.html</strong> deve ficar como exibido abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/05.png"><img title="05"  alt="05" src="http://blob.vitormeriat.com.br/images/2014/03/05.png" width="560" height="418" /></a></p>
<p align="justify">Sendo assim, já estamos consumindo nosso serviço localmente. Como estamos utilizando <strong>CORS</strong> e <strong>JSONP</strong> este é o mesmo princípio dos posts anteriores. Não tem segredo, não precisa de configurações ou EndPoints adicionais. Estamos rodando tudo baseado em <strong>HTTP</strong>, de maneira simples e direta nosso serviço já está rodando em ambiente <strong>SaaS</strong> e pronto para ser consumido pela gama de clientes que forem necessários. Tenha em mente que não importa se estamos rodando local ou hospedado na nuvem, nosso serviço está pronto para fornercer os dados requiridos.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/06.png"><img title="06"  alt="06" src="http://blob.vitormeriat.com.br/images/2014/03/06.png" width="560" height="335" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">&#160;</p>
<h2 align="justify">Cloud-Host com IaaS</h2>
<p align="justify">Neste exemplo vamos utilizar um modelo Self-Hosting, onde vamos disponibilizar nosso serviço por meio de um Console Aplication rodando em uma VM no Windows Azure. Este é mais uma abordagem em que podemos utilizar o WebAPI para disponibilizar serviços.</p>
<p align="justify">Para continuar, baixe o projeto Console CLICANDO AQUI! Este projeto nada mais é que o serviço que já estamos utilizando adaptado para um projeto Console. Algumas observações:</p>
<p align="justify">Para esta implementação utilizei os mesmos passos do post xxx</p>
<p align="justify">Note que em </p>
<p align="justify">Agora vamos criar nossa VM para a hospedagem do nosso serviço. Selecione a opção de Virtual Machines no portal de gestão do Windows Azure, + NEW, VIRTUAL MACHINE e QUICK CREATE. Estou criando uma VM com Windows Server 2012 em uma instância Extra Small, mas sinta-se avontade para selecionar outra versão de Windows Server.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/003.png"><img title="003"  alt="003" src="http://blob.vitormeriat.com.br/images/2014/03/003.png" width="560" height="301" /></a></p>
<p align="justify">Para saber mais sobre Virtual Machines no Azure indico o seguinte link: <a href="http://www.windowsazure.com/en-us/documentation/services/virtual-machines/" target="_blank">VIRTUAL MACHINES!</a></p>
<p align="justify">Com nossa VM rodando, clique sobre ela e vá para a aba INSTANCES e na barra inferior clique em CONNECT. Será baixado um arquivo .rdp com o qual você pode se conectar remotamente a sua VM. </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/004.png"><img title="004"  alt="004" src="http://blob.vitormeriat.com.br/images/2014/03/004.png" width="560" height="324" /></a></p>
<p>&#160;</p>
<p>Para não estender muito, vamos realizar as outras configurações e a implantação do modelo IaaS com Self-Hosting na continuação deste POST.</p>
<p>No fim, vou publicar todo o código fonte utilizado neste séria para download no GitHub.</p>
<p>&#160;</p>
<h2><font color="#9bbb59"><font style="font-weight:bold;">Até mais e bom estudo a todos!</font></font></h2>
