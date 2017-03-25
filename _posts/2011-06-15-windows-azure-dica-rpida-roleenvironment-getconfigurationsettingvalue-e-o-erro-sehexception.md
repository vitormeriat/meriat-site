---
layout: post
title: 'Windows Azure dica rápida: RoleEnvironment.GetConfigurationSettingValue e o erro SEHException'
date: 2011-06-15
categories:
  - Cloud Computing
  - Microsoft Azure
  - Microsoft Azure Storage
---

Hoje recebi um email com uma pegunta interessante de um desenvolvedor que utilizava o exemplo do post <a href="http://vitormeriat.wordpress.com/2011/05/25/cloudstorageaccount-e-o-mtodo-setconfigurationsettingpublisher/" target="_blank">CloudStorageAccount e o método SetConfigurationSettingPublisher</a>e obteve um **SEHException** durante sua execução. Como este é um erro comum, resolvi fazer um post para esta resposta.

O <a href="http://www.microsoft.com/windowsazure/sdk/" target="_blank">Windows Azure SDK</a> atualmente na versão 1.4 disponibiliza um ambiente para o desenvolvimento de aplicações na plataforma Azure. Este ambiente foi disponibilizado para que possamos localmente **“emular”** os recursos oferecidos na nuvem.

<p>Dito isso é provável que antes de executar uma aplicação para o Azure, você decida iniciar o ambiente para emular nossa “nuvem local”. Provavelmente o resultado será este:</p>

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/06/aa.png"><img alt="aa" src="http://blob.vitormeriat.com.br/images/2011/06/aa.png"/></a></p>

Com nosso ambiente em pleno funcionamento, você decide iniciar sua aplicação e se depara com um **SEHException** em sua tela como na imagem abaixo:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/06/bb.png"><img alt="bb" src="http://blob.vitormeriat.com.br/images/2011/06/bb.png"/></a></p>

Este erro ocorre na chamada **RoleEnvironment.GetConfigurationSettingValue** dentro do arquivo Global.asax.cs, e se deve a um fato interessante:

> Sua aplicação não está executando dentro do ambiente do Windows Azure Emulator…

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/06/cc.png"><img alt="cc" src="http://blob.vitormeriat.com.br/images/2011/06/cc.png"/></a></p>

Mesmo tendo iniciado os serviços para emular o ambiente azure, o projeto que estava como <em>Set as StartUp Project</em> era o WebRole. A solução para este problema é muito simples:

* Definir o projeto <em>Windows Azure</em> como inicial utilizando o <em>Set as StartUp Project.

É claro que podemos(e devemos) utilizar estratégias para evitar este tipo de erro, mas vou abordar isto no próximo post.

Como já está no título este é apenas uma dica rápida!

<h4>Um grande abraço, ótimo estudo e até a próxima!</h4>