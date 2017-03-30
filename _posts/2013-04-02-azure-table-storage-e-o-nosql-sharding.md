---
layout: post
title: Azure Table Storage e o NoSQL – Sharding
date: 2013-04-02 
categories:
- Cloud Computing
- Microsoft Azure
- Microsoft Azure Storage

---
<p align="justify">Vamos continuar nossa viagem no mundo do cloud storage, agora com foco na necessidade da escalabilidade para a computação na nuvem.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/04/sharddiagram-4.jpg"><img title="ShardDiagram-4" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="ShardDiagram-4" src="http://blob.vitormeriat.com.br/images/sharddiagram-4.jpg" width="560" height="229" /></a></p>
<p align="justify">A <strong>escalabilidade</strong> é um tema amplo, portanto para este post vamos vislumbrar este tema sobre o ângulo dos Bancos de Dados, um assunto extremamente delicado no cenário de desenvolvimento atual. Não espere algo no nível internals, vou apenas introduzir o assunto para prosseguir no assunto desta mini-série.</p>
<p align="justify">Vamos pensar no cenário atual que já me referi anteriormente. Sistemas web e aplicativos mobile com milhares de usuários simultâneos cada vez mais exigentes. Seu banco de dados têm de ser &quot;escalado&quot;, porque, com um número X de usuários não importa o quanto você otimizar o desempenho, em algum ponto você não será capaz de processar tudo dentro de um servidor db. Isto é particularmente verdade para os prestadores de serviços on-line, os softwares como serviço (<strong>SaaS</strong>), empresas e sites de redes sociais. Com isso você será obrigado a dividir seus dados em vários servidores. Isso acaba criando um novo problema: Você precisa ser capaz de descobrir em qual servidor seus dados estão...</p>
<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; ... A solução .... <strong>Sharding</strong></p>
<p><!--more-->
<p align="justify">O movimento NoSQL tenta proteger seus usuário desta complexidade implementando o sharding de maneira transparente, embora eu ache que mesmo assim, devemos conhecer o conceito básico de sharding antes de prosseguirmos neste assunto.</p>
<p>&#160;</p>
<h2 align="justify">Necessidade</h2>
<p align="justify">Sharding é uma abordagem altamente escalável para melhorar o desempenho. Desde o início do banco de dados relacional que os engenheiros e arquitetos de software têm exigido cada vez maior desempenho e capacidade pela simples observação que os bancos de dados envolvidos nos negócios atuais crescem rapidamente com o tempo. </p>
<p align="justify">Vamos usar de exemplo o poderoso <strong>Facebook</strong>. No início de 2004 ele era &quot;só&quot; um anuário online utilizado apenas pelos estudantes de Harvard. Não era necessário mais do que um servidor para suprir todos os requisitos de armazenamento e carga de consulta. Quatro anos depois apenas os aplicativos para o Facebook contabilizavam cerca de 5.000 visualizações por segundo, sendo que cada um requer consultas em back-end para o preenchimento de dados. Isso demanda custos para a CPU, Memória e capacidade de armazenamento. Em 2009 o Facebook tinha 40.000.000.000 arquivos físicos para representar cerca de 10 bilhões de fotos que é mais de um petabyte de armazenamento. Mesmo sendo improvável o armazenamento real de fotos em um banco de dados relacional, seus metadados e identificadores ainda exigiriam de maneira extrema do armazenamento para representar essas fotos no banco de dados. Você acha que o banco de dados original do Facebook estava preparado para os terabytes de armazenamento vindouros?</p>
<p align="justify">Como qualquer <strong>DBA</strong> ou desenvolvedor experiente sabe, é evidente que o tamanho e o volume de transações de um banco de dados cresce de maneira linear, neste caso o tempo de resposta tende a crescer exponencialmente. Observe o diagrama abaixo:</p>
<p align="justify">&#160;</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/03/0001.png"><img title="0001" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="0001" src="http://blob.vitormeriat.com.br/images/0001.png" width="392" height="324" /></a></p>
<p align="justify"><em>O crescimento nas transações e do volume do banco de dados tem impacto no tempo de resposta.</em></p>
<p align="justify">&#160;</p>
<h2 align="justify">Conceito</h2>
<p align="justify">Sharding banco de dados fornecem um método para escalabilidade em servidores independentes, cada um com a sua própria CPU, memória e disco. O conceito de uma implementação de banco de dados &quot;shared-nothing&quot; tem estado sob observação na última década, mas ao que parece, somente agora o mercado de aplicativos de negócios está demandando desta tecnologia devido o aumento exponencial do volume de dados nos últimos anos. </p>
<p align="justify">Sharding é um padrão que permite aumentar a escalabilidade e a performance de grandes bases de dados. Aplicar este padrão a uma base de dados significa “partir” essa base de dados em pedaços menores e distribui-los por vários servidores de modo a obter escalabilidade. A cada pedaço resultante chamamos de <strong>shard</strong> (fragmento).</p>
<p align="justify">Um fragmento é um ou mais servidores em <strong>cluster*</strong> que são responsáveis por um subconjunto de dados. Se tivéssemos um cluster com 1.000.000 de documentos que representam os usuários de um site, neste caso um shard pode conter informações sobre 200 mil destes usuários. </p>
<blockquote><p align="justify">Cluster na sua forma mais básica é um sistema que compreende dois ou mais computadores ou sistemas (denominados nodos) na qual trabalham em conjunto para executar aplicações ou realizar outras tarefas, de tal forma para que os usuários que os utilizam tenham a impressão que somente um único sistema responde para eles, criando assim uma ilusão de um recurso único (computador virtual).</p>
</blockquote>
<p align="justify">O conceito básico de Sharding é muito simples: pegue um grande banco de dados, e quebre-o em uma série de bancos de dados menores. O conceito é ilustrado no diagrama a seguir:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/04/white-paper-dbshards.png"><img title="white-paper-dbshards" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="white-paper-dbshards" src="http://blob.vitormeriat.com.br/images/white-paper-dbshards.png" width="344" height="358" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Neste padrão são as linhas das tabelas que são divididas pelos vários servidores. Uma outra opção seria realizar o particionamento vertical. No particionamento vertical os dados são separados por distribuição de tabelas completas entre os servidores. Meter a tabela de clientes num servidor e a tabela de vendas noutro servidor seria um exemplo de partição vertical. A partição de dados por valor (sharding) permite atingir maior escalabilidade porque, por exemplo, não está limitada ao número de tabelas existentes na aplicação e permite a divisão de tabelas com mais acessos.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/03/5165-image005.png"><img title="5165.image005" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="5165.image005" src="http://blob.vitormeriat.com.br/images/5165-image005.png" width="241" height="102" /></a></p>
<p align="center"><em>Sharding de uma base de dados</em></p>
<p align="justify">&#160;</p>
<p align="justify">Nas aplicações multi-tenant podemos começar com uma única base de dados e, à medida que o volume de carga vai crescendo, usar o padrão de sharding para distribuir os dados dos clientes por várias bases de dados.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/03/3250-image006.png"><img title="3250.image006" style="background-image:none;float:none;padding-top:0;padding-left:0;margin:0 auto 1px;display:block;padding-right:0;border-width:0;"   alt="3250.image006" src="http://blob.vitormeriat.com.br/images/3250-image006.png" width="257" height="100" /></a></p>
<p align="center"><em>Sharding numa aplicação multi-tenant</em></p>
<p align="justify">&#160;</p>
<p align="justify">Sharding requer algum tipo de search (pesquisa). Imagine que você criou uma tabela para armazenar nomes de cidades em ordem alfabética. Precisamos de algum mecanismo para identificar as cidades por exemplo, de A até D estão no servidor SERVER1, e de P até Z estão no SERVER4 e etc.</p>
<p align="justify">&#160;</p>
<h2>Categorias</h2>
<p align="justify">Conceitualmente, Sharding pode ser enquadrado em três categorias:</p>
<ol>
<li>
<div align="justify"><strong>O particionamento Vertical </strong>- Todos os dados relacionados com uma característica específica são armazenadas nas mesmas máquinas. </div>
</li>
<li>
<div align="justify"><strong>Chaves de particionamento</strong> - Um fragmento de dados em si é usado para fazer o particionamento. A forma mais comum é a utilização de um algoritmo de hashing para mapear os dados que serão direcionados a um dos fragmentos para serem armazenados. Utilizar hashes com intervalos de tempo também é uma prática comum. </div>
</li>
<li>
<div align="justify"><strong>Diretório de particionamento </strong>- Neste esquema, uma tabela que mantém o controle de quais dados são armazenados em que fragmento é mantido no cluster. A desvantagem desta abordagem: o diretório se torna um ponto único de falha e há uma sobrecarga de desempenho já que o diretório precisa ser acessado constantemente.</div>
</li>
</ol>
<p>&#160;</p>
<h2>Vantagens</h2>
<p align="justify">A vantagem óbvia da abordagem do Sharding é a melhoria, escalabilidade crescente de uma forma quase linear como mais servidores sendo adicionados à rede. No entanto, existem várias outras vantagens de bases de dados mais pequenas, que não devem ser ignoradas quando se considera uma solução sharding:</p>
<ul>
<li>
<div align="justify">Bancos de dados menores são mais fáceis de gerenciar. Bases de dados de produção devem ser totalmente gerenciados para backups regulares, otimização e outras tarefas comuns. Com uma base de dados única (estamos falando de um DB grande), estas tarefas de rotina podem ser muito difíceis de realizar. Algumas tarefas podem durar horas ou dias, tornando em alguns casos a manutenção regular inviável. Ao utilizar a abordagem sharding, cada &quot;shard&quot; individual pode ser mantida de forma independente, proporcionando um cenário muito mais gerenciável, realizando tarefas de manutenção, em paralelo. </div>
</li>
<li>
<div align="justify">Bancos de dados menores são mais rápidos. A escalabilidade do sharding é aparente, conseguida através da distribuição e processamento de múltiplos fragmentos de servidores na rede. Ao hospedar cada banco de dados shard em um próprio servidor, a relação entre memória e os dados no disco é muito melhor, reduzindo assim o consumo de I/O. Isso resulta em menos contenção de recursos, maior desempenho de junção, buscas mais rápidas de índice e menos bloqueios de banco de dados.    </div>
</li>
</ul>
<p align="justify">Não há dúvida de que Sharding de banco de dados é uma solução viável para muitas organizações, apoiadas pelo número de grandes organizações de <strong>SaaS</strong> que implementaram a tecnologia (gigantes como a Microsoft, Amazon, eBay e Google).</p>
<p>&#160;</p>
<h2><font style="font-weight:bold;" color="#d19049">Até mais e bom estudo a todos!</font></h2>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 15px 0 0;display:inline;"   alt="Me Azul" align="left" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" height="110" /></a></p>
<h3><font color="#309c3e"><font style="font-weight:bold;" size="4">Twitter:</font></font><font style="font-weight:bold;"> </font><a href="http://twitter.com/#!/vitormeriat"><font color="#1a79b3"><font style="font-weight:bold;">@vitormeriat</font></font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font color="#1a79b3"><font style="font-weight:bold;">vitormeriat@gmail.com</font></font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font color="#1a79b3"><font style="font-weight:bold;">vitor.pereira@studentpartner.com</font></font></a></h3>
