---
layout: post
title: IIS Express. Para um desnvolvimento web mais prático!
date: 2010-07-07
categories:
    - IIS
---

Os usuários do ASP.NET desde sua versão 1.1, já tem bastante contato com o servidor Web disponibilizado pela Microsoft chamado Cassini.

> Ele nasceu da necessidade de tornar o desnvolvimento web mais prático e acessível.

O Cassini Web server é um servidor Web simples que hospeda o ASP.NET criado utilizando System.Net.Sockets.

Quais são algumas limitações de funcionalidade conhecidos do Cassini Web server?
* Ele pode hospedar apenas uma aplicação do ASP.NET por porta.
* Não suporta HTTPS.
* Não suporta a autenticação.
* Responde apenas a solicitações localhost.  

Com isso, a Microsoft prepara o lançamento da versão de testes do seu novo servidor Web. Conhecido como IIS Express. 
<p><a href="http://blob.vitormeriat.com.br/images/2010/07/image_thumb_417a15b25b25d.png"><img alt="image_thumb_417A15B2" src="http://blob.vitormeriat.com.br/images/2010/07/image_thumb_417a15b25b25d.png" /></a></p>

De acordo com Scott Guthrie, da Microsoft, o IIS Express “combina o uso do Microsoft ASP.Net Web Server com todo poder do IIS”, que é integrado ao Windows.

Guthrie disse que a primeira versão de testes pública do IIS Express será lançada em breve, mas não mencionou nenhuma data específica. E assim como outros produtos da linha Express, é muito provável que a versão final seja disponibilizada gratuitamente. 

Segundo ele, o IIS Express será pequeno (menos de 10MB) e terá uma instalação “super rápida”.

Além disso, o novo IIS não precisará de uma conta de administrador para executar/depurar aplicações a partir do Visual Studio. O IIS Express terá suporte para SSL, URL Rewrite e todos os outros módulos do IIS 7.x.

O IIS Express funcionará no Windows XP e todas as versões do Windows lançadas depois dele e também poderá ser usado com o Visual Studio 2008 e 2010.

O mesmo será facilmente utilizado com o Visual Studio 2010. Será possível usá-lo em vez de ASP.NET Web Server como o servidor padrão no ASP.NET Projetos.

O IIS Express torna ainda mais fácil de construir, executar e testar aplicações web. Ele funciona com todas as versões do ASP.NET e suporta todos os tipos de aplicações ASP.NET (incluindo, obviamente, ASP.NET Web Forms e aplicações ASP.NET MVC). 

O melhor de tudo - você não precisa alterar nenhum código para tirar proveito dele. Você será capaz de usá-lo, opcionalmente, com todos os seus projetos em curso hoje.

A Microsoft lançará uma atualização para o Visual Studio 2010 e Visual Web Developer 2010 Express nos próximos meses para permitir que os desenvolvedores lancem e usem o IIS Express ao invés do ASP.Net Developer Server integrado. Futuras versões do Visual Studio já virão com esta funcionalidade. 

A data de lançamento da versão final do IIS Express ainda não foi definida.
