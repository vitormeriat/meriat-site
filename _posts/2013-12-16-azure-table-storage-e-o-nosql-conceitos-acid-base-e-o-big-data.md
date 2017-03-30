---
layout: post
title: Azure Table Storage e o NoSQL – Conceitos, ACID, BASE e o Big Data
date: 2013-12-16 13:20:34.000000000 -02:00
type: post
published: true
status: publish
categories:
- Big Data
- Cloud Computing
- Microsoft Azure
- Microsoft Azure Storage
- NoSQL

---
<p align="justify">Segue mais um capítulo desta saga. Desta vez vamos passar por alguns conceitos sobre <strong>NoSQL</strong>, sua forma e arquitetura base, escalabilidade, desempenho e sua relação com o <strong>Big Data</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/capa.png"><img title="capa" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="capa" src="http://blob.vitormeriat.com.br/images/capa.png" width="560" height="340" /></a></p>
<p><!--more-->
<p>Antes de prosseguir, recomendo a leitura dos seguintes posts:</p>
<ul>
<ul>
<li><a href="http://vitormeriat.com.br/2013/03/05/azure-table-service-e-o-nosql-introduo/" target="_blank">Azure Table Service e o NoSQL – Introdução</a> </li>
<li><a href="http://vitormeriat.com.br/2013/03/20/azure-table-storage-e-o-nosql-cluster-e-dht/" target="_blank">Azure Table Storage e o NoSQL – Cluster e DHT</a> </li>
<li><a href="http://vitormeriat.com.br/2013/04/02/azure-table-storage-e-o-nosql-sharding/" target="_blank">Azure Table Storage e o NoSQL – Sharding</a> </li>
</ul>
</ul>
<p align="justify">Nestes posts abordei alguns dos temas principais para o surgimento do tão falado NoSQL. Uma abordagem explicando algumas das limitações e necessidades que levaram ao surgimento de uma tecnologia capaz de atender alguns dos requisitos da <strong>Big Data</strong>, <strong>Big Users</strong> e escalabilidade.</p>
<p>&#160;</p>
<h2>Introdução</h2>
<p align="justify">As tecnologias e sistemas tem evoluído a passos largos. Sistemas web e aplicativos mobile tem arquiteturas com suporte a milhões de usuários simultâneos, espalhando sua carga em um conjunto de servidores atrás de um <strong>balanceador de carga</strong>. Muito se tem exigido dos bancos de dados dentro deste cenário, mesmo que estes não tenham acompanhado esta evolução na mesma proporção.</p>
<blockquote><p align="justify">Em alguns aspectos, este é o último dominó a cair na marcha inevitável em direção a uma arquitetura de software totalmente distribuída (se é possível ansiar por isso). </p>
</blockquote>
<p align="justify">Li isto em um artigo que afirmava ser um empecilho o famoso modelo de dados relacional. É claro que para as novas necessidades temos técnicas como sharding horizontal e vertical, cache distribuído e desnormalização de dados mas, essas táticas &quot;anulam&quot; os principais benefícios do modelo relacional, enquanto aumentam o custo e complexidade do desenvolvimento.</p>
<p align="justify">Ainda não encontrei uma linha de pensamento afirmando (o que faz todo o sentido) que todo o modelo relacional é ultrapassado e obsoleto, na verdade, o consenso é que existem novas necessidades e que em certos pontos fica inviável se utilizar do modelo atual.</p>
<p align="justify">O modelo de banco de dados relacional tem sido por convenção o modelo mais adotado até o presente momento. Muito provavelmente se você é programador aprendeu os princípios de sua profissão no desenvolvimento orientado ao modelo. Primeiro passo é fazer o modelo de dados, depois você faz a lógica e por último a casca... É como alguns pensam.</p>
<p align="justify"><strong>Martin Fowler</strong> em seu livro &quot;<strong>NoSQL Distilled</strong>&quot;, traz alguns questionamentos importantes sobre o destino do banco de dados relacional. A sábia conclusão é que caminhamos para uma pluralidade de persistências onde empresas ou aplicativos usem distintas tecnologias de gerenciamento de dados conforme a necessidade. O termo introduzido por ele e <strong>Polyglot Persistence</strong> (Persistência Poliglota).</p>
<p align="justify">Neste livro algumas ideias e conceitos de Fowler que me chamaram a atenção:</p>
<ul>
<ul>
<li>
<div align="justify">A ascensão do NoSQL marca o fim da era de domínio do Banco de Dados Relacional... Entendendo que os bancos de dados relacionais não serão a &quot;escolha automática&quot;.</div>
</li>
<li>
<div align="justify">BIG DATA é o caminho de ascensão para o NoSQL, mas não é o único motivo para usá-lo... Não é apenas pelo fato de ser um modelo de banco de dados projetado para um melhor funcionamento com grandes quantias de dados. Sua utilização se justifica em aplicações com estruturas de modelos simples.</div>
</li>
<li>
<div align="justify">A mudança é um fato e você precisa aproveitá-la... A ideia que o NoSQL é um necessidade e que os profissionais de dados vão precisar combinar as tecnologias para uma melhor solução conforme a necessidade.</div>
</li>
</ul>
</ul>
<p>Sob qualquer ângulo isso implica necessariamente em estar familiarizado com o conceito do NoSQL, o que passa por uma nova visão sobre a modelagem e consistência de dados.</p>
<p>&#160;</p>
<h2>NoSQL is BORN</h2>
<p align="justify">Como já falei nos posts anteriores, a ênfase de um banco de dados relacional se baseia em um conjunto de propriedades chamada <strong>ACID</strong> (<strong>A</strong>tomicidade, <strong>C</strong>onsistência, <strong>I</strong>solamento e <strong>D</strong>urabilidade). De maneira simplificada, podemos dizer que este conjunto de propriedades garantem confiabilidade as transações com uma série de restrições a fim de garantir a integridade do dado. O lado negativo em relação ao <strong>Big Data </strong>é que estas mesmas restrições tornam o RDBMS padrão menos adequado para aplicações em escala.</p>
<p align="justify">Em geral os bancos de dados <strong>NoSQL</strong> seguem o padrão <strong>BASE</strong> (<strong>B</strong>asically <strong>A</strong>vailable, <strong>S</strong>oft-state, and <strong>E</strong>ventually Consistent). Este modelo premia a disponibilidadem detrimento a consistência, com o foco em arquiteturas de dados altamente escaláveis e acessíveis, o que gera algumas discuções sobre o nível de falha ou falta de coerência aceito ao se implementar este tipo de arquitetura.</p>
<p align="justify">O grande impulso para todo o movimento NoSQL veio em 2006 com o <strong>BigTable</strong> da <strong>Google</strong> e posteriormente em 2007 com o <strong>DynamoDB</strong> da <strong>Amazon</strong> que praticamente definiram o padrão para qualquer implementação de banco de dados <strong>NoSQL</strong>.</p>
<p>&#160;</p>
<h2>O NoSQL</h2>
<p>Os bancos de dados NoSQL são subdivididos pela maneira como trabalham com o dados, sendo classificados em quatro frentes:</p>
<ol>
<ol>
<li>
<h6>Key / Value Store</h6>
</li>
<li>
<h6>Wide Columns Store</h6>
</li>
<li>
<h6>Document Store</h6>
</li>
<li>
<h6>Graph Store</h6>
</li>
</ol>
</ol>
<h6>&#160;</h6>
<h3><font style="font-weight:bold;">Key / Value Store</font></h3>
<p align="justify">Armazena os dados utilizando um par construído com base em uma chave de índice e um valor. Cada dado é armazendado em pares de chave/valor, onde os dados podem ser consultados com base na chave que é indexada.</p>
<p align="justify">Este esquema tem o desempenho de consulta mais rápido e são mais adequados para aplicações que necessitem de armazenamento de conteúdo em cache, por exemplo, um site de jogo que atualiza constantemente as 10 melhores pontuações dos jogadores.</p>
<p align="justify"><strong>Exemplos:</strong> Azure Table Storage, Dynamo DB, Redis, BerkleyDB.</p>
<p><b>Prós:</b></p>
<ul>
<ul>
<li>Modelo de dados simples </li>
<li>Altamente escalável </li>
</ul>
</ul>
<p><b>Contras:</b></p>
<ul>
<ul>
<li>Não há relacionamentos, você tem que criar suas próprias chaves estrangeiras </li>
<li>Não é adequado para modelos de dados complexos </li>
</ul>
</ul>
<p><font color="#777777"></font></p>
<h3><font style="font-weight:bold;"></font></h3>
<h3><font style="font-weight:bold;"></font></h3>
<h3><font style="font-weight:bold;">Wide Columns Store</font></h3>
<p>Tenta realizar uma abordagem híbrida misturando características de um banco de dados relacional junto ao modelo NoSQL. Suportam&#160; várias linhas e colunas, além de permitir subcolunas.</p>
<p><strong>Exemplos:</strong> Google Bigtable, Cassandra, HBase.</p>
<p><b>Prós:</b></p>
<ul>
<ul>
<li>Suporta dados semi-estruturados </li>
<li>Naturalmente indexado </li>
<li>Escalável </li>
</ul>
</ul>
<p><b>Contras:</b></p>
<ul>
<ul>
<li>Não é adequado para dados relacionais </li>
</ul>
</ul>
<p>&#160;</p>
<h3><font style="font-weight:bold;"></font></h3>
<h3><font style="font-weight:bold;">Document Store</font></h3>
<p align="justify">Podemos ver como uma extensão da simplicidade do modelo Key/Value, onde os valores são armazenados em documentos estruturados como XML ou JSON. </p>
<p align="justify">Um banco de dados de documentos é esquema livre onde você não tem que definir um esquema. Ela nos permite armazenar dados complexos em formatos de documento (JSON, XML etc.)</p>
<p align="justify">As bases de dados de documentos não suportam relações. Cada documento no armazenamento é independente e não existe integridade relacional.</p>
<p><strong>Exemplos:</strong> MongoDB, CouchDB, Lotus Notes.</p>
<p><b>Prós:</b></p>
<ul>
<ul>
<li>Modelo de dados simples e poderoso </li>
<li>Escalabilidade </li>
</ul>
</ul>
<p><b>Contras:</b></p>
<ul>
<ul>
<li>Não é adequado para dados relacionais </li>
<li>Consultas limitadas a chaves e índices </li>
<li>Map Reduce para consultas maiores </li>
</ul>
</ul>
<p><font color="#777777"></font></p>
<h3><font style="font-weight:bold;"></font></h3>
<h3><font style="font-weight:bold;"></font></h3>
<h3><font style="font-weight:bold;">Graph Store</font></h3>
<p>Com uma complexibilidade maior, esses bancos de dados guardam objetos, e não registros como os outros tipos de NoSQL. A busca desses itens é feita pela navegação desses objetos. </p>
<p><b>Prós:</b> </p>
<ul>
<ul>
<li>Extremamente poderoso </li>
<li>Dados conectados é indexados localmente </li>
<li>Pode fornecer ACID </li>
</ul>
</ul>
<p><b>Contras:</b> </p>
<ul>
<ul>
<li>Difícil dimensionar, porém pode escalar para cima </li>
</ul>
</ul>
<p>&#160;</p>
<p>&#160;</p>
<h2>Questões sobre a&#160; escalabilidade</h2>
<p align="justify">O principal problema é referente a distribuição horizontal da carga de dados. O fato é que as soluções <strong>RDBMS</strong> não podem facilmente atingir <strong>SHARDING</strong> automático de dados. Isso por que o <strong>Sharding</strong> de dados exige entidades distintas que podem ser distribuídas e processadas de forma independente.</p>
<p align="justify">Um banco de dados relacional baseado em <strong>ACID</strong> não consegue fazer isso devido sua <strong>arquitetura</strong> baseada em <strong>tabelas</strong>. </p>
<p align="justify">É neste ponto que as soluções <strong>NoSQL</strong> se diferenciam. Sua arquitetura não é baseada na distribuição lógica de uma entidade entre várias tabelas, sendo armazenda em um determinado local. Uma entidade lógica pode ser qualquer coisa a partir de um valor simples ou um objeto complexo. Não existe a imposição da integridade referencial entre as entidades lógicas, apenas a consistência dentro de uma única entidade e às vezes nem isso.</p>
<p align="justify">Este é o aspecto que permite a distribuição automática de dados através de um grande número de nós em um banco de dados além de escrevê-las intedependentemente. </p>
<p align="justify">Temos que levar em consideração que ao trabalhar com multi-database temos algumas particularidades. Imanige que você precisa relizar um <strong>Commit</strong> de duas fases.</p>
<blockquote><p align="justify">Commit em duas fases refere-se a uma transação que pode utilizar dois ou mais bancos de dados (<strong>multi-database</strong>), que podem estar localizados em servidores diferentes. Durante uma transação em bancos com essa característica garante-se que o Commit seja realizado em todos os bancos participantes ou em nenhum, ou seja, ou grava tudo ou não grava nada. </p>
<p align="justify">Por exemplo, se sua aplicação atualiza dados em 2 banco de dados e você faz um commit, o recurso de commit em duas fases previne situações como a de um dos bancos ficar indisponível e suas mudanças serem atualizadas somente em um dos bancos envolvidos.</p>
</blockquote>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/architecture.png"><img title="architecture" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="architecture" src="http://blob.vitormeriat.com.br/images/architecture.png" width="560" height="373" /></a></p>
<p align="justify">Se você for escrever <strong>20 entidades</strong> para um cluster de banco de dados com <strong>3 nós</strong>, a ideia é gravar os dados de maneira uniforme entre todos eles. O banco de dados não precisa sincronizar entre os nós para que isso aconteça, e não há a necessidade de um <strong>Commint</strong> de duas fases, com o efeito visível que um cliente pode ver as mudanças no nó 1 antes do<strong> Cliente 2</strong> gravar todas as <strong>20 entidades</strong>.</p>
<p align="justify">Uma solução <strong>RDBMS</strong> distribuída por outro lado, precisa garantir a consistência em todos os três nós. Isso significa que um cliente irá ou não ver qualquer mudança até todos os três nós tenhan confirmado todas as fases da gravação. Além disso a sincronização do <strong>RDBMS</strong> também precisa ler os dados a partir de outros nós, a fim de assegurar a integridade referencial.</p>
<p align="justify">O fato de que de uma solução <strong>NoSQL</strong> poder escalar horizontalmente também significa que pode alavancar sua natureza distribuída para alta disponibilidade. Isso é muito importante na nuvem, já que um nó pode falhar a qualquer momento.</p>
<p>&#160;</p>
<h2>Questões sobre o desempenho</h2>
<p align="justify">Utilizar um banco de dados <strong>NoSQL</strong> não significa que sua aplicação vai ter uma super melhora de desempenho! Na verdade o desempenho vai muito de se escolher a implementação correta para cada cenário, avaliando todas as nuances que envolvem o projeto.</p>
<p align="justify">Soluções de armazenamento <strong>Key / Value</strong> podem ser muito simples, e mesmo assim é possível usá-lo mal. Por ser um conceito diferente do já habitual modelo relacional e uma má concepção do modelo de dados vai matar o seu desempenho.</p>
<p align="justify">Além dos fatores óbvios de <strong>disco I/O</strong>, rede e armazenamento em cache (o que você deve, naturalmente, levar em consideração), tanto o desempenho do aplicativo quanto a escalabilidade dependem fortemente dos dados em si, mais especificamente sobre a distribuição em todo o cluster de banco de dados. Isto leva a um outro fator que influência até na adoção de um banco de dados <strong>NoSQL</strong>, a administração!</p>
<p>&#160;</p>
<h2>E o DBA?</h2>
<p align="justify">Há um outro fator que irá desempenhar um papel fundamental na escolha entre os bancos de dados <strong>NoSQL</strong> em detrimento aos mais tradicionais.&#160; As empresas hoje já possuem expertise no uso de bancos de dados <strong>RDBMS</strong>, com especialistas e <strong>DBAs</strong> já rodados. <strong>NoSQL</strong> é novo e ainda pouco compreendido. A administração é diferente. Performance tuning e análise de desempenho são bem diferentes, assim como os padrões de problemas que vemos no dia a dia. </p>
<p align="justify">O processo mais importante para o desempenho e configuração estão agora regidos pelas aplicações clientes e não mais em <strong>index tuning</strong>.</p>
<p align="justify">&#160;</p>
<p align="justify">No próximo post vou abordar especificamente sobre o <strong>Azure Table Service</strong> dentre deste contexto.</p>
<p>&#160;</p>
<h2>Até mais e bom estudo a todos!</h2>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/me-azul.png"><img title="Me Azul" style="float:left;margin:0 20px 0 0;display:inline;"   alt="Me Azul" src="http://blob.vitormeriat.com.br/images/me-azul.png?w=110&amp;h=110&amp;h=110" width="110" align="left" height="110" /></a></p>
<h3><font style="font-weight:bold;" color="#4f81bd">Twitter: </font><a href="http://twitter.com/#!/vitormeriat"><font style="font-weight:bold;" color="#9bbb59">@vitormeriat</font></a></h3>
<h3><a href="mailto:vitormeriat@gmail.com"><font style="font-weight:bold;" color="#9bbb59">vitormeriat@gmail.com</font></a></h3>
<h3><a href="mailto:vitor.pereira@studentpartners.com.br"><font style="font-weight:bold;" color="#9bbb59">vitor.pereira@studentpartner.com</font></a></h3>