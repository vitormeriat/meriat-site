---
layout: post
title: Porque SetConfigurationSettingPublisher precisa ser chamado antes de FromConfigurationSetting?
date: 2011-06-07
categories:
    - Cloud Computing
    - Microsoft Azure
    - Microsoft Azure Storage
---

No post anterior(ver <a href="http://vitormeriat.com.br/2011/05/25/cloudstorageaccount-e-o-mtodo-setconfigurationsettingpublisher/">aqui</a>) falei sobre a experiência ou aventura que é montar uma estratégia para o credenciamento da conta no Azure. Como já recebi alguns emails com perguntas e críticas, resolvi me apressar para liquidar(pelo menos em parte) com este assunto.

Quem durante seus estudos sobre Azure não se deparou com o famoso erro:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/06/011.png"><img alt="01" src="http://blob.vitormeriat.com.br/images/2011/06/011.png" /></a></p>

Quando utilizamos o método <em>FromConfigurationSetting</em>, o Azure irá procurar por um editor de configuração.

A descrição de <a href="http://msdn.microsoft.com/query/dev10.query?appId=Dev10IDEF1&amp;l=EN-US&amp;k=k(MICROSOFT.WINDOWSAZURE.CLOUDSTORAGEACCOUNT.FROMCONFIGURATIONSETTING);k(TargetFrameworkMoniker-%22.NETFRAMEWORK%2cVERSION%3dV4.0%22);k(DevLang-CSHARP)&amp;rd=true" target="_blank">CloudStorageAccount.FromConfigurationSetting</a> no próprio site da <a href="http://msdn.microsoft.com" target="_blank">MSDN</a> é a seguinte:

> Create a new instance of a CloudStorageAccount object from a specified configuration setting. This method may be called only after the SetConfigurationSettingPublisher method has been called to configure the global configuration setting publisher.

Note que na descrição do método está um aviso em alto e bom som indicando que este método só pode ser <span style="text-decoration:underline;">chamado</span> após o método SetConfigurationSettingPublisher ser <span style="text-decoration:underline;">chamado</span> para configurar o editor global de definição de configuração. (…)</p>
<p align="justify">O método FromConfigurationSetting executa o delegate com a lógica específica para obter as credenciais da conta. Este delegate por sua vez é invocado pelos método SetConfigurationSettingPublisher e este é o motivo pelo qual a mensagem de erro diz que este método <span style="text-decoration:underline;">deve ser chamado primeiro</span>. Em resumo:

* Você chama SetConfigurationSettingPublisher passando a lógica para obter os dados da conta;
* Você chama FromConfigurationSetting passando o nome da configuração que o delegate(ou outra lógica…) vai usar para selecionar o valor correto;
* FromConfigurationSetting executa o delegate e cria o ambiente que permite a criação correta da instância de CloudStorageAccount. Nosso ponto de partida para as credenciais de conta no Azure.


Até aqui é tudo muito tranquilo, o interessante aqui é que o método FromConfigurationSetting não sabe onde você armazena as informações de conexão, é com SetConfigurationSettingPublisher que conseguimos adquirir as informações da conexão, bem como sua fonte. Sendo assim podemos utilizar de outras estratégias para armazenar nossas credenciais. Mas isto fica para o próximo post!

### Um grande abraço e ótimo Estudo!
