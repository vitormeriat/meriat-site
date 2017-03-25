---
layout: post
title: CloudStorageAccount e o método SetConfiguration SettingPublisher
date: 2011-05-25
categories:
    - Cloud Computing
    - Microsoft Azure
    - Microsoft Azure Storage
---

Aqueles que estão estudando ou trabalhando como Azure certamente já tiveram de obter as credenciais da conta de armazenamento. Neste momento você recorre ao Windows Azure Platform Training Kit e os ainda poucos artigos que tratam do assunto.

Provavelmente o código que você vai encontrar será este(do próprio WAPTK):

<p><a href="http://blob.vitormeriat.com.br/images/2011/05/013.png"><img alt="01" src="http://blob.vitormeriat.com.br/images/2011/05/013.png" /></a></p>

Confesso que não sou um usuário assíduo dos delagates mas uma declaração que envolve um delegate Func(T1, T2) , dentro de outro, Action(T1,T2) para mim já é preciosismo…

A falta de objetividade e clareza na documentação do Azure (o que com certeza irá mudar) aliado a esta sintaxe nada amigável (e que fique bem claro que nem sempre soluções extremamente elegantes são as melhores) cria uma espécie de antipatia para alguns desenvolvedores.

Em resumo, você está invocando um método que espera um método que utiliza um método como um parâmetro. Sei que isto parece confuso então vamos explorar a expressão lambda para entendermos melhor qual a utilização deste método:

* O método<a href="http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.cloudstorageaccount.setconfigurationsettingpublisher.aspx" target="_blank">SetConfigurationSettingPublisher</a> espera um único parâmetro que é do tipo <a href="http://msdn.microsoft.com/en-us/library/018hxwa8.aspx" target="_blank">Action</a>: Action&lt;string,Func&lt;string,bool&gt;&gt;.
* Notem que os parâmetros que passados ​​para o nosso método, são uma string (chamada <strong>configName</strong> ) e um Func&lt;string,bool&gt; (chamado <strong>configSettingPublisher</strong>). Em outras palavras, Azure vai retornar o nome da configuração que está sendo recuperado, bem como um método que espera uma string e retorna um valor booleano. 
 

Neste caso poderíamos fazer sem a expressão Lambda e definir o método como no exemplo abaixo…

<p><a href="http://blob.vitormeriat.com.br/images/2011/05/022.png"><img alt="02" src="http://blob.vitormeriat.com.br/images/2011/05/022.png" /></a></p>

> Para os que ainda não estiverem familiarizados com as expressões Lambda, sugiro a leitura: <a href="http://vitormeriat.com.br/2011/04/20/dissecando-as-expresses-lambda/" target="_blank">Dissecando as expressões Lambda</a>

Agora no momento que uma chamada é feita para recuperar as credenciais, teremos a execução do método MeuEditorDeConfiguracao.

Quando utilizamos o método <em>CloudStorageAccount.FromConfigurationSetting</em>, o Azure procura por um editor de configuração. Devido uma chamada anterior a <em>SetConfigurationSettingPublisher, </em>ele encontra o nosso método customizado e utilizando o <em>RoleEnvironment.GetConfigurationSettingValue</em>, nosso código obtém os valores da nossa conta e invoca o método previsto com o parâmetro Func&lt;string, bool&gt;.

No próximo post vamos explorar algumas possibilidades para nossas estratégias de obtenção das credenciais da conta de armazenamento&nbsp; no Azure.

<a href="http://cid-bd055aa47a388023.office.live.com/self.aspx/.Public/CredenciaisAzure.rar" target="_blank">Código fonte do Artigo</a>
