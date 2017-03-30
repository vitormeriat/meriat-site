---
layout: post
title: ASP.NET Web API – Criando um CRUD e consumindo em um domínio diferente. CORS,
  AJAX e JSONP [Parte 3]
date: 2013-10-30 10:37:57.000000000 -02:00
type: post
published: true
status: publish
categories:
- Services
- WebAPI

---
<p align="justify">Neste post final da série vamos implementar as funções do nosso <strong>CRUD</strong> utilizando <strong>JSONP</strong> e <strong>CORS</strong> para consumir nosso serviço em um domínio diferente. Como já criamos todos os subsídios nos posts anteriores, bem como já exploramos os motivos para esta abordagem, neste post vamos focar no velho e bom “<strong>mão na massa</strong>”.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/capa1.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="capa" src="http://blob.vitormeriat.com.br/images/capa.png" alt="capa" width="560" height="294"   /></a></p>
<p><!--more--></p>
<p>De posse do nosso site, vamos implementar as funções Ajax para consumir nosso serviço. O primeiro ponto é colocar nosso serviço para rodar. Acesse a aplicação <strong>CloudHostingMunicipios </strong>que criamos no primeiro post da série.</p>
<p>Nosso próximo passo é iniciar site <strong>Web API CORS Client</strong>, que é um simples site <strong>HTML</strong> que foi disponibilizado no post anterior da série.</p>
<p>&nbsp;</p>
<h2>Implementando JSONP</h2>
<p align="justify">Com nosso recurso em mãos vamos partir para a mão na massa: Acesse o arquivo index.html onde iremos utilizar o <strong>JSONP</strong> para realizar nossa listagem de municípios. Insira o seguinte código dentro da tag <strong>&lt;script&gt;</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura00.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura00" src="http://blob.vitormeriat.com.br/images/figura00.png" alt="figura00" width="560" height="490"   /></a></p>
<p align="justify">É importante lembrar de substituir a porta do serviço caso esteja rodando em uma diferente da minha. Sendo assim, até este momento, meu serviço está rodando em <a href="http://localhost:56601/">http://localhost:56601</a> e meu cliente está em <a href="http://localhost:6135/">http://localhost:6135</a>. Agora, se dermos um <strong>refresh</strong> em nosso cliente vamos obter o seguinte resultado:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura01.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura01" src="http://blob.vitormeriat.com.br/images/figura01.png" alt="figura01" width="560" height="438"   /></a></p>
<p align="justify">Como vimos em nosso código, caso o retorno da nossa função seja um erro ele exibe a mensagem acima. Vamos olhar mais a fundo o problema:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura02.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura02" src="http://blob.vitormeriat.com.br/images/figura02.png" alt="figura02" width="560" height="346"   /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura03.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura03" src="http://blob.vitormeriat.com.br/images/figura03.png" alt="figura03" width="560" height="346"   /></a></p>
<p align="justify">Como vimos no post anterior, já preparamos nossa aplicação para retornar um <strong>JSONP</strong> ao invés de um <strong>JSON</strong>. O erro que temos aqui é um problema de formatação. Para que os valores sejam exibidos corretamente, precisamos definir em nossa aplicação <strong>(lado do servidor)</strong>, uma maneira para que o servidor reconheça que o pedido partiu de uma solicitação JSONP a fim de responder adequadamente.</p>
<p align="justify">Para isso, temos a possibilidade de escrever em nossa aplicação o nosso próprio <strong>Media Type</strong> Formatter. Para facilitar nossa vida, vamos utilizar o <strong>NuGet</strong> para obter nosso formatter. Clique com o botão direito em <strong>References</strong> e <strong>Manage NuGet Packeges…</strong> e instale o pacote online <strong>WebApiContrib.Formatting.Jsonp</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura04.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura04" src="http://blob.vitormeriat.com.br/images/figura04.png" alt="figura04" width="560" height="297"   /></a></p>
<p align="justify">Agora precisamos criar nossa classe de configuração para conseguirmos registrar nosso formatter. Clique com o botão direito na pasta <strong>App_Start</strong> e adicione uma nova classe chamada <strong>FormatterConfig</strong> e insira o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura05.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura05" src="http://blob.vitormeriat.com.br/images/figura05.png" alt="figura05" width="560" height="394"   /></a></p>
<p align="justify">Agora acesse seu arquivo <strong>Global.asax.cs</strong> e insira a seguinte linha de código:</p>
<ul>
<li>
<div align="justify"><strong>FormatterConfig.RegisterFormatters(GlobalConfiguration.Configuration.Formatters);</strong></div>
</li>
</ul>
<p align="justify">Seu <strong>Application_Start()</strong> deve ficar como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura06.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura06" src="http://blob.vitormeriat.com.br/images/figura06.png" alt="figura06" width="560" height="234"   /></a></p>
<p align="justify">Agora se dermos um refresh na página é possível perceber em que nosso retorno tem algo como um  <strong>jQuery17208638584909494966_1345764737438&amp;_=1345764737668([{ jsondata }]), </strong>que é reconhecido pela nossa <strong>função calback</strong>. Agora temos o seguinte resultado:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura07.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura07" src="http://blob.vitormeriat.com.br/images/figura07.png" alt="figura07" width="560" height="348"   /></a></p>
<p align="justify">Note que agora ele não está devolvendo apenas o <strong>JSON</strong>. Agora temos a chamada da nossa função <strong>JSONP</strong>.</p>
<p align="justify">Agora acesse o arquivo <strong>getbyuf.html </strong>e insira o seguinte código na tag <strong>&lt;script&gt;</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura09.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura09" src="http://blob.vitormeriat.com.br/images/figura09.png" alt="figura09" width="560" height="528"   /></a></p>
<p><strong>Substitua </strong>a linha do botão pelo código abaixo:</p>
<ul>
<li><strong>&lt;input name="submit" type="submit" id="submit" value="Buscar" onclick="getByUF(); return false;" /&gt;</strong></li>
</ul>
<p>Agora, ao pesquisar um determinada <strong>UF</strong> teremos todos os municípios cadastrados:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura08.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura08" src="http://blob.vitormeriat.com.br/images/figura08.png" alt="figura08" width="560" height="382"   /></a>Vamos repetir este processo para o <strong>getbycodigo.html</strong>. Incluía o seguinte código na tag <strong>&lt;script&gt; </strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura11.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura11" src="http://blob.vitormeriat.com.br/images/figura11.png" alt="figura11" width="560" height="279"   /></a></p>
<p><strong>Substitua </strong>a linha do botão pelo código abaixo:</p>
<ul>
<li><strong>&lt;input name="submit" type="submit" id="submit" value="Buscar" onclick="getByCodigo(); return false;" /&gt;</strong></li>
</ul>
<p>O resultado será como se segue:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura10.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura10" src="http://blob.vitormeriat.com.br/images/figura10.png" alt="figura10" width="560" height="335"   /></a></p>
<p align="justify">Neste momento já cobrimos nossa solução com as funções e chamadas <strong>JONSP</strong>. Agora para os verbos seguintes, vamos precisar trabalhar com <strong>CORS</strong>.</p>
<p>&nbsp;</p>
<h2>Implementando CORS</h2>
<p align="justify">Algo importante a ser levado em consideração é que para se implantar <strong>CORS</strong> é necessário haver do lado do servidor um mecanismo para dar permissão ao  domínio que realiza a requisição caso atenda aos requisitos necessários. O servidor deve ser capaz de reconhecer estes requisitos necessários a fim de permitir a ação.</p>
<p align="justify">Sendo assim precisamos criar um manipulador para analisar o cabeçalho da requisição de entrada e permitir o acesso. Clique com o botão direito sobre a pasta <strong>App_Start</strong> e inclua uma nova classe chamada <strong>CorsHandler</strong>. Agora altere o código como o descrito abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura12.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura12" src="http://blob.vitormeriat.com.br/images/figura12.png" alt="figura12" width="560" height="626"   /></a></p>
<p align="justify">Com nosso manipulado pronto, precisamos registra-lo no <strong>Application_Start</strong> do arquivo <strong>Global.asax.cs</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura13.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura13" src="http://blob.vitormeriat.com.br/images/figura13.png" alt="figura13" width="560" height="216"   /></a></p>
<p>Com todas as alterações do lado do servidor implementadas, vamos alterar nosso cliente para testar os resultados. Inclua o seguinte código na tag <strong>&lt;script&gt;</strong> do arquivo <strong>post.html</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura14.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura14" src="http://blob.vitormeriat.com.br/images/figura14.png" alt="figura14" width="546" height="495"   /></a></p>
<p><strong>Substitua </strong>a linha do botão pelo código abaixo:</p>
<ul>
<li><strong>&lt;input name="submit" type="submit" id="submit" tabindex="5" value="Enviar" onclick="AddMunicipio(); return false;" /&gt;</strong></li>
</ul>
<p>Agora é possível cadastrar um novo município:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura15.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura15" src="http://blob.vitormeriat.com.br/images/figura15.png" alt="figura15" width="560" height="382"   /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/10/figura16.png"><img style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;" title="figura16" src="http://blob.vitormeriat.com.br/images/figura16.png" alt="figura16" width="560" height="382"   /></a></p>
<p align="justify">Para que o post não fique ainda maior, não vou publicar as outras funções, até porque agora não tem mais nada de diferente, apenas a mesma linha de atuação para a alteração e deleção do municípios. Não se preocupe, pois na aplicação de exemplo você vai ter todos os exemplos implementados e funcionais. O exemplo do código pode ser baixado <a href="http://1drv.ms/1kZL79S" target="_blank">CLICANDO AQUI!</a></p>
<p align="justify">No próximo post vou estar publicando esta aplicação na nuvem utilizando <strong>IaaS</strong> e <strong>PaaS </strong>para hospedar e consumir nosso serviço.</p>
<p>&nbsp;</p>
<h1>Até mais e bom estudo a todos!</h1>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img style="float:left;margin:0 20px 0 0;display:inline;" title="Me Azul" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" alt="Me Azul" width="110" height="110" align="left"   /></a></p>
<h3><span style="font-weight:bold;"><span style="color:#4bacc6;">Twitter:</span> </span><a href="http://twitter.com/#!/vitormeriat"><span style="font-weight:bold;color:#9bbb59;">@vitormeriat</span></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><span style="font-weight:bold;color:#9bbb59;">vitormeriat@gmail.com</span></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><span style="font-weight:bold;color:#9bbb59;">vitor.pereira@studentpartner.com</span></a></h3>