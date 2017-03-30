---
layout: post
title: 'Windows Azure Storage: Azure Storage Emulator e Armazenamento na Nuvem'
date: 2011-08-10
categories:
    - Cloud Computing
    - Microsoft Azure
    - Microsoft Azure Storage
---

<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/06.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border-width:0;margin:0 10px 0 0;" title="06"   alt="06" align="left" src="http://blob.vitormeriat.com.br/images/2011/08/06.png" width="310" height="218" /></a>
<p align="justify">Uma das vantagens de uma oferta SaaS é poder oferecer uma baixa curva de aprendizagem para o desenvolvimento de aplicações. Como já vimos anteriormente, o Windows Azure no modelo software como serviço traz aos desenvolvedores esta facilidade. Toda a estrutura de um projeto Azure mantém familiaridade a um projeto Web comum, seja WebForm ou MVC por meio de seus papeis.
<p align="justify">Para acessarmos nossa conta de armazenamento no Windows Azure, assim como necessário para qualquer aplicação web, devemos fornecer as credenciais para tal fim. É comum encontrarmos em ambientes de desenvolvimento com bases de produção e homologação, e é ai que se inicia a brincadeira.
<p align="justify">É na string de conexão que informamos os parâmetros que são necessários para acessar a conta de armazenamento. Você pode configurar a string de conexão para as seguintes finalidades:
<ul>
<ul>
<li>
<div align="justify">Conectar o Windows Azure Storage Emulator para testes locais.</div>
</li>
<li>
<div align="justify">Conectar a uma conta de armazenamento no Windows Azure usando os terminais (endpoints) padrão.</div>
</li>
<li>
<div align="justify">Conectar a uma conta de armazenamento no Windows Azure usando terminais (endpoints) explícitos.</div>
</li>
</ul>
</ul>
<p><!--more-->
<p align="justify">Assim como em uma aplicação Web, podemos por meio das definições de configuração fornecer uma ou mais strings de conexão. Isso nos possibilita a conforme a necessidade apontar para uma conta diferente. </p>
<p align="justify">&nbsp;</p>
<h3 align="justify">Armazenamento no Azure Storage Emulator</h3>
<p align="justify">A plataforma Azure fornece um ambiente de desenvolvimento por meio do <b>Windows</b> <b>Azure storage emulator</b> que funciona como uma “nuvem local” para os serviços de armazenamento (blobs, queues, tables) para que você possa construir e testar suas aplicações antes da implantação no Windows Azure. Esta conta local possui um nome e chave comuns a todos os usuários o que nos possibilita o uso de uma sequência de “atalho” que faz referência a conta de armazenamento, a saber: <b>UseDevelopmentStorage=true</b>. Esta conta e chave comuns só permitem o acesso aos serviços locais de armazenamento. A título de informação:
<ul>
<ul>
<li>
<div align="justify"><b>AccountName</b>: devstoreaccount1</div>
</li>
<li>
<div align="justify"><b>AccountKey</b>: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1 SZFPTOtr/KBHBek soGMGw==</div>
</li>
</ul>
</ul>
<p align="justify"><font color="#777777"></font>Observe o código abaixo: </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/01.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="01"   alt="01" src="http://blob.vitormeriat.com.br/images/2011/08/01.png" width="570" height="229" /></a>
<p align="justify">Quando estamos desenvolvendo no ambiente de desenvolvimento temos acesso as credenciais da conta de armazenamento local por meio da propriedade DevelopmentStorageAccount da classe CloudStorageAccount que obtém um objeto do mesmo tipo que referência a conta de armazenamento de desenvolvimento.
<p align="justify">Seguindo a lógica citada anteriormente, podemos fornecer o nome e chave de acesso a nossa conta de armazenamento de desenvolvimento como no código abaixo:
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/02.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="02"   alt="02" src="http://blob.vitormeriat.com.br/images/2011/08/02.png" width="570" height="219" /></a>
<p align="justify">Cabe aqui fazer uma observação: O esquema de URI trabalhado pelo emulador de armazenamento é diferente do esquema utilizado pelos serviços de armazenamento na nuvem. No ambiente de desenvolvimento o nome da conta faz parte do caminho hierárquico da URI já no armazenamento na nuvem o nome da conta faz parte do nome de domínio. Isto ocorre devido a resolução de nomes de domínio estarem disponíveis na nuvem, mas não no computador local. </p>
<p align="justify">Devido a limitação citada acima, o esquema URI do emulador de armazenamento&nbsp; segue este formato:</p>
<p align="justify"><a href="http://&lt;endereco-maquina-local&gt;:&lt;porta&gt;/&lt;nome-da-conta&gt;/&lt;recurso">http://&lt;endereco-maquina-local&gt;:&lt;porta&gt;/&lt;nome-da-conta&gt;/&lt;recurso</a>&gt;</p>
<p align="justify">Os serviços&nbsp; podem ser acessados com os seguintes esquemas URI:</p>
<ul>
<ul>
<li>
<div align="justify">Blob: http://127.0.0.1:10000/&lt;nome-da-conta&gt;/&lt;recurso&gt;</div>
</li>
<li>
<div align="justify">Queue: http://127.0.0.1:10001/&lt;nome-da-conta&gt;/&lt;recurso&gt;</div>
</li>
<li>
<div align="justify">Table: http://127.0.0.1:10002/&lt;nome-da-conta&gt;/&lt;recurso&gt;</div>
</li>
</ul>
</ul>
<p align="justify"><font color="#777777">Um exemplo prático de endereço usado para acessar um blob no emulador de armazenamento seria:</font></p>
<p align="justify"><a href="http://127.0.0.1:10000/minhaconta/meucontainer/meublob.txt">http://127.0.0.1:10000/minhaconta/meucontainer/meublob.txt</a></p>
<blockquote><p align="justify">O emulador de armazenamento se baseia em um Microsoft SQL Server e fornece serviços semelhantes aos do armazenamento no Windows Azure. Por padrão, o emulador de armazenamento é configurado para um banco de dados Microsoft SQL Server Express nas versões 2005 ou 2008. Você pode instalar o SQL Server Management Studio Express para gerenciar sua instalação do SQL Server Express. Não é recomendado alterar a base gerada.</p>
</blockquote>
<p align="justify">O emulador de armazenamento é um processo (DSService.exe) que permite a utilização de uma interface para iniciar, parar, redefinir instâncias ou simplesmente desligar os serviços. Você pode acessar a interface seguindo os passos abaixo.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/05.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="05"   alt="05" src="http://blob.vitormeriat.com.br/images/2011/08/05.png" width="570" height="247" /></a></p>
<p align="justify">&nbsp;</p>
<h3 align="justify">Armazenamento na Nuvem</h3>
<p align="justify">Você pode definir uma string de conexão para uma conta de armazenamento no Windows Azure de duas formas:
<ul>
<ul>
<li>
<div align="justify">Utilizar os endpoints padrão para os serviços de armazenamento. Esta é a opção mais simples uma vez que quando você usa este formato é necessário apenas informar o nome da conta e a chave e indicar se deseja conectar através de&nbsp; HTTP ou HTTPS. </div>
</li>
<li>
<div align="justify">Especificar endpoints explícitos para os serviços de armazenamento, permitindo especificar endpoints para os serviços incluindo um nome de domínio personalizado ou minimizando a exposição de informações para um acesso compartilhado etc.</div>
</li>
</ul>
</ul>
<p align="justify"><font color="#777777">Formato utilizando endpoints padrão:</font></p>
<ul>
<li>
<div align="justify"><code>DefaultEndpointsProtocol=[http|https];AccountName=nomeConta;AccountKey=chaveConta</code></div>
</li>
</ul>
<p align="justify">Formato utilizando endpoints explícitos: </p>
<ul>
<li>
<div align="left">BlobEndpoint=meuBlobEndpoint;QueueEndpoint=meuQueueEndpoint;&nbsp; TableEndpoint=meuTableEndpoint; AccountName=meuAccountName; AccountKey=meuAccountKey</div>
</li>
</ul>
<p align="justify">O esquema básico de endereçamento para utilizar os recursos de armazenamento na nuvem é: &lt;http|https&gt;://&lt;account-name&gt;.&lt;service-name&gt;.core.windows.net/&lt;resource-path&gt; onde account-name representa o nome da conta, service-name o nome do serviço que esta sendo acessado e resource-path o recurso solicitado. Segue um exemplo com os esquemas URI para cada um dos serviços:</p>
<ul>
<ul>
<li>
<div align="justify">Blob: &lt;http|https&gt;://&lt;nome-da-conta&gt;.blob.core.windows.net/&lt;recurso&gt;</div>
</li>
<li>
<div align="justify">Queue: &lt;http|https&gt;://&lt;nome-da-conta&gt;.queue.core.windows.net/&lt;recurso&gt;</div>
</li>
<li>
<div align="justify">Table: &lt;http|https&gt;://&lt;nome-da-conta&gt;.table.core.windows.net/&lt;recurso&gt;</div>
</li>
</ul>
</ul>
<p align="justify">Um exemplo prático de endereço acessando um blob seria:</p>
<p align="justify"><a href="http://vitormeriat.blob.core.windows.net/meucontainer/meublob.txt">http://vitormeriat.blob.core.windows.net/meucontainer/meublob.txt</a></p>
<p align="justify">O código fonte do exemplo utilizado neste artigo pode ser baixado <a href="https://skydrive.live.com/?cid=bd055aa47a388023#!/?cid=bd055aa47a388023&amp;sc=documents&amp;uc=1&amp;id=BD055AA47A388023%21218" target="_blank">aqui!</a></p>
<p>
<hr />
<p>PS: Estreando outro desenho do mascote…</p>
<p>&nbsp;</p>
<h3>Um grande abraço e ótimo estudo!</h3>