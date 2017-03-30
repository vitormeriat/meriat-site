---
layout: post
title: 'Windows Azure Internals: Trabalhando com Storage Service e API REST (parte
  2)'
date: 2012-03-21 13:00:00.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure

---
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/figura2.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;border-top:0;margin-right:auto;border-right:0;padding-top:0;" title="Figura2"   alt="Figura2" src="http://blob.vitormeriat.com.br/images/figura2.png" width="560" height="358" /></a></p>
<p><!--more--><br />
<h2>&#160;</h2>
<h2>Os primeiros passos</h2>
<p align="justify">Antes de continuar nosso artigo, é importante repassarmos alguns termos importantes juntamente com o seu comportamento em relação ao Azure.</p>
<h3 align="justify"><font>URL</font></h3>
<p align="justify">A URL identifica o recurso que você deseja obter. No armazenamento do Windows Azure, isso normalmente inclui o nome da conta no hostname, e o recurso informado no caminho.</p>
<h3 align="justify"><font>Headers (cabeçalhos)</font></h3>
<p align="justify">Para cada requisição (<strong>request</strong>) ou resposta(<strong>response</strong>) em HTTP, temos um cabeçalho que fornece as informações necessárias sobre o pedido. Você pode se utilizar destes cabeçalhos para gerar um novo cabeçalho para permitir que o servidor valide sua origem, identificando como seu. Existem também cabeçalhos personalizados para determinadas operações. No Windows Azure Storage Service, todos os cabeçalhos personalizados tem um prefixo <strong>x-ms-</strong>.</p>
<h3 align="justify"><font>Métodos HTTP</font></h3>
<p align="justify">O método HTTP indica a ação exata a ser executada. O Windows Azure utiliza apenas os seguinte métodos:</p>
<ul>
<li>
<div align="justify"><strong>GET</strong>: Recupera a representação padrão de um recurso. Para uma Queue, este é o conteúdo de uma mensagem. Para uma entidade da tabela, esta será uma versão XML da entidade, e assim por diante. </div>
</li>
<li>
<div align="justify"><strong>PUT</strong>: Cria ou atualiza um recurso. Você normalmente colocar a URL de um recurso com o corpo do pedido contendo os dados que você deseja carregar. </div>
</li>
<li>
<div align="justify"><strong>POST</strong>: É usado para atualizar os dados de uma entidade. Ele é semelhante ao PUT, diferindo apenas no fato que normalmente você espera que o recurso já existe na URL informada. </div>
</li>
<li>
<div align="justify"><strong>DELETE</strong>: Exclui o recurso especificado na URL. </div>
</li>
</ul>
<h3 align="justify"><font>Status code (Código de Status)</font></h3>
<p align="justify">A especificação HTTP documenta mais de 40 códigos de status diferentes. Felizmente, você tem que se preocupar com apenas um pequeno subconjunto desses 40 códigos. Estes são usados para contar-lhe o resultado da operação-se bem sucedida ou não, e se não, uma dica a respeito de porque ele falhou. Aqui estão as principais classes de códigos de status:</p>
<ul>
<li>
<div align="justify"><strong>2xx (Está tudo OK)</strong>     <br />Códigos de resposta na gama 2xx geralmente significar que a operação teve êxito. Quando você criar com êxito um blob, você recebe de volta um 201, e quando você enviar um GET para um blob, você recebe de volta um 200. </div>
</li>
<li>
<div align="justify"><strong>3xx (Não Modificado)</strong>     <br />No mundo web padrão, os códigos na gama 3xx são usados para controlar o cache e redirecionamento. No Azure, apenas o código 304 pode ocorrer. Quando você trabalha com um recurso, você obtém uma <strong>ETag</strong> associada a ele. Você pode pensar em uma ETag como um identificador exclusivo que especifica qual é o estado atual dos dados no servidor. Se houver alteração de dados durante a manipulação do recurso, sua ETag também vai mudar. Se você especificar uma ETag sem que o recurso tenha sido alterado, você receberá um código 304. ETags também são utilizados para implementar concorrência otimista. </div>
</li>
<li>
<div align="justify"><strong>4xx (Bad request)</strong>     <br />Códigos na faixa 4xx significam que a solicitação falhou por algum motivo. Isto pode ocorrer devido cabeçalhos incorretos, URL incorreta, a conta ou recurso não existe, etc. O corpo da resposta conterá mais informações sobre o motivo da falha na resposta. Dois códigos a serem observados são 403 (informações de autenticação inválidas) e 404 (recurso inexistente). </div>
</li>
<li>
<div align="justify"><strong>5xx (Tenso… Algo de errado aconteceu no servidor)  <br /></strong>Se existe um código que você não vai querer ver, serão os códigos desta faixa. Eles sinalizam que um erro desconhecido ocorreu no servidor ou o menos provável, que ele está ocupado demais para lidar com as solicitações. Caso isso aconteça, o mais provável é que você tenha solicitado um conjunto de dados muito grande e a operação expirou. </div>
</li>
</ul>
<p align="justify"><font color="#777777">.</font></p>
<h2 align="justify"><font color="#777777">Codificando RESTful no Windows Azure Storage</font></h2>
<p align="justify"><font color="#777777">Agora vamos iniciar a parte pesada da brincadeira, codificar nossa API de acesso ao Storage do Windows Azure. Esta não é uma coisa habitual a se fazer, a intenção e conhecer mais a fundo o funcionamento dos serviços de Storage do Azure e não focar na criação da API em si. </font><font color="#777777">Vamos explorar apenas alguns serviços dos blobs, queues e tables.</font></p>
<p align="justify"><font color="#777777"></font></p>
<p align="justify">
<p align="justify"><font color="#777777"></font></p>
<p><font color="#777777"></font></p>
<h3><font>1º passo: Classe Base</font></h3>
<p align="justify">Vamos criar uma classe base <strong>StorageAzure</strong>, contendo as constantes do cabeçalho e um construtor para instanciar as credenciais da conta no Azure. Observem que temos quatro campos para instanciarmos a conta, senha e host do serviço seja do ambiente de desenvolvimento local seja da subcription do azure, e um campo que define em que ambiente estamos trabalhando respectivamente. </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem1.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;margin:0;" title="Listagem1_thumb4"   alt="Listagem1_thumb4" src="http://blob.vitormeriat.com.br/images/listagem1.png" width="560" height="360" /></a></p>
<p align="justify">Com isso já é possível codificar o método <strong>RequisicaoDeArmazenamento</strong> que será responsável por montar e executar a requisição com base no recurso solicitado. Vamos observar o método <strong>RequisicaoDeArmazenamento:</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem2.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;margin:0;" title="Listagem2_thumb2"   alt="Listagem2_thumb2" src="http://blob.vitormeriat.com.br/images/listagem2.png" width="560" height="479" /></a></p>
<p align="justify">Primeiro criamos o pedido definindo a <strong>URI </strong>e criando a requisição. Como nossa API está flexível para trabalhar na nuvem ou utilizar o <strong>Storage Emulator</strong>, então estou fazendo uma verificação de qual ambiente está sendo utilizado para montar a URI corretamente. Informamos o método <strong>HTTP</strong> a ser trabalhado, se há dados e caso haja informa o tamanho do conteúdo e o seu tipo. Adiciona no cabeçalho a propriedade <strong>x-ms-date</strong> que é obrigatória e define o <a href="http://pt.wikipedia.org/wiki/Tempo_Universal_Coordenado" target="_blank">UTC</a>(<i>Universal Time Coordinated</i>) para a solicitação. Adiciona as propriedades específicas do cabeçalho de solicitação e chama a rotina para assinatura da solicitação.</p>
<p align="justify">Existem mais dois outros métodos para criar a assinatura da requisição. Notem que existe um método específico para a assinatura da requisição quando trabalhamos com Tabelas, veremos mais detalhes no próximo passo.</p>
<p align="justify">&#160;</p>
<p align="justify">
<h3 align="justify"><font>2º passo: Assinatura</font></h3>
<p align="justify">Já vimos que o serviço de armazenamento do azure é exposto via REST, já montamos nossa requisição e o cabeçalho então agora é só fazer o pedido. Certo? Bem, nós podemos mas a tarefa se torna um pouco complexo devido à necessidade de um cabeçalho de autorização válida. Quando você criar seu projeto Azure Storage, uma chave de acesso principal é criado. Esta é a chave que você usará para assinar sua mensagem. Esta mensagem assinada é passada no cabeçalho HTTP de autorização. O servidor irá usar isso para autenticar o pedido. Sem este trecho de código não será possível obter sucesso nas requisições. Mesmo tendo a URI e todos os cabeçalhos corretos, sem a assinatura e autorização corretos nossa requisição vai falhar. </p>
<p align="justify">Confira a listagem do método <strong>AssinarRequisicao</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem3.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;margin:0;" title="Listagem3_thumb2"   alt="Listagem3_thumb2" src="http://blob.vitormeriat.com.br/images/listagem3.png" width="560" height="434" /></a></p>
<p align="justify">O primeiro elemento da assinatura é o método <strong>HTTP</strong> a ser utilizado. o Segundo elemento define o <strong>hash MD5 </strong>para a verificação da integridade, é opcional e não será utilizado neste exemplo. Adicionamos o Content-Type da requisição. O próximo elemento é a Data, desde que este elemento tenha sido definido no cabeçalho podemos passar uma string vazia. Classifica e ordena os cabeçalhos que se iniciam com <strong>x-ms</strong>. Com a sequência pronta, vamos utilizar nossa <strong>secret key</strong> para gerar um <strong>hash HMAC SHA256</strong> e adicionar a autorização no cabeçalho.</p>
<p>Confira a listagem do método <strong>AssinarRequisicaoParaTable</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/listagem4.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;margin:0;" title="Listagem4_thumb2"   alt="Listagem4_thumb2" src="http://blob.vitormeriat.com.br/images/listagem4.png" width="560" height="281" /></a></p>
<p align="justify">Para se acessar o serviço de armazenamento de tabelas do azure foi necessário um pouco mais de trabalho da minha parte. O fato de trabalhar através de ADO.NET Data Services requer algumas especificações em relação aos demais serviços. </p>
<p align="justify">Observe que, para a assinatura de armazenamento da tabela, estou removendo a string de consulta a partir do recurso, mas para armazenamento de blobs e queues não há esta necessidade. Isso está documentado na API embora eu não tenha notado e isto tenha me valido um bom tempo.</p>
<p align="justify">Qual a real importância de se usar essas chaves? Cada pedido que você faz para o serviço de armazenamento tem uma URL e cabeçalhos que são incluídos com o pedido. Você usa a chave para assinar o pedido, e inseri a assinatura no pedido como um cabeçalho. Mesmo que o pedido seja interceptado, não será possível recuperar a sua chave privada a partir da solicitação. Como a data e a hora é parte do pedido, caso ele seja interceptado não será possível usá-lo para fazer novos pedidos.</p>
<p align="justify">No próximo post vamos falar sobre a codificação dos serviços de Blob, Queues, Tables e definições de conta.</p>
<p align="justify"><a href="http://vitormeriat.wordpress.com/2012/03/21/windows-azure-internals-trabalhando-com-storage-service-e-api-rest-parte-1/" target="_blank">Windows Azure Internals: Trabalhando com Storage Service e API REST (parte 1)</a></p>
<h3>
<p>&#160;</p>
<h2><font color="#666666">Um ótimo estudo a todos….</font></h2>
<p><a href="http://meriat.files.wordpress.com/2012/03/ass-copy.png"><img style="display:inline;float:left;margin:0 20px 0 0;" title="Ass copy"   alt="Ass copy" align="left" src="http://blob.vitormeriat.com.br/images/ass-copy.png?w=120&amp;h=120" width="106" height="106" /></a></p>
<h2><font color="#ff8000"><font>Twitter:</font></font> <font color="#4f81bd"><font>@vitormeriat</font></font></h2>
<h2><a href="mailto:vitormeriat@gmail.com"><font color="#4f81bd">vitormeriat@gmail.com</font></a></h2>
<h2><a href="mailto:vitor.pereira@studentpartners.com.br"><font color="#4f81bd" size="4">vitor.pereira@</font></a><a href="https://www.google.com.br/search?hl=pt-BR&amp;sa=X&amp;ei=cctpT6OgFcvBgAfRjbnUCQ&amp;ved=0CCUQvwUoAA&amp;q=studentpartners&amp;spell=1"><i><font color="#4f81bd" size="4">studentpartners</font></i></a><font color="#4f81bd" size="4">.com.br</font></h2>
</h3>