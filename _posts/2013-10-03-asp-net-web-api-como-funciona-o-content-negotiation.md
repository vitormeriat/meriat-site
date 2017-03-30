---
layout: post
title: ASP.NET Web API - Como funciona o Content Negotiation
date: 2013-10-03 17:08:13.000000000 -03:00
type: post
published: true
status: publish
categories:
- Services

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/cn.png"><img title="CN" style="background-image:none;float:left;padding-top:0;padding-left:0;margin:10px 30px 0 0;display:inline;padding-right:0;border-width:0;"   alt="CN" align="left" src="http://blob.vitormeriat.com.br/images/cn.png" width="213" height="235" /></a>Nos posts anteriores (<a href="http://vitormeriat.com.br/2013/09/20/asp-net-web-api-criando-e-consumindo-dados-parte-1/" target="_blank">ASP.NET Web API – Criando e consumindo dados [Parte 1]</a>, <a href="http://vitormeriat.com.br/2013/09/23/asp-net-web-api-criando-e-consumindo-dados-parte-2/" target="_blank">[Parte 2]</a> e <a href="http://vitormeriat.com.br/2013/09/30/asp-net-web-api-base-architecture/" target="_blank">ASP.NET Web API – Base Architecture</a>), falamos sobre os componentes e recursos disponíveis no WebAPI. Dentre eles o Content Negotiation (Negociação de Conteúdo), que é o mecanismo do WebAPI que permite ao servidor web devolver o mesmo conteúdo, utilizando a mesma URL mas em formatos diferentes.&#160; Neste post, vamos realizar alguns exemplos e focar em entender como funciona este, que é um dos recursos mais interessantes e importantes do ASP.NET Web API.</p>
<p><!--more-->
<p><font color="#555555">Realmente tenho notado a importância do Content Negotiation. Não só por ter tido … </font></p>
<p>Os exemplos deste post podem ser baixados no link ao final do artigo.</p>
<p>&#160;</p>
<h2><font color="#555555">O que é o Content Negotiation e qual seu papel no WebAPI</font></h2>
<p align="justify">Estamos falando de uma especificação HTTP que foi definida na <a href="http://www.w3.org/Protocols/rfc2616/rfc2616.html" target="_blank">RFC 2616.</a>Este documento define que o Content Negotiation é o processo de selecionar a melhor representação de conteúdo para uma determinada resposta quando houver múltiplas representações disponíveis. Neste caso, qualquer resposta que contém em seu corpo uma entidade pode ser objeto de negociação incluindo respostas de erro.</p>
<p align="justify">Já no WebAPI o Content Negotiation é o algoritmo utilizado para determinar com base na requisição do cliente, qual o media type formatter deve ser utilizado na resposta. Quando falamos em .NET, ele realmente decide como enviar o objeto CLR para o cliente através do protocolo HTTP.</p>
<p align="justify">Um passo fundamental para entender o Content Negotiation é saber sobre os seus dois pilares:</p>
<ul>
<ul>
<li>
<div align="justify"><strong>Media type</strong> – Definido pela W3C como campos do cabeçalho a fim de fornecer tipos de dados e tipos de negociação; </div>
</li>
<li>
<div><strong>Media type formatter </strong>– É a classe responsável por ler e escrever um objeto CLR do ou para o corpo da solicitação o requisição. Dependendo do sentido do fluxo HTTP. </div>
</li>
</ul>
</ul>
<p align="justify">Existem dois resultados possíveis para a negociação de conteúdo: O cliente e o servidor podem ou não concordar com o formato. Caso haja discordância quanto ao formato, cabe ao cliente realizar a ação, como por exemplo, registrar o erro.</p>
<p align="justify">Outro ponto importante a se considerar são os cabeçalhos envolvidos no processo. Para trabalhar com Content Negotiation no WebAPI vamos precisar constantemente destes dois cabeçalhos:</p>
<ul>
<ul>
<li>
<div>Accept</div>
</li>
<li>
<div>Content-Type</div>
</li>
</ul>
</ul>
<p align="justify">&#160;</p>
<h2>Iniciando no Content Negotiation</h2>
<p align="justify">Se você estiver implementando negociação de conteúdo na mão, a maneira mais simples será capturar os parâmetros HTTP GET e mudar os filtros de entrada e saída para o formato escolhido, como no exemplo abaixo onde o conteúdo é entre em XML e JSON.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/untitled.png"><img title="Untitled" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="Untitled" src="http://blob.vitormeriat.com.br/images/untitled.png" width="306" height="427" /></a></p>
<p align="justify">Além desta implementação é possível criar um interprete de acordo com a extensão do recurso. O recurso é o mesmo que o visto anteriormente mas requer lógica do lado do servidor. O lado bom é que esta abordagem nos permite definir diferentes controladores que serão chamados de acordo com a extensão do recurso. </p>
<p>Se você leu os posts anteriores já deve estar notando o papel do WebAPI dentro desta necessidade. </p>
<p>&#160;</p>
<h2>Content Negotiation no Web API</h2>
<p align="justify">Agora vamos partir para um pouco de código. Para entender melhor sobre o Content Negotiation. Vamos utilizar a aplicação que construímos no <a href="http://vitormeriat.com.br/2013/09/20/asp-net-web-api-criando-e-consumindo-dados-parte-1/" target="_blank">ASP.NET Web API – Criando e consumindo dados [Parte 1]</a> e que pode ser baixado <a href="https://skydrive.live.com/?cid=BD055AA47A388023&amp;id=BD055AA47A388023%213193" target="_blank">CLICANDO AQUI!</a>&#160;</p>
<p align="justify">Agora que você já tem a aplicação rodando, vamos repassar algumas informações: Neste exemplo estamos utilizando um Entity Data Model apontando para o banco de dados Northwind. Nosso exemplo foi construído baseado na tabela Customer. Também fiz algumas alterações no layout mas o código completo está publicado no final do post.</p>
<p align="justify">Agora, vamos para Views, Home e Index.cshtml. Neste arquivo vamos inserir o seguinte código na tag header vamos adicionar a chamada para o Jquery e o código abaixo que chama o cliente WebAPI.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/untitled1.png"><img title="Untitled" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="Untitled" src="http://blob.vitormeriat.com.br/images/untitled.png" width="560" height="561" /></a></p>
<p align="justify">O código acima utiliza a função<strong> $.ajax() </strong>do JQuery para realizar a chamada ao cliente WebAPI. Notem que temos um objeto client que armazena todas as configurações necessárias para chamar nossa WebAPI. Neste primeiro exemplo vamos trabalhar com os valores padrão, sendo assim não é necessário definir os cabeçalhos <strong>Accept</strong> e <strong>Content-Type</strong>.</p>
<p align="justify">Na função <strong>lerResultadoJSON()</strong>, passamos o resultado da solicitação quando a mesma ocorrer com sucesso. O resultado será renderizado em uma tabela dentro de uma <strong>div container</strong> que você pode criar dentro da <strong>div body </strong>do nosso exemplo. </p>
<p align="justify">Como já dito anteriormente, o formato padrão com o qual o <strong>WebAPI</strong> trabalha é o <strong>JSON</strong>, e nossa função trata o retorno como sendo uma matriz <strong>JSON</strong>, percorrendo cada elemento e montando a tabela com os resultados pesquisados.</p>
<p align="justify">A função <strong>exibirError()</strong> é responsável por “exibir” o erro e seu código caso ocorra qualquer falha durante a chamada do serviço.</p>
<p align="justify">Rode a aplicação e o resultado será como se segue:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/json.png"><img title="json" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="json" src="http://blob.vitormeriat.com.br/images/json.png" width="560" height="720" /></a></p>
<p align="justify">Por motivos de espaço não estou exibindo todos os resultados ok?</p>
<p align="justify">Vamos olhar para nossa requisição e resposta:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/headersjson.png"><img title="headersjson" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="headersjson" src="http://blob.vitormeriat.com.br/images/headersjson.png" width="560" height="466" /></a></p>
<p align="justify">Repare que nosso cabeçalho Accept não contem valor. Já na resposta o valor de retorno é o padrão JSON, como podemos ver na aba Preview.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/previewjson.png"><img title="previewjson" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="previewjson" src="http://blob.vitormeriat.com.br/images/previewjson.png" width="560" height="394" /></a></p>
<p align="justify">
<p align="justify">Agora vamos brincar com o <strong>Content Negotiation</strong>. Em nosso código <strong>JQuery</strong>, altere o código exatamente como o descrito abaixo: </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/9898.png"><img title="9898" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="9898" src="http://blob.vitormeriat.com.br/images/9898.png" width="560" height="209" /></a></p>
<p align="justify">Neste trecho de código apenas inseri a seguinte linha: <strong>client.headers = { &quot;accept&quot;: &quot;application/xml;charset=utf-8&quot; };</strong> e alterei criei uma chamada para uma função <strong>lerResultadoXML()</strong>.</p>
<p align="justify">Com apenas este cabeçalho, estamos dizendo para o <strong>WebAPI</strong> para enviar os dados em formato XML. Note que agora vamos precisar criar uma função específica para exibir os dados em XML. Insira o código abaixo para a função <strong>lerResultadoXML()</strong>, que vai tratar o XML de resposta exibindo os dados corretamente.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/lerxml.png"><img title="lerxml" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="lerxml" src="http://blob.vitormeriat.com.br/images/lerxml.png" width="560" height="231" /></a></p>
<p align="justify">Para este exemplo, alterei as colunas a fim de exibir valores diferentes para facilitar na visualização do recurso que acabamos de alterar. O resultado será o seguinte:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/xml.png"><img title="xml" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="xml" src="http://blob.vitormeriat.com.br/images/xml.png" width="560" height="720" /></a></p>
<p align="justify">Se olharmos para nossa requisição e reposta veremos que nosso cabeçalho Accept solicita que a resposta seja em <strong>XML</strong>. Nosso Content-Type está marcado como <strong>JSON</strong> por padrão, mesmo não informando este valor no <strong>objeto client</strong>. Já na resposta nosso <strong>Content-Type</strong> está setado com o formato XML.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/headersxml.png"><img title="headersxml" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="headersxml" src="http://blob.vitormeriat.com.br/images/headersxml.png" width="560" height="481" /></a></p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/previewxml.png"><img title="previewxml" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="previewxml" src="http://blob.vitormeriat.com.br/images/previewxml.png" width="560" height="398" /></a></p>
<p align="justify">Se apenas utilizando o cabeçalho <strong>Accept</strong> conseguimos o resultado esperado, qual a necessidade do cabeçalho <strong>Content-Type</strong>? </p>
<p align="justify">Este cabeçalho é utilizado para quando o formato solicitado para a resposta no cabeçalho Accept não pode ser entregue pelo servidor. Vamos a um exemplo prático.</p>
<p align="justify">Altere o código JQuery para:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/6666666.png"><img title="6666666" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="6666666" src="http://blob.vitormeriat.com.br/images/6666666.png" width="560" height="217" /></a></p>
<p align="justify">Note que no objeto client inserimos a propriedade <strong>contentType</strong> definido o formato como JSON. Já em headers alteramos nosso cabeçalho inserindo um valor inválido xml123. Ao executar nossa aplicação não vamos ver nenhum Customer exibido na tela, mas ao analisar o nossa requisição vamos ver que houve uma <strong>resposta 200 – OK.</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/headerscontent.png"><img title="headerscontent" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="headerscontent" src="http://blob.vitormeriat.com.br/images/headerscontent.png" width="560" height="467" /></a></p>
<p align="justify">Note em Request Headers que o nosso pedido foi realizado apontando para o formato inválido xml123, porém na resposta o formato utilizado foi o JSON. Para verificar a veracidade desta informação, basta trocar a chamada de sucesso para <strong>client.success = lerResultadoJSON;</strong> e os resultados serão apresentados na tela corretamente.</p>
<p>&#160;</p>
<h2>Como Assim?</h2>
<p>Para que os exemplos que postei aqui possam ocorrer com sucesso, foram executados os seguintes passos: </p>
<ol>
<li>Mapeamento do tipo de mídia – Mapeia o tipo de mídia a ser utilizada na requisição;</li>
<li>Aceitação dos cabeçalhos emitidos pelo cliente – Verifica os cabeçalhos da solicitação para que o pedido seja validado;</li>
<li>Inspeção do tipo de conteúdo solicitado – Inspeciona o tipo de conteúdo solicitado já que o mesmo pode um tipo de conteúdo específico. Neste ponto cabe ao MediaTypeMappings a verificação do cabeçalho Accept;</li>
<li>Verificar se o formatador pode serializar o tipo de conteúdo para a resposta – O Content Negotiation varre sua coleção de formatadores até encontrar um que possa tratar o conteúdo da resposta adequadamente.</li>
</ol>
<p>&#160;</p>
<p>O código fonte pode ser baixado <a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%213197" target="_blank">CLICANDO AQUI!</a></p>
<p><font color="#777777"></font></p>
<h2><font color="#777777">Conclusão</font></h2>
<p align="justify"><font color="#777777">Com isso concluímos aqui nossa visão sobre o Content Negotiation no ASP.NET Web API. No próximo post vou mostrar como consumir o Web API realizando um CRUD apenas com HTML e JQuery.</font></p>
<p>&#160;</p>
<h2>Até mais e bom estudo a todos!</h2>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" align="left" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" height="110" /></a></p>
<h3><font style="font-weight:bold;"><font color="#9bbb59">Twitter:</font> </font><a href="http://twitter.com/#!/vitormeriat"><font style="font-weight:bold;" color="#4f81bd">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font style="font-weight:bold;" color="#4f81bd">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font style="font-weight:bold;" color="#4f81bd">vitor.pereira@studentpartner.com</font></a></h3>