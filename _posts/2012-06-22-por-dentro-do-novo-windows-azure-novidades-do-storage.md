---
layout: post
title: Por dentro do novo Windows Azure. Novidades do Storage
date: 2012-06-22
categories:
- Cloud Computing
- Microsoft Azure
- Microsoft Azure Storage

---
<p align="justify">Ao longo da minha parca experiência com o <strong>Windows Azure</strong> pude ver em diversos momentos algumas solicitações e anseios da comunidade por mudanças em alguns recursos do serviço de storage do Azure. Parece que o time de Azure estava bem atento e trouxe novidades significativas nesta release, tornando o <strong>Windows Azure Storage</strong> mais “atraente”.</p>
<p>As novidades para o serviço de armazenamento do Windows Azure não foram tantas, porém foram essenciais. Neste post vou relatar de forma resumida estas alterações.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/big-data-on-windows-azure.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Big Data on Windows Azure"   alt="Big Data on Windows Azure" src="http://blob.vitormeriat.com.br/images/big-data-on-windows-azure.png" width="560" height="146" /></a></p>
<p><!--more-->
<p>&#160;</p>
<h2><font>Recursos de Lease para Blobs aprimorados</font></h2>
<p align="justify">Trabalhar com concorrência no mundo dos sistemas distribuídos como o Azure pode muitas vezes se tornar uma dor de cabeça. Este é um recurso de locação do blob que permite criar um bloqueio exclusivo em determinado blob para impedir que ele seja modificado ou excluído. Mas como citado no início do parágrafo, outro uso para esta funcionalidade é gerenciar a concorrência em um ambiente <strong>multi-threaded</strong>. Para saber mais detalhes indico o ótimo post <a href="http://blog.smarx.com/posts/managing-concurrency-in-windows-azure-with-leases" target="_blank">Managing Concurrency in Windows Azure with Leases</a> do Steve Marx. </p>
<p align="justify">Segue a lista com as melhorias da funcionalidade de lease:</p>
<ul>
<li>
<div align="justify">Agora operações de locação podem ser realizadas em um contêiner blob. Nas versões anteriores isso só podia ser feito diretamente em blobs; </div>
</li>
<li>
<div align="justify">Agora você pode adquirir um contrato de locação que nunca termina. Anteriormente você só podia adquirir locação de um blob em um período válido por apenas 1 minuto; </div>
</li>
<li>
<div align="justify">Além de adquirir um contrato de locação sem fim, você também pode adquirir locação de curta duração sendo válido a partir de 15 até 60 segundos; </div>
</li>
</ul>
<p align="justify"><font color="#777777">Mais detalhes indico a leitura do artigo <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/new-blob-lease-features-infinite-leases-smaller-lease-times-and-more.aspx" target="_blank">New Blob Lease Features: Infinite Leases, Smaller Lease Times, and More.</a></font></p>
<h2>&#160;</h2>
<h2><font>Copiando Blobs para diferentes contas de armazenamento</font></h2>
<p align="justify">Ai está uma baita novidade. Nas versões anteriores não era possível copiar um Blob para outra conta de armazenamento. Considere o seguinte cenário: Você precisa fazer o “backup” de seus dados de uma conta de origem para uma conta de destino. Antes seria necessário buscar todo o conteúdo da conta origem para depois fazer o upload para a conta destino. Agora podemos resolver isso facilmente.</p>
<p align="justify">Claro que como nem tudo são flores é necessário ter alguns cuidados:</p>
<ul>
<li>
<div align="justify">Este recurso só é valido para contas de armazenamento criadas após 07/06/2012; </div>
</li>
<li>
<div align="justify">Para se copiar dados de uma conta origem, a mesma deve ter acesso público. Caso contrário a URL gerada deve ser assinada usando uma assinatura de acesso compartilhado que tenha acesso de “leitura” ao blob origem; </div>
</li>
<li>
<div align="justify">Nas versões anteriores copiar um blob era uma operação síncrona, agora a cópia de blobs é trabalhada de forma assíncrona; </div>
</li>
<li>
<div align="justify"><font color="#ff0000"><strong>[Essa merece destaque]</strong></font> Agora para copiar um blob não precisamos mais que ele esteja no Windows Azure Sotorage podendo ser por exemplo um objeto da <strong>Amzaon S3</strong>. A exigência fica por conta do acesso que deve ser público ou ter a URL assinada como citado anteriormente. Isto é realmente útil no sentido da integração e evita a necessidade de salvar certos conteúdos como blobs no Azure para sincronizar em uma base destino. Agora fica fácil utilizar o Windows Azure Storage como backup de seus dados de blobs armazenados em outro provedor de armazenamento na nuvem. </div>
</li>
<li>
<div align="justify"><font color="#555555">Caso sua conta de destino em um centro de dados diferente da conta de origem será cobrado a saída de dados… lógico, nem tudo são flores… kkk</font> </div>
</li>
</ul>
<p>&#160;</p>
<h2><font>Assinatura de acesso compartilhado para Tables</font></h2>
<p align="justify">Nas versões anteriores somente sendo proprietário de uma conta de armazenamento do Windows Azure era possível executar operações CRUD. Agora o <strong>WAS</strong>(Windows Azure Storage), ampliou a funcionalidade de Shared Access Signature.</p>
<p align="justify">Na prática o SAS (<strong>Shared Access Signature</strong>), fornece acesso granular aos recursos de armazenamento. Você precisa fornecer um token SAS com permissão predefinido (leitura, escrita, lista, exclusão, etc), que aparece na URL assinada. Logo um usuário em posse desta URL assinada tem permissão para executar operações permitidas pelo token SAS usando API REST sem realmente ter acesso as credenciais da conta de armazenamento. <img style="border-style:none;" class="wlEmoticon wlEmoticon-smile" alt="Sorriso" src="http://blob.vitormeriat.com.br/images/wlemoticon-smile.png" /></p>
<p align="justify">Alguns comentários sobre o SAS para os recursos da tabela:</p>
<ul>
<li>
<div align="justify">Você pode conceder acesso a uma tabela como um todo <strong>(ou seja, todos os dados na tabela)</strong> ou a um intervalo da tabela <strong>(ou seja, dados selecionados da uma tabela)</strong>. Vamos dizer que você está construindo uma aplicação multi-tenant e você está armazenando os dados de cada inquilino em uma tabela separada, agora você pode usar esta funcionalidade de SAS para criar tokens para tabelas separadas e dar uma URL assinada para cada inquilino;</div>
</li>
<li>
<div align="justify">Você pode conceder direitos de acesso a uma tabela específica ou intervalo da tabela, <strong>tais como Pesquisar, Adicionar, Alterar, Excluir ou uma combinação deles</strong> . O que isto significa é que você pode ter o controle realmente refinado sobre o que um usuário tem acesso de fazer por meio da URL assinada;</div>
</li>
<li>
<div align="justify">Você pode <strong>definir um horário de início e fim para fornecer acesso em tempo limitado ou fornecer acesso a grandes períodos de tempo.</strong></div>
</li>
</ul>
<p><strong><font color="#777777"></font></strong></p>
<h2><strong><font color="#777777"></font></strong></h2>
<h2><strong><font color="#777777">Assinatura de acesso compartilhado para Queues</font></strong></h2>
<p align="justify"><font color="#777777">Assim como foi supracitado, você tem os mesmos benefícios de Shared Access Signature para o serviço de Filas do Windows Azure. Vamos as observações:</font></p>
<ul>
<li>
<div align="justify">Você pode conceder direitos de acesso a uma fila específica, como Read ou Peek das mensagens o que isto significa é que você pode ter o controle realmente refinado sobre o que um usuário tem acesso de fazer por meio da URL assinada;</div>
</li>
<li>
<div align="justify">Você pode <strong>definir um horário de início e fim para fornecer acesso em tempo limitado ou fornecer acesso a grandes períodos de tempo;</strong></div>
</li>
<li>
<div align="justify">Como o SAS para blobs, é possível gerar tokens SAS com ou sem política de acesso, sendo recomendável a utilização de políticas de acesso para uma melhor admininstração.</div>
</li>
</ul>
<p align="justify"><font color="#777777"></font></p>
<h2 align="justify"><font color="#777777"><font></font></font></h2>
<h2 align="justify"><font color="#777777"><font>A nova API</font></font></h2>
<p align="justify"><font color="#777777">Com estas alterações vieram as novidades na API REST. Abaixo segue uma pequena lista com os novos recurso bem como as atualizações:</font></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/dd894037" target="_blank">Copy Blob (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee691972" target="_blank">Lease Blob (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj159098" target="_blank">Abort Copy Blob (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj159103" target="_blank">Lease Container (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj159100" target="_blank">Get Table ACL (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj159102" target="_blank">Set Table ACL (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj159101" target="_blank">Get Queue ACL (REST API)</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj159099" target="_blank">Set Queue ACL (REST API)</a></p>
