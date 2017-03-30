---
layout: post
title: Trabalhando com o GitHub em 7 passos
date: 2013-05-31
categories:
- Agile
- ALM

---
<p>Neste post vou apresentar como em 7 passos é possível instalar e utilizar o GitHub, uma ferramenta de <strong> Controle de Versão </strong>cada vez mais popular e que recentemente foi integrada ao <strong>Visual Stuio 2012</strong> e ao próprio <strong>Team Foundation Server</strong> sendo uma das novidades mais comentadas dentro da plataforma de&#160; <strong>Application Lifecycle Management da Microsoft</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/collabocats.jpg"><img title="collabocats"   alt="collabocats" src="http://blob.vitormeriat.com.br/images/2013/05/collabocats.jpg" width="560" height="283" /></a></p>
<p align="justify">A plataforma <strong>TFS (Team Foundation Server)</strong> tem um controle de versão chamado internamente de Team Foundation Server Version Control<strong> (TFSVC)</strong>. O que muda agora é que você terá toda a experiência do <strong>Visual Studio / Team Explorer / Work Itens / Scrum</strong> e poderá escolher qual o seu controle de versão <strong>(GIT / TFSVC)</strong>.</p>
<p align="justify">Sendo assim vamos partir para a prática…</p>
<p><!--more-->
<p align="justify">Antes de prosseguirmos segue uma dica: Descobri que comumente um repositório é apelidado de Repo na documentação do GitHub.</p>
<p align="justify">&#160;</p>
<h2>Passo 1. Download e instalação GitHub</h2>
<p align="justify">Acesse a página do GitHub na seguinte URL: <a href="http://windows.github.com/">http://windows.github.com/</a> </p>
<p align="justify">Logo após faça o download do arquivo de instalação, clique em <strong>Executar</strong>, e em seguida, Instalar. O processo de instalação pode demorar alguns minutos enquanto baixa os arquivos para instalação. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/1-0.png"><img title="1.0"   alt="1.0" src="http://blob.vitormeriat.com.br/images/2013/05/1-0.png" width="560" height="326" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/1-1.png"><img title="1.1"   alt="1.1" src="http://blob.vitormeriat.com.br/images/2013/05/1-1.png" width="545" height="320" /></a></p>
<p>&#160;</p>
<h2>Passo 2. Conectando-se ao GitHub</h2>
<p align="justify">Uma vez instalado, o aplicativo do <strong>GitHub</strong> irá iniciar solicitando o nome de usuário e senha para a conexão ao servidor. Caso você não tenha uma conta no GitHub é só clicar no link na parte inferior da tela e criar sua conta de forma gratuita. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/2.png"><img title="2"   alt="2" src="http://blob.vitormeriat.com.br/images/2.png" width="560" height="373" /></a></p>
<p>&#160;</p>
<h2>Passo 3. Adicionando um Repositório</h2>
<p align="justify">Depois de logar, o GitHub vai te perguntar se você deseja adicionar um <strong>repositório</strong>. Caso você já tenha repositórios criados através do site ou por linha de comando, você pode pular esta etapa e simplesmente baixar cópias locais (<strong>clones</strong>). Se esta é a primeira vez usando o GitHub, nomeie sua <strong>repo</strong> e clique em <strong>CREATE</strong>. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/3.png"><img title="3"   alt="3" src="http://blob.vitormeriat.com.br/images/2013/05/3.png" width="560" height="344" /></a></p>
<p>&#160;</p>
<h2>Passo 4. Repositório, localização e adição de arquivos</h2>
<p align="justify">GitHub para Windows irá criar uma pasta para o seu repositório. Por default ele aponta para <strong>C:Users&lt;YourUserName&gt;GitHub&lt;RepoName&gt;</strong>. Sinta-se a vontade para trocar este caminho para um de sua escolha. Note que estou apontado meu repositório para um caminho no disco <strong>D:</strong>. Agora escreva em <strong>NAME</strong> o nome do repositório. Note que ele é automaticamente incluído no caminho apontado logo abaixo da descrição. </p>
<p align="justify">Você deve colocar o código dentro dessa pasta. Uma boa prática para criar um arquivo <strong>README</strong> contendo todas as instruções relevantes sobre o código a ser versionado. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/4.png"><img title="4"   alt="4" src="http://blob.vitormeriat.com.br/images/2013/05/4.png" width="560" height="261" /></a></p>
<p>&#160;</p>
<h2>Passo 5. Abrindo seu Repositório</h2>
<p align="justify">Assim que você terminar de adicionar os arquivos na pasta do repositório, volte ao aplicativo do GitHub e clique no nome do repositório. Você verá dois ícones : O primeiro é um <strong>PC</strong> e te mostra que você tem uma cópia local do repositório em sua máquina, o segundo é uma <strong>SETA</strong> e indica que você terá que clicar no link para abrir o repositório. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/41.png"><img title="4"   alt="4" src="http://blob.vitormeriat.com.br/images/2013/05/4.png" width="560" height="346" /></a></p>
<p>&#160;</p>
<h2>Passo 6. Submeter suas alterações </h2>
<p align="justify">Depois de abrir o repositório, você verá uma lista de arquivos a serem &quot;<strong>commitados</strong>&quot;. Você deve escrever um título para o <strong>commit</strong>, e opcionalmente uma descrição. Quando estiver pronto, clique no botão <strong>Commit</strong>. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/6.png"><img title="6"   alt="6" src="http://blob.vitormeriat.com.br/images/2013/05/6.png" width="560" height="326" /></a></p>
<p>&#160;</p>
<h2>Passo 7. Publicando seu Commit</h2>
<p align="justify">Para publicar seu commit no GitHub você clicar no link <strong>Publish</strong> no topo do aplicativo. Pronto! Agora você já enviou o seu primeiro commit ao GitHub! </p>
<p align="justify">Você também vai notar agora que o botão de publicar as alterações para <strong>&quot;In Sync&quot;</strong> (em sincronia) para confirmar que o repositório está atualizado em sua máquina local e no GitHub. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/7-1.png"><img title="7.1"   alt="7.1" src="http://blob.vitormeriat.com.br/images/2013/05/7-1.png" width="560" height="326" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/7-2.png"><img title="7.2"   alt="7.2" src="http://blob.vitormeriat.com.br/images/2013/05/7-2.png" width="560" height="326" /></a></p>
<p>&#160;</p>
<h2><font style="font-weight:bold;">Conclusão</font></h2>
<p align="justify">É muito fácil trabalhar com o GitHub, há vários outros recursos que pretendo abordar em futuros posts. Caso você se interesse recomendo o seguinte site como referência: <a href="https://help.github.com/">https://help.github.com/</a></p>
<p>&#160;</p>
<h2><font style="font-weight:bold;">Até mais e bom estudo a todos!</font></h2>
 
