---
layout: post
title: Azure Mobile Service–Gerenciando Logs, deploy e o projeto Kudu
date: 2014-09-11
categories:
- Cloud Computing
- Microsoft Azure
- Mobile
image: "http://blob.vitormeriat.com.br/images/2014/09/capa.png"
---

<p align="justify">Esta semana recebi um pergunta em relação ao post anterior <a href="http://vitormeriat.com.br/2014/09/05/azure-mobile-servicelogging-local-e-na-nuvem-com-backend-net-webapi/" target="_blank">Azure Mobile Service–Logging local e na nuvem com backend .NET WebAPI</a>. A pergunta era como deletar os logs gerados. </p>
<p align="justify">Se você já utilizou o <strong>Azure Mobile Service</strong> e precisou dos <strong>LOGS</strong>, sabe que via portal não conseguimos fazer a gestão dos mesmos. Levando em consideração que Serviços Móveis são criados com suporte a utilização em massa, essa se torna uma necessidade real.</p>
<p align="justify">Sendo assim este POST é ao mesmo tempo uma dica e também serve de introdução ao <strong>Projeto Kudu</strong>, com o qual vamos fazer o backup e deleção dos LOGS. </p>
<p><img title="capa"   alt="capa" src="http://blob.vitormeriat.com.br/images/2014/09/capa.png" width="100%" /></p>
<p align="justify">O primeiro ponto é relembrar do anuncio do deploy no <strong>Azure Web Sites</strong> utilizando <a href="http://git-scm.com/" target="_blank">GIT</a>. Isso foi realmente bacana mas qual a ligação com o nosso assunto? O que poucos sabem é que a engine que suporta este recurso é o projeto <strong>Open Source</strong> codinome <a href="https://github.com/projectkudu/kudu" target="_blank">Kudu</a>.</p>
<p><!--more-->
<p align="justify">O projeto Kudu está no <a href="https://github.com/" target="_blank">GitHub</a> e foi liberado via Apache License 2.0, o que te permite rodar em qualquer máquina utilizando um IIS local, por exemplo.</p>
<p><img alt="LOG02" src="http://blob.vitormeriat.com.br/images/2014/09/log02.png" width="100%" /></p>
<p align="justify">Já sabemos que para todo <a href="http://azure.microsoft.com/pt-br/services/mobile-services/" target="_blank">Azure Mobile Service</a> criado temos uma <a href="http://azure.microsoft.com/pt-br/services/websites/" target="_blank">Azure Web Site</a> associando onde é realizado o deploy desta aplicação. Sendo assim podemos utilizar o <strong>Kudu</strong> para gerir as informações do nosso serviço, dentre elas os <strong>LOGS</strong>.</p>
<p>&#160;</p>
<p><a href="https://github.com/projectkudu/kudu/wiki" target="_blank">Antes de iniciar sugiro a leitura da documentação do KUDU, e que você realize os teste em um projeto novo primeiro.</a></p>
<p>&#160;</p>
<p align="justify">Então vamos lá, acesse o Mobile Service. No meu caso vou utilizar o mesmo serviço criado no POST anterior: <font size="4"><strong><a href="https://meriatwebapi.azure-mobile.net/">https://meriatwebapi.azure-mobile.net/</a></strong></font></p>
<p><img alt="LOG01" src="http://blob.vitormeriat.com.br/images/2014/09/log01.png" width="100%" /></p>
<p align="justify">Notem que já tenho uma diversidade de LOGS, os quais eu quero deletar. O primeiro passo é acessar a página do Kudu para o Mobile Service correspondente:</p>
<p><strong><font size="4">https://[O NOME DO SEU WAMS].scm.azure-mobile.net/</font></strong></p>
<p>No meu caso o enderço ficou assim:</p>
<p><font size="4"><strong>https://meriatwebapi.scm.azure-mobile.net/</strong></font></p>
<p align="justify">Caso você já esteja logado na Subscription em que foi criado o serviço, o acesso será imediato. Caso contrário é só entrar com sua<strong> Microsoft Account</strong> para ter acesso a página de gestão do serviço.</p>
<p><img alt="LOG05" src="http://blob.vitormeriat.com.br/images/2014/09/log05.png" width="100%" /></p>
<p align="justify">Vamos direto a parte da gestão de <strong>LOGS</strong>. Pretendo abordar o resto com mais detalhes em outro post. Sendo assim, no menu superior acesse a opção <strong>Debug Console</strong> e selecione qualquer das opções. No exemplo vou estar utilizando a opção <strong>PowerShell</strong>.</p>
<p><img alt="LOG06" src="http://blob.vitormeriat.com.br/images/2014/09/log06.png" width="100%" /></p>
<p align="justify">Note que foi aberto um console do <strong>PS</strong> no browser. Também vai aparecer uma estrutura de pastas: <strong><u>LogFiles</u></strong> e <strong><u>site</u></strong>.</p>
<p><img alt="LOG04" src="http://blob.vitormeriat.com.br/images/2014/09/log04.png" width="100%" /></p>
<p align="justify">Clique na pasta <strong>LogFiles</strong>. Será exibido os arquivos físicos onde está sendo realizado a gravação real dos <strong>LOGS,</strong> que são exibidos no Portal do Microsoft Azure.</p>
<p><img alt="LOG03" src="http://blob.vitormeriat.com.br/images/2014/09/log03.png" width="100%" /></p>
<p>Nas opções do lado esquerdo podemos:</p>
<ul>
<li>Fazer o download do arquivo </li>
<li>Abrir para visualização ou edição </li>
<li>Excluir o arquivo de LOG </li>
</ul>
<p align="justify">Note que a console do PowerShell exibe os comandos que estamos executando via interface do usuário. ;)</p>
<p align="justify">Clicando na opção de download podemos baixar o arquivo txt, ou no caso do IE exibir via browser.</p>
<p align="justify"><img alt="LOG08" src="http://blob.vitormeriat.com.br/images/2014/09/log08.png" width="100%" /></p>
<p align="justify">Realize a deleção de todos os arquivos txt que não forem necessários. Como é possível ler, exclua somente o que você jugar desnecessário. No meu caso deletei tudo.</p>
<p align="justify"><img alt="LOG09" src="http://blob.vitormeriat.com.br/images/2014/09/log09.png" width="100%" /></p>
<p align="justify">Voltando ao portal do Microsoft Azure e acessando o serviço correspondente, só precisamos rodar o <strong>REFRESH</strong> e pronto. Nenhum LOG será exibido.</p>
<p align="justify"><img alt="Result" src="http://blob.vitormeriat.com.br/images/2014/09/result.png" width="100%" /></p>
<p align="justify">&#160;</p>
<p align="justify">Pronto, agora podemos “versionar” os LOGS ou simplesmente excluir o arquivo para zerar a visualização via Portal do Microsoft Azure.</p>
<p>Pessoal, não esqueçam de testar e ler a documentação primeiro… assim não se corre o risco de excluir LOGS em produção ou afetar a implementação do serviço.</p>
<p>&#160;</p>
<h2>Referências:</h2>
<p><a title="https://github.com/projectkudu/kudu" href="https://github.com/projectkudu/kudu">https://github.com/projectkudu/kudu</a></p>
<p><a title="https://github.com/projectkudu/kudu/wiki" href="https://github.com/projectkudu/kudu/wiki">https://github.com/projectkudu/kudu/wiki</a></p>
<p><a title="http://azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/" href="http://azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/">http://azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/</a></p>
<p>&#160;</p>
<h6></h6>
<h4><font color="#ccb400">Bons estudos e até a próxima pessoal&#160; ;)</font></h4>
