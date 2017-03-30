---
layout: post
title: 'Windows Azure Internals: Trabalhando com Storage Service e API REST (parte 1)'
date: 2012-03-21
categories:
- Cloud Computing
- Microsoft Azure
image: "http://blob.vitormeriat.com.br/images/2012/03/imagem1.png"
---

<p align="justify">Neste artigo, estarei abordando um pouco das entranhas do <strong>serviço de armazenamento do Windows Azure</strong> (<strong>Blob, Tables e Queues</strong>). Com exceção do <strong>SQL Azure</strong>, que transfere dados usando o protocolo <strong>TDS</strong> em uma conexão <strong>SSL</strong> (não oferecendo suporte a conexões não criptografadas), todos os serviços de armazenamento são expostos através de uma API HTTP <strong>RESTful</strong>. Sendo assim, vamos <strong>codificar</strong> nossa API RESTful para aprendizado. O código completo estará disponível na parte final do artigo.</p>
<blockquote><p align="justify">“Chama-se <strong>RESTful</strong> os sistemas e APIs que seguem os princípios REST”.</p>
</blockquote>
<p align="justify">Entender o funcionamento destes “protocolos” vai nos possibilitar uma maior interação com os serviços de armazenamento, mais agilidade na identificação / correção de erros e um maior poder de fogo na criação de estratégias para consumo e desempenho de nossa aplicação. </p>
<p align="justify">Existe várias vantagens na utilização deste modelo, pretendo discorrer sobre isto de forma a entendermos quais os benefícios e possibilidades que podemos explorar. Minha intenção com este artigo não é dissecar o <strong>REST</strong>, vamos apenas arranhar sua superfície.</p>
<br />

<h2>Por que RESTful</h2>
<p align="justify">Me lembro que no início de meus estudos com Azure, me perguntei sobre os motivos que levaram o time de Azure a adotar o RESTful. A medida que vamos compreendendo os modelos de programação na nuvem, bem como as vantagens menos obvias desta implementação, tudo vai ficando mais claro.</p>
<p align="justify">Vou iniciar minha argumentação relembrando um ponto chave do pensamento sobre cloud computing e seus serviços: “Acredita-se que no futuro, ninguém precisará instalar nenhum tipo de software em seu computador, seja para editar textos, assistir vídeos, ou até mesmo editar imagens, tudo estará disponível na nuvem”. Utilizando-se da internet como meio de consumo, o modelo <a href="http://www.google.com.br/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=5&amp;cts=1331140650889&amp;ved=0CFAQFjAE&amp;url=http%3A%2F%2Fvitormeriat.wordpress.com%2F2011%2F07%2F08%2Fmodelos-de-servio-na-nuvem-iaas-paas-e-saas%2F&amp;ei=AZhXT7bZBoXhggemvsTrDA&amp;usg=AFQjCNHkwyO-GYLg9-wuatzzVd8KdKFpbQ" target="_blank">SaaS</a>objetiva disponibilizar os mesmos recursos de software para um número ilimitado de clientes. A palavra chave aqui é disponibilizar. </p>
<p align="justify">Tornar os serviços do Azure altamente disponíveis foi uma grande jogada. Você pode continuar utilizando seu site em PHP consumindo apenas dados do Blob Storage ou utilizar o serviço de Filas sem ter que codificar sua aplicação em Windows Azure. Este é o modelo comum adotado para computação na nuvem, como por exemplo o caso do Twitter que executa o código em sua própria infra-estrutura mas utiliza o Amazon Simple Storage Service da Amazon (Amazon S3) para armazenar as imagens dos perfis.</p>
<p align="justify">Outra vantagem bem aparente de se utilizar API RESTful é a facilidade em criar uma biblioteca para acesso em outras linguagens. Hoje é fácil encontrar clientes Azure para Python, Ruby, Erlang, PHP entre outros. </p>
<p align="justify">&#160;</p>
<h2 align="justify">Recursos na API RESTful</h2>
<p align="justify">Quando estamos navegando na internet, o que ocorre são séries de requisições e respostas HTTP. No momento em que clicamos em um link qualquer, realizamos um pedido ao navegador web para que nos envia a página solicitada realizando um GET junto a URL. Em caso de existência, o servidor devolve um código HTTP de resposta (200), seguido pelo conteúdo da página. Caso não exista, o servidor devolve um código HTTP para página não encontrada (404). Como na imagem abaixo:</p>
<<<<<<< HEAD
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/03/imagem1.png"><img alt="Imagem1" src="http://blob.vitormeriat.com.br/images/2012/03/imagem1.png"/></a></p>
=======
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/03/imagem1.png"><img alt="Imagem1" src="http://blob.vitormeriat.com.br/images/2012/03/imagem1.png" /></a></p>
>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77
<p align="justify">Podemos notar que o navegador&#160; solicita um recurso (neste caso uma página) que é identificado por sua URL. Logo após isso, é solicitado ao servidor que execute um método GET sobre o recurso. Esta é a natureza do REST e o motivo pelo qual é relativamente fácil de codificar em uma grande gama de linguagens. Se há suporte para HTTP, então é possível criar uma API RESTful para acessar recursos por meio de HTTP (Embora seja certamente possível usar alguns ou todos os princípios de REST em outros protocolos).</p>
<p align="justify">O modelo RESTful está basicamente voltado para interações com recursos. Um recurso é qualquer informação que você deseja disponibilizar, pode ser a lista de empregados de sua empresa, as fotos de passeio em família etc. É um mapeamento conceitual para uma determinada entidade ou conjunto de entidades que você quer “trafegar” para seu serviço. Observe a URI abaixo:</p>
<p><a title="http://vitormeriat.blob.core.windows.net/teste/Meriat.png" href="http://vitormeriat.blob.core.windows.net/teste/Meriat.png">http://vitormeriat.blob.core.windows.net/teste/Meriat.png</a></p>
<p align="justify">Ela aponta para uma imagem que está armazenada no Blob Storage do Azure. Para o navegador isto pouco importa, ele conversa HTTP com o Azure Blob Service que devolve os bytes solicitados como o esperado. O fato de ser o Azure Storage Service não é relevante uma vez que é uma requisição HTTP trabalhando exatamente como as URLs devem trabalhar. Vamos observar os esquema abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/03/arquitetura-storage-azure.png"><img alt="Arquitetura Storage Azure" src="http://blob.vitormeriat.com.br/images/2012/03/arquitetura-storage-azure.png" /></a></p>
<p align="justify">A API REST expõe os blobs, tables e queues como objetos HTTP padrão. Sendo assim, podemos utilizar para estes objetos (recursos em REST) os métodos padrão do HTTP como GET, POST, PUT e DELETE. </p>
<p align="justify">Todos os recursos do serviço de armazenamento do Azure se comportam da mesma maneira quando se trata de operações HTTP. Se você deseja obter um recurso qualquer, deve-se executar uma solicitação HTTP GET. Se a intenção for criar um objeto, você vai enviar uma requisição HTTP PUT. Da mesma forma, para se excluir um objeto você vai enviar uma requisição DELETE. A ressalva fica por conta do serviço de Tables que vai exigir mais elaboração para as consultas.</p>
<p>No próximo post vou abordar sobre a nomenclatura REST e os primeiros passos para a codificação da nossa API.</p>
<p>&#160;</p>
<<<<<<< HEAD
<h4><font color="#666666">Um ótimo estudo a todos….</font></h4>
=======
<h2><font color="#666666">Um ótimo estudo a todos….</font></h2>
>>>>>>> fc19c35aaf9d0aae2c5a94f9ddc93deb1b95af77