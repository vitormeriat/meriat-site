---
layout: post
title: Por dentro do novo Windows Azure
date: 2012-06-10
categories:
- Cloud Computing
- Microsoft Azure

---
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/titulo.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Titulo"   alt="Titulo" src="http://blob.vitormeriat.com.br/images/titulo.png" width="463" height="286" /></a></p>
<p align="justify">No dia 07-06-2012 foi anunciado mundialmente direto de San Francisco através de um grande evento online o novo <strong>Windows Azure</strong>. Algumas features já eram aguardadas com anseio pela comunidade e desenvolvedores Azure, outras foram de certa forma surpresas extremamente agradáveis. Vou estar condensando neste post as melhorias e novos recursos do Windows Azure.</p>
<p><!--more-->
<p align="justify">A organização lógica do novo Windows Azure está dividida em 5 “tipos” de recursos:</p>
<ul>
<li>Web Sites </li>
<li>Virtual Machines </li>
<li>Cloud Services </li>
<li>Big Data (Storage Service e SQL) </li>
<li>Media </li>
</ul>
<p>Você pode saber mais sobre isto <a href="https://www.windowsazure.com/en-us/home/features/overview/" target="_blank">na área Features do Azure acessando aqui!</a></p>
<p>&#160;</p>
<hr />
<h1>Novidades</h1>
<p>&#160;</p>
<h2>Novo Portal de Administração</h2>
<p align="justify">A mudança mais “aparente” é o novo portal de administração que é muito rápido e possui uma maior fluidez suportando filtragem e classificação dos dados funcionando em todos os navegadores. Uma informação importante disponibilizada por <strong>Scott Guthrie</strong> é que o novo portal é construído em cima de uma API de gerenciamento baseada no modelo REST dentro da Windows Azure - e tudo o que você pode fazer através do portal também pode ser feito através de programação acessando esta Web API.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/portal1.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="portal1"   alt="portal1" src="http://blob.vitormeriat.com.br/images/portal1.png" width="560" height="265" /></a></p>
<p>&#160;</p>
<h2>Windows Azure Virtual Machines</h2>
<p align="justify">As novidades em relação as Máquinas Virtuais são a possibilidade de subir o seu próprio Windows Server customizado ou imagens de Linux e migrar cargas de trabalho do SQL Server ou Sharepoint para a nuvem. As máquinas virtuais são acessadas via&#160; <strong>PowerShell</strong> ou usando o novo <strong>Windows Azure SDK (June 2012)</strong>.</p>
<p>Os sistemas operacionais e imagens disponíveis são:</p>
<p><strong>Windows Server</strong></p>
<ul>
<li>Windows Server 2008 R2 </li>
<li>Windows Server 2008 R2 com SQL Server 2012 Eval </li>
<li>Windows Server 2012 RC </li>
</ul>
<p><strong>Linux</strong></p>
<ul>
<li>OpenSUSE 12.1 </li>
<li>CentOS 6.2 </li>
<li>Ubuntu 12.04 </li>
<li>SUSE Linux Enterprise Server 11 SP2 </li>
</ul>
<p align="justify">Os usuários poderão escolher e instalar&#160; uma distribuição Linux a partir do Microsoft Windows Azure Image Gallery, e serão cobrados por hora. Os clientes também poderão implementar aplicações que foram feitas com o Suse Studio IDE (sigla para ambiente de desenvolvedor integrado, em tradução livre) diretamente&#160; para o Azure. Nesse caso, não precisarão se preocupar a respeito imagem da máquina - ao invés disso, irão inserir o Azure ID no Suse Studio antes de enviar a aplicação para a nuvem.</p>
<p><strong></strong></p>
<p><strong></strong></p>
<p>&#160;</p>
<h2>Windows Azure Web Sites</h2>
<p align="justify">Dedicado a implantação fácil e altamente elástica de aplicações web. Você pode fazer o deploy (implantação) para web-sites em segundos usando FTP, Git, TFS e Web Deploy.</p>
<p align="justify">É possível integrar a publicação de aplicações web com o controle de código fonte usando a integração com o novo serviço online de TFS (que permite um fluxo de trabalho do TFS completo - incluindo um build elástico e suporte a testes), ou você pode criar um repositório Git e referenciá-lo como um remote para executar implantações automáticas.</p>
<p align="justify">O Windows Azure também permite que você implante até 10 web-sites em um ambiente de hospedagem <strong>gratuito</strong> e compartilhado entre múltiplos usuários e bancos de dados (onde um site que você implantar será um dos vários sites rodando em um conjunto compartilhado de recursos do servidor). Isso te fornece uma maneira fácil para começar a desenvolver projetos sem nenhum custo envolvido.</p>
<p>&#160;</p>
<h2>Windows Azure Virtual Network</h2>
<p>Este novo serviço oferece uma maneira simples de criar um ambiente privado (chamada de rede virtual ou Vnet para o short) no Windows Azure e, opcionalmente, conectá-lo à sua rede no local usando um gateway VPN. Dentro da rede virtual que você tem controle sobre a topologia da rede - por exemplo, você pode configurar intervalos de endereços IP para as máquinas virtuais ou até mesmo especificar seu próprio DNS.</p>
<p>&#160;</p>
<h2>Serviços do Azure ganham novos nomes</h2>
<p>Uma das alterações ficou por conta dos novos nomes para alguns dos serviços na nuvem:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/06/novos-nomes-azure.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Novos nomes Azure"   alt="Novos nomes Azure" src="http://blob.vitormeriat.com.br/images/novos-nomes-azure.png" width="530" height="423" /></a></p>
<p>&#160;</p>
<hr />
<h1>Melhorias</h1>
<p>&#160;</p>
<h2 align="justify">Armazenamento</h2>
<p align="justify">Como uma opção adicional para a opção de armazenamento Geo-redundante, o armazenamento local redundante já está disponível para clientes que não necessitam de geo-replicação e estão procurando custos de armazenamento reduzidos.</p>
<p align="justify">&#160;</p>
<h2 align="justify">Caching</h2>
<p align="justify">O serviço de Cache no Windows Azure permite que você construa aplicações altamente escaláveis ​​e sensível, trazendo dados mais perto dos usuários finais. O “Caching Preview” oferece um novo modelo de arrendamento, novos recursos de visualização e melhor desempenho.&#160; Uma camada de cache dedicada pode ser criada para uma ou mais aplicações de múltiplas funções de operador proporcionando tamanhos de cache quase ilimitadas e de escala.</p>
<p align="justify">&#160;</p>
<h2 align="justify">Compliance</h2>
<p align="justify">O relatório de auditoria SSAE 16 (SOC 1 Type 2) já está disponível para os serviços principais do Windows Azure.</p>
<p align="justify">&#160;</p>
<h2 align="justify">SQL Reporting</h2>
<p align="justify">Agora disponível com um SLA totalmente apoiado,&#160; o Windows Azure SQL Reporting permite que você construa recursos de relatórios de fácil acesso no seu aplicativo Windows Azure. SQL Reporting permite criar relatórios com tabelas, gráficos, mapas, indicadores e mais, bem como implantá-los em ambas as nuvens privadas e públicas. Com a nuvem ao seu serviço, não há necessidade de gerir ou manter sua infra-estrutura de relatórios.</p>