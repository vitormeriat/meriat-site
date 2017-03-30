---
layout: post
title: Azure Mobile Service - Primeiros passos com backend .NET WebAPI
date: 2014-08-12 18:54:30.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure
- Mobile

---
<p>O <strong>M</strong>icrosoft <strong>A</strong>zure <strong>M</strong>obile <strong>S</strong>ervice <strong>(MAMS)</strong> é um serviço que oferece backend escalável, seguro e multiplataforma, e teve como origem o <strong>NodeJS </strong>para backend server-side. Um dos pontos mais interessantes do MAMS é a capacidade de dar ao programador o poder de customizar e adicionar lógica ao backend.</p>
<p>A ideia neste post é trazer uma primeira visão sobre o <strong>Microsoft Azure Mobile Service</strong> com backend<strong> .NET</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig015.png"><img title="FIG015"  alt="FIG015" src="http://blob.vitormeriat.com.br/images/2014/08/fig015.png" width="700" height="313" /></a></p>
<p align="justify">Assim que a Microsoft anunciou o backend <strong>.NET</strong> para o <strong>MAMS,</strong> ouve uma&#160; grande aceitação da comunidade, principalmente dos desenvolvedores <strong>.NET</strong>.</p>
<p align="justify">Minha primeira impressão em relação ao backend <strong>.NET</strong> era que isso se dava apenas pela falta de familiaridade dos desenvolvedores .NET com o código JavaScript server-side, e tiro isso por mim, porém isto não é de todo verdade<strong>…</strong></p>
<p><!--more-->
<p align="justify">O novo backend .NET te traz mais poder de customização em relação ao NodeJS, porém como diria o tio Ben Parker, grandes poderes trazem grandes responsabilidades. Sendo assim o poder de customização também traz consigo a necessidade de um arcabouço de conhecimentos&#160; que muitas vezes não fazem parte de quem está trabalhando com APPs: WebAPI, Self Hosting, Injeção de Dependência, Entity Framework etc...</p>
<p>&#160;</p>
<h2>Principais Diferenças entre o backend .NET e o backend JavaScript</h2>
<ul>
<li>Você precisa definir suas tabelas e data-model usando Code First </li>
<li>O backend .NET usa Web API 2. Actions e Controller Methods </li>
<li>Você tem que definir as permissões de acesso para os métodos </li>
<li>Alterações no modelo de dados devem ser propagadas usando Entity Framework Code First Migrations </li>
<li>A forma padrão para enviar notificações push é utiliznado o Notification hub </li>
</ul>
<p>&#160;</p>
<h2>Diferenças no portal de gestão do Microsoft Azure Mobile Service</h2>
<p align="justify">O primeiro passo é acessar o poral de gestão do Microsoft Azure. No exemplo abaixo estou acessando a área de Mobile Service e exibindo os menus de dois serviços diferentes.&#160; O primeiro com <u>backend .NET</u> chamado <strong>meriatwebapi</strong> e o segundo com o <u>backend NodeJS</u> chamado <strong>meriatnodejs</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig011.png"><img title="FIG01"  alt="FIG01" src="http://blob.vitormeriat.com.br/images/2014/08/fig01.png" width="700" height="308" /></a></p>
<p>Apenas de olhar já conseguimos ver algumas mudanças: As opções <strong>DATA</strong> e <strong>API</strong> não estão disponíveis para o backend .NET. Existem ainda algumas diferenças internas que podemos ver acessando os itens específicos do menu. São eles:</p>
<p><strong><font size="4">PUSH</font></strong></p>
<p>Agora por padrão é criado um <strong>Notification Hub</strong> para o backend .NET. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig021.png"><img title="FIG02"  alt="FIG02" src="http://blob.vitormeriat.com.br/images/2014/08/fig02.png" width="700" height="475" /></a></p>
<p align="justify">Já para o ambiente JavaScript precisamos habilitar o <strong>&quot;Enhanced Push&quot;</strong> para o mesmo cenário. Lembrando que isso vale para os serviços já criados.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig031.png"><img title="FIG03"  alt="FIG03" src="http://blob.vitormeriat.com.br/images/2014/08/fig03.png" width="700" height="529" /></a></p>
<p>&#160;</p>
<p><font size="4"><strong>CONFIGURE</strong></font></p>
<p align="justify">Note que na sessão Source Control não temos as seguinte opções em .NET</p>
<ul>
<li>
<div align="justify">Dynamic Schema </div>
</li>
<li>
<div align="justify">Cross-Origin Resource Sharing (CORS) </div>
</li>
</ul>
<p align="justify">Em NodeJS é uma boa prática utilizar o GIT para gerenciar os scripts, o que é desnecessário no caso do backend .NET onde o serviço é compilado. A vantagem do NodeJS é que por ser interpretado podemos ter as alteração publicadas de maneira mais simples.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig05.png"><img title="FIG05"  alt="FIG05" src="http://blob.vitormeriat.com.br/images/2014/08/fig05.png" width="700" height="915" /></a></p>
<p align="justify">Também não temos a opção de <strong>dynamic schema</strong>, que por sinal é algo muito bom no NodeJS, onde é possível forçar que o esquema do Banco de Dados se ajuste utilizando como modelo o JSON do request para operações de inserçao ou alteração. Em .NET trabalhamos com WebAPI e controllers fortemente tipados.</p>
<p align="justify">No backend .NET o controle de CORS é feito programaticamente seguindo o modelo do WebAPI, logo também tornou-se desnecessária.</p>
<p>&#160;</p>
<h2>Criando um serviço com backend .NET</h2>
<p align="justify">Vamos dar uma olhada na estrutura do projeto padrão. Para isso acesse o portal do Microsoft Azure e crie seu mobile service com backend .NET. É muito simples, basta clicar na opção <strong>+ NEW</strong>, selecionar <strong>COMPUTE</strong>, <strong>MOBILE SERVICE</strong> e clique em <strong>CREATE</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig06.png"><img title="FIG06"  alt="FIG06" src="http://blob.vitormeriat.com.br/images/2014/08/fig06.png" width="700" height="255" /></a></p>
<p align="justify">Na tela que se segue informe o <strong>Nome/URL</strong> do serviço, o <strong>Database</strong> que pode ser um existente, uma nova instância de SQL ou uma opção FREE e compartilhada de 20MB. Selecione também a <strong>Região/Datacenter</strong> e é claro, como <strong>BACKEND</strong> a opção <strong>.NET </strong>e<strong> </strong>vá para o próximo passo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig07.png"><img title="FIG07"  alt="FIG07" src="http://blob.vitormeriat.com.br/images/2014/08/fig07.png" width="700" height="543" /></a></p>
<p align="justify">No próximo passo é a área de Database Settings, onde você vai fornercer as configurações para o novo banco ou apenas informar a senha de um banco já existente. Para mais informações sobre a criação de Serviços no Azure Mobile Services vide referências.</p>
<p>&#160;</p>
<h2>Estrutura do projeto</h2>
<p align="justify">Existem dois caminhos para analisarmos a estrutura de um projeto Windows Azure Mobile Service: Baixando a aplicação atravéz do portal ou criando via Visual Studio.</p>
<p align="justify">Para baixar um exemplo do projeto funcional via portal Azure é só acessar o seu projeto <strong>MOBILE SERVICE</strong> e&#160; clicar na <strong>NUVENZINHA</strong>, expandir a opção <strong>CREATE A NEW WINDOWS STORE APP</strong> (pode ser qualquer cliente mas neste exemplo estou utilizando esta opção), e selecionar a linguagem da aplicação. Isso não afeta o serviço que é WEB API.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig08.png"><img title="FIG08"  alt="FIG08" src="http://blob.vitormeriat.com.br/images/2014/08/fig08.png" width="700" height="677" /></a></p>
<p>Para criar um novo projeto via Visual Studio, é só acessar o <strong>VS2013 Update 2</strong>, selecionar a linguagem, menu Cloud, selecionar o <strong>.NET Framework 4.5.1</strong> e o template Windows Azure Mobile Service como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig09.png"><img title="FIG09"  alt="FIG09" src="http://blob.vitormeriat.com.br/images/2014/08/fig09.png" width="700" height="446" /></a></p>
<p>A próxima tela é apenas de aceite…&#160; até o presente momento as outras opções são apenas de leitura.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig010.png"><img title="FIG010"  alt="FIG010" src="http://blob.vitormeriat.com.br/images/2014/08/fig010.png" width="700" height="524" /></a></p>
<p>A estrutura final do projeto será como se segue na abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig0111.png"><img title="FIG011"  alt="FIG011" src="http://blob.vitormeriat.com.br/images/2014/08/fig011.png" width="700" height="427" /></a></p>
<p>Note que eu estou apontando as pastas que foram criadas por padrão no template. Vou estar abordando resumidamente cada uma, bem como sua ligação com o modelo NodeJS.</p>
<p>&#160;</p>
<p><font size="5"><strong>DataObjects</strong></font></p>
<p>Aqui temos uma classe de exemplo <strong>&quot;TodoItem.cs&quot;</strong> com apenas duas propriedades:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod01.png"><img title="COD01"  alt="COD01" src="http://blob.vitormeriat.com.br/images/2014/08/cod01.png" width="700" height="498" /></a></p>
<p align="justify">Você vai notar no entanto, que não é apenas um POCO, ele realmente tem uma classe base <strong>&quot;EntityData&quot;</strong>, que é uma implementação abstrata de <strong>“Tables.ITableData&quot;. </strong>Este cara é responsável pela representação do modelo base:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod02.png"><img title="COD02"  alt="COD02" src="http://blob.vitormeriat.com.br/images/2014/08/cod02.png" width="700" height="626" /></a></p>
<p>&#160;</p>
<p><font size="5"><strong>Models</strong></font></p>
<p align="justify">Por padrão nosso <strong>&quot;serviçoContext.cs&quot;</strong> (no meu caso meriatwebapiContext) é criado com um Entity Framework DbContext padrão.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod03.png"><img title="COD03"  alt="COD03" src="http://blob.vitormeriat.com.br/images/2014/08/cod03.png" width="700" height="695" /></a></p>
<p>&#160;</p>
<p><font size="5"><strong>Controllers</strong></font></p>
<p align="justify">O controlador implementa a classe base <strong>“TableController&lt;T&gt;”</strong> que se derivada de <strong>TableController</strong> e <strong>ApiController</strong>. O <strong>EntityDomainManager</strong> é responsável por gerenciar o acesso ao contexto de banco de dados do EF.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod04.png"><img title="COD04"  alt="COD04" src="http://blob.vitormeriat.com.br/images/2014/08/cod04.png" width="700" height="929" /></a></p>
<p>&#160;</p>
<p><strong><font size="5">App_Start</font></strong></p>
<p align="justify">O “<strong>WebApiConfig”</strong> contém o código para iniciar o serviço Web API e Entity Framework. Aqui temos uma classe <strong>seuserviço<u>Initialiser</u></strong> criada por padrão apontando para o contexto original e que herda de <strong>DropCreateDatabaseIfModelChanges&lt;T&gt;</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod05.png"><img title="COD05"  alt="COD05" src="http://blob.vitormeriat.com.br/images/2014/08/cod05.png" width="700" height="793" /></a></p>
<p>&#160;</p>
<p><font size="5"><strong>Scheduled Jobs</strong></font></p>
<p align="justify">A classe <strong>'SampleJob'</strong> traz um exemplo de como criar <strong>JOBs</strong> para serem executados sob demanda ou agendados. É importante citar que esta classe não é um componente do WebAPI porém deriva de um controller.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod06.png"><img title="COD06"  alt="COD06" src="http://blob.vitormeriat.com.br/images/2014/08/cod06.png" width="700" height="416" /></a></p>
<p>Aqui temos nosso esqueleto do <strong>ScheduleJob</strong>, que deriva de um <strong>JobsController</strong> e não de uma <strong>ApiController</strong> padrão. Mesmo assim ele é chamado através de uma solicitação <strong>POST</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/cod07.png"><img title="COD07"  alt="COD07" src="http://blob.vitormeriat.com.br/images/2014/08/cod07.png" width="700" height="713" /></a></p>
<p>&#160;</p>
<h2>Rodando localmente</h2>
<p align="justify">Um dos benefícios do backend .NET é a capacidade de rodar e testar seu serviço e o armazenamento localmente, só dependendo do deploy da aplicação.</p>
<p align="justify">Vamos utilizar o projeto que criamos acima para testar nosso serviço modelo criado por padrão no template da aplicação,&#160; simplesmente apertando o famoso <strong>F5</strong>. Abaixo segue o exemplo do serviço rodando localmente:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig012.png"><img title="FIG012"  alt="FIG012" src="http://blob.vitormeriat.com.br/images/2014/08/fig012.png" width="700" height="671" /></a></p>
<p align="justify">Note que na tela inicial temos um help. É só acessar o link <strong><u>try it out</u></strong>. A tela abaixo mostra o exemplo do help que traz uma mini-documentação de como utilizar o serviço:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig013.png"><img title="FIG013"  alt="FIG013" src="http://blob.vitormeriat.com.br/images/2014/08/fig013.png" width="700" height="490" /></a></p>
<p align="justify">Como vimos no acima, podemos utilizar o GET para obter o retorno JSON do nosso serviço.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/fig014.png"><img title="FIG014"  alt="FIG014" src="http://blob.vitormeriat.com.br/images/2014/08/fig014.png" width="700" height="98" /></a></p>
<p>&#160;</p>
<h2>E a IDE?</h2>
<p align="justify">Do lado do Visual Studio temos muito mais do que apenas diferinciar os serviços pelos ícones. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/code23.png"><img title="code23"  alt="code23" src="http://blob.vitormeriat.com.br/images/2014/08/code23.png" width="700" height="219" /></a></p>
<p align="justify">Temos duas opções ótimas e simples de utilizar: <strong>Attach Debugger</strong> e <strong>View Logs.</strong> Vou abordar com mais detalhes sobre estes itens nos próximos posts.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/code21.png"><img title="code21"  alt="code21" src="http://blob.vitormeriat.com.br/images/2014/08/code21.png" width="700" height="324" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/08/code22.png"><img title="code22"  alt="code22" src="http://blob.vitormeriat.com.br/images/2014/08/code22.png" width="700" height="326" /></a></p>
<p>&#160;</p>
<h2>Referências:</h2>
<p><a title="http://azure.microsoft.com/blog/2014/07/28/azure-mobile-services-net-updates/" href="http://azure.microsoft.com/blog/2014/07/28/azure-mobile-services-net-updates/">http://azure.microsoft.com/blog/2014/07/28/azure-mobile-services-net-updates/</a></p>
<p><a title="http://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn629482.aspx" href="http://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn629482.aspx">http://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn629482.aspx</a></p>
<h4></h4>
<h2><font color="#ffc000">Bons estudos e até a próxima pessoal&#160; ;)</font></h2>