---
layout: post
title: WCF Tips–Bounded Generics, Serialization e o Data Contract
date: 2015-01-18
categories:
  - Services
  - SOA
  - WCF
---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2015/01/contract_generic.jpg"><img title="contract_generic" style="border-top:0;border-right:0;background-image:none;border-bottom:0;float:left;padding-top:0;padding-left:0;margin:5px 30px 0 0;border-left:0;display:inline;padding-right:0;"   alt="contract_generic" src="http://blob.vitormeriat.com.br/images/2015/01/contract_generic.jpg" width="449" align="left" height="300" /></a>Essa é uma dica que eu acho importante compartilhar. Ultimamente por conta de uma necessidade acabei topando com algumas reclamações em relação ao uso de <strong>Generics</strong> em contatos de dados no <strong>WCF</strong>, o que me motivou a escrever este post abordando o uso e também o motivo desta implementação no <strong>Windows Communication Foundation</strong>.</p>
<p align="justify">É comum que um desenvolvedor<strong> .NET</strong> trabalhar com generics. Sendo assim, ao iniciar no WCF também será comum que ele mantenha a mesma mentalidade, criado novos tipos e métodos genéricos. O problema disso é que WCF <u><strong>não suporta a exposição de tipos genéricos</strong></u>!</p>
<p align="justify">A primeira informação crucial aqui é que <strong><u>isso não é culpa ou limitação do WCF</u> :D</strong></p>
<p><!--more-->
<p align="justify">O que leva então a este tipo de implementação no WCF? Como sabemos o WCF segue os padrões definidos no <strong>Web Services Specifications</strong>. Sendo assim, nossa limitação ocorre por conta do <strong><u>WSDL</u></strong> <strong>(Web Services Description Language)</strong>, um padrão definido pela <strong>W3C</strong> para especificar as atividades a serem realizadas pelo serviço, que em nosso caso é utilizado para expor os <strong>metadados</strong> do serviço aos consumidores. </p>
<p align="justify">Não existe nenhuma construção dentro do WSDL para definir um tipo genérico, o que faz sentido, já que este tipo de implementação diminui o acoplamento entre cliente e serviço. Generics são específicos do .NET e seu uso na exposição dos serviços viola a natureza Orientada a Serviços no qual o WCF se baseia.</p>
<p align="justify">O Windows Communication Foundation usa um mecanismo de serialização no contrato de dados para serializar ou desserializar dados, e isso funciona bem para todos os tipos primitivos de .NET Framework , como Int e String. Para tipos complexos você deve definir um contrato de dado para que o mesmo seja serializável. Você pode ter uma visão melhor sobre tipos com suporte neste link: <a href="http://msdn.microsoft.com/pt-br/library/ms731923(v=vs.110).aspx" target="_blank">Tipos com suporte pelo serializador do contrato de dados</a></p>
<p align="justify">Mesmo assim podemos trabalhar com objetos genéricos no WCF, chamados neste caso de <strong>Bounded Generics</strong>. Vamos ao exemplo ):</p>
<p><a href="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded01.png"><img title="wcfbounded01" alt="wcfbounded01" src="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded01.png" width="700" height="447" /></a></p>
<p align="justify">Basicamente, temos uma classe genérica para o <strong>Data Contract</strong> que fica restrito ao tipo que será utilizado na operação do serviço. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded02.png"><img title="wcfbounded02" alt="wcfbounded02" src="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded02.png" width="700" height="372" /></a></p>
<p align="justify">Note que o objeto que é exposto é o genérico <strong>ObjetoGenerico&lt;T&gt;</strong>, porém em nosso <strong>Operation Contract</strong> existe a restrição aos tipos <strong>int</strong> e <strong>string</strong>. Isso é o <strong>Bounded Generic</strong>, ou traduzindo <strong>Genérico Delimitado</strong>.</p>
<p align="justify">Eis aqui o motivo em dizer que não há suporte para o generics em relação a sua exposição no serviço. Mesmo realizando a implementação acima, o cliente não vai saber nada sobre isso. Como a <strong>"delimitação"</strong> aponta para um dos tipos base, os <strong>metadados</strong> gerados vão descrever a operação do serviço, contrato de dados e tudo mais como uma classe padrão.</p>
<p align="justify">Observe a implementação do serviço:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded03.png"><img title="wcfbounded03" alt="wcfbounded03" src="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded03.png" width="700" height="515" /></a></p>
<p>Agora vamos ao cliente. Observe o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded04.png"><img title="wcfbounded04" alt="wcfbounded04" src="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded04.png" width="700" height="519" /></a></p>
<p align="justify">Criei uma console application para consumir as operações expostas no serviço. A primeira coisa que quero chamar atenção é no tipo gerado para o <strong>ObjetoGenerico</strong>, no caso, as duas linhas com o traço amarelo em destaque. </p>
<p align="justify">Note que foi gerado um nome com o seguinte padrão: <strong>Generic Class Name</strong> + <strong>"Of"</strong> + <strong>Type Parameter Name</strong>, gerando os seguintes nomes:</p>
<ul>
<li><strong>ObjetoGenericoOfstring</strong>  </li>
<li><strong>ObjetoGenericoOfint</strong></li>
</ul>
<p align="justify">Observando as classes geradas podemos notar que os métodos são assinados com os tipos base <strong>String</strong> e <strong>Int</strong>, ou seja, não existe nada de diferente da perspectiva do cliente. Observe o retorno da execução de nosso serviço: </p>
<p><a href="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded05.png"><img title="wcfbounded05" alt="wcfbounded05" src="http://blob.vitormeriat.com.br/images/2015/01/wcfbounded05.png" width="700" height="313" /></a></p>
<p>&nbsp;</p>
<p align="justify">Voltando a minha afirmação de que o WCF <strong><u>não suporta a exposição de tipos genéricos.</u></strong> Você vai encontrar várias referências falando que é possível a exposição de genéricos porém com algumas limitações. Ao meu ponto de ver isso é errado. Como já citei esta é uma estrutura que não existe no WSDL, logo é um implementação local e particular do .NET que assume um comportamento padrão do lado do cliente. </p>
<p align="justify">Embora possamos usar generics na construção de nossos serviços, sua exposição será sempre a padrão, utilizando os tipos específicos.</p>
<p align="justify">&nbsp;</p>
<p><a href="http://1drv.ms/1xGdUV2" target="_blank">O CÓDIGO FONTE PODE SER BAIXADO AQUI!!!</a></p>
<p>&nbsp;</p>

<h1>Referências</h1>
<p><a href="http://www.w3schools.com/webservices/ws_wsdl_intro.asp" target="_blank">Introduction to WSDL</a></p>
<p><a href="http://msdn.microsoft.com/pt-br/library/dd456779%28v=vs.110%29.aspx" target="_blank">Windows Communication Foundation</a></p>
<p><a href="https://www.safaribooksonline.com/library/view/programming-wcf-services/0596526997/ch03s09.html" target="_blank">Programming WCF Services</a></p>
<p>&nbsp;</p>

<h2><font color="#666666">Bons estudos e até a próxima pessoal&nbsp; ;)</font></h2>