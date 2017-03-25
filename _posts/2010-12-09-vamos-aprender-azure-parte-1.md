---
layout: post
title: Vamos aprender azure!   Parte 1
date: 2010-12-09
categories:
    - Cloud Computing
    - Microsoft Azure
---

Estou partindo para mais um desafio profissional e agora estou focando meus estudos no Azure. Isto mesmo, O Windows Azure é o sistema operacional para serviços na nuvem que é utilizado para o desenvolvimento, hosting e gerenciamento dos serviços dentro do ambiente da plataforma.

Pois bem, estou participando da promoção Indique Azure e convido vossas senhorias a aprenderem um pouco sobre o azure e ainda de quebra me ajudar na promoção.

Meu objetivo aqui e ajudá-los a criar uma conta conhecer um pouco do portal Azure, sendo assim, vamos simplesmente cadastrar uma foto.

Então vamos lá!

O primeiro passo é possuir os "Pré-Requisitos" para utilizarmos o Azure. São eles:

<ul>
<li><a href="http://www.microsoft.com/downloads/en/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en" target="_blank">Microsoft .NET Framework 4.0</a></li>
<li><a href="http://www.microsoft.com/visualstudio/en-us/products/2010-editions" target="_blank">Visual Studio 2010</a></li>
<li><a href="http://www.iis.net/" target="_blank">Microsoft Internet Information Server 7</a></li>
</ul>

Após o ambiente devidamente instalado, vamos criar uma conta no portal do Windows Azure.<br />
Não é preciso pânico! Enquanto estiver cadastrando sua conta, será necessário informar um cartão de crédito, porém, estes dados só seram acessados caso você exceda os 500MB de Storage que você tem direito. Não se preocupe, pois se você atingir o limite da conta, receberá um aviso e poderá suspender o serviço a qualquer momento.<br />
Os passos para a criação da conta estão em : <a href="http://www.slideshare.net/indiqueazure/como-assinar-windows-azure">http://www.slideshare.net/indiqueazure/como-assinar-windows-azure</a>.

Agora iremos publicar uma foto (somente extensão JPG), no Storage Azure. O processo é muito simples. Crie um projeto do tipo Windows Forms Application e acrescente os campos conforme a figura abaixo.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2010/12/f1.png"><img src="http://blob.vitormeriat.com.br/images/2010/12/f1.png" alt="f1" /></a></p>
<p>Não vou me ater na construção da interface pois o código e o instalador da solução estão disponíveis para download conforme os links abaixo.</p>
<ul>
<li><a href="http://winazureblobuploader.codeplex.com/releases/view/54012" target="_blank">Baixe o código fonte da aplicação</a></li>
<li><a href="http://www.sharpcode.com.br/downloads/SetupBlobUp.zip" target="_blank">Baixe o Programa SetupBlobUp para fazer o Upload do arquivo</a></li>
</ul>
<p>No próximo artigo iremos analizar o código e como obter os dados necessários para a publicação de arquivos no portal Azure.</p>
