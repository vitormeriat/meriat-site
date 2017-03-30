---
layout: post
title: 'Windows Azure Storage: Decolando com armazenamento na Nuvem!'
date: 2011-08-03
categories:
    - Cloud Computing
    - Microsoft Azure
    - Microsoft Azure Storage
---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/windows-azure-storage-ttulo.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border-width:0;margin:0 10px 0 0;" title="Windows-Azure-Storage T&iacute;tulo"   alt="Windows-Azure-Storage T&iacute;tulo" align="left" src="http://blob.vitormeriat.com.br/images/2011/08/windows-azure-storage-ttulo.png" width="355" height="257" /></a>Como já tratamos anteriormente, o Windows Azure é um “Sistema Operacional” para a tão famosa cloud computing. Utilizando principalmente a oferta PaaS (Plataforma como Serviço)* temos o benefício de uma pequena curva de aprendizagem já que essencialmente temos ferramentas de desenvolvimento já conhecidas da plataforma.
<p align="justify">O Azure disponibiliza meios para que os desenvolvedores escrevam serviços escalonáveis e altamente disponíveis como computação virtualizada, gerenciamento automatizado um poderoso SDK e é claro, armazenamento escalável.
<p align="justify">O objetivo do Windows Azure Storage é oferecer um armazenamento Escalável, Durável ser altamente disponível e proporcionar ao usuário pagar somente o quanto ele usar. É de fácil acesso a seus dados com interfaces <a href="http://pt.wikipedia.org/wiki/REST" target="_blank">REST</a>simples, disponíveis remotamente e em datacenters. Cabe aqui um comentário: estes são alguns dos motivos que fazem acreditar tão fortemente na Cloud Computing.</p>
<p><!--more-->
<p align="justify">Os serviços de armazenamento são oferecidos em quatro níveis de abstração:
<ul>
<ul>
<li>
<div align="justify"><font color="#333333"><b>Blobs</b> – Fornece uma interface simples para armazenamento de grandes itens de dados. </font></div>
</li>
<li>
<div align="justify"><font color="#333333"><b>Tabelas</b> – Fornecem um conjunto de entidades, que contêm um conjunto de propriedades. Um aplicativo pode manipular as entidades e consultar qualquer uma das propriedades armazenadas em uma tabela. </font></div>
</li>
<li>
<div align="justify"><font color="#333333"><b>Filas</b> – Fornecer armazenamento confiável para entrega de mensagens propiciando expedição assíncrona de trabalhos para habilitar a comunicação entre os serviços de diferentes partes (papéis) de sua aplicação.</font></div>
</li>
<li>
<div align="justify"><font color="#333333"><b>Drives</b> – Fornece volumes NTFS duráveis para aplicações.</font></div>
</li>
</ul>
</ul>
<p align="justify">O acesso ao armazenamento e o balanceamento de carga é realizado automaticamente através de um conjunto de nós responsáveis pelo armazenamento físico proporcionando escalabilidade e disponibilidade. </p>
<p align="justify">Para podermos utilizar o os serviços de armazenamento do Windows Azure, o usuário precisa criar uma conta de acesso ao portal de gerenciamento da plataforma Windows azure no endereço <a href="http://windows.azure.com" target="_blank">Windows Azure</a>e acessando a opção “Serviços Hospedados, Contas de Armazenamento e CDN” criar uma “Nova Conta de Armazenamento” seguindo os passos conforme a figura abaixo:
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/08/figura01.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Figura01"   alt="Figura01" src="http://blob.vitormeriat.com.br/images/2011/08/figura01.png" width="520" height="522" /></a>
<p align="justify">Com a criação da conta de armazenamento você irá receber uma chave secreta de 256 bits que será usada para autenticar as solicitações do usuário no sistema de armazenamento criando e incluindo uma assinatura <a href="http://en.wikipedia.org/wiki/HMAC" target="_blank">HMAC</a>(Hash-based Message Authentication Code) em cada uma das solicitações. Esta chave é associada a conta de armazenamento e compõem as requisições para a devida autorização.
<p align="justify">Algo muito importante de se notar é a URI utilizada para acessar os dados:
<ul>
<ul>
<li>
<div align="justify">http(s)://nomeDaConta.<strong>blob</strong>.core.windows.net/<font color="#22a6cc"><b>&lt;nomeDoContainer&gt;/&lt;nomeDoBlob&gt;</b></font></div>
</li>
<li>
<div align="justify">http(s)://nomeDaConta.<strong>queue</strong>.core.windows.net/<font color="#22a6cc"><b>&lt;nomeDaFila&gt;</b></font></div>
</li>
<li>
<div align="justify">http(s)://nomeDaConta.<strong>table</strong>.core.windows.net/<font color="#22a6cc"><b>&lt;nomeDaTabela&gt;</b></font></div>
</li>
</ul>
</ul>
<p align="justify">Podemos notar que a primeira parte do nome do Host (nomeDaConta) trata-se do nome que foi registrado no portal de gerenciamento da plataforma Azure. Isto possibilita o uso via DNS (<b><i>D</i>omain <i>N</i>ame <i>S</i>ystem</b> - Sistema de Nomes de Domínios) redirecionando seu pedido para o local onde estão os dados de armazenamentos para a conta em questão. Isto ocorre para todas as solicitações. Após o nome da conta temos as palavras chave blob, queue e table que irão redirecionar a requisição ao serviço correspondente. Blob, Queue e Table são serviços distintos contendo cada um espaço diferente na conta de armazenamento. Logo é possível criar um Blob Container, uma Queue e uma Table com o mesmo nome.</p>
<p align="justify"><u></u></p>
<p align="justify">Como não poderia faltar, para utilizarmos o ambiente de armazenamento devemos fornecer a nossa aplicação os dados necessários para viabilizar esta conexão. Quando trabalhamos com os arquivos de configuração e definição dos projetos Azure devemos ter em mente que podemos executar nossa aplicação em dois ambientes distintos: na nuvem e local.
<p align="justify">As credenciais necessárias para a geração da assinatura HMAC são especificadas no arquivo de configuração do respectivo papel do Windows Azure. Os formatos para string de conexão do armazenamento local e na nuvem respectivamente são:
<p><a href="http://blob.vitormeriat.com.br/images/2011/08/configuration.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="Configuration"   alt="Configuration" src="http://blob.vitormeriat.com.br/images/2011/08/configuration.png" width="570" height="144" /></a></p>
<pre>&nbsp;</pre>
<p align="justify">Não há nenhuma noção específica de segurança baseada por papel do Windows Azure Storage, assim uma solicitação autenticada terá acesso completo ao armazenamento. Uma exceção a isso é o container blob, que pode ser público (anônimo) ou privado. A autorização é da responsabilidade da aplicação que consome os serviços da camada de armazenamento.</p>
<p align="justify">&nbsp;</p>
<hr />
<p align="justify">Espero que tenham gostado. Nos próximos artigos estarei detalhando alguns pontos importantes no tocante ao Windows Azure Storage. Minha ideia é postar um artigo sobre cada um dos níveis de abstração do serviço de armazenamento do Azure com exemplo prático. Agora é mão no código.</p>
<p align="justify">&nbsp;</p>
<h2>Um grande abraço e ótimo estudo!</h2>