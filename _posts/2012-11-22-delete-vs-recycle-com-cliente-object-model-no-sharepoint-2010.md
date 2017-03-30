---
layout: post
title: Delete vs. Recycle com Cliente Object Model no Sharepoint 2010
date: 2012-11-22
categories:
- Sharepoint

---
<p align="justify">Bem, se você como eu está iniciando no mundo do (ou que é o) Sharepoint 2010, ai segue uma dica sobre o uso do <strong>Client Object Model</strong> introduzido no Sharepoint 2010.</p>
<p align="justify">Em geral, na mecânica do Sharepoint quando <strong>“deletamos”</strong> um item ele é movido para a lixeira ao invés de ser <u>excluído permanentemente</u>. Com isso os usuários mais rodados de sharepoint vão esperar que suas aplicações sigam o mesmo comportamento. Contudo o que vemos com muita facilidade até mesmo na documentação oficial são exemplos usando o método <strong>SPListItem.Delete()</strong>.</p>
<p><!--more-->
<p align="justify">Como meu foco não é abordar os conceitos de Cliente Object Model, então vamos observar o trecho de código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/11/01.png"><img title="01" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="01" src="http://blob.vitormeriat.com.br/images/01.png" width="560" height="280" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Se utilizarmos este trecho de código o item deletado será excluído total e permanentemente. Mesmo que a lista esteja configurada para reciclar ou mandar os itens para a lixeira, isto não ocorrerá se usarmos o método <strong>SPListItem.Delete()</strong>. Essa confusão pode ocorrer (como já citado acima) devido a mecânica de deleção do <strong>Sharepoint</strong>. Pode ser que a semelhança dos nomes te leve a pensar que o comportamento deste método será igual ao comportamento utilizando a interface do usuário. Para este fim devemos utilizar o seguinte trecho de código ilustrado abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/11/02.png"><img title="02" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="02" src="http://blob.vitormeriat.com.br/images/02.png" width="560" height="280" /></a></p>
<p>&#160;</p>
<p>A descrição do método <strong>SPListItem.Recycle()</strong> diz: <u>“Recicla o item e retorna seu GUID”</u>. Não é muito divulgado nem comum nos exemplos mas é este o método que vai realizar o comportamento mais comum das aplicações em <strong>Sharepoint</strong>.</p>
<p>&#160;</p>
<h3><font style="font-weight:bold;">Referências:</font></h3>
<p><a href="http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.splistitem.recycle.aspx">SPListItem.Recycle method</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.splistitem.delete.aspx" target="_blank">SPListItem.Delete method</a></p>