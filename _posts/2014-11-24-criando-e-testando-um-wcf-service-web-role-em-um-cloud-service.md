---
layout: post
title: Services now–Criando e testando um WCF Service Web Role em um Cloud Service
date: 2014-11-24
categories:
  - Microsoft Azure
  - Services
  - WCF
image: "http://blob.vitormeriat.com.br/images/2014/11/capawcf1.png"
---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/capawcf1.png"><img title="capaWCF1" alt="capaWCF1" src="http://blob.vitormeriat.com.br/images/2014/11/capawcf1.png" /></a></p>
<p align="justify">Esta é a continuação do post anterior: <a href="http://vitormeriat.com.br/2014/11/23/criando-e-testando-um-wcf-service-web-role-on-premise/" target="_blank">Criando e testando um WCF Service Web Role On-Premise</a>. Neste post vamos utilizar o serviço WCF criado anteriormente, para realizar a publicação do mesmo na nuvem, hospedado e um <strong>Cloud Service </strong>no <strong>Microsoft Azure</strong>.</p>
<p><!--more-->
<p align="justify">Estou levando em conta que você já executou os passos do post anterior ou que já tem um serviço WFC já criado. </p>
<p align="justify">Sendo assim vamos ao <strong>deploy da aplicação</strong>. Clique com o botão direito sobre o projeto do <strong>Coud Service </strong>(no caso do exemplo o projeto WindowsAzureWCF), e selecione a opção <strong>Publish…</strong></p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo1.png"><img title="artgo1" alt="artgo1" src="http://blob.vitormeriat.com.br/images/2014/11/artgo1.png" /></a></p>
<p align="justify">Agora estou levando em conta que você já tem uma subscription ativa do Microsoft Azure. Caso contrário<strong> </strong><a href="http://azure.microsoft.com/pt-br/"><strong>acesse esse link</strong></a>. Na tela que segue, logo após selecionar a subscription correta, teremos a exibição da tela para a criação do Cloud Service onde o serviço será hospedado. Informe o nome do serviço e a Região (Datacenter) onde o mesmo será hospedado.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo2.png"><img title="artgo2" alt="artgo2" src="http://blob.vitormeriat.com.br/images/2014/11/artgo2.png" /></a></p>
<p align="justify">Após prover estas informações é só esperar a criação do Cloud Service. Quando criado teremos a tela abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo3.png"><img title="artgo3" alt="artgo3" src="http://blob.vitormeriat.com.br/images/2014/11/artgo3.png" /></a></p>
<p align="justify">Agora clique em Publish e aguarde o final do processo. Você pode acompanhar o status do deploy no próprio Visual Studio:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo4.png"><img title="artgo4" alt="artgo4" src="http://blob.vitormeriat.com.br/images/2014/11/artgo4.png" /></a></p>
<p align="justify">Ao final teremos o status de <strong>Completed</strong> e a <strong>URL </strong>onde o serviço está exposto.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo5.png"><img title="artgo5" alt="artgo5" src="http://blob.vitormeriat.com.br/images/2014/11/artgo5.png" /></a></p>
<p align="justify">Simples não é? Agora só falta testar o nosso serviço. Notem que conseguimos acessar a URL exatamente como fizemos on-premisse, porém utilizando endereço do Cloud Service.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo6.png"><img title="artgo6" alt="artgo6" src="http://blob.vitormeriat.com.br/images/2014/11/artgo6.png" /></a></p>
<p align="justify">Agora nosso serviço já está hospedado na nuvem. Vamos para o console de teste que criamos no post anterior. A única coisa que&nbsp; precisamos alterar é o <strong>endpoint</strong> de acesso ao serviço. Como no post anterior o teste foi local, ainda estamos apontando para um <strong>address</strong> <a title="http://127.0.0.1:4318/Service1.svc" href="http://127.0.0.1:4318/Service1.svc">http://127.0.0.1:4318/Service1.svc</a>. Agora só precisamos alterar este valor em nosso App.config incluindo a URL recém criada, como no exemplo abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo7.png"><img title="artgo7" alt="artgo7" src="http://blob.vitormeriat.com.br/images/2014/11/artgo7.png" /></a></p>
<p>Agora execute a aplicação… o resultado vai ser o mesmo!</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/artgo8.png"><img title="artgo8" alt="artgo8" src="http://blob.vitormeriat.com.br/images/2014/11/artgo8.png" /></a></p>
<p align="justify">&nbsp;</p>
<p align="justify">Pronto, já criamos nosso<strong> WCF Service Web Role</strong>, testamos o serviço localmente rodando tudo on-premisse utilizando a estrutura do <strong>Computer Emulator</strong>, publicamos no <strong>Microsoft Azure</strong> e consumimos o serviço rodando na nuvem. Esta é apenas uma dica, nos próximos posts vou abordar este assunto com mais propriedade.</p>
<p align="justify">&nbsp;</p>
<p>O código fonte deste exemplo pode ser baixado <a href="http://1drv.ms/1xp8dLF" target="_blank">CLICANDO AQUI...</a></p>
<p>&nbsp;</p>
<h4><font color="#000000">Bons estudos e até a próxima pessoal&nbsp; ;)</font></h4>