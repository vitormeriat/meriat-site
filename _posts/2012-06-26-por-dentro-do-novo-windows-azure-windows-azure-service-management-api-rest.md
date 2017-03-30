---
layout: post
title: Por dentro do novo Windows Azure. Windows Azure Service Management API REST
date: 2012-06-26 
categories:
- Cloud Computing
- Microsoft Azure

---
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/windows-azure.png"><img style="background-image:none;margin:0 20px 0 0;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border-width:0;" title="Windows Azure"   alt="Windows Azure" align="left" src="http://blob.vitormeriat.com.br/images/windows-azure.png" width="320" height="183" /></a></p>
<p align="justify">Como já andei postando anteriormente, o mês de junho foi de grandes novidades para os <strong>“azureiros”</strong>. Dentre as novidades do Windows Azure SDK 1.7.0.0, algo particularmente interessante foram as relacionadas a API do <strong>Windows Azure Service Management</strong> <strong>(WASM)</strong>. Neste post irei falar sobre as novas funcionalidades e as e as alterações na <strong>API REST</strong> do serviço de administração do Windows Azure. Não estarei abordando o uso prático neste momento.</p>
<p><!--more-->
<p align="justify">Com a API do Windows Azure Service Management você pode gerenciar seus serviços de hospedagem, contas de armazenamento e muito mais. Essas são as funcionalidades que você tem ao utilizar a o portal de administração do Azure (<a href="http://manage.windowsazure.com" target="_blank">manage.windowsazure.com</a>), porém, com a liberdade de implementação e utilização conforme a sua necessidade e gosto. Como já abordei nos artigos da série <a href="http://blob.vitormeriat.com.br/images/2012/03/21/windows-azure-internals-trabalhando-com-storage-service-e-api-rest-parte-1/" target="_blank">Windows Azure Internals: Trabalhando com Storage Service e API REST</a>, todos os serviços de armazenamento são expostos através de uma <strong>API HTTP RESTful</strong>.</p>
<p>&#160;</p>
<h1><font>As novidades</font></h1>
<p align="justify">O foco das novidades do WASM visa agilizar o trabalho com funcionalidades para economizar o tempo de administração como veremos abaixo:</p>
<p align="justify">&#160;</p>
<h3 align="justify"><font>Get Package (obter pacote)</font></h3>
<p align="justify">Esta funcionalidade permite a recuperação dos arquivos do pacote (arquivos cspkg e cscfg), para serem copiados no container blob que você especificar.</p>
<table   cellspacing="0" cellpadding="2" width="568">
<tbody>
<tr>
<td valign="top" width="31">
<p align="left">POST</p>
</td>
<td valign="top" width="535">https://management.core.windows.net/subscriptions/&lt;subscription-id&gt;/compute/&lt;service-name&gt;/deployments/&lt;deployment-name&gt;?containerUri=&lt;container-uri&gt;</td>
</tr>
<tr>
<td valign="top" width="31">POST</td>
<td valign="top" width="535">https://management.core.windows.net/subscriptions/&lt;subscription-id&gt;/compute/&lt;service-name&gt;/deployments/&lt;deployment-name&gt;/&lt;deployment-slot&gt;?containerUri=&lt;container-uri&gt;</td>
</tr>
</tbody>
</table>
<p align="justify">Mais informações em na documentação de desenvolvimento <a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj154121" target="_blank">Get Package</a></p>
<p align="justify">&#160;</p>
<h3 align="justify"><font>Check Hosted Service Name Availability (Verificar a disponibilidade do nome de host)</font></h3>
<p align="justify">Verifica se o nome selecionado para host está disponível. Na versão anterior você devia tentar criar o host e esperar por um erro para só então saber se este nome estava disponível.</p>
<div align="justify">
<table   cellspacing="0" cellpadding="2" width="568">
<tbody>
<tr>
<td valign="top" width="10">GET</td>
<td valign="top" width="556">https://management.core.windows.net/&lt;subscription-id&gt;/services/hostedservices/operations/isavailable/&lt;service-name&gt;</td>
</tr>
</tbody>
</table></div>
<p align="justify">Mais informações em <a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj154116" target="_blank">Check Hosted Service Name Availability</a></p>
<p align="justify">&#160;</p>
<h3 align="justify"><font>Check Storage Account Name Availability ( Verifica a disponibilidade do nome da conta)</font></h3>
<p align="justify">Como a função acima, agora é possível verificar a disponibilidade de um nome para sua conta de armazenamento evitando o “teste” de criação.</p>
<table   cellspacing="0" cellpadding="2" width="566">
<tbody>
<tr>
<td valign="top" width="10">GET</td>
<td valign="top" width="554">https://management.core.windows.net/&lt;subscription-id&gt;/services/storageservices/operations/isavailable/ &lt;service-name&gt;</td>
</tr>
</tbody>
</table>
<p align="justify">Mai informações em <a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj154125" target="_blank">Check Storage Account Name Availability</a></p>
<p>&#160;</p>
<h1><font>As alterações</font></h1>
<p align="justify">As duas mudanças mais significativas em relação a versão passada é que agora você não pode escolher uma região qualquer dos EUA, Europa ou Ásia. Para a criação de um serviço no Windows Azure você deve especificar o local exato em que o serviço deve ser hospedado. A outra mudança é que agora você pode definir metadados personalizados para sua conta de armazenamento e serviço hospedado. Estes metadados são conhecidos como “Extended Properties” que nada mais é que uma coleção de “name / value” que pode ter no máximo 50 itens.</p>
<p align="justify">Abaixo segue a lista de referência para os serviços atualizados nesta versão:</p>
<p align="justify">&#160;</p>
<h3 align="justify"><font>Create Storage Account</font></h3>
<p align="justify">Definir propriedades estendidas e habilitar ou desabilitar a geo-replicação para as contas de armazenamento que por padrão vem habilitadas.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/hh264518" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/hh264518</a></p>
<h3 align="justify"><font>Update Storage Account</font></h3>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/hh264516" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/hh264516</a></p>
<h3 align="justify"><font>List Storage Accounts</font></h3>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460787" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460787</a></p>
<h3 align="justify"><font>Get Storage Account Properties</font></h3>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460802" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460802</a></p>
<h3 align="justify"><font>List Affinity Groups</font></h3>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460797" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460797</a></p>
<h3 align="justify"><font>Get Affinity Group Properties</font></h3>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460789">http://msdn.microsoft.com/en-us/library/windowsazure/ee460789</a></p>
<h3 align="justify"><font>List Locations</font></h3>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460797">http://msdn.microsoft.com/en-us/library/windowsazure/ee460797</a></p>
<h3 align="justify"><font>List Hosted Services</font></h3>
<p align="justify">Esta funcionalidade agora retorna os detalhes adicionais do serviço hospedado como descrição, grupo de afinidade, status, localização, data de criação, hora e data da última atualização e etc.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460781" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460781</a></p>
<h3 align="justify"><font>Create Deployment</font></h3>
<p align="justify">Nesta versão é possível criar propriedades estendidas para um deploy no momento de sua criação. </p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460813">http://msdn.microsoft.com/en-us/library/windowsazure/ee460813</a></p>
<h3 align="justify"><font>Create Hosted Service</font></h3>
<p align="justify">Agora é possível criar propriedades estendidas para o serviço de host no momento de sua criação.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/gg441304" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/gg441304</a></p>
<h3 align="justify"><font>Update Hosted Service</font></h3>
<p align="justify">Atualizar as propriedades estendidas de um serviço de host.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/gg441303" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/gg441303</a></p>
<h3 align="justify"><font>Get Hosted Service Properties</font></h3>
<p align="justify">Retorna as informações e detalhes adicionais de um determinado serviço hospedado como status, data e hora da criação e última atualização, propriedades estendidas, informações sobre o tempo de inatividade de um VM ou seu status de atualização.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460806" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460806</a></p>
<h3 align="justify"><font>Change Deployment Configuration</font></h3>
<p align="justify">Atualizar propriedades estendidas para um deploy.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460809" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460809</a></p>
<h3 align="justify"><font>Upgrade Deployment</font></h3>
<p align="justify">Atualiza as propriedades estendidas do deploy.</p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/ee460809" target="_blank">http://msdn.microsoft.com/en-us/library/windowsazure/ee460809</a></p>