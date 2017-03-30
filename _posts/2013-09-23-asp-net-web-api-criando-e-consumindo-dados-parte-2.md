---
layout: post
title: ASP.NET Web API – Criando e consumindo dados [Parte 2]
date: 2013-09-23 16:06:40.000000000 -03:00
type: post
published: true
status: publish
categories:
- Services

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/09/gg_mobile_japon.jpg"><img title="gg_mobile_japon" style="background-image:none;float:left;padding-top:0;padding-left:0;margin:0 15px 0 0;display:inline;padding-right:0;border-width:0;"   alt="gg_mobile_japon" align="left" src="http://blob.vitormeriat.com.br/images/gg_mobile_japon.jpg" width="390" height="225" /></a>Nesta segunda parte do artigo vamos focar no consumo do serviço bem como em enteder algumas das nuances que fazem do ASP.NET Web API uma tecnologia com inúmeras possibilidades dentro do cenário atual.</p>
<p><!--more-->
<p align="justify">Agora vamos criar uma aplicação console para consumir o serviço que criamos no <a href="http://vitormeriat.com.br/2013/09/20/asp-net-web-api-criando-e-consumindo-dados-parte-1/" target="_blank">post anterior.</a> O código fonte está disponível no fim do post.</p>
<p align="justify">Crie um novo projeto <strong>Console Application.</strong> Neste exemplo estou nomeando como <strong>AspNetWebApiCliente</strong>. É válido salientar que estou utilizando o <strong>Visual Studio 2013 RC, </strong>mas já realizei o mesmo teste no <strong>Visual Studio 2012 </strong>seguindo exatamente os mesmos passos.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/0012.png"><img title="001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="001" src="http://blob.vitormeriat.com.br/images/001.png" width="560" height="324" /></a></p>
<p>Clique com o botão direito sobre o projeto recém criado e selecione <strong>Manage NuGet Packeges…</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/0021.png"><img title="002" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="002" src="http://blob.vitormeriat.com.br/images/002.png" width="480" height="323" /></a></p>
<p align="justify">Na tela que se segue selecione a opção para os pacotes Online e pesquise por <strong>Microsoft ASP.NET Web API Client Libaries</strong>. Realize a instalação e vamos estar prontos para realizar nossos testes.</p>
<p align="justify">O próximo passo é adicionar os seguintes <strong>namespaces</strong>:</p>
<ul>
<ul>
<li><strong>using System.Net.Http;</strong> </li>
<li><strong>using System.Net.Http.Headers;</strong> </li>
</ul>
</ul>
<p align="justify">Agora precisamos iniciar o cliente <strong>HTTP</strong>, definir o endereço base para o consumo e definir o cabeçalho da requisição para retorno como <strong>JSON</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/041.png"><img title="04" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="04" src="http://blob.vitormeriat.com.br/images/04.png" width="560" height="178" /></a></p>
<p align="justify">Vamos criar nossa classe de <strong>Customer</strong> para a representação do objeto no lado do cliente. Sendo assim certifique-se que a definição da classe é a mesma que a do lado o servidor. Clique com o botão direito sobre o projeto, <strong>Add</strong> e <strong>Class… </strong>Crie uma classe chamada<strong> Customer</strong>. E insira o seguinte trecho de código:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/06.png"><img title="06" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="06" src="http://blob.vitormeriat.com.br/images/06.png" width="508" height="612" /></a></p>
<p align="justify">Se esta é a primeira vez que você usou ou olhou um código no <strong>Visual Studio 2013 RC </strong>e está estranhando este “<strong>0 references</strong>”, fique tranquilo que já preparei um post para esplicar este recurso que é algo bem interessante. Mas vamos em frente…</p>
<p align="justify">&#160;</p>
<h2 align="justify">Buscando todos os Customers (HTTP GET)</h2>
<p align="justify">Nosso primeiro método vai listar todos os <strong>Customers</strong>, ler o serviço e exibir na tela o resultado. Para isso estamos buscando os registros utilizando o método <strong>GetAsync</strong> da classe <strong>HttpClient</strong> passando como parâmetro a entidade a ser pesquisada. Após buscar os registros com sucesso, vamos realizar a leitura dos dados em formato <strong>JSON </strong>usando o método <strong>Conent.ReadAsAsync()</strong> da classe <strong>HttpResponseMessage</strong>. Como no código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/071.png"><img title="07" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="07" src="http://blob.vitormeriat.com.br/images/07.png" width="560" height="252" /></a></p>
<p>segue o resultado:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/getall1.png"><img title="getall" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="getall" src="http://blob.vitormeriat.com.br/images/getall.png" width="560" height="594" /></a></p>
<p><strong>OBS:</strong> Alguém já viu alguma família Arquibaldo por aqui no Brasil??? kkk</p>
<p>&#160;</p>
<h2>Inserindo um Customer (HTTP POST)</h2>
<p align="justify">Para inserir um registro, que no nosso caso será um customer, precisamos criar o <strong>Customer</strong> a ser inserido e executar o método <strong>PostAsJsonAsync</strong> da classe <strong>HttpClient</strong> passando nosso objeto <strong>Customer</strong> como parâmetro. Caso tudo tenha ocorrido com sucesso exibimos o código e o status correspondente.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/08.png"><img title="08" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="08" src="http://blob.vitormeriat.com.br/images/08.png" width="560" height="310" /></a></p>
<p>Segue o resultado:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/created.png"><img title="created" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="created" src="http://blob.vitormeriat.com.br/images/created.png" width="560" height="219" /></a></p>
<p>Se pesquisarmos pelo nosso ID diretamente no browser vamos ter o xml de retorno como abaixo: </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/10.png"><img title="10" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="10" src="http://blob.vitormeriat.com.br/images/10.png" width="560" height="259" /></a></p>
<p>&#160;</p>
<h2>Alterando um Customer (HTTP PUT)</h2>
<p>Para alterar um registro iremos utilizar a mesma lógica da inserção só que utilizando o método <strong>PutAsJsonAsync</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/update1.png"><img title="update" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="update" src="http://blob.vitormeriat.com.br/images/update.png" width="560" height="340" /></a></p>
<p>Segue o resultado :</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/13.png"><img title="13" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="13" src="http://blob.vitormeriat.com.br/images/13.png" width="549" height="204" /></a></p>
<p>Ao pesquisarmos novamente vamos ter o seguinte retorno:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/11.png"><img title="11" alt="11" src="http://blob.vitormeriat.com.br/images/11.png" width="560" height="258" /></a></p>
<p>&#160;</p>
<h2>Excluindo um Customer (HTTP DELETE)</h2>
<p align="justify">Para excluir um customer é só utilizar o método DeleteAsync passando como parâmetro a URI do recurso a ser excluído:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/delete1.png"><img title="delete" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="delete" src="http://blob.vitormeriat.com.br/images/delete.png" width="560" height="198" /></a></p>
<p align="justify">Se a sua entidade tiver um ID com valor inteiro, basta apenas informar a URI como se segue: “<strong>customerID/1</strong>”.&#160; Isso por conta da engine de roteamento. Ela procura dentro do controller os métodos correspondentes e verifica o parâmetro esperado.</p>
<p align="justify">O resultado retornado como Status vai ser um <strong>200 (OK)</strong>. Sendo assim acabamos de excluir nosso registro.</p>
<p align="justify">Neste momento já estamos consumindo os recursos que criamos no <a href="http://vitormeriat.com.br/2013/09/20/asp-net-web-api-criando-e-consumindo-dados-parte-1/" target="_blank">post anterior.</a></p>
<p align="justify">O código fonte deste exemplo <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%213194" target="_blank">pode ser baixado clicando aqui!</a></p>
<p align="justify">&#160;</p>
<p align="justify">No próximo post vou abordar sobre a arquitetura do ASP.NET Web API bem como trazer uma análise sobre questões referentes ao <strong>Consumo,</strong> <strong>Routing e <strong>Host</strong></strong>.</p>
<p>&#160;</p>
<h2>Até mais e bom estudo a todos!</h2>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" align="left" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" height="110" /></a></p>
<h3><font style="font-weight:bold;" color="#4f81bd"><font color="#9bbb59">Twitter:</font> </font><a href="http://twitter.com/#!/vitormeriat"><font style="font-weight:bold;" color="#4f81bd">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font style="font-weight:bold;" color="#4f81bd">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font style="font-weight:bold;" color="#4f81bd">vitor.pereira@studentpartner.com</font></a></h3>
