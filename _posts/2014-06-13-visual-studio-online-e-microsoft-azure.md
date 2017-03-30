---
layout: post
title: Microsoft Azure e o Visual Studio Online
date: 2014-06-13 21:46:11.000000000 -03:00
type: post
published: true
status: publish
categories:
- Cloud Computing
- Microsoft Azure

---
<p align="justify">Olá pessoal. Neste post vou abordar sobre o novo recurso disponível em integração com o Microsoft Azure. Estou falando aqui da possibilidade de interagir o seu<strong> Visual Studio Online</strong> (VSO) com o <strong>Azure Active Directory</strong> (AAD) utilizando novas contas de maneira simples e rápida.</p>
<p align="justify">Para facilitar o post vou utilizar a seguinte nomenclatura:</p>
<ul>
<ul>
<li>
<div align="justify"><strong>VSO</strong> – Visual Studio Online </div>
</li>
<li>
<div align="justify"><strong>AAD</strong> – Azure Active Directory </div>
</li>
</ul>
</ul>
<p align="justify">Como o anunciado por <strong>Brian Harry</strong> (Product Unit Manager for Team Foundation Server), uma das maiores solicitações dos usuários do VSO é a autenticação federada. E qual o motivo disso?</p>
<p align="justify">Primeiro as inúmeras solicitações para se utilizar contas corporativas e não só o famoso <strong>Live ID</strong>. Outro ponto é que anteriormente só era possível ter a correspondência entre o VSO e uma única conta do Microsoft Azure. Isso se aplica muito bem caso seu cenário seja de trabalhar apenas com projetos próprios, já se houver a necessidade de interagir com outras contas (empresariais, clientes e afins), você ficava limitado.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/capa1.png"><img title="capa"  alt="capa" src="http://blob.vitormeriat.com.br/images/2014/06/capa.png" width="700" height="671" /></a></p>
<p><!--more-->
<p align="justify">É importante falar que este recurso se aplica as contas novas após o lançamento deste recuso, porém, como o anunciado por Brian Harry, nos próximos sprints já será possível adicionar contas já existentes. </p>
<blockquote><p>Important: Unfortunately, we do not yet support linking an existing VS Online account to AAD, and therefore there's no way to use your AD credentials to log into an account you've already created.</p>
</blockquote>
<p align="justify">Seguindo no que temos hoje, é possível de maneira muito simples criar uma nova conta do <strong>VSO</strong> já vinculando a mesma do Microsoft Azure.</p>
<p align="justify">Para isso basta simplesmente logoar no portal e acessar a área do <strong>VISUAL STUDIO ONLINE</strong> no painel da esquerda como na imagem abaixo. Você pode utilizar o link caso ainda não tenha uma conta vinculada ou com este serviço selecionado clicar em <strong>+ NEW</strong> no canto esquerdo inferior.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/06/04.png"><img title="04"  alt="04" src="http://blob.vitormeriat.com.br/images/2014/06/04.png" width="700" height="400" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Agora temos duas opções, criar uma nova conta ou vincular uma conta existente.&#160; Neste exemplo eu já possuo uma conta e estou criando uma do zero. Aqui eu já tenho a opção de definir se quero ou não vincular minha conta ao meu AAD. </p>
<p align="justify">Em outras palavras em minutos estou subindo um <strong>TFS</strong> e já vou ter a possíbilidade de trabalhar com contas corporativas em um cenário mais comun ao das grandes empresas.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/06/05.png"><img title="05"  alt="05" src="http://blob.vitormeriat.com.br/images/2014/06/05.png" width="700" height="400" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Note que&#160; agora na opção para linkar uma conta existente, ele exibe o meu VSO padrão que já está associado ao LIVE ID. Como já citei anteriormente o recurso para vinculação ao AAD só é possível para novas contas criadas apartir do lançamento do VSO. Sendo assim para minha conta padrão não consigo (por hora) utilizar este recurso.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/06.png"><img title="06"  alt="06" src="http://blob.vitormeriat.com.br/images/2014/06/06.png" width="700" height="397" /></a></p>
<p>&#160;</p>
<p>No fim deste exemplo, é só entrar no portal do <strong>VSO</strong> para ver as contas listadas ao seu <strong>LIVE ID</strong>. No meu caso, a conta <strong><u>meriat</u></strong> foi criada via portal do Microsoft Azure e já está viculada ao meu <strong>AAD</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/06/07.png"><img title="07"  alt="07" src="http://blob.vitormeriat.com.br/images/2014/06/07.png" width="700" height="286" /></a></p>
<p>&#160;</p>
<h2><font color="#ffc000">Bons estudos e até a próxima pessoal&#160; ;)</font></h2>