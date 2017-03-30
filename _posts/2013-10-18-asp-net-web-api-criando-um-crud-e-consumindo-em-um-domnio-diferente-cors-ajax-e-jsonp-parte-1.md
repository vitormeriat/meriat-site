---
layout: post
title: ASP.NET Web API - Criando um CRUD e consumindo em um domínio diferente. CORS,
  AJAX e JSONP [Parte 1]
date: 2013-10-18 12:52:36.000000000 -03:00
type: post
published: true
status: publish
categories:
- Services
- WebAPI

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/capa01.png"><img title="capa01" alt="capa01" align="left" src="http://blob.vitormeriat.com.br/images/capa01.png" width="376" height="308" /></a>Se você também está utilizando WebAPI ou pretende utilizar em breve, e bem possível que você queira utilizar o mesmo em outras plataformas fora do .NET. Isso faz todo sentido, uma vez que o WebAPI expõe os métodos via HTTP e logo tem como maior benefício a possibilidade de ser consumido por um número maior de clientes. Neste post, vamos explorar este ponto criando uma solução WebAPI e como cliente um site HTML com JQuery.</p>
<p><!--more-->
<p>Cabe salientar alguns pontos:</p>
<ul>
<ul>
<li>Esta aplicação será utilizada nos próximos posts da série; </li>
<li>Vou utilizar o Visual Studio 2013RC, mas estou testando também no VS2012; </li>
<li>Este post será dividido em três partes a fim de facilitar o passo a passo. </li>
</ul>
</ul>
<p align="justify">Basicamente, vamos criar uma solução ASP.NET Web API expondo nosso serviço. Em outro projeto iremos criar uma solução cliente utilizando apenas HTML e JQuery para simular um cenário mais real possível. Com esta aplicação cliente, iremos fazer um CRUD completo, especializando algumas buscas. Todo o código fonte do post está disponível para download. Ai vai uma prévia do nosso cliente:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/000000.png"><img title="000000" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="000000" src="http://blob.vitormeriat.com.br/images/000000.png" width="560" height="351" /></a></p>
<p>&#160;</p>
<h2 align="justify">Criando o serviço </h2>
<p align="justify">O primeiro passo é criar nosso serviço. Vamos criar como exemplo um serviço para manter a lista de municípios brasileiros com código, uf e nome. Este exemplo também será utilizado nos próximos posts, então mãos a obra.</p>
<p align="justify">Abra o <strong>Visual Studio</strong> e selecione a opção <strong>New Project… ASP.NET Web Application </strong>e nomeie o seu projeto para <strong>CloudHostingMunicipios</strong> e clique em <strong>OK</strong>. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/001.png"><img title="001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="001" src="http://blob.vitormeriat.com.br/images/001.png" width="560" height="324" /></a></p>
<p align="justify">Na próxima tela selecione o <strong>template Web API</strong> e em <strong>Create Project</strong>. Agora vamos criar nosso modelo. Clique com o botão direito na pasta <strong>Models, Add e Class… </strong>Nomeie sua classe como <strong>Municipio.cs</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/003.png"><img title="003" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="003" src="http://blob.vitormeriat.com.br/images/003.png" width="560" height="324" /></a></p>
<p>Agora insira o seguinte código a sua classe:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/002.png"><img title="002" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="002" src="http://blob.vitormeriat.com.br/images/002.png" width="493" height="563" /></a></p>
<p align="justify">Nosso próximo passo é criar nosso repositório. Inicialmente eu planejei este post utilizando o <strong>Azure Table Storage</strong> para armazenar os dados, mas acabei decidindo por uma solução mais simples e independente para os testes. Sendo assim vamos trabalhar nossa fonte de dados em um arquivo txt. Para isso, vou disponibilizar o arquivo contendo todos os 5565 municípios brasileiros. Para prosseguir no post, você pode fazer o download do arquivo <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%213206" target="_blank">CLICANDO AQUI</a>. Após isso, adicione o arquivo na pasta Models para ser utilizado como nossa fonte de dados.</p>
<p align="justify">Agora, clique com o botão direito na pasta Models e insira uma classe chamada IMunicipiosRepository.cs. Esta classe deverá conter o seguinte código:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/004.png"><img title="004" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="004" src="http://blob.vitormeriat.com.br/images/004.png" width="560" height="509" /></a></p>
<p align="justify">Estamos determinando em nosso “<strong>contrato</strong>” os métodos que serão trabalhados no repositório. Basicamente vamos implementar um <strong>CRUD</strong>, onde o vamos ter um método especializado que busca apenas um município dado o seu código e um método que busca todos os municípios de uma determinada UF. Fora isso vamos realizar apenas um <strong>CRUD</strong>.</p>
<p align="justify">Com nosso <strong>contrato </strong>especificado, clique com o botão direito na pasta Models e crie uma nova classe intitulada <strong>MunicipiosRepository.cs</strong>. Assim que a classe for gerada, faça ela herdar de <strong>IMunicipiosRepository</strong>. Como vamos trabalhar com um arquivo físico hospedado em nosso site, insira o uma variável caminho para informar o caminho do arquivo dentro do servidor. Seu código deve ficar assim:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/005.png"><img title="005" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="005" src="http://blob.vitormeriat.com.br/images/005.png" width="560" height="209" /></a></p>
<p>Agora vamos aos métodos:</p>
<h3><font style="font-weight:bold;">ListAllMunicipios()</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/006.png"><img title="006" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="006" src="http://blob.vitormeriat.com.br/images/006.png" width="560" height="374" /></a></p>
<p>O método acima apenas lê todas a linhas do arquivo txt e devolve como uma lista de Munícipio. Antes do retorno estou aproveitando para ordenar por UF já que a lista não usa este critério.</p>
<h3><font style="font-weight:bold;">GetAll, GetByCodigo e GetByUF</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/007.png"><img title="007" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="007" src="http://blob.vitormeriat.com.br/images/007.png" width="560" height="406" /></a></p>
<p>Nos métodos acima, estamos apenas realizando buscas sobre nossa coleção de municípios.</p>
<h3><font style="font-weight:bold;">AddMunicipio()</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/008.png"><img title="008" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="008" src="http://blob.vitormeriat.com.br/images/008.png" width="560" height="366" /></a></p>
<h3><font style="font-weight:bold;">UpdateMunicipio()</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/009.png"><img title="009" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="009" src="http://blob.vitormeriat.com.br/images/009.png" width="556" height="635" /></a></p>
<h3><font style="font-weight:bold;">DeleteMunicipio()</font></h3>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/010.png"><img title="010" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="010" src="http://blob.vitormeriat.com.br/images/010.png" width="560" height="272" /></a></p>
<p>Com nossa classe de repositório já implementada, vamos criar nossa Controller. Clique com o botão direito na pasta <strong>Controllers, Add… e Web API Controller Class (v1)</strong>. Na tela que se segue nomeie o seu controller como <strong>MunicipioController</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/03.png"><img title="03" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="03" src="http://blob.vitormeriat.com.br/images/03.png" width="560" height="322" /></a></p>
<p>Substitua o código da controller pelo trecho de código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/011.png"><img title="011" alt="011" src="http://blob.vitormeriat.com.br/images/011.png" width="560" height="851" /></a></p>
<p>Observe que:</p>
<ul>
<li>Para as solicitações de <strong>POST, PUT e DELETE</strong> estamos retornando um <strong>StatusCode NotFound</strong> em caso de erro; </li>
<li>Para as solicitações <strong>PUT </strong>e<strong> DELETE </strong>estamos retornando um <strong>StatusCode OK</strong> em caso de sucesso; </li>
<li>Para a solicitação <strong>POST</strong> retornamos um <strong>StatusCode Created </strong>para sinalizar o sucesso da operação; </li>
<li>Os demais métodos retornam os objetos selecionados. </li>
</ul>
<p>&#160;</p>
<p>Neste momento já temos o nosso serviço funcional. É só executar a aplicação para testar.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/012.png"><img title="012" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="012" src="http://blob.vitormeriat.com.br/images/012.png" width="560" height="569" /></a></p>
<p>&#160;</p>
<p align="justify">No próximo post vamos criar nossa aplicação cliente apenas utilizando HTML e JQUERY para o consumo do serviço criado neste post. Também veremos algumas particularidades para do consumo de serviços entre domínios diferentes.</p>
<p align="justify">O código fonte do serviço pode ser baixado <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%213206" target="_blank">CLICANDO AQUI!</a></p>
<p>&#160;</p>
<h1>Até mais e bom estudo a todos!</h1>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" align="left" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" height="110" /></a></p>
<h3><font style="font-weight:bold;" color="#4f81bd"><font color="#9bbb59">Twitter:</font> </font><a href="http://twitter.com/#!/vitormeriat"><font style="font-weight:bold;" color="#4f81bd">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font style="font-weight:bold;" color="#4f81bd">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font style="font-weight:bold;" color="#4f81bd">vitor.pereira@studentpartner.com</font></a></h3>