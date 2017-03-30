---
layout: post
title: Azure Mobile Service–Logging local e na nuvem com backend .NET WebAPI
date: 2014-09-05
categories:
  - Microsoft Azure
  - WebAPI
---
<p align="justify">Um dos pontos de maior adoção ao <strong>backend .NET WebAPI</strong> para o serviços mobile do Microsoft Azure, é a facilidade de testar localmente. Fora isso, Se comparado a arquitetura do <strong>backend NodeJS</strong> temos muito mais capacidade em realizar debug e auditoria em nossa aplicação.</p>
<p><img alt="fig04" src="http://blob.vitormeriat.com.br/images/2014/09/fig04.png" width="100%" /></p>
<p>Neste post vou exemplificar como utilizar o mecanismo de log do <strong>Microsoft Azure Mobile Services</strong> com backend .NET WebAPI local e na nuvem de forma rápida e simples.</p>
<p><!--more-->
<p align="justify">O primeiro passo e criar um serviço mobile caso você ainda não o tenha feito. Essa é uma tarefa realmente muito simples porém se você nunca o fez pode se&#160; basear no artigo anterior: <a href="http://vitormeriat.com.br/2014/08/12/azure-mobile-service-primeiros-passos-com-backend-net-webapi/" target="_blank">Azure Mobile Service – Primeiros passos com backend .NET WebAPI</a>. </p>
<p align="justify">Neste artigo vou utilizar o mesmo serviço que havia criado no artigo anterior. Para isso vou no portal de gestão do Microsoft Azure, acesso meu serviço (no caso meriatwebapi) e acessando a nuvenzinha azul clico em <strong>CONNECT AN EXISTING WINDOWS OR WINDOWS PHONE APP</strong>. Será baixado um serviço com o exemplo ToDo já implementado, como o descrito anteriormente.</p>
<p align="justify">Vamos iniciar implementando o LOG para os testes locais. Para isso acesse a classe TodoItemController na pasta Controllers, e insira os seguintes códigos nos métodos GetAllTodoItems e GetTodoItem respectivamente: </p>
<ul>
<li>this.Services.Log.Info(&quot;[GetAllTodoItems] GET all items&quot;); </li>
<li>this.Services.Log.Info(&quot;[GetTodoItem] GET item: &quot; + id ?? &quot;&lt;&lt;no id&gt;&gt;&quot;); </li>
</ul>
<p>O seu código deve ficar assim:</p>
<p><img alt="FIG02" src="http://blob.vitormeriat.com.br/images/2014/09/fig02.png" width="100%" /></p>
<p>Simples assim… <strong>Habemus LOG!!!</strong></p>
<p align="justify">Vale notar que o LOG é uma propriedade de <strong>ApiServices</strong> do WindowsAzure.Mobile.Service, e que está acessível em <strong>TableController&lt;T&gt;</strong>.</p>
<p><img alt="FIG03" src="http://blob.vitormeriat.com.br/images/2014/09/fig03.png" width="100%" /></p>
<p>&#160;</p>
<h2>Rodando Local</h2>
<p>Executando o a aplicação localmente, podemos observar os Logs de duas maneiras:</p>
<ul>
<li>Debugando a aplicação e visualizando no Console Output </li>
<li>Gravando o LOG fisicamente </li>
</ul>
<p><strong><font size="4">Console Output</font></strong></p>
<p align="justify">Apenas rode sua aplicação com o&#160; famoso “<strong>F5</strong>”. Atache um <strong>breakpoint</strong> no <strong>GetAllTodoItems</strong>. Note que seu serviço vai executar no <strong>localhost</strong>. Ai é só realizar o get (<strong>localhost:{sua-porta}/tables/TodoItem</strong>).</p>
<p><img title="FIG04"  alt="FIG04" src="http://blob.vitormeriat.com.br/images/2014/09/fig04.png" width="100%" /></p>
<p>Já na aplicação, abra a console <strong>Output</strong> e execute os próximos passos até o <strong>LOG</strong>.</p>
<p><img alt="FIG05" src="http://blob.vitormeriat.com.br/images/2014/09/fig05.png" width="100%" /></p>
<p align="justify">Como podemos ver, o <strong>LOG</strong> vai ser exibido na console <strong>Output</strong>. É claro que nem sempre estamos debugando a aplicação, mesmo que rodando localmente. Isso nos leva a segunda solução:</p>
<p><strong><font size="4">Gravando o LOG fisicamente</font></strong></p>
<p align="justify">Neste ponto vamos gravar um arquivo txt em algum lugar. Não tem nada de novo nisso. Vamos apenas criar um um diagnostico para concatenar os logs em um arquivo texto. Para isso vamos alterar nosso <strong>Web.config</strong> incluindo o seguinte código:</p>
<blockquote><p><strong><font size="2">&lt;system.diagnostics&gt;  <br />&#160;&#160;&#160; &lt;trace autoflush=&quot;true&quot;&gt;   <br />&#160;&#160;&#160;&#160;&#160; &lt;listeners&gt;   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;default&quot; initializeData=&quot;C:developmentmylog.txt&quot;   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; type=&quot;System.Diagnostics.TextWriterTraceListener&quot; /&gt;   <br />&#160;&#160;&#160;&#160;&#160; &lt;/listeners&gt;   <br />&#160;&#160;&#160; &lt;/trace&gt;   <br />&#160; &lt;/system.diagnostics&gt;</font></strong></p>
</blockquote>
<p>Seu config vai ficar como o descrito abaixo:</p>
<p><img alt="FIG06" src="http://blob.vitormeriat.com.br/images/2014/09/fig06.png" width="100%" /></p>
<p align="justify">Neste caso estou definindo que meus logs devem ser gravados em um arquivo chamado <strong>mylog.txt</strong> na pasta <strong>development</strong> no meu diretório <strong>C</strong>. Executando novamente a aplicação e executando os métodos <strong>GetAllTodoItems</strong> (http://localhost:50269/tables/TodoItem) e <strong>GetTodoItem</strong> (http://localhost:50269/tables/TodoItem/1) vamos ter o seguinte:</p>
<p><img alt="FIG07" src="http://blob.vitormeriat.com.br/images/2014/09/fig07.png" width="100%" /></p>
<p>&#160;</p>
<h2>Rodando na Nuvem</h2>
<p align="justify">Esse é realmente simples. Só precisamos publicar as alterações do nosso serviço. Para isso basta clicar com o botão direito no projeto e clicar em <strong>Publish</strong>.</p>
<p><img alt="fig01" src="http://blob.vitormeriat.com.br/images/2014/09/fig01.png" width="100%" /></p>
<p>Na tela que se segue selecione a opção Microsoft Azure Mobile Services.</p>
<p><img alt="fig02" src="http://blob.vitormeriat.com.br/images/2014/09/fig02.png" width="100%" /></p>
<p>Neste momento será realizado sua autorização e será listados todos os seus serviços bem como a opção de criar um novo serviço para o deploy da aplicação.</p>
<p><img alt="fig03" src="http://blob.vitormeriat.com.br/images/2014/09/fig03.png" width="100%" /></p>
<p align="justify">Em nosso caso vamos apenas selecionar o serviço correspondente e realizar o <strong>Publish</strong>.</p>
<p align="justify">Pronto!!! Após a finalização do processo o navegador será aberto na página inicial do nosso serviço hospedado na nuvem. Agora é só realizar o mesmo procedimento dos testes locais.</p>
<p align="justify">No meu caso a execução foi:</p>
<ul>
<li>https://meriatwebapi.azure-mobile.net/tables/TodoItem </li>
<li>https://meriatwebapi.azure-mobile.net/tables/TodoItem/1 </li>
</ul>
<p><img alt="fig06" src="http://blob.vitormeriat.com.br/images/2014/09/fig06.png" width="100%" /></p>
<p>Para o resultado é só acessar a aba LOGS para visualizar.</p>
<p><img alt="fig05" src="http://blob.vitormeriat.com.br/images/2014/09/fig05.png" width="100%" /></p>
<p align="justify"><strong>PS:</strong> Vale notar que ao executar na nuvem será solicitado sua autenticação no brwoser. É só informar seu usuário da subscription (o nome antes do @ no e-mail de acesso ao portal), e a chave do serviço.</p>
<p>&#160;</p>
<p align="justify">Esta é só a introdução e serve de base para que você possa realizar suas implementações necessárias a fim de gerar todos os seus LOGS. </p>
<p>&#160;</p>
<h2>Referências:</h2>
<p><a href="http://azure.microsoft.com/blog/2014/07/28/azure-mobile-services-net-updates/">http://azure.microsoft.com/blog/2014/07/28/azure-mobile-services-net-updates/</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn629482.aspx">http://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn629482.aspx</a></p>
<h6></h6>
<h2><font color="#d19049">Bons estudos e até a próxima pessoal&#160; ;)</font></h2>