---
layout: post
title: ASP.NET Web API - Criando e consumindo dados [Parte 1]
date: 2013-09-20 16:11:24.000000000 -03:00
type: post
published: true
status: publish
categories:
- C#
- Services

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/09/orchard-cms-and-asp-net-web-api.jpg"><img title="Orchard-CMS-and-ASP.NET-Web-API" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="Orchard-CMS-and-ASP.NET-Web-API" src="http://blob.vitormeriat.com.br/images/orchard-cms-and-asp-net-web-api.jpg" width="523" height="190" /></a>Bom, o ASP.NET Web API é um framwork que permite o desenvolvimento de serviços HTTP. Isso vem da necessidade cada vez mais crescente de arquiteturas orientadas a serviço . Sendo assim, o ASP.NET Web API tem como premissa tornar o desenvolvimento mas simples já encapsulando formatos como o JSON e XML que agora são nativos. Isso facilita e muito na ora de testar, consumir e manter, o tornando a plataforma ideal para o desenvolvimento de aplicativos RESTful no .NET Framework.</p>
<p><!--more-->
<p align="justify">A ideia por detraz do ASP.NET Web API é expor via HTTP serviço que serão consumidos e acessados de forma direto por vários dispositivos, como browsers e mobiles.</p>
<p align="justify">Sendo assim vamos para a nossa demo com os seguintes passos:</p>
<ol>
<ol>
<li>
<div align="justify">Criando um ASP.NET Web API </div>
</li>
<li>
<div align="justify">Criando um modelo de dados </div>
</li>
<li>
<div align="justify">Criando o repositório&#160; </div>
</li>
<li>
<div align="justify">Consumindo o serviço </div>
</li>
</ol>
</ol>
<p>&#160;</p>
<h2>Criando um ASP.NET Web API</h2>
<p>Inicie o Visual Studio 2012, crie um novo projeto e seleciono o template ASP.NET MVC 4 Web Application como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/011.png"><img title="01" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="01" src="http://blob.vitormeriat.com.br/images/01.png" width="560" height="348" /></a></p>
<p>&#160;</p>
<p>Logo após selecione o&#160; modelo WEB API e como View engine Razor.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/021.png"><img title="02" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="02" src="http://blob.vitormeriat.com.br/images/02.png" width="560" height="510" /></a></p>
<p>Note que ao criar um projeto ASP.NET Web API, diferentemente de um projeto MVC padrão, temos uma nova Controller, que representa os exemplos de uma aplicação Web API.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/001.png"><img title="001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="001" src="http://blob.vitormeriat.com.br/images/001.png" width="347" height="619" /></a></p>
<p align="justify">Neste exemplo não iremos utilizar esta Controller. Você pode excluir este arquivo pois iremos criar uma Web API Controller específica vinculada ao nosso Modelo de Dados.</p>
<p>&#160;</p>
<h2>Criando um modelo de dados</h2>
<p align="justify">O próximo passo é adicionar o modelo de dados. Clique com o botão direito na pasta Models e selecione a opção Add New Item e ADO.NET Entity Data Model.</p>
<p align="justify">Logo após, configure as propriedades de conexão. Para este exemplo estou utilizando o famoso Northwind (que pode ser encontrado facilmente), como nas imagens 4 e 5 logo abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/04-05.png"><img title="04-05" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="04-05" src="http://blob.vitormeriat.com.br/images/04-05.png" width="560" height="430" /></a></p>
<p>Na próxima tela clique em Next e selecione as tabelas Customers e Employees, caso você esteja usado o mesmo banco de dados do exemplo. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/07.png"><img title="07" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="07" src="http://blob.vitormeriat.com.br/images/07.png" width="560" height="497" /></a></p>
<p>&#160;</p>
<h2>Criando o Repositório</h2>
<p align="justify">Neste momento precisamos criar nosso repositório. Para isso vamos criar nossa <strong>interface</strong> do repositório para os <strong>Customers</strong>. Vamos criar esta interface com o nome de <strong>ICustomersRepository</strong>. É nessa interface que vamos definier todas as operações necessárias para a tabela <strong>Customers</strong>.</p>
<p align="justify">Clique com o botão direito sobre a pasta <strong>Models</strong>, onde já está o nosso modelo de dados, selecione <strong>Add</strong>, <strong>New Item</strong>, <strong>Interface</strong> e nomeie o arquivo como <strong>ICustomersRepository.</strong></p>
<p align="justify">Insira o seguinte código na em <strong>ICustomersRepository.</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/012.png"><img title="01" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="01" src="http://blob.vitormeriat.com.br/images/01.png" width="560" height="387" /></a></p>
<p align="justify">Agora vamos definier nossa <strong>ICustomersRepository</strong>. Para isso vamos criar uma classe <strong>CustomersRepository</strong> e implementar todos os métodos definidos em nossa <strong>interface</strong>. Clique com o botão direito sobre a pasta <strong>Models</strong>, <strong>Add</strong> e <strong>Class</strong>… Nomeie o arquivo como <strong>CustomersRepository</strong> e clique em OK.</p>
<p align="justify">Iclua o seguinte código ao <strong>CustomersRepository:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/022.png"><img title="02" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="02" src="http://blob.vitormeriat.com.br/images/02.png" width="560" height="252" /></a></p>
<p align="justify">Este código não compila, já que estamos herdando de <strong>ICustomerRepository</strong> mas ainda não implementamos os métodos definidos na interface. Adicione os seguintes trechos de código iniciando pelo <strong>GetAllCustomers</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/getall.png"><img title="getAll" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="getAll" src="http://blob.vitormeriat.com.br/images/getall.png" width="560" height="157" /></a></p>
<p><strong>GetCustomersById</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/getallbyid.png"><img title="getAllById" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="getAllById" src="http://blob.vitormeriat.com.br/images/getallbyid.png" width="560" height="198" /></a></p>
<p><strong>AddCustomer:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/add.png"><img title="add" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="add" src="http://blob.vitormeriat.com.br/images/add.png" width="560" height="294" /></a></p>
<p><strong>UpdateCustomer:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/update.png"><img title="update" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="update" src="http://blob.vitormeriat.com.br/images/update.png" width="560" height="461" /></a></p>
<p><strong>DeleteCustomer:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/delete.png"><img title="delete" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="delete" src="http://blob.vitormeriat.com.br/images/delete.png" width="560" height="461" /></a></p>
<p align="justify">Agora com nosso repositório já criado, vamos gerar nosso <strong>Controller</strong>. Clique com o botão direito sobre a pasta <strong>Controllers, Add </strong>e <strong>Controller</strong>… Nomeie como <strong>CustomerController</strong> utilizando o Template <strong>Empty MVC controller:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/03.png"><img title="03" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="03" src="http://blob.vitormeriat.com.br/images/03.png" width="560" height="371" /></a></p>
<p>No Controller gerado, realize as seguintes alterações: </p>
<ul>
<ul>
<li><font color="#555555">Inclua uma diretiva using System.Web.Http;</font> </li>
<li><font color="#555555">Substituir a herança padrão de Controller para ApiController;</font> </li>
<li>Crie a instância do repositório. </li>
</ul>
</ul>
<p><font color="#777777">Sua Controller deve ficar assim:</font></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/04.png"><img title="04" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="04" src="http://blob.vitormeriat.com.br/images/04.png" width="560" height="256" /></a></p>
<p align="justify">Vamos olhar o código para as operações a serem testadas e depois realizo as considerações necessárias. Vamos começar olhando o <strong>GetAllCustomers</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/0011.png"><img title="001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="001" src="http://blob.vitormeriat.com.br/images/001.png" width="560" height="144" /></a></p>
<p><strong>GetCustomersById</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/002.png"><img title="002" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="002" src="http://blob.vitormeriat.com.br/images/002.png" width="560" height="132" /></a></p>
<p><strong>PostCustomer</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/003.png"><img title="003" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="003" src="http://blob.vitormeriat.com.br/images/003.png" width="560" height="240" /></a></p>
<p><strong>PutCustomer</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/put.png"><img title="put"   alt="put" src="http://blob.vitormeriat.com.br/images/put.png" width="560" height="238" /></a></p>
<p><strong>DeleteCustomer</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/005.png"><img title="005" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="005" src="http://blob.vitormeriat.com.br/images/005.png" width="560" height="258" /></a></p>
<p align="justify">Nestes exato momento já temos o nosso <strong>ASP.NET Web API</strong> criado e com um <strong>CRUD</strong> implementado para a tabela <strong>Customer</strong> do banco de dados <strong>Northwind</strong>.</p>
<p align="justify">Bom, para testar nosso serviço, basta apenas rodar nossa aplicação. O que se segue neste caso e a página padrão do template MVC4. Como dito anteriormente, a grande sacada do ASP.NET Web API é disponibilizar o serviço via HTTP. Sendo assim, como estamos rodando localmente, para listar todos os nossos Customers bastaria apenas informar o seguinte endereço: <strong>localhost:porta/api/customer. </strong>Se optar por realizar uma pesquisa baseada no ID de um Customer o endereço é: <strong>localhost:porta/api/customer/?customerID=id.</strong></p>
<p align="justify">&#160;</p>
<h2>Como isso é possível?</h2>
<p><strong></strong></p>
<p align="justify">O HTTP possui alguns verbos, dentre os mais conhecidos temos o GET, POST, PUT e DELETE, onde cada um indica uma ação a ser executada. O ASP.NET Web API mapeia todos os verbos criados dentro da Conroller. Então quando ele recepciona uma requisição, a própria engine sabe qual método executar.</p>
<p align="justify">Para que isso ocorra é necessário comunicar a engine o que o nosso método faz. Para isso definimos no nome do método o verbo correspondente. <strong>GetAllCustomers, DeleteCustomer, PutCustomer. </strong>Também é possível decorar o método e utilzar um nome mais significativo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/013.png"><img title="01" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="01" src="http://blob.vitormeriat.com.br/images/01.png" width="539" height="168" /></a></p>
<p><font color="#777777"></font></p>
<p>O código fonte deste artigo pode ser baixada <a href="https://skydrive.live.com/?cid=BD055AA47A388023&amp;id=BD055AA47A388023%213193" target="_blank">CLICANDO AQUI&quot;</a></p>
<p>&#160;</p>
<h2>Conclusão</h2>
<p align="justify">No próximo post vamos explorar o passo 4 (Consumindo o Serviço), e analizar algumas das nuances e facilidades do uso desta tecnologia. Vou estar utilizando esta mesma estrutura para avaliar algumas particularidades do ASP.NET Web API implementando o mesmo CRUD para a tabela <strong>Employee</strong> que também mapeamos neste post.</p>
<p align="justify">Para os interessados em aprofundar o conhecimento, recomendo como leitua o exelente e-Book escrito pelo Israel Aece que pode ser baixado clicando aqui: <a href="http://www.israelaece.com/post/e-Book-Introducao-ao-ASPNET-Web-API.aspx">http://www.israelaece.com/post/e-Book-Introducao-ao-ASPNET-Web-API.aspx</a></p>
<p>&#160;</p>
<h2>Até mais e bom estudo a todos!</h2>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" align="left" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" height="110" /></a></p>
<h3><font style="font-weight:bold;" color="#4f81bd">Twitter: </font><a href="http://twitter.com/#!/vitormeriat"><font style="font-weight:bold;" color="#9bbb59">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font style="font-weight:bold;" color="#9bbb59">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font style="font-weight:bold;" color="#9bbb59">vitor.pereira@studentpartner.com</font></a></h3>