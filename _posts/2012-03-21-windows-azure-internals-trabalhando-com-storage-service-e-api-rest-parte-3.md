---
layout: post
title: 'Windows Azure Internals: Trabalhando com Storage Service e API REST (parte
  3)'
date: 2012-03-21 13:36:08.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure

---
<h3><font><a href="http://blob.vitormeriat.com.br/images/2012/03/figura3.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;border-top:0;margin-right:auto;border-right:0;padding-top:0;" title="Figura3"   alt="Figura3" src="http://blob.vitormeriat.com.br/images/figura3.png" width="540" height="223" /></a></font></h3>
<p><!--more--><br />
<h3><font>3º passo: Blobs</font></h3>
<p>API de referência: <a href="http://msdn.microsoft.com/en-us/library/dd135733.aspx">http://msdn.microsoft.com/en-us/library/dd135733.aspx</a></p>
<p align="justify">Na listagem abaixo temos a classe <strong>BlobStorage </strong>que herda de <strong>StorageAzure</strong>. Nossa classe tem uma constante para definir o host a ser utilizado. Implementamos o construtor da classe base e logo após temos os três métodos da nossa API: <strong>CriaContainer</strong>, <strong>CriaBlob</strong> e <strong>DeleteBlob.</strong></p>
<p align="justify">O método <strong>CriaContainer</strong> possui como argumentos o nome do container a ser criado e uma variável booleana indicando se este container deve ser público (acessível a todos) ou privado (acessível somente com sua chave de acesso). Neste exemplo iremos trabalhar apenas com o container público. Feito a verificação, adicionamos ao elemento <strong>HeaderPrefixProperties</strong> a propriedade <strong>publicaccess=true</strong>, indicando acesso público ao nosso container.</p>
<p align="justify">Agora ficou muitos simples. É só chamar o método <strong>RequisicaoDeArmazenamento</strong> da classe base e passar o nome do container a ser criado, o método HTTP a ser executado e o cabeçalho. Verificamos em nosso response por meio do código de status se o container foi criado.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem5_thumb9.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;margin:0;" title="Listagem5_thumb9_thumb"   alt="Listagem5_thumb9_thumb" src="http://blob.vitormeriat.com.br/images/listagem5_thumb9_thumb.png" width="560" height="980" /></a></p>
<p align="justify">No Método <strong>CriaBlob</strong>, nosso recurso é composto pelo nome do container (que obviamente deve estar criado e ser público) e do blob a ser criado. Utilizamos o método PUT e não precisamos alterar nada no cabeçalho. A diferença aqui é que devemos adicionar o arquivo e o seu tipo. Segundo a documentação oficial, o <strong>Content-Type</strong> não é obrigatório tendo seu valor padrão como “<strong>application/octet-stream</strong>”, mas neste caso iremos gravar um <strong>text/plain</strong>. Quando definimos o <strong>Content-Type</strong>, esse valor fica armazenado na propriedade <strong>x-ms-blob-content-type</strong> do cabeçalho de pedido. Para deletar o recurso só é preciso informar o método DELETE na assinatura do RequisicaoDeArmazenamento.</p>
<p align="justify">&#160;</p>
<h3><font>4º passo: Queues</font></h3>
<p>API de referência: <a href="http://msdn.microsoft.com/en-us/library/dd179363.aspx">http://msdn.microsoft.com/en-us/library/dd179363.aspx</a></p>
<p align="justify">Em suma nossa <strong>QueueStorage</strong> segue a mesma mecânica da classe <strong>BlobStorage</strong>. Herdamos de <strong>StorageAzure</strong>, implementamos o construtor padrão e primeiro método a ser implementado é o <strong>CriaFila</strong> como na listagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem6.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;margin:0;" title="Listagem6_thumb2_thumb"   alt="Listagem6_thumb2_thumb" src="http://blob.vitormeriat.com.br/images/listagem6_thumb2_thumb.png" width="560" height="526" /></a></p>
<p>É possível notar que não difere em nada do método <strong>CriaContainer</strong> na classe <strong>BlobStorage. </strong>Creio que é desnecessário explicar todo o algoritmo, vou direto para as diferenças em relação ao que já codificamos anteriormente. Então vamos ao método CriaMensagem:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem7.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;margin:0;" title="Listagem7_thumb2_thumb"   alt="Listagem7_thumb2_thumb" src="http://blob.vitormeriat.com.br/images/listagem7_thumb2_thumb.png" width="560" height="443" /></a></p>
<p align="justify">Para criar uma mensagem devemos observar o seguinte critério: A mensagem deve estar em um formato que possa ser incluído em uma solicitação <strong>XML</strong> com codificação <strong>UTF-8</strong>.</p>
<p align="justify">Observe que estou incluindo a mensagem recebida via parâmetro entre as tags </p>
<p align="justify"><strong>&lt;QueueMessage&gt;&lt;MessageText&gt;&quot;</strong> e <strong>&quot;&lt;/MessageText&gt;&lt;/QueueMessage&gt;&quot;.</strong> O corpo do pedido contém os dados da mensagem já obedecendo o formato XML. Note que o conteúdo da mensagem deve estar em um formato que pode ser codificado em UTF-8, neste caso, informo como <strong>contetType</strong> o valor <strong>&quot;text/plain&quot;</strong> na chamada do método. Uma operação bem sucedida retorna código de status 201 (Created). </p>
<p align="justify">&#160;</p>
<h3><font>5ºpasso: Tables</font></h3>
<p>API de referência: <a href="http://msdn.microsoft.com/en-us/library/dd179423.aspx">http://msdn.microsoft.com/en-us/library/dd179423.aspx</a></p>
<p>A classe <strong>TableStorage</strong> segue o mesmo modelo das classes <strong>BlobStorage</strong> e <strong>QueueStorage</strong>. Neste caso vamos direto aos seus métodos. Nesta classe vamos trabalhar apenas com dois métodos, a saber: <strong>ListarTabelas </strong>e <strong>PesquisaTabela</strong>. </p>
<p>O primeiro vai listar todas as tabelas da conta informada. O segundo vai listar todos os dados da tabela informada, podendo realizar as consultas especializadas informado os critérios necessário para tal. Vamos começar pelo método <strong>ListarTabelas:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem8.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;margin:0;" title="Listagem8_thumb2_thumb"   alt="Listagem8_thumb2_thumb" src="http://blob.vitormeriat.com.br/images/listagem8_thumb2_thumb.png" width="560" height="463" /></a></p>
<p>Azure Storage Table é exposta através de ADO.NET Data Services. Com isso é possível realizar as consultas (embora não haja suporte a diversos recursos).</p>
<p>Segundo a documentação, a operação <strong>Query Tables</strong> retorna uma a lista das tabelas de uma determinada conta como um conjunto de entidades ADO.NET em um feed Atom. Sendo assim, podemos realizar a exibição baseado em um XML de retorno. O que estou fazendo é utilizar o elemento “d: TableName” para expor o nome das tabelas.</p>
<p>Segue o método <strong>PesquisaTabela:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem9.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;margin:0;" title="Listagem9_thumb2_thumb"   alt="Listagem9_thumb2_thumb" src="http://blob.vitormeriat.com.br/images/listagem9_thumb2_thumb.png" width="560" height="474" /></a></p>
<p>Agora tudo fica mais simples. A diferença aqui fica por conta das consultas, basta apenas incluir no parâmetro consulta o nome da tabela a ser pesquisada e a query a ser executada. Como no exemple abaixo:</p>
<ol>
<li>
<h3>TableStorage table = new TableStorage(conta);</h3>
</li>
<li>
<h3>table.PesquisaTabela(&quot;Municipios?$filter=UF eq 'DF'&quot;);</h3>
</li>
</ol>
<h3></h3>
<p>Neste exemplo estou buscando todos os municípios onde o campo UF for igual a DF. O formato geral para recuperar dados de uma tabela é “<strong>minhatabela</strong>$filter=&lt;expressao-de-consulta&gt;”. Você tem mais informações <a href="http://msdn.microsoft.com/en-us/library/dd179421.aspx" target="_blank">aqui!</a></p>
<p>Existe outras estratégias caso você necessite trabalhar com os serviços de tabela, mas isto fica para outro post.</p>
<p>&#160;</p>
<h3><font>6º passo: Definições de conta</font></h3>
<p align="justify">Esta classe serve apenas para nos auxiliar na escolha de qual ambiente utilizar. Existem algumas diferenças entre o desenvolvimento na nuvem e utilizando o storage emulator. Algo bem aparente é a mudança nas URIs que serão utilizadas.</p>
<p align="justify">Se você já tiver uma conta na nuvem, basta apenas substituir os campos minha-conta e minha-senha pelos seus dados de conta do azure. Se não, você pode ter a opção de testar localmente.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem10.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="Listagem10_thumb[2]_thumb"   alt="Listagem10_thumb[2]_thumb" src="http://blob.vitormeriat.com.br/images/listagem10_thumb2_thumb.png" width="560" height="407" /></a></p>
<p>&#160;</p>
<h3><font>Fim</font></h3>
<p align="justify">Como explicitei, minha intenção neste artigo foi aprofundar os conhecimentos no serviço de armazenamento do Azure. Podemos notar a flexibilidade em se trabalhar com os dados na nuvem sem ter que codificar especificamente para windows Azure e podendo acessar estes dados diretamente de aplicações&#160; <strong>on-premises </strong>(aplicação que não está hospedada na nuvem) utilizando as APIs REST. Um exemplo bacana do que pode ser feito é a biblioteca <a href="http://azureblobstoragejs.codeplex.com/">Azure BlobStorage Javascript Library</a> que está disponível no codeplex. No mais, não há limites para a imaginação.</p>
<p align="justify">&#160;</p>
<h3 align="justify"><font color="#4f81bd"><a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21229&amp;sc=documents" target="_blank">Baixe aqui o Código Fonte utilizado no artigo.</a></font></h3>
<p align="justify">&#160;</p>
<p align="justify"><a href="http://vitormeriat.wordpress.com/2012/03/21/windows-azure-internals-trabalhando-com-storage-service-e-api-rest-parte-1/" target="_blank">Windows Azure Internals: Trabalhando com Storage Service e API REST (parte 1)</a></p>
<p><a href="http://vitormeriat.wordpress.com/2012/03/21/windows-azure-internals-trabalhando-com-storage-service-e-api-rest-parte-2/" target="_blank">Windows Azure Internals: Trabalhando com Storage Service e API REST (parte 2)</a></p>
<p>&#160;</p>
<h2><font color="#666666">Um ótimo estudo a todos….</font></h2>
<p><a href="http://meriat.files.wordpress.com/2012/03/ass-copy.png"><img style="display:inline;float:left;margin:0 20px 0 0;" title="Ass copy"   alt="Ass copy" align="left" src="http://blob.vitormeriat.com.br/images/ass-copy.png?w=120&amp;h=120" width="106" height="106" /></a></p>
<h2><font color="#ff8000"><font>Twitter:</font></font> <font color="#4f81bd"><font>@vitormeriat</font></font></h2>
<h2><a href="mailto:vitormeriat@gmail.com"><font color="#4f81bd">vitormeriat@gmail.com</font></a></h2>
<h2><a href="mailto:vitor.pereira@studentpartners.com.br"><font color="#4f81bd" size="4">vitor.pereira@</font></a><a href="https://www.google.com.br/search?hl=pt-BR&amp;sa=X&amp;ei=cctpT6OgFcvBgAfRjbnUCQ&amp;ved=0CCUQvwUoAA&amp;q=studentpartners&amp;spell=1"><i><font color="#4f81bd" size="4">studentpartners</font></i></a><font color="#4f81bd" size="4">.com.br</font></h2>