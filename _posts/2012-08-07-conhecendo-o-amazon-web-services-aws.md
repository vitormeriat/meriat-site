---
layout: post
title: Conhecendo o Amazon Web Services – AWS
date: 2012-08-07 
categories:
- Amazon Web Service
- Cloud Computing

---
<p><a href="http://blob.vitormeriat.com.br/images/2012/08/amazon-web-services.png"><img style="background-image:none;margin:0 20px 0 0;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border-width:0;" title="amazon-web-services" src="http://blob.vitormeriat.com.br/images/amazon-web-services.png" alt="amazon-web-services" width="320" height="130" align="left"   /></a></p>
<p align="justify"><strong>Amazon Web Services (AWS)</strong> é a plataforma de computação na nuvem da Amazon. Se trata de um conjunto de serviços de computação remota (também chamados <strong>web services</strong>) que juntos, constituem uma plataforma de computação em nuvem, proporcionada através da Internet pela Amazon.com. Neste <strong>post</strong> vamos iniciar com os primeiros passos para se conhecer e trabalhar com a plataforma de cloud computing da Amazon.</p>
<p><!--more--></p>
<p align="justify">Caso você não esteja familiarizado com os conceitos de cloud computing recomendo a leitura dos seguintes postes publicados aqui: <a href="http://vitormeriat.wordpress.com/2011/01/17/entrando-na-nuvem/" target="_blank">ENTRANDO NA NUVEM!</a>&amp; <a href="http://vitormeriat.wordpress.com/2011/01/17/o-que-esperar-da-nuvem/" target="_blank">O QUE ESPERAR DA NUVEM?</a></p>
<p align="justify">Desde o início de 2006, a Amazon Web Services (AWS) tem fornecido às empresas de todos os portes uma infraestrutura de serviços web com plataforma em nuvem. Com a AWS é possível calcular o poder de computação, armazenamento e outros serviços relacionados. Esta plataforma oferece acesso ao serviços de infraestrutura de TI elástica como exigido por seus negócios. Com a AWS, você tem a flexibilidade de escolher qualquer plataforma de desenvolvimento ou modelo de programação que se adapte aos problemas que você está tentando resolver.</p>
<p align="justify">Seguindo o modelo de <strong>SaaS (Software as a Service)</strong>, a AWS oferece um modelo maduro de cobrança e monitoramento para que você saiba exatamente o que está pagando. É importante lembrar que um dos pilares da cloud computing é pagar somente pelo que usar, sem despesas iniciais ou compromissos de longo prazo.<br />
Usando a <strong>A</strong>mazon <strong>W</strong>eb <strong>S</strong>ervices, um website de comércio eletrônico pode resistir facilmente a uma demanda imprevista; uma empresa farmacêutica pode "alugar" poder de computação para executar simulações em grande escala; uma empresa de mídia pode disponibilizar um número ilimitado de vídeos, música e muito mais; e uma empresa pode implantar serviços e treinamento utilizando largura de banda para sua força de trabalho móvel.</p>
<p align="justify">
<p align="justify">A AWS oferece uma gama de serviços e produtos como podemos observar na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/08/arquitetura-aws.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Arquitetura AWS" src="http://blob.vitormeriat.com.br/images/arquitetura-aws.png" alt="Arquitetura AWS" width="560" height="492"   /></a></p>
<p>&nbsp;</p>
<p>Podemos dividir os seus produtos e serviços nos seguintes agrupamentos lógicos:</p>
<ul>
<ul>
<li>Computacional</li>
<li>Rede</li>
<li>Entrega de Conteúdo</li>
<li>Pagamentos e faturamento</li>
<li>Banco de dados</li>
<li>Armazenamento</li>
<li>Implementação e gerenciamento</li>
<li>Suporte</li>
</ul>
</ul>
<p align="justify">Quando falamos de AWS os serviços mais populares são o <strong>Amazon EC2</strong> e o <strong>Amazon S3,</strong> mas como vimos na imagem anterior a AWS fornece um número muito grande de serviços e produtos. Muito disto se dá pelo tempo e maturidade que a Amazon alcançou ao longo destes anos. Um exemplo disto pode ser o <strong>Spot Instances</strong>. A idéia é simples: a Amazon faz leilão automático de recursos computacionais. Se a demanda pela nuvem da Amazon diminui, os recursos tendem a baratear. Caso aumentem, os recursos tornam-se mais caros. É uma estratégia de precificação dinâmica. Funciona assim: baseada na lei da oferta e procura a Amazon determina um valor mínimo para as instâncias. Estes preços flutuam livremente, de acordo com a demanda, influenciados, por exemplo, pela hora do dia. O usuário dá seu lance. Se o seu lance é maior que o preço esperado pela Amazon, a instância é alocada a ele, que pode começar a executar. Quando o preço da instância torna-se maior que o lance oferecido, a instância é suspensa e só volta a rodar quando o lance se tornar maior novamente. Toda a operação é automática. Claro que esta oferta só vale para determinados tipos de aplicação, que não sejam dependentes de tempo.</p>
<blockquote>
<p align="justify">É indiscutível que o modelo de cloud computing ainda é um work in progress e a cada dia aprendemos um pouco mais.</p>
</blockquote>
<p align="justify">Como em qualquer investimento de TI, a primeira coisa a fazer é certificar-se de seu modelo de negócio está alinhado com seu plano de TI. Saber onde e como tirar proveito de recursos de nuvem requer conhecer estes recursos. Abaixo temos um descritivo dos serviços da AWS.</p>
<p>&nbsp;</p>
<h3 align="justify"><strong>Amazon Elastic Compute Cloud (Amazon EC2)</strong></h3>
<p align="justify">A Amazon Elastic Compute Cloud oferece a capacidade computacional pague conforme usar integrada.</p>
<h3 align="justify"><strong>Amazon Simple Storage Service (Amazon S3)</strong></h3>
<p align="justify">O Amazon Simple Storage Service fornece uma infraestrutura de armazenamento de dados totalmente redundante para armazenar e recuperar qualquer quantidade de dados, a qualquer momento, de qualquer local na Web.</p>
<h3 align="justify"><strong>Amazon Virtual Private Cloud (Amazon VPC)</strong></h3>
<p align="justify">O Amazon Virtual Private Cloud (Amazon VPC) permite-lhe aproveitar uma seção privada e isolada da nuvem da Amazon Web Services (AWS) onde você pode executar recursos AWS em uma rede virtual que você mesmo define. Com o Amazon VPC, é possível definir uma topologia de rede virtual que lembra muito uma rede tradicional que você poderá operar no seu próprio Datacenter.</p>
<h3 align="justify"><strong>Amazon CloudFront</strong></h3>
<p align="justify">O Amazon CloudFront é um serviço da Web que facilita a distribuição de conteúdo com baixa latência por meio de um rede global de pontos de presença.</p>
<h3 align="justify"><strong>Amazon Route 53</strong></h3>
<p align="justify">O Amazon Route 53 é um serviço web de Domain Name System (DNS) altamente disponível e escalável.</p>
<h3 align="justify"><strong>Amazon Relational Database Service (Amazon RDS)</strong></h3>
<p align="justify">O Amazon Relational Database Service é um serviço da Web que facilita a configuração, a operação e o escalonamento de um banco de dados relacional na nuvem.</p>
<h3 align="justify"><strong>Amazon SimpleDB</strong></h3>
<p align="justify">O Amazon SimpleDB funciona em conjunto com o Amazon S3 e o Amazon EC2 para executar consultas em dados estruturados em tempo real.</p>
<h3 align="justify"><strong>Amazon Simple Queue Service (Amazon SQS)</strong></h3>
<p align="justify">O Amazon Simple Queue Service fornece uma fila hospedada para armazenar mensagens à medida que elas são transferidas entre os computadores, facilitando a criação de um fluxo de trabalho automatizado entre os serviços da Web.</p>
<h3 align="justify"><strong>Amazon Simple Notification Service (Amazon SNS)</strong></h3>
<p align="justify">O Amazon Simple Notification Service é um serviço da Web que facilita a configuração, a operação e o envio de notificações com base na nuvem.</p>
<h3 align="justify"><strong>Amazon Elastic MapReduce</strong></h3>
<p align="justify">O Amazon Elastic MapReduce é um serviço da Web que permite às empresas, pesquisadores, analistas de dados e desenvolvedores processar, de modo fácil e econômico, grandes quantidades de dados.</p>
<p>&nbsp;</p>
<p align="justify">Para mais informações acesse <a href="http://aws.amazon.com/pt/" target="_blank">http://aws.amazon.com/pt/</a></p>
<p align="justify">No próximo poste estarei falando sobre a arquitetura da AWS. Já nos próximos posts vamos ver sobre alguns serviços específicos da plataforma focando em exemplos de implementação no <strong>.NET</strong>.</p>