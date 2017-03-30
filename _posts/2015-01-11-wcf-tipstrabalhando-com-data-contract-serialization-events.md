---
layout: post
title: WCF TIPS–Trabalhando com Data Contract Serialization Events
date: 2015-01-11
categories:
  - Services
  - WCF
image: "http://blob.vitormeriat.com.br/images/2014/12/capa.png"
---
<p align="justify">Este post nasceu de uma necessidade durante uma implementação em <strong>WCF</strong> (<a href="http://msdn.microsoft.com/en-us/library/ms731082%28v=vs.110%29.aspx" target="_blank">Windows Communication Foundation</a>). Como já sabemos, em WCF temos de trabalhar com serialização de dados. O que pode ocorrer, é a necessidade algum tipo de tratamento antes ou após este processo. Para isso temos os <strong>Eventos de Serialização</strong>, que vou exemplificar aqui. </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/capa.png"><img title="CAPA" alt="CAPA" src="http://blob.vitormeriat.com.br/images/2014/12/capa.png" width="700" height="324" /></a></p>
<p align="justify">&nbsp;</p>
<p><!--more-->
<p align="justify">O <strong>.NET</strong> traz o suporte aos Eventos de Serialização que são utilizados pelo WCF quando trabalhamos com <strong>Data Contracts</strong>. Antes de ir para o “mão na massa”, vamos entender quais são os eventos envolvidos na serialização de dados do WCF, são eles:</p>
<ul>
<li>
<div align="justify">OnSerializing</div>
</li>
<li>
<div align="justify">OnSerialized</div>
</li>
<li>
<div align="justify">OnDeserializing</div>
</li>
<li>
<div align="justify">OnDeserialized</div>
</li>
</ul>
<p align="justify">Para realizar esta tarefa é necessário criar métodos para manipular os eventos por meio do uso de <strong>method attributes</strong>. Exatamente como no exemplo abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/cod01.png"><img title="COD01" alt="COD01" src="http://blob.vitormeriat.com.br/images/2014/12/cod01.png" width="700" height="522" /></a></p>
<p align="justify">O método pode ter qualquer nome, porém deve ser <strong>void</strong> e ter como parâmetro a <strong>struct</strong> <strong>StreamingContext</strong>. Outro ponto importante é que os métodos devem pertencer a uma classe decorada com o atributo <strong>DataContract</strong>.</p>
<p>Quando aos eventos, podemos dividi-los&nbsp; em dois blocos:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img01.png"><img title="IMG01" alt="IMG01" src="http://blob.vitormeriat.com.br/images/2014/12/img01.png" width="700" height="195" /></a></p>
<p align="justify">Onde temos o <strong>OnSerializing</strong> que ocorre antes da serialização, e o <strong>OnSerialized</strong> que ocorre ao final do processo de serialização. Para mais detalhes consultes os links na área de referência ao final do post.</p>
<p><!--EndFragment-->
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img02.png"><img title="IMG02" alt="IMG02" src="http://blob.vitormeriat.com.br/images/2014/12/img02.png" width="700" height="186" /></a></p>
<p align="justify">O segundo bloco segue a mesma mecânica, só que agora no sentido inverso, a deserialização. Temos o <strong>OnDeserializing</strong> que ocorre&nbsp; antes da deserialização, e o <strong>OnDeserialized</strong> que ocorre no fim da deserialização.</p>
<p>&nbsp;</p>
<h2>Vamos a Demo</h2>
<p align="justify">Crie uma aplicação do tipo <strong>WCF Service Libary</strong>. Vamos utiliza o próprio serviço criado, fazendo apenas algumas customizações.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img03.png"><img title="IMG03" alt="IMG03" src="http://blob.vitormeriat.com.br/images/2014/12/img03.png" width="700" height="444" /></a></p>
<p>Acesse a interface <strong>IService1</strong> e deixe apenas a propriedade <strong>StringValue</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/cod02.png"><img title="COD02" alt="COD02" src="http://blob.vitormeriat.com.br/images/2014/12/cod02.png" width="700" height="286" /></a></p>
<p align="justify">Na classe <strong>Service1</strong> realiza a alteração abaixo, na implementação do método <strong>GetDataUsingDataContract</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/cod03.png"><img title="COD03" alt="COD03" src="http://blob.vitormeriat.com.br/images/2014/12/cod03.png" width="700" height="202" /></a></p>
<p align="justify">Agora vamos fazer criar um cliente para consumir e testar o serviço. Crie um novo projeto na mesma solução do tipo <strong>Console Application</strong> e adicione a referência ao serviço. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/cod04.png"><img title="COD04" alt="COD04" src="http://blob.vitormeriat.com.br/images/2014/12/cod04.png" width="700" height="601" /></a></p>
<p align="justify">Clique com o botão direito sobre o projeto cliente e no menu <strong>Debug</strong> clique em <strong>Start new instance, </strong>e observe o resultado.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img04.png"><img title="IMG04" alt="IMG04" src="http://blob.vitormeriat.com.br/images/2014/12/mg04.png" width="700" height="216" /></a></p>
<p align="justify">Vamos analisar o que ocorreu. Na primeira chamada estamos criando o objeto e informando um valor. Na segunda chamada estamos criando outro objeto porém sem informar nenhum valor para a propriedade <strong>StringValue</strong>. Logo, teremos o valor informado exibido na primeira chamada, e um retorno vazio na segunda chamada.</p>
<p align="justify">Agora vamos fazer um tratamento para o momento em que o dado é deserializado. Para isso vamos incluir o seguinte código na classe <strong>CompositeType.</strong></p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/cod05.png"><img title="COD05" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="COD05" src="http://blob.vitormeriat.com.br/images/2014/12/cod05.png" width="700" height="781" /></a></p>
<p align="justify">Agora, considere um cenário de tempo real em que o usuário não informou um determinado valor, neste caso vamos precisar tratar isso em algum momento.</p>
<p align="justify">Em nosso caso o tratamento está sendo realizado no para o evento <strong>OnDeserialized</strong>, logo no fim da deserilização haverá o tratamento específico. </p>
<p align="justify">Rode novamente a aplicação. Para comprovar o que estou falando você pode simplesmente colocar um breakpoint em cada um dos métodos para testar a sequência em que os eventos são executados.</p>
<p align="justify">Agora, na segunda chamada, quando o manipulador apontar para o fim da deserialização, como não informamos um valor para a propriedade <strong>StringValue</strong>, nosso tratamento irá setar o valor de não informado, exatamente como o mostrado na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img05.png"><img title="IMG05" alt="IMG05" src="http://blob.vitormeriat.com.br/images/2014/12/img05.png" width="700" height="235" /></a></p>
<p>Essa é apenas uma dica de algo que para mim foi muito útil.</p>
<p>&nbsp;</p>
<h1>Referências &amp; Código fonte</h1>
<p><a href="http://msdn.microsoft.com/en-us/library/ms731073%28v=vs.110%29.aspx" target="_blank">Serialization and Deserialization</a></p>
<p><a href="http://www.amazon.com/Programming-WCF-Services-Mastering-AppFabric/dp/0596805489" target="_blank">Programming WCF Services, 3rd Edition</a></p>
<p><a href="http://1drv.ms/1zBYkia" target="_blank">Baixe o código fonte aqui!!!</a></p>