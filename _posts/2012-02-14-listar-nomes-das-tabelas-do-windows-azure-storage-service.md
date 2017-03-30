---
layout: post
title: Listar nomes das tabelas do Windows Azure Storage Service
date: 2012-02-14
categories:
  - Cloud Computing
  - Microsoft Azure
  - Microsoft Azure Storage
---
<p align="justify">Ai vai uma dica rápida para quem está trabalhando com <strong>Azure</strong>.</p>
<p align="justify">Hoje tive a necessidade de listar todas as minhas tabelas do serviço de armazenamento do Windows Azure. Eu tinha que listar os nomes de todas as tabelas do desenvolvimento local e das minhas contas de acesso na nuvem.&#160; Com isso era preciso acessar e ler todas as tabelas modificando apenas meu <strong>Subscription ID</strong>. Considere esta necessidade quando você tem 100 ou mais tabelas penduradas no <strong>ATS</strong> (Azure Table Service) e ou várias contas no Azure</p>

<p align="justify">O código completo segue na imagem abaixo:</p>
<<<<<<< HEAD
<p><a href="http://blob.vitormeriat.com.br/images/2012/02/02.png"><img alt="02" src="http://blob.vitormeriat.com.br/images/2012/02/02.png" /></a></p>
=======
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2012/02/02.png"><img alt="02" src="http://blob.vitormeriat.com.br/images/2012/02/02.png"/></a></p>
>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<p align="justify">Tudo é muito simples: Nas linhas 6 e 7 fazemos referência aos <strong>namespaces</strong> necessários para a utilização da <strong>API</strong> do Azure.</p>
<p align="justify">Na linha 18 informo a string de conexão ao serviço de armazenamento de tabelas do Azure. Neste caso estou utilizando uma string que aponta para o desenvolvimento local por meio do <strong>Storage Emulator</strong>. Para listar as tabelas de uma conta na nuvem, basta apenas informar a string conforme o modelo da linha 17 alterando os campos “<strong>MinhaConta</strong>” e “<strong>MinhaSenha</strong>” para os respectivos valores de sua Subscription.</p>
<p align="justify">O método ListaNomesTabelas (linha 30) retorna uma lista de strings e recebe como parâmetro a string de conexão. Na linha 32 criamos a conta de acesso ao <strong>CloudStorage</strong> e na linha 34 criamos o <strong>CloudTableClient</strong> que fornece o cliente para acesso ao serviço de tabelas.</p>
<p align="justify">Agora ficou fácil, depois que criamos o TableClient basta apenas chamar o método <strong>ListTables() </strong>(linha 37)<strong> </strong>que teremos a lista com os nomes das tabelas pesquisadas. Ai é só escrever as informações na tela.</p>
<<<<<<< HEAD
<p><a href="http://blob.vitormeriat.com.br/images/2012/02/03.png"><img alt="03" src="http://blob.vitormeriat.com.br/images/2012/02/03.png" /></a></p>
<p>O código deste exemplo pode ser baixado <a href="https://skydrive.live.com/?cid=BD055AA47A388023&amp;id=BD055AA47A388023%21125&amp;sc=documents#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21224&amp;sc=documents" target="_blank">aqui!</a></p>
<p>&#160;</p>
=======
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2012/02/03.png"><img alt="03" src="http://blob.vitormeriat.com.br/images/2012/02/03.png"/></a></p>
<p>O código deste exemplo pode ser baixado <a href="https://skydrive.live.com/?cid=BD055AA47A388023&amp;id=BD055AA47A388023%21125&amp;sc=documents#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21224&amp;sc=documents" target="_blank">aqui!</a></p>
>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<h4><strong>Um ótimo estudo a todos.</strong></h4>