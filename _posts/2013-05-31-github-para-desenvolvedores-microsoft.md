---
layout: post
title: GitHub para desenvolvedores Microsoft
date: 2013-05-31 18:21:20.000000000 -03:00
type: post
published: true
status: publish
categories:
- Agile
- ALM

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/05/octocat.png"><img title="octocat" style="background-image:none;float:left;padding-top:0;padding-left:0;margin:0 20px 0 0;display:inline;padding-right:0;border-width:0;" border="0" alt="octocat" align="left" src="http://blob.vitormeriat.com.br/images/octocat_thumb.png" width="280" height="280" /></a>Desenvolver hoje é um desafio. Equipes grandes, muitos papeis, estimativas irrealistas, problemas de comunicação, escritórios lotados e uma série de outro fatores que influenciam na qualidade e saúde do código. Quando levamos estes fatores em consideração, se torna claro a necessidade de ferramentas que nos auxiliem a garantir esta saúde ou possibilidade de manter as versões saudáveis com os arquivos de código fonte sob algum tipo de controle ou versionamento.</p>
<p align="justify">O controle de versão é um sistema que registra as mudanças feitas em um arquivo ou um conjunto de arquivos ao longo do tempo de forma que você possa recuperar versões específicas.</p>
<p><!--more-->
<p align="justify">Se você é desenvolvedor colaborativo sabe a importância dos sistemas de versionamento de código fonte. Manter o controle das alterações e novas funcionalidades torna-se fundamental. É nesse cenário que optar por um <strong>Sistema de Controle de Versão (Version Control System ou VCS)</strong> é uma decisão sábia.</p>
<p align="justify">Um <strong>VCS</strong> permite reverter arquivos para um estado anterior, reverter um projeto inteiro para um estado anterior, comparar mudanças feitas ao decorrer do tempo, ver quem foi o último a modificar algo que pode estar causando problemas, quem introduziu um bug e quando, e muito mais. Usar um VCS normalmente significa que se você estragou algo ou perdeu arquivos, poderá facilmente reavê-los. Além disso, você pode controlar tudo sem maiores esforços.</p>
<p align="justify">Para os desenvolvedores Microsoft o<strong> Team Foundation Server (TFS)</strong> tem sido a grande opção. É claro que o <strong>TFS</strong> não é apenas um simples controle de versão e sendo assim acaba sendo algo muito grande para determinadas necessidades. Com base nisso apresento o <strong>GitHub</strong>.</p>
<p align="justify">O GitHub é um serviço web compartilhado para projetos e que usa o controle de versão <strong>Git</strong>. O GitHub possui planos comerciais e gratuitos para projetos de código aberto. Sendo assim ele é utilizado como repositório online de códigos fonte para projetos de código aberto.</p>
<p align="justify">Além disto, o GitHub possui funcionalidades de uma rede social como feeds, followers, wiki e um gráfico que mostra como os desenvolvedores trabalham as versões de seus repositórios. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/05/github.png"><img title="GitHub" style="border-top:0;border-right:0;background-image:none;border-bottom:0;float:none;padding-top:0;padding-left:0;margin-left:auto;border-left:0;display:block;padding-right:0;margin-right:auto;" border="0" alt="GitHub" src="http://blob.vitormeriat.com.br/images/github_thumb.png" width="560" height="434" /></a></p>
<p align="justify">O Git é o principal controle de versão do mercado quando o assunto é Distributed Concurrent Versions System (DCVS) permitindo ao desenvolvedor ter um sistema de controle de versões distribuído independente do servidor.</p>
<p align="justify">No GitHub temos a possibilidade de trabalhar com repositórios espalhados onde push’s e pull’s são trocados entre diferentes desenvolvedores de um mesmo projeto. Isso é claro pode virar um caos. Pode acontecer de chegar a uma situação onde 'n' diferentes desenvolvedores tem 'n' diferentes versões do software, o que não seria legal.</p>
<p align="justify">Para resolver esse problema é uma prática comum adotar um repositório como sendo &quot;O Repositório&quot;, e esse repositório será aquele que terá sempre a versão mais recente, e mais completa, do software e de onde novos desenvolvedores que começarem a participar do seu desenvolvimento poderão obter a cópia mais atualizada.</p>
<p align="justify">O GitHub funciona como sendo &quot;O Repositório&quot;. Cada diferente desenvolvedor que quiser trabalhar em um mesmo projeto simplesmente pede uma cópia desse repositório e começa a trabalhar. É lógico que, para os usuários mais xiitas do terminal, tudo isso pode ser feito por linha de comando, mas nada melhor do que ter um ambiente onde tudo isso é feito com 1 clique e ainda seja possível verificar quantas pessoas pegaram uma cópia do seu repositório, e mesmo quem, com a mesma facilidade.</p>
<p align="justify">Além disso o GitHub ainda cria uma interface para que, quando um desenvolvedor quiser enviar as modificações que fez para &quot;O Repositório&quot;, os administradores desse repositório central possam fazer comentários e sugerir alterações antes de aceitar essa modificação.</p>
<p align="justify">&#160;</p>
<p>No próximo post vamos conhecer o GitHub na prática.</p>
<h2><font style="font-weight:bold;">Até mais e bom estudo a todos!</font></h2>