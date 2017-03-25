---
layout: post
title: Códigos de Erro do Azure para serviços de Armazenamento.
date: 2011-03-24
categories:
    - Cloud Computing
    - Microsoft Azure
    - Microsoft Azure Storage
---

<p>Como já havia falado em um post anterior, algumas mensagens de erro do Windows Azure representam uma curva maior para a solução do problema. Como os serviços de Armazenamento fazem acesso a dados com interfaces REST(HTTP e HTTPs) por meio das emissões de pedidos de URLs HTTP, é muito comum que erros relacionados ao Windows Azure Storage retornarem código de erro HTTP.</p>
<p>Pensando nisso, resolvi reunir os códigos de erro para os serviços de armazenamento no Windows Azure, como está descrito nas tabelas abaixo:</p>
<ol>
<li><a href="#linkTable">Códigos de Erro para serviços de Table;</a></li>
<li><a href="#linkBlob">Códigos de Erro para serviços de Blob;</a></li>
<li><a href="#linkFila">Códigos de Erro para serviços deFila.</a></li>
</ol>
<div id="linkTable">
<h3>Códigos de Erro para Serviços de Table no Azure</h3>
</div>
<table style="vertical-align:middle;border-collapse:collapse;font-family:Verdana;border:1px solid #bbb;">
<tbody>
<tr>
<th> Error code</th>
<th> HTTP status code</th>
<th> User message</th>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">DuplicatePropertiesSpecified</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">A property is specified more than one time.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">EntityAlreadyExists</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The specified entity already exists.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">EntityTooLarge</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The entity is larger than the maximum size permitted.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">HostInformationNotPresent</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The required host information is not present in the request. You must send a non-empty <em>Host</em> header or include the absolute URI in the request line.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">InvalidValueType</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The value specified is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">JsonFormatNotSupported</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Unsupported Media Type (415)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">JSON format is not supported.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">MethodNotAllowed</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Method Not Allowed (405)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The requested method is not allowed on the specified resource.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">NotImplemented</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Not Implemented (501)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The requested operation is not implemented on the specified resource.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">PropertiesNeedValue</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">Values have not been specified for all properties in the entity.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">PropertyNameInvalid</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The property name is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">PropertyNameTooLong</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The property name exceeds the maximum allowed length.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">PropertyValueTooLarge</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The property value is larger than the maximum size permitted.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">TableAlreadyExists</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The table specified already exists.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">TableBeingDeleted</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The specified table is being deleted.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">TableNotFound</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Not Found (404)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The table specified does not exist.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">TooManyProperties</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The entity contains more properties than allowed.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">UpdateConditionNotSatisfied</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The update condition specified in the request was not satisfied.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">XMethodIncorrectCount</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">More than one <em>X-HTTP-Method</em> is specified.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">XMethodIncorrectValue</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The specified <em>X-HTTP-Method</em> is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="157">XMethodNotUsingPost</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="102">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="203">The request uses <em>X-HTTP-Method</em> with an HTTP verb other than POST.</td>
</tr>
</tbody>
</table>
<div id="linkBlob">
<h3>Códigos de Erro para Serviços de Blob no Azure</h3>
</div>
<table style="vertical-align:middle;border-collapse:collapse;font-family:Verdana;border:1px solid #bbb;">
<tbody>
<tr>
<th>Error code</th>
<th>HTTP status code</th>
<th>User message</th>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">InvalidBlobOrBlock</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified blob or block content is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">InvalidBlockId</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified block ID is invalid. The block ID must be Base64-encoded.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">InvalidBlockList</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified block list is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">ContainerNotFound</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Not Found (404)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified container does not exist.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">BlobNotFound</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Not Found (404)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified blob does not exist.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">ContainerAlreadyExists</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified container already exists.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">ContainerDisabled</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified container has been disabled by the administrator.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">ContainerBeingDeleted</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified container is being deleted.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">BlobAlreadyExists</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The specified blob already exists.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseNotPresentWith<br />
BlobOperation</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">There is currently no lease on the blob.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseLost</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">A lease ID was specified, but the lease for the blob has expired.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseIdMismatchWith<br />
BlobOperation</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The lease ID specified did not match the lease ID for the blob.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseIdMissing</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">There is currently a lease on the blob and no lease ID was specified in the request.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseNotPresentWith<br />
LeaseOperation</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">There is currently no lease on the blob.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseIdMismatchWith<br />
LeaseOperation</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The lease ID specified did not match the lease ID for the blob.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseAlreadyPresent</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">There is already a lease present.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseAlreadyBroken</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The lease has already been broken and cannot be broken again.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">LeaseIsBrokenAnd<br />
Cannot<br />
BeRenewed</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The lease ID matched, but the lease has been broken explicitly and cannot be renewed.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">SnapshotsPresent</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">This operation is not permitted because the blob has snapshots.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">InvalidBlobType</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The blob type is invalid for this operation.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">InvalidVersionForPage<br />
BlobOperation</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">All operations on page blobs require at least version 2009-09-19.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">InvalidPageRange</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Requested Range Not Satisfiable (416)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The page range specified is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">SequenceNumber<br />
ConditionNotMet</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The sequence number condition specified was not met.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">SequenceNumber<br />
IncrementTooLarge</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The sequence number increment cannot be performed because it would result in overflow of the sequence number.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">SourceConditionNotMet</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The source condition specified using HTTP conditional header(s) is not met.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">TargetConditionNotMet</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Precondition Failed (412)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The target condition specified using HTTP conditional header(s) is not met.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;">CopyAcrossAccounts<br />
NotSupported</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="100">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="232">The copy source account and destination account must be the same.</td>
</tr>
</tbody>
</table>
<div id="linkFila">
<h3>Códigos de Erro para Serviços de Fila (Queue) no Azure</h3>
</div>
<table style="vertical-align:middle;border-collapse:collapse;font-family:Verdana;border:1px solid #bbb;">
<tbody>
<tr>
<th> Error code</th>
<th>HTTP status code</th>
<th> User message</th>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">MessageTooLarge</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The message exceeds the maximum allowed size.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">InvalidMarker</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified marker is invalid.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">PopReceiptMismatch</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Bad Request (400)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified pop receipt did not match the pop receipt for a dequeued message.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">QueueNotFound</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Not Found (404)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified queue does not exist.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">MessageNotFound</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Not Found (404)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified message does not exist.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">QueueDisabled</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified queue has been disabled by the administrator.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">QueueAlreadyExists</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified queue already exists.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">QueueBeingDeleted</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified queue is being deleted.</td>
</tr>
<tr>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="120">QueueNotEmpty</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="110">Conflict (409)</td>
<td style="vertical-align:middle;text-align:left;border:1px solid #bbb;" width="239">The specified queue is not empty.</td>
</tr>
</tbody>
</table>