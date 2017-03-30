---
layout: post
title: 'Dicas Azure: Cuidado com o deploying travado. Deployment at Busy or Initializing Status for long time'
date: 2012-02-28
categories:
    - Cloud Computing
    - Microsoft Azure
image: "http://blob.vitormeriat.com.br/images/2012/02/01.png"
---
<p align="justify">O pessoal que está trabalhando ou estudando o <strong>Azure</strong>, provavelmente já esbarrou com este problema. Fazer um deploy da aplicação na nuvem e o mesmo ficar “eras” em estado de “<strong>Busy</strong>” ou “<strong>Initializing</strong>”, exatamente como na imagem abaixo:</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2012/02/01.png"><img alt="01" src="http://blob.vitormeriat.com.br/images/2012/02/01.png"/></a></p>
<p align="justify">Neste caso específico (e que havia ocorrido anteriormente comigo), meu arquivo <strong>ServiceConfiguration.cscfg</strong> que tem a diretiva <strong>DiagnosticsConnectionString</strong> estava apontando para o desenvolvimento local. Este é o comportamento esperado, o seu estado default.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/02/021.png"><img alt="02" src="http://blob.vitormeriat.com.br/images/2012/02/02.png"/></a></p>
<p align="justify">&#160;</p>
<h2 align="justify">O problema</h2>
<p align="justify">Quando tentamos fazer um deploy da aplicação neste estado, estamos exigindo que o pacote inicialize a aplicação executando nosso <strong>Diagnostics</strong> para se conectar ao armazenamento local, o que não existe na nuvem. Como não é possível iniciar, o deploy se perde e fica preso em <strong>Busy / Initializing</strong>…</p>
<p align="justify">&#160;</p>
<h2 align="justify">A solução</h2>
<p align="justify">Para evitar que isto ocorra, basta apenas adicionar a conta e senha de seu subscription no Azure, tal qual você faria para acessar seu storage na nuvem.</p>
<p align="justify">&#160;</p>
<h2 align="justify">A dica</h2>
<p align="justify">Por mais simples que possa parecer, erros como este consomem muito tempo. Por vezes ficamos esperando com cara de tacho por um deploy que insiste em travar, e geralmente o erro é nosso. Publicar na nuvem deve ser uma tarefa realizada com atenção e planejamento, até porque estamos falando de uma plataforma onde se paga o que se “usa”.</p>
<p align="justify">Antes de publicar se projeto, verifique se seus arquivos de configuração(ServiceConfiguration) e definição(ServiceDefinition) estão corretos. Se suas strings de conexão estão apontando para o lugar correto. São detalhes que podem te salvar de uma boa dor de cabeça…</p>
<p align="justify">&#160;</p>
<h4><font>Um ótimo estudo a todos.</font></h4>