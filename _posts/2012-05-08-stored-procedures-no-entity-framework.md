---
layout: post
title: Stored Procedures no Entity Framework
date: 2012-05-08 
categories:
- C#
- ORM

---
<p align="justify">Aqui vai um post sobre o uso de stored procedures no Entity Framework. Não vou entrar no mérito da importância de SPs ou se ORMs como o EF eliminam esta necessidade. Vou apenas me ater as funcionalidades e motivos de algumas estranhezas ao se falar em SPs no Entity Framework.</p>
<p><!--more--><br />
<h2 align="justify">&#160;</h2>
<h2 align="justify">Introdução</h2>
<p align="justify">Para este fim criei uma aplicação <strong>MVC Razor</strong> com um Banco e duas tabelas, Cliente e Compra. Como na imagem abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/01.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="01"   alt="01" src="http://blob.vitormeriat.com.br/images/01.png" width="374" height="489" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Agora vamos mapear o banco a ser trabalhado inserindo na pasta <strong>Models</strong> o modelo de dados. Clique com o botão direito e&#160; selecione as opções <strong>Add &gt; NewItem &gt; ADO.NET Entity Data Model &gt; Add.</strong> O próximo passo e apontar para o banco a ser mapeado, com já disse anteriormente, neste exemplo estaremos trabalhando com um banco local na aplicação. Após isto será apresentado a tela onde você vai selecionar os recursos do banco que serão mapeados:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/02.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="02"   alt="02" src="http://blob.vitormeriat.com.br/images/02.png" width="560" height="585" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Observe que estou selecionando duas <strong>SPs</strong>. Com este passo completo iremos obter o arquivo <strong>edmx</strong> e uma janela exibindo o modelo será aberta:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/03.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="03"   alt="03" src="http://blob.vitormeriat.com.br/images/03.png" width="431" height="272" /></a></p>
<p align="justify">&#160;</p>
<h2 align="justify">Analise do problema</h2>
<p align="justify">Primeiro vamos observar o painel <strong>Model Browser</strong>:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/04.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="04"   alt="04" src="http://blob.vitormeriat.com.br/images/04.png" width="442" height="452" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">É possível notar que nosso modelo <strong>edmx </strong>possuí dois nós de navegação. No segundo nó temos uma pasta chamada <strong>Stored Procedures </strong>e dentro deste diretório temos as duas procedures que selecionamos no momento da criação do modelo.</p>
<p align="justify">Neste ponto você “acha” que já é possível consumir as procedures mas não é o caso. Para que seja possível consumir estes procedimentos, é necessário associarmos nossas <strong>SPs</strong> como funções do modelo.</p>
<p align="justify">Por padrão, o <strong>Entity Framework </strong>realiza operações diretamente nas tabelas do banco de dados. Isso ocorre devido ao mapeamento entre os esquemas conceituais e de armazenamento. Para utilizarmos <strong>SPs </strong>devemos então alterar os esquemas de mapeamento.</p>
<p align="justify">Podemos fazer isso de duas maneiras: Criando uma função de importação no modelo conceitual que irá mapear a <strong>stored procedure</strong> ou mapear na mão… vamos ver apenas a primeira opção (pelo menos por agora).</p>
<p align="justify">&#160;</p>
<h2 align="justify">A solução</h2>
<p align="justify">Observe na figura acima que no primeiro nó do modelo conceitual temos uma pasta chamada <strong>Functions Imports </strong>e ela está vazia. Pois bem, é aqui que a magia vai acontecer.</p>
<p align="justify">O que iremos fazer agora é criar uma função para mapear a <strong>SP</strong> desejada.</p>
<p align="justify">Quando criamos uma função o <strong>EF</strong> cria um método correspondente dentro do <strong>ObjectContext</strong> mapeando a <strong>SP</strong> desejada. Neste momento estamos vinculando a execução deste procedimento ao nosso modelo conceitual. Neste momento também é possível definir o tipo de retorno. </p>
<p align="justify">Clique com o o botão direito em Function Imports &gt; Add Function Import… Na janela seguinte você pode definir o nome da função, a SP a ser mapeada e o tipo de retorno, exatamente como a imagem abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/10.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="10"   alt="10" src="http://blob.vitormeriat.com.br/images/10.png" width="543" height="610" /></a></p>
<p align="justify">Sobre os tipos de retorno:</p>
<ul>
<li>
<div align="justify"><font color="#555555"><strong>None</strong>: Nenhum tipo de retorno;</font></div>
</li>
<li>
<div align="justify"><font color="#555555"><strong>Scalars</strong>: Retorna tipos específicos como Int32, Boolean, Binary etc;</font></div>
</li>
<li>
<div align="justify"><font color="#555555"><strong>Complex</strong>: Retorna um tipo coplexo. Este tipo possui propriedades correspondentes as colunas retornadas pela storede procedure. Este tipo é gerado automaticamente ao clicar no botão <strong>Create New Complex Type</strong>;</font></div>
</li>
<li>
<div align="justify"><font color="#555555"><strong>Entities</strong>: Retorna em uma entidade padrão do modelo.</font></div>
</li>
</ul>
<p align="justify">&#160;</p>
<p align="justify">Neste momento vou demonstrar a importação de uma SP que retorna um tipo <strong>Complex</strong>. O arquivo com o exemplo está disponível no fim do POST. A <strong>SP</strong> a ser importada é <strong>proc_ListarComprasDetalhadas</strong>. Vamos dar uma olhada em sua sintaxe:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/11.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="11"   alt="11" src="http://blob.vitormeriat.com.br/images/11.png" width="560" height="273" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Como podemos notar estou fazendo um <strong>INNER JOIN </strong>e retornando dados das duas tabelas. Ao importar a <strong>SP</strong> utilizo um retono do tipo <strong>Complex</strong> e o próprio <strong>EF</strong> cria um tipo correspondente.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/05.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="05"   alt="05" src="http://blob.vitormeriat.com.br/images/05.png" width="536" height="663" /></a></p>
<p align="justify">&#160;</p>
<p align="justify">Agora ao vamos importar a <strong>proc_BuscarComprasDoCliente</strong>. Esta retorna um tipo já mapeado pelo modelo conceitual, neste caso a entidade Compra. Sendo assim posso simplesmente apontar o tipo de retorno como <strong>Entities</strong> e selecionar a entidade correspondente. Vamos analisar a sintaxe da <strong>SP</strong> e a tela de importação correspondente:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/12.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="12"   alt="12" src="http://blob.vitormeriat.com.br/images/12.png" width="560" height="178" /></a></p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/05/06.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="06"   alt="06" src="http://blob.vitormeriat.com.br/images/06.png" width="557" height="659" /></a></p>
<p>&#160;</p>
<p align="justify">Se observamos o painel <strong>Model Browser</strong> vamos perceber que nossas procedures foram mapeadas e que um novo tipo foi criado na pasta <strong>Complex Types</strong> como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/05/07.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;border-top:0;margin-right:auto;border-right:0;padding-top:0;" title="07"   alt="07" src="http://blob.vitormeriat.com.br/images/07.png" width="329" height="509" /></a></p>
<p>&#160;</p>
<p align="justify">Deste momento em diante é possível consumir a função e trabalhar com o novo tipo de maneira simples:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2012/05/09.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;border-top:0;margin-right:auto;border-right:0;padding-top:0;" title="09"   alt="09" src="http://blob.vitormeriat.com.br/images/09.png" width="552" height="542" /></a></p>
<p>&#160;</p>
<p><a href="https://skydrive.live.com/?cid=bd055aa47a388023#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21365" target="_blank"><font size="3">Baixe aqui o exemplo utilizado neste POST!</font></a></p>