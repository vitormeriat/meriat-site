---
layout: post
title: Windows Azure Availability Set e a Vulnerabilidade a Falhas
date: 2014-03-09 05:57:14.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure

---
<p><a href="http://blob.vitormeriat.com.br/images/2014/03/as01.png"><img title="as01" alt="as01" src="http://blob.vitormeriat.com.br/images/2014/03/as01.png" width="400" align="left" height="232" /></a></p>
<p align="justify">A primeira informação aqui é lembrar que a infra-estrutura do <strong>Windows Azure</strong> está disposta entre seus diversos <strong>Datacenters</strong> em máquinas físicas em racks de servidores. Embora a base da <strong>Cloud Computing</strong> seja a virtualização, esta infra física necessária para proporcionar os serviços é como qualquer outra e está <strong>vulnerável a falhas</strong> e problemas da mesma maneira que as demais, não é possível descartar falhas locais de rede, falhas de hardware, discos e afins. É lógico que a Microsoft toma todas as precauções necessárias e podemos contar com a <strong>SLA</strong> para os seus serviços mas em casos extremos de falha em um lote de rack isso acarretaria na breve interrupção de todos os serviços (e VMs) rodando neste rack.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/03/updatedomains.png"><img title="updatedomains" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="updatedomains" src="http://blob.vitormeriat.com.br/images/2014/03/updatedomains.png" width="554" height="339" /></a></p>
<p><!--more-->
<p align="justify">Para evitar um ponto único de falha, você pode implantar duas instâncias de um serviço, por exemplo a implantação de dois <strong>Domain Controllers (DCs)</strong> no Windows Azure. No entanto, você não tem nenhuma garantia dessas duas instâncias vão estar rodnado racks distintos, e, portanto, uma falha no rack afetaria ambos os serviços!</p>
<blockquote><p align="justify">Você sempre deve especificar um conjunto disponibilidade ao criar mais de uma máquina virtual para a mesma finalidade.</p>
</blockquote>
<p align="justify">Agora vamos implementar duas VMs usando o <strong>Availability Set</strong>. Usando este conceito, estamos dizendo de maneira explícita que queremos nossas máquinas em domínios de falha diferentes, ou seja, em racks diferentes. A ideia é evitar um único ponto de falha que possa afetar todas as instâncias de um serviço.</p>
<p align="justify">Você pode criar um Availability Set no momento da criação de uma VM ou adicionar uma VM a um Availability Set já existente.</p>
<p>&#160;</p>
<h3>Criando um Availability Set</h3>
<p><a href="http://blob.vitormeriat.com.br/images/2014/03/as03.png"><img title="as03" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="as03" src="http://blob.vitormeriat.com.br/images/2014/03/as03.png" width="560" height="365" /></a></p>
<h3>&#160;</h3>
<h3>Adicionando uma VM a um Availability Set já existente</h3>
<p><a href="http://blob.vitormeriat.com.br/images/2014/03/av02-copy.png"><img title="av02 copy" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="av02 copy" src="http://blob.vitormeriat.com.br/images/2014/03/av02-copy.png" width="560" height="362" /></a></p>
<p align="justify">O Availability Set surge no cenário para garantir que nem todas as&#160; VMs do conjunto criado possam sofrer falhas ao mesmo tempo. Isto significa que em um Availability Set é possível ter duas VMs no mesmo domínio de falha. O domínio de falha pode ser visto acessando a sessão Cloud Services e selecionando um item específico e visualizando a guia INSTANCES.</p>
<p align="justify">&#160;</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/03/as05.png"><img title="as05" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="as05" src="http://blob.vitormeriat.com.br/images/2014/03/as05.png" width="560" height="209" /></a></p>
<p align="justify">Perceba que temos valores diferentes para os domínios de falhas – neste caso temos duas VMs no Conjunto de Disponibilidade, onde uma VM terá um domínio de falhas de número 0 e o outro um domínio de uma falha de número 1.</p>
<p align="justify">Repare no exemplo abaixo eu tenho três VMs no Conjunto de Disponibilidade sendo que dois deles estão no mesmo domínio de falha. É, portanto, muito importante para garantir que os conjuntos de disponibilidade só contêm VMs executando exatamente a mesma função. Isso porque, se você misturar as funções em um único conjunto de disponibilidade, é possível que estas VMs acabem no mesmo domínio de falha, o que é exatamente o contrário desta estratégia.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/03/azureiaasavailset2.jpg"><img title="AzureIaaSAvailSet2" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="AzureIaaSAvailSet2" src="http://blob.vitormeriat.com.br/images/2014/03/azureiaasavailset2.jpg" width="560" height="184" /></a></p>
<p>&#160;</p>
<p>Para mais informações indico o seguinte artigo: <a href="http://www.windowsazure.com/en-us/documentation/articles/manage-availability-virtual-machines/" target="_blank">Manage the Availability of Virtual Machines</a></p>
<p>&#160;</p>
<h2><font color="#9bbb59">Até mais e bom estudo a todos!</font></h2>