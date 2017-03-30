---
layout: post
title: ASP.NET Web API - Criando um CRUD e consumindo em um domínio diferente. CORS,
  AJAX e JSONP [Parte 2]
date: 2013-10-24 13:13:45.000000000 -02:00
type: post
published: true
status: publish
categories:
- Services
- WebAPI

---
<p align="justify">Neste post vamos conhecer alguns conceitos e entender o resultado de alguns testes bem como algumas limitações que nos levam ao uso de técnicas como CORS ou JSONP. Também vamos “tentar” consumir nosso serviço utilizando apenas <strong>HTML / JQuery</strong>, demonstrando como é possível realizar o consumo utilizando apenas código client side. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/capa.png"><img title="capa" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="capa" src="http://blob.vitormeriat.com.br/images/capa.png" width="560" height="196" /></a></p>
<p><!--more-->
<p>&#160;</p>
<p align="justify">Lembre-se, quando trabalhamos como WebAPI, estamos expondo dados via <strong>HTTP</strong>. Essa mecânica geralmente indica que nosso serviço vai ser utilizado por uma gama de diferentes clientes em potencial. Sendo assim, devemos entender algumas das nuances que envolvem o fornecimento e o consumo dentro deste cenário.</p>
<p align="justify">O cenário mais comum envolve a hospedagem do serviço em um determinado local (domínio) e o consumo do mesmo por clientes em locais (domínios) diferentes.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0081.png"><img title="008" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="008" src="http://blob.vitormeriat.com.br/images/008.png" width="485" height="540" /></a></p>
<p align="justify">Para consumir nosso serviço que está exposto via HTTP, vamos trabalhar com requisições assíncronas no Ajax. Nada de diferente do utilizado atualmente. </p>
<p align="justify">Para exemplificar o que já foi dito, utilize a aplicação que construímos no post passado. Clique com o botão direito sobre o projeto e adicione um arquivo HTML chamado <strong>index.html</strong>. Com o arquivo criado insira o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0061.png"><img title="006" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="006" src="http://blob.vitormeriat.com.br/images/006.png" width="560" height="671" /></a></p>
<p align="justify">Neste momento já estamos realizando a consulta dos dados utilizando Ajax. Note que estamos listando todos o Municípios lendo o retorno json de nossa requisição. O importante aqui é notar que nosso cliente (<strong>página HTML</strong>), está no mesmo domínio (<strong>localhost:56601</strong>) do serviço. Sendo assim estamos realizando o <strong>Request</strong> e <strong>Response </strong>de maneira transparente.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/000.png"><img title="000" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="000" src="http://blob.vitormeriat.com.br/images/000.png" width="560" height="565" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0031.png"><img title="003" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="003" src="http://blob.vitormeriat.com.br/images/003.png" width="560" height="497" /></a></p>
<p align="justify">Agora utilize este mesmo arquivo HTML abrindo ele localmente. Você vai receber um erro como o descrito abaixo de presente. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0021.png"><img title="002" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="002" src="http://blob.vitormeriat.com.br/images/002.png" width="513" height="427" /></a></p>
<p align="justify">Você pode pensar que o problema ocorre devido nossa página não estar hospedada em um servidor. OK, abra ela como uma projeto web site em uma nova instância do <strong>Visual Studio</strong>, ou crie na solução atual um novo projeto web e execute nosso exemplo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0011.png"><img title="001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="001" src="http://blob.vitormeriat.com.br/images/001.png" width="517" height="430" /></a></p>
<p align="justify">Este erro indica erro indicando que o solicitante não é tem permissão para fazer o pedido. Vamos ver se o <strong>Fiddler</strong> tem algo mais a nos dizer:</p>
<h3><font style="font-weight:bold;">localhost:56601</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0051.png"><img title="005" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="005" src="http://blob.vitormeriat.com.br/images/005.png" width="560" height="489" /></a></p>
<h3><font style="font-weight:bold;">localhost:61139</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0041.png"><img title="004" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="004" src="http://blob.vitormeriat.com.br/images/004.png" width="560" height="461" /></a></p>
<p align="justify">Repare que ambas as chamadas retornam o resultado consultado, porém na chamada para o domínio diferente (<strong>localhost:61139</strong>) , nós temos um <strong>“Origin: null”.</strong></p>
<p>&#160;</p>
<h2>Ajax</h2>
<p align="justify">Estamos utilizando Ajax pois este tem a capacidade de realizar solicitações HTTP assíncronas utilizando o objeto <strong>HMLHttpRequest</strong>, ou seja, enquanto nossos usuários estão utilizando nossa interface estamos realizando o acesso a dados em segungo plano. </p>
<p align="justify">Estou tocando neste ponto pois é parte do cenário mais atual, onde nossos sites e aplicativos consomem cada vez mais recursos remotos, como nosso exemplo. No entanto, é aqui que as coisas complicam um pouco, já que vimos não ser possível realizar estas solicitações sem violar a política de segurança imposta pelos navegadores.</p>
<p align="justify">Isto ocorre devido um conceito em linguagens de programação do lado do cliente/navegador (como <strong>JavaScript</strong>), que permite o acesso a recursos no mesmo local (<strong>mesmo domínio</strong>), mas impede o acesso a recursos em diferentes domínios. Isso pode parecer sem sentido mas é um salva-vidas para proteger as nossas aplicações web contra uma variedade de ataques maliciosos.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/0071.png"><img title="007" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="007" src="http://blob.vitormeriat.com.br/images/007.png" width="518" height="530" /></a></p>
<p align="justify">Mesmo assim você pode querer expor sua WebAPI para outros sites, agora espere um pouco, se temos esta limitação o que fazer? Para solucionar nosso problema, vamos apelar para duas soluções: <strong>JSONP e CORS</strong>.</p>
<p>&#160;</p>
<h2>JSONP (JSON with Padding)</h2>
<p align="justify">O JSONP nada mais é que um código javascript simples com <strong>prefixo</strong> que servirá de namespace para um objeto literal através de uma função. Ele aproveita que as tags <strong>&lt;script&gt;</strong> não sofrem restrição de domínio cruzado para solicitar o retorno dos dados dentro de uma nova tag <strong>&lt;script&gt;</strong>. Isto pode ser realizado utilizando o atributo src da tag para retornar um fluxo <strong>JSON</strong>. </p>
<p align="justify">Na verdade isso apenas inclui um monte de JSON em nossa página, o que não é muito útil se não for possível interagir com ele. É ai que entra o Padding. Pedimos para o servidor devolver nosso JSON em um wrapper (envolver) dentro de uma função utilizando callback.</p>
<p align="justify">Isso é muito bom, porém JSONP não trabalha com “os outros” verbos HTTP. Isso mesmo, apenas podemos utilizar JSONP para a realização de GET. Sendo assim vamos precisar implementar o CORS.</p>
<p>&#160;</p>
<h2>CORS (Cross Origin Resource Sharing)</h2>
<p align="justify"><strong>Cross-origin resource sharing</strong> (CORS) ou compartilhamento de recursos de origem cruzada, é o mecanismo que permite ao JavaScript de uma página web para fazer um <strong>XMLHttpRequests</strong> para um domínio diferente do domínio de origem.</p>
<p align="justify">Tais pedidos &quot;cross-domain&quot; seriam proibidas pelo navegador web, por conta da política de segurança de origem. CORS define uma forma em que o navegador e o servidor podem interagir para determinar se devem ou não permitir o pedido de origem cruzada.</p>
<p>&#160;</p>
<h2>Implementação</h2>
<p>Bom, vamos utilizar um simples site em HTML que está disponível para download <a href="sdrv.ms/HfUIf2" target="_blank">CLICANDO AQUI!</a></p>
<p>Nosso site possui a seguinte estrutura de páginas:</p>
<ul>
<ul>
<li><strong>index.html </strong>[Tela inicial, lista todos os municípios] </li>
<li><strong>getbyuf.html </strong>[Busca todos os municípios de uma determianda UF] </li>
<li><strong>getbycodigo.html </strong>[Busca o município dado seu Código] </li>
<li><strong>post.html </strong>[Cria um Município] </li>
<li><strong>put.html </strong>[Altera um Município] </li>
<li><strong>delete.html </strong>[Deleta um Município] </li>
</ul>
</ul>
<p>Eu optei por criar tudo na mão e depois abrir pelo Visual Studio como um Web Site, mas sinta-se livre para executar localmente ou publicar no IIS para os testes. Se você navegar no site vai ver que não temos ainda nenhuma interação com nosso serviço.&#160; </p>
<p>No próximo post vamos implementar nossa solução com as chamadas AJAX utilizando JSONP e CORS. Também vamos realizar algumas configurações em nosso serviço para tornar possível o consumo para os diversos clientes.</p>
<p>&#160;</p>
<h1><font color="#9bbb59">Até mais e bom estudo a todos!</font></h1>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" align="left" height="110" /></a></p>
<h3><font style="font-weight:bold;" color="#4f81bd"><font color="#9bbb59">Twitter:</font> </font><a href="http://twitter.com/#!/vitormeriat"><font style="font-weight:bold;" color="#4f81bd">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font style="font-weight:bold;" color="#4f81bd">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font style="font-weight:bold;" color="#4f81bd">vitor.pereira@studentpartner.com</font></a></h3>