---
layout: post
title: Services now–Criando e testando um WCF Service Web Role On-Premise
date: 2014-11-23
categories:
  - Microsoft Azure
  - Services
  - WCF
image: "http://blob.vitormeriat.com.br/images/2014/11/capawcf.png"
---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/capawcf.png"><img alt="capaWCF" src="http://blob.vitormeriat.com.br/images/2014/11/capawcf.png" /></a></p>
<p align="justify">O <strong>WCF Service Role</strong> nos permite criar um serviço <strong>WFC </strong>hospedado em um <strong>Cloud Service</strong> no <strong>Microsoft Azure</strong>. Neste post vamos criar e testar um WCF Service Web Role local e na nuvem.</p>
<p><!--more-->
<p align="justify">Com o WCF (<em><strong>Windows Communication Foundation</strong></em>), a Microsoft unificou as várias tecnologias de programação distribuídas em um único modelo baseado na arquitetura orientada à serviços (SOA). Não vou falar especificamente sobre o WCF neste post, porém vou abordar especificamente sobre isso em breve.</p>
<p align="justify">Agora vamos criar o nosso projeto: Inicie o <strong>Visual Studio</strong> e selecione a opção <strong>New Project</strong>. Em <strong>Templates</strong> selecione <strong>Cloud</strong> e crie um <strong>Windows Azure Cloud Service</strong>. No meu exemplo estou chamando de <strong>WindowsAzureWCF</strong>. Vale notar que o ambiente utilizado neste post foi o <strong>Visual Studio 2013</strong> e o<strong> Windows Azure SDK 2.5</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg01.png"><img alt="ATG01" src="http://blob.vitormeriat.com.br/images/2014/11/atg01.png" /></a></p>
<p>&nbsp;</p>
<p align="justify">Na próxima tela selecionamos a <strong>WCF Service Web Role</strong>. Neste exemplo estou alterando o nome para <strong>WCFService.Bissexto</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg02.png"><img alt="ATG02" src="http://blob.vitormeriat.com.br/images/2014/11/atg02.png" /></a></p>
<p>&nbsp;</p>
<p>Você vai perceber que ele cria uma estrutura idêntica a um serviço WCF padrão:</p>
<ol>
<ol>
<li><strong>IService1.cs </strong>(Contrato do Serviço)  </li>
<li><strong>Service1.svc.cs</strong> (Definição do Serviço)  </li>
<li><strong>Web.config </strong>(Configuração dos EndPoints) </li>
</ol>
</ol>
<p align="justify">Agora vamos alterar nosso contrato e o nosso serviço para o retorno esperado. Só para não perder a oportunidade, vamos adicionar ao método padrão <strong>GetData</strong>, uma lógica para verificar se o ano é <strong>bissexto </strong>ou não. Para isso, devemos saber que os anos são bissextos quando forem divisíveis por 4, excluindo os que sejam divisíveis por 100, porém não os que sejam divisíveis por 400. Isso porque os anos divisíveis por 4 são bissextos, porém a cada 400 anos devemos eliminar 3 anos bissextos.</p>
<p align="justify">No arquivo de definição do serviço, <strong>Service1.svc.cs,</strong> você pode deletar o outro método padrão e incluir a lógica da verificação do ano bissexto, deixando o código como o descrito abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg03.png"><img alt="ATG03" src="http://blob.vitormeriat.com.br/images/2014/11/atg03.png" /></a></p>
<p>&nbsp;</p>
<p>Altere também o contrato conforme o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg04.png"><img title="ATG04" alt="ATG04" src="http://blob.vitormeriat.com.br/images/2014/11/atg04.png" /></a></p>
<p align="justify">Não iremos alterar o nosso <strong>Web.config </strong>. Verifique se o Visual Studio está rodando com permissão de <strong>Administrator</strong>, que o projeto <strong>WindowsAzureWCF</strong> esteja setado como <strong>StartUp Project</strong> e o <strong>Windows Azure Compute Emulator</strong> esteja rodando. Depois é só inicar a aplicação normalmente.</p>
<p align="justify">Se você observar o <strong>Computer Emulator</strong> (que emula o mesmo ambiente encontrado na nuvem), vai ver que o nosso serviço WCF está executando normalmente:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/11/atg06.png"><img alt="ATG06" src="http://blob.vitormeriat.com.br/images/2014/11/atg06.png"  /></a></p>
<p>Note que a seguinte tela é apresentada:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg08.png"><img alt="ATG08" src="http://blob.vitormeriat.com.br/images/2014/11/atg08.png" /></a></p>
<p align="justify">Navegue para a o serviço. Sua URL deve ficar <a href="http://127.0.0.1:4318/Service1.svc">http://127.0.0.1:4318/Service1.svc</a>. Se tudo estiver correto você vai ver esta página:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg09.png"><img alt="ATG09" src="http://blob.vitormeriat.com.br/images/2014/11/atg09.png" /></a></p>
<p align="justify">Pronto, neste ponto você já tem o serviço funcional e rodando no ambiente local. O próximo passo será a criação do cliente para consumir nosso serviço. Sendo assim, clique com o botão direito na solução e adicione um novo projeto do tipo <strong>Console Application</strong>.</p>
<p align="justify">Neste exemplo eu criei um projeto chamado <strong>TesteWCFAzure</strong>. No projeto, clique com o botão direito sobre <strong>References</strong> e selecione a opção <strong>Add Service Reference</strong>. Neste ponto você tem duas opções, <strong>Discover</strong> para que seja buscado um serviço na solução, ou <strong>Go</strong> caso você já saiba exatamente qual o serviço a ser consumido. Neste exemplo, informe o <u>endereço do serviço rodando localmente. </u>Note que são exibidas os métodos que estão expostos no contrato, neste caso apenas o <strong>GetData</strong>. Para seguir este exemplo apenas clique na opção <strong>Go</strong>. Não é necessário alterar mais nada.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg010.png"><img alt="ATG010" src="http://blob.vitormeriat.com.br/images/2014/11/atg010.png" /></a></p>
<p align="justify">Agora com as seguintes referências, só precisamos codificar nosso cliente criando nossa proxy de chamada ao serviço. Insira o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg011.png"><img alt="ATG011" src="http://blob.vitormeriat.com.br/images/2014/11/atg011.png" /></a></p>
<p align="justify">Agora é só clicar com o botão direito no projeto, <strong>Debug</strong> e <strong>Start new instance</strong>. O resultado será a resposta das duas chamadas realizadas no código acima. A resposta será como se segue abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/11/atg012.png"><img alt="ATG012" src="http://blob.vitormeriat.com.br/images/2014/11/atg012.png" /></a></p>
<p align="justify">Pronto, já temos o nosso serviço <strong>WCF</strong> criado e testado. No próximo post vamos publicar e consumir nosso serviço na nuvem.</p>
<p align="justify">O código fonte completo vai estar disponível no próximo post: <strong><u>Criando e testando um WCF Service Web Role em um Cloud Service</u></strong>.</p>
<p>&nbsp;</p>
<h4><font color="#9bbb59">Bons estudos e até a próxima pessoal&nbsp; ;)</font></h4>
