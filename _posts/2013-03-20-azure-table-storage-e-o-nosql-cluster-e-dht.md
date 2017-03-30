---
layout: post
title: Azure Table Storage e o NoSQL - Cluster e DHT
date: 2013-03-20
categories:
- Cloud Computing
- Microsoft Azure
- Microsoft Azure Storage

---
<p align="justify">Dando prosseguimento a esta mini-série, veremos alguns conceitos sobre <strong>cluster</strong> e <strong>DHT</strong>. No primeiro momento você pode se perguntar: Sou um desenvolvedor, só quero saber como criar um CRUD no <strong>Azure</strong> então para que tudo isso? O fato é estes pontos são a base desta estrutura, que levaram a evolução inevitável de se pensar em nuvem. Na verdade são conceitos que justificam toda a computação na nuvem mais vamos focar no<strong> Azure Table Service</strong>.</p>
<p align="justify">A computação na nuvem acontece de maneira distribuída semelhante a um grid ou cluster. Também devido a esta &quot;maneira&quot; distribuída é que topamos com estruturas como a do <strong>ATS</strong>, <strong>Queues</strong> e <strong>Blobs</strong> no caso do Azure. O próprio <strong>SQL Databases</strong> (antigo <strong>SQL Azure</strong>), possui algumas diferenças em relação a sua versão <strong>on-premise</strong>. Isto ocorre devido a infra que torna possível a <strong>cloud computing</strong>. Esta infra surge em resposta a algumas necessidades que veremos nos próximos tópicos.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/10/dthcapa.png"><img title="dthCapa"   alt="dthCapa" src="http://blob.vitormeriat.com.br/images/dthcapa.png" width="560" height="226" /></a></p>
<p><!--more--><br />
<h2 align="justify">&#160;</h2>
<h2 align="justify">CLUSTER</h2>
<p align="justify">Podemos definir um cluster como um mecanismo de dois ou mais computadores ou sistemas (chamados de <strong>nodos</strong> ou <strong>nós</strong>), que trabalhando em conjunto para a execução de aplicações ou realizando tarefas diversas de tal forma que os usuários tenham a impressão de um recurso único (computador virtual),disponibilizando tudo. Estamos falando na transparência do sistema, que tem como características fundamentais a confiabilidade, distribuição de carga e performance.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/03/cluster.png"><img title="Cluster" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="Cluster" src="http://blob.vitormeriat.com.br/images/cluster.png" width="488" height="491" /></a></p>
<p align="justify">Um cluster é um tipo de sistema de processamento paralelo que consiste de uma coleção de computadores independentes interconectados através de uma rede, trabalhando cooperativamente como um único e integrado recurso computacional.&#160;&#160;&#160;&#160;&#160;&#160; </p>
<p align="justify">A unidade básica do cluster é um único computador, chamado de nó ou nodo. Podemos aumentar um cluster simplesmente adicionando outras máquinas. O cluster como um todo será mais poderoso quanto mais rápidos forem os seu computadores individualmente e quanto mais rápida for a rede de interconexão que os conecta.</p>
<p align="justify">A ideia por detrás do uso de clusters é espalhar as cargas entre todos os computadores disponíveis, usando ao máximo os recursos que estão livres nas máquinas.</p>
<p align="justify">Basicamente existem 3 tipos de clusters:</p>
<ul>
<li>
<div align="justify"><strong>Tolerância à falhas / Alta Disponibilidade (High Availability (HA) and Failover) </strong></div>
<ol>   </ol>
<ol>
<li>
<div align="justify">Estes modelos de clusters são construídos para prover uma disponibilidade de serviços e recursos de forma ininterruptas através do uso da redundância implícitas ao sistema </div>
</li>
<li>
<div align="justify">A ideia geral é que se um nó do cluster vier a falhar (failover), aplicações ou serviços possam estar disponíveis em outro nó </div>
</li>
<li>
<div align="justify">Utilizados para base de dados de missões críticas, correio, servidores de arquivos e aplicações </div>
</li>
</ol>
</li>
<li>
<div align="justify"><strong>Balanceamento de Carga (Load Balancing) </strong></div>
<ol>   </ol>
<ol>
<li>
<div align="justify">Este modelo distribui o tráfego entrante ou requisições de recursos provenientes dos nodos que executam os mesmos programas entre as máquinas que compõem o cluster </div>
</li>
<li>
<div align="justify">Todos os nodos estão responsáveis em controlar os pedidos. Se um nó falhar, as requisições são redistribuídas entre os nós disponíveis no momento. </div>
</li>
<li>
<div align="justify">Este tipo de solução é normalmente utilizado em fazendas de servidores de web (web farms) </div>
</li>
</ol>
</li>
<li>
<div align="justify"><strong>Computação de Alto Desempenho </strong></div>
</li>
</ul>
<h3>&#160;</h3>
<h3>Maiores Desafios</h3>
<ul>
<li>Escalabilidade (física e da aplicação) </li>
<li>Disponibilidade (gerenciamento de falhas) </li>
<li>Imagem Única do Sistema (parecer ao usuário único sistema em execução) </li>
<li>Comunicação Rápida (redes e protocolos de comunicação) </li>
<li>Balanceamento de Carga (CPU, Rede, Memória, Discos) </li>
<li>Segurança e Encriptação </li>
<li>Gerenciabilidade (administração e controle) </li>
<li>Programabilidade (API simples) </li>
<li>Aplicabilidade (aplicações voltadas para o cluster) </li>
</ul>
<h3>&#160;</h3>
<h3 align="justify">Por que utilizar cluster?</h3>
<ul>
<li>
<div align="justify">Quanto mais computadores na rede mais rápido fica sua estrutura (se você implementar da maneira correta ok?) </div>
</li>
<li>
<div align="justify">Maior agilidade no processamento </div>
</li>
<li>
<div align="justify">Componentes de fácil disponibilidade </div>
</li>
<li>
<div align="justify">Fácil manutenção - A manutenção geralmente fica por conta do grupo de usuários, que ganha com experiência e economia de recursos </div>
</li>
<li>
<div align="justify">Independência de fornecedores de hardware </div>
</li>
<li>
<div align="justify">Custos muito baixos </div>
</li>
<li>
<div align="justify">Se um computador do sistema parar não precisa esperar seu conserto para continuar seu trabalho </div>
</li>
<li>
<div align="justify">Disponibilidade de sistema operacional e ferramentas de apoio gratuitas </div>
</li>
<li>
<div align="justify">Uma configuração inicial pode ser facilmente atualizada, sem desperdício de investimento </div>
</li>
</ul>
<p>&#160;</p>
<h2>DTH - Distributed Hash Table</h2>
<p align="justify">As pesquisas em <strong>DHT</strong> surgiram originalmente motivadas pelos sistemas peer-to-peer. O DTH surge da uma necessidade em se obter e alocar informações de uma maneira descentralizada, escalável, balanceada e de excelente performance. Estamos falando da era que antecede a famosa explosão de dados que vivemos hoje.</p>
<p align="justify">Assim como o <strong>DNS</strong> tornou-se uma necessidade [já que em 1983 já existiam milhões de hosts na Internet], o P2P [<strong>peer-to-peer</strong>] é o resultado de uma tendência natural do desenvolvimento da engenharia de software em relação a disponibilidade de tecnologia para a criação de redes maiores. Não cabe aqui falar sobre a importância ou influência do <strong>P2P</strong> para a computação na nuvem mas sim do mecanismo que tornou isso possível: <strong>Distributed Hash Table</strong>.</p>
<p align="justify">No mundo da descentralização, DTHs tiveram um efeito revolucionário com uma arquitetura de topologia emergente, propriedade demonstrável e excelente desempenho.</p>
<p align="justify">A DTH formam infra-estruturas que provisionam um serviço de lookup semelhante a já conhecida tabela <strong>HASH</strong> ( um sistema que funciona em pares <strong>CHAVE-VALOR</strong>), que são armazenados de forma a qualquer nó participante possa recuperar de forma eficiente o valor associado a uma determinada chave. A responsabilidade de manter o mapeamento de chaves para valores é distribuída entre os nós de maneira que as mudanças causem o mínimo possível de desordem. Com isso as DTHs escalam um número extremamente grande de nós e gerenciam chegadas, saídas e falhas contínuas.</p>
<p align="justify">Observe a imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/03/dth1.png"><img title="DTH1" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="DTH1" src="http://blob.vitormeriat.com.br/images/dth1.png" width="560" height="315" /></a></p>
<p>&#160;</p>
<p align="justify">Aqui, cada posição de uma tabela hash normal é um peer e este é o responsável por ter o objeto que sofrerá ação. Na imagem acima, quando o usuário invoca uma operação sobre um objeto, a requisição chega a camada de roteamento já com o <strong>GUID</strong> do objeto. A camada de roteamento faz o search e encaminha a requisição até encontrar o nó com o objeto e realizar a operação.</p>
<p align="justify">No modelo DHT, a GUID do objeto é gerada com uma função hash, usada para determinar o posicionamento e a localização, por isso, esses sistemas que usam uma camada de roteamento são conhecidos como tabelas hash distribuídas. Com isso, há três operações básicas, <strong>put</strong> (GUID, dados) para armazenar, <strong>remove</strong> (GUID) para remover todas as referências do objeto e <strong>get</strong> (GUID) para recuperar o objeto de um dos nós que o armazena.</p>
<p align="justify">Agora, o interessante de tudo isso são as buscas. Como se busca numa DHT? É ai que a mágica toda acontece. Não vou abordar sobre isso já que estamos vendo apenas alguns conceitos para fortalecer nossa consciência de cloud computing, mas vale a pena dar uma olhada melhor em tempo oportuno.</p>
<p align="justify">DHTs são usadas para construir serviços complexos com sistemas de arquivos distribuídos, compartilhamento de arquivos peer-to-peer, <strong>web caching</strong>, multcast, mensageria dentre outros. Algum destes serviços te lembra algo em relação ao Azure? Não é simples coincidência.</p>
<p align="justify">&#160;</p>
<p align="justify">Nos próximos posts vamos continuar vendo sobre alguns dos mecanismos que tornaram a cloud computing possível e sua influência sobre o serviços de storage na nuvem.</p>

