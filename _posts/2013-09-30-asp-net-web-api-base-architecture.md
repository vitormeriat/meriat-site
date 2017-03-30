---
layout: post
title: ASP.NET Web API - Base Architecture
date: 2013-09-30 15:04:30.000000000 -03:00
type: post
published: true
status: publish
categories:
- Services

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/09/0009.png"><img title="0009" style="background-image:none;float:left;padding-top:0;padding-left:0;margin:15px 15px 0 0;display:inline;padding-right:0;border-width:0;"   alt="0009" align="left" src="http://blob.vitormeriat.com.br/images/0009.png" width="369" height="166" /></a>A <strong>WebAPI</strong> é uma plataforma ideal para a construção de serviços baseados em <strong>HTTP</strong>, onde o pedido e a resposta acontecem no protocolo <strong>HTTP</strong>. Sendo assim o cliente pode fazer uma requisição <strong>GET, PUT, POST e DELETE</strong> obtendo a resposta adequadamente. Nos posts anteriores fiz um resumo sobre o WebAPI, onde codificamos e consumimos um serviço <strong>HTTP</strong>. Neste post, vamos analisar a arquitetura de processamento, trazendo alguns detalhes sobre o que acontece entre a recepção de um pedido <strong>HTTP</strong> e o retorno da resposta.</p>
<p><!--more-->
<p align="justify">A arquitetura WebAPI é composta de três camadas: hosting, message handler pipeline, controller handling. Como pode ser visto na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/processingmodel.png"><img title="ProcessingModel" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="ProcessingModel" src="http://blob.vitormeriat.com.br/images/processingmodel.png" width="560" height="704" /></a></p>
<p>Antes de falar sobre estas camadas, precisamos consolidar alguns conceitos base do WebAPI:</p>
<p>&#160;</p>
<h2>Route</h2>
<p align="justify">A configuração de roteamento no WebAPI é ligeiramente diferente do roteamento do <strong>ASP.NET MVC</strong>. Enquanto temos as classes <a href="http://msdn.microsoft.com/pt-br/library/system.web.routing.route(v=vs.100).aspx" target="_blank">Route</a>e <a href="http://msdn.microsoft.com/pt-br/library/system.web.routing.routecollection(v=vs.100).aspx" target="_blank">RouteCollection</a>no ASP.NET MVC, no WebAPI iremos trabalhar com Route e <a href="http://msdn.microsoft.com/en-us/library/system.web.http.httproutecollection(v=vs.108).aspx" target="_blank">HttpRouteCollection.</a>Mesmo o time do WebAPI tendo utilizado a mesma lógica de routing do MVC, estes se diferem na estrutura. A ideia é tornar o Roteamento independente das classes ASP.NET, afim de ampliar sua capacidade de hospedagem.</p>
<p align="justify">Para determinar qual a ação deve ser invocada, existe uma tabela de roteamento. Logo abaixo temos o caminho predefinido, que está configurado no arquivo Global.asax da sua aplicação WebAPI.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/04-rout.png"><img title="04 rout" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="04 rout" src="http://blob.vitormeriat.com.br/images/04-rout.png" width="560" height="207" /></a></p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/09/untitled.png"><img title="Untitled" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="Untitled" src="http://blob.vitormeriat.com.br/images/untitled.png" width="560" height="272" /></a></p>
<p align="justify">Neste momento o <strong>framework</strong> do WebAPI recebe a solicitação HTTP e tenta encontrar a URI correspondente dentro do modelo de rotas na tabela de roteamento. Caso não seja encontrado, o retorno será um erro <strong>404</strong>. A figura abaixo representa o fluxo </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/09/routing-webapi-copy.png"><img title="Routing WebAPI copy" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="Routing WebAPI copy" src="http://blob.vitormeriat.com.br/images/routing-webapi-copy.png" width="560" height="614" /></a></p>
<p align="justify">Para tipos simples, o WebAPI utiliza apenas os dados da rota e os parâmetros de consulta a partir da <strong>URI</strong> requisitada. Já para tipos complexos, é necessário trabalhar com MediaTypeFormatters que são usados para serializar o corpo da solicitação com base no tipo de conteúdo (<strong>JSON, XML</strong>, etc).</p>
<p>&#160;</p>
<h2>Content Negotiation</h2>
<p align="justify">O content negotiation no WebAPI, representa o processo de selecionar a melhor representação para uma determinada resposta. A engine do WebAPI implementa um tipo de negociação de conteúdos, o que permite ao cliente solicitar dados para um tipo específico de mídia.</p>
<p align="justify">Sendo assim, este é um mecanismo que permite ao servidor web devolver conteúdo em formato diferente usando a mesmo <strong>URL</strong>. A imagem abaixo explica este processo:</p>
<p align="justify">
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/02-content-negotiatio.png"><img title="02 Content Negotiatio" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="02 Content Negotiatio" src="http://blob.vitormeriat.com.br/images/02-content-negotiatio.png" width="560" height="502" /></a></p>
<p>Por padrão o <strong>WebAPI</strong> retorna os dados em formato <strong>JSON</strong>, mas graças ao content negotiation é possível solicitar um recurso especificando a mídia de retorno. Não vou aprofundar neste item pois já tenho um post específico sobre ele no forno.</p>
<p>&#160;</p>
<h2>Implementation&#160;&#160;&#160; </h2>
<p align="justify">Para uma implementação genérica do WebAPI, precisamos criar uma classe que deriva de ApiController. Ele é o responsável por fazer a mágica. Se na sua classe você tem um método prefixado ou decorado com <strong>GET</strong>, isso significa que você está tentando retornar dados com base em uma requisição. Sendo assim, você tem apenas que se certificar que todos os método codificados estão prefixados ou decorados com o tipo de solicitação desejada (<strong>GET, POST, PUT, DELETE</strong>). </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/09/089898.png"><img title="089898" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="089898" src="http://blob.vitormeriat.com.br/images/089898.png" width="560" height="344" /></a></p>
<p align="justify">Isto significa dizer que não estamos dependentes de utilizar única e exclusivamente a interface WebAPI dos templates <strong>WEB</strong> do <strong>Visual Studio</strong>. Podemos criar um serviço WebAPI partindo de uma console aplication, e isso é possível graças a camada de Hospedagem que será o nosso próximo passo.</p>
<p>&#160;</p>
<h2>Hosting</h2>
<p align="justify">A primeira camada ou camada inferior desta arquitetura é a hospedagem. Esta camada atua como uma interface entre a WebAPI e uma infra-estrutura subjacente para o HTTP como o próprio ASP.NET clássico. Em resumo esta camada cria o <strong>HttpRequestMessage</strong> enviando para o manipulador da camada superior. É também na camada de hospedagem que temos o processamento do <strong>HttpResponseMessage</strong> antes de ser devolvido ao handler pipeline.</p>
<p align="justify">Lembre-se que <strong>HttpRequestMessage</strong> e <strong>HttpResponseMessage</strong> são classes novas para representar mensagens <strong>HTTP</strong>, introduzidas na versão 4.5 do Framework. </p>
<p>Hoje, as opções de hospedagem são: <strong>self-hosting</strong>,<strong> web-hosting </strong>e<strong> cloud-hosting</strong>.</p>
<h3><font style="font-weight:bold;">Self-Hosting</font></h3>
<p align="justify">Sef-hosting ou Auto-Hosting é a opção de hospedar APIs em um processo que não seja o IIS. Sendo assim, podemos utilizar por exemplo um Console Application ou um Windows Service como hospedagem do serviço. Isto é possível por que este tipo de hospedagem é baseada no ASP.NET clássico.</p>
<h3><font style="font-weight:bold;">Web-Hosting</font></h3>
<p align="justify">Nesta opção é utilizado o <strong>IIS </strong>para hospedar <strong>APIs Web</strong>, o que nos dá traz uma série de recursos para a gestão dessas APIs, como controle de acesso, segurança, reciclagem de processo e outros. Neste modelo de hospedagem reutiliza a infraestrutura do <strong>ASP.NET</strong> ou <strong>ASP.NET MVC </strong>para executar os serviços. O web-hosting é baseado em <strong>IHttpAsyncHandler</strong> que chama <strong>HttpControllerHandler</strong> que converte uma <strong>HttpRequest</strong> em <strong>HttpRequestMessage</strong>.</p>
<p align="justify">É neste caso que utilizamos o template Web disponível no Visual Studio para construir nossos serviços. Exatamente como no exemplo do post: <a href="http://vitormeriat.com.br/2013/09/20/asp-net-web-api-criando-e-consumindo-dados-parte-1/" target="_blank">ASP.NET Web API – Criando e consumindo dados [Parte 1]</a></p>
<h3><font style="font-weight:bold;">Cloud-Hosting</font></h3>
<p align="justify">Utiliza o Windows Azure para publicar e rodar as APIs. O principal atrativo desta opção é a facilidade em escalonar sem a necessidade de mudanças na API, já que a responsabilidade fica por conta dos mecanismos de gestão e execução do Windows Azure que são capazes de identificar a necessidade de adicionar novas instâncias ao load balance a fim de atender a demanda solicitada.</p>
<h3><font style="font-weight:bold;">Outros</font></h3>
<p align="justify">O WebAPI não se limita a estas opções. Há já alguns hosts adicionais, contribuídos pela comunidade:</p>
<ul>
<ul>
<li>
<div align="justify"><a href="http://owin.org/" target="_blank">OWIN</a> </div>
</li>
<li>
<div align="justify"><a href="https://www.windowsazure.com/en-us/develop/net/how-to-guides/service-bus-relay/" target="_blank">Azure Service Bus relaying</a> </div>
</li>
</ul>
</ul>
<p>Para uma melhor compreenção, segue um exemplo de self-hosting do WebAPI:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/031.png"><img title="03" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="03" src="http://blob.vitormeriat.com.br/images/03.png" width="560" height="369" /></a></p>
<p align="justify">No exemplo acima, a aplicação escuta em uma URL específica, no caso a <strong>localhost 8080</strong>. Para executar este código é necessário ter privilégios de administrador. Caso ocorra o erro: <strong>“HTTP could not register URL”</strong>, basta executar o comando abaixo no <strong>command prompt</strong> executando como Adminstrador.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/01-cmd.png"><img title="01 cmd" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="01 cmd" src="http://blob.vitormeriat.com.br/images/01-cmd.png" width="560" height="117" /></a></p>
<p align="justify">Como pode ser visto, estamos utilizando um projeto console para hospedar nosso serviço, mas neste tipo de hopedagem poderia ser qualquer outro processo do .NET.</p>
<p>&#160;</p>
<h2>Message handler pipeline</h2>
<p align="justify">O manipulador de mensagem é a classe que recebe a requisição <strong>HTTP</strong> e retorna a resposta da requisição. Os manipuladores são classes que herdam da classe abstrata <strong>HttpMessageHandler</strong>.</p>
<p align="justify">Esta camada da arquitetura é composta por um manipulador de mensagens semelhante ao que existe no <strong>WCF</strong>. Esta pipeline é exposta pela classe <strong>HttpServer</strong>. O manipulador de mensagem é simplesmente uma abstração para uma operação que recebe uma mensagem de requisição <strong>HTTP</strong> (<strong>HttpRequestMessage</strong>) e retorna uma mensagem de resposta HTTP (<strong>HttpResponseMessage</strong>).</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/09/656565.png"><img title="656565" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="656565" src="http://blob.vitormeriat.com.br/images/656565.png" width="484" height="397" /></a></p>
<p align="justify">Esta organização do pipeline proporciona uma grande flexibilidade no tipo de operações que podem ser realizadas, mas em suma, a requisição é enviada, tratada pelo <strong>DelegatingHandler</strong> que é o cara responsável por manter uma referência para o manipulador interno. Após isso já com o método da <strong>URI</strong> definido, o manipulador guarda o código de status da resposta para ser devolvido a camada de cima.</p>
<p>&#160;</p>
<h2>Controller Handling</h2>
<p align="justify">A camada superior da arquitetura do WebAPI, corresponde ao processamento do controller a saber:</p>
<ul>
<ul>
<li>
<div align="justify"><strong>Action selection </strong>– Realiza a seleção das ações baseado em reflexão;</div>
</li>
<li>
<div align="justify"><strong>Filter execution </strong>– Define os métodos a serem utilizados para os filtros das ações;</div>
</li>
<li>
<div align="justify"><strong>Model binding </strong>– Define os métodos necessários para a ligação com o modelo;</div>
</li>
<li>
<div align="justify"><strong>Action invocation </strong>– Invoca os métodos para a ação de um controlodor;</div>
</li>
<li>
<div align="justify"><strong>Response content creation via formatters</strong> – Classe base para trabalhar com a serialização e desserilalização tipados usando ObjectContent.</div>
</li>
</ul>
</ul>
<p align="justify">Todo o processo ocorre dentro do ApiController e é chamado pela HttpControllerDispatcher. Sua função nesta brincadeira é selecionar, criar e chamar o controlador correto para realizar a requisição.</p>
<p>&#160;</p>
<h2>Conclusão</h2>
<p align="justify">A ideia deste post é trazer mais uma luz sobre a motivação por trás da criação do ASP.NET Web API fazendo uma análise do seu modelo base de programação atravéz de sua arquitetura.</p>
<p>&#160;</p>
<h1>Até mais e bom estudo a todos!</h1>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" align="left" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" height="110" /></a></p>
<h3><font color="#4f81bd"><font style="font-weight:bold;">Twitter:</font></font> <a href="http://twitter.com/#!/vitormeriat"><font color="#9bbb59">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font color="#9bbb59">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font color="#9bbb59">vitor.pereira@studentpartner.com</font></a></h3>