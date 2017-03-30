---
layout: post
title: 'Dicas Azure: Evite Deployments não validados no Windows Azure'
date: 2012-03-05
categories:
- Cloud Computing
- Microsoft Azure
image: "http://blob.vitormeriat.com.br/images/2012/03/01.png"
---
<<<<<<< HEAD

<p align="justify">Ai vai mais uma dica de “produtividade” para o <strong>Windows Azure</strong>. Se tinha uma coisa irritante nas versões anteriores ao <strong>SDK 1.4 </strong>era a não validação de pacotes para <strong>deploy </strong>do <strong>Azure</strong>. Vamos supor o seguinte: Você fez sua aplicação para o Azure e codificou uma <strong>class libary</strong> chamada <strong>MinhaDependencia </strong>com suas regras de negócio. Neste ponto seu projeto tem uma dependência do assembly <strong>MinhaDependencia.dll</strong>. Se por algum motivo esta dependência não estiver anexada ao pacote, seu deploy irá falhar e possivelmente você vai encarar um <a href="http://vitormeriat.wordpress.com/2012/02/28/dicas-azure-cuidado-com-o-deploying-travado-deployment-at-busy-or-initializing-status-for-long-time/">Deploy Travado em Busy ou Initializing,</a> como já tratei anteriormente.</p>
<p><!--more-->
=======
<p align="justify">Ai vai mais uma dica de “produtividade” para o <strong>Windows Azure</strong>. Se tinha uma coisa irritante nas versões anteriores ao <strong>SDK 1.4 </strong>era a não validação de pacotes para <strong>deploy </strong>do <strong>Azure</strong>. Vamos supor o seguinte: Você fez sua aplicação para o Azure e codificou uma <strong>class libary</strong> chamada <strong>MinhaDependencia </strong>com suas regras de negócio. Neste ponto seu projeto tem uma dependência do assembly</p> <strong>MinhaDependencia.dll</strong>. Se por algum motivo esta dependência não estiver anexada ao pacote, seu deploy irá falhar e possivelmente você vai encarar um <a href="http://vitormeriat.wordpress.com/2012/02/28/dicas-azure-cuidado-com-o-deploying-travado-deployment-at-busy-or-initializing-status-for-long-time/">Deploy Travado em Busy ou Initializing,</a> como já tratei anteriormente.</p>
>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<p>Quando iniciamos o deploy, fornecemos dois arquivos: um é o pacote de serviço do aplicativo (.cspkg), o outro é o arquivo de configuração (.cscfg). No momento em que o pacote está sendo gerado, o windows azure faz uma gama de validações para garantir que você não haverá problemas na hora de publicar na nuvem.</p>
<p>&#160;</p>
<h2>O problema</h2>
<p align="justify">Quando o mecanismo de validação encontra algo de errado, é gerado uma advertência. como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/01.png"><img alt="01" src="http://blob.vitormeriat.com.br/images/2012/03/01.png"/></a></p>
<p align="justify">É uma advertência sobre a falta de uma determinada dependência no pacote gerado. Isso é algo que certamente fará seu deploy falhar, contudo é retornado como uma simples advertência.</p>
<p align="justify">No meu ponto de vista, se eu gero um pacote para implantação na nuvem, eu realmente vou querer que ele funcione. Se existe algo nele que vai fazer meu deploy falhar, então deveria ser retornado como erro. Quando estamos trabalhando em um projeto grande, é comum termos algumas “várias” mensagens de advertência, e ter uma algo tão significativo perdido no meio de outras mensagens como variáveis que não estão sendo usadas é algo inconveniente. </p>
<p>&#160;</p>
<h2>A solução</h2>
<p align="justify">Você pode ir nas opções do projeto cloud clicando com o botão direito sobre o projeto, ir na aba <strong>Develompent</strong>, na sessão <strong>Validation</strong> e alterar a opção <strong>Treat warnings as erros</strong> (Tratar avisos como erros) que por padrão é false para true. Como na imagem abaixo:</p>
<<<<<<< HEAD
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/03/03.png"><img alt="03" src="http://blob.vitormeriat.com.br/images/2012/03/03.png"/></a></p>
=======
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/03/03.png"><img alt="03" src="http://blob.vitormeriat.com.br/2012/03/images/03.png"/></a></p>
>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<p align="justify">Sendo assim, todas as mensagens que a validação do pacote gerar que antes eram tratadas como&#160; advertências agora serão tratadas como erros. Exatamente como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/02.png"><img alt="02" src="http://blob.vitormeriat.com.br/images/2012/03/02.png"/></a></p>
<p align="justify">Espero que está dica possa ajudar quem como eu, perdeu um bom tempo por causa de uma simples advertência…</p>
<p align="justify">&#160;</p>
<h4><font>Um grande abraço e ótimo estudo a todos!</font></h4>