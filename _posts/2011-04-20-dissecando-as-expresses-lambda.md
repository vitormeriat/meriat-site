---
layout: post
title: Dissecando as expressões Lambda
date: 2011-04-20
categories:
  - C#
---
<p>Esta semana fui questionado sobre o que singificava aquele “<strong>treco</strong>” que todo mundo usa quando vai fazer uma consulta linq. São as expressões lambda, eu disse. Acabei percebendo que na turma ninguém sabia o que eram expressões lambda, apesar de todos as utilizarem.</p>
<p>O primeiro passo para entendermos as expressões lambda é desvendar sua origem. Nosso estudo deve, portanto, se iniciar pelos delegates...</p>
<p>O conceito de delegates não é algo tão novo. O pessoal mais nostalgico vai se animar com este assunto. Este conceito já era utilizado no na linguagem <strong>C</strong> e era intitulado "<strong>ponteiro para função</strong>". Terminologia que deixa mais claro o que um delegate realmente faz.</p>
<p>O delegate assim como o ponteiro para função, guarda uma referência a uma função(ou método) e permite que chamemos essa função quando precisarmos.</p>
<p>Em .Net estes "ponteiros" foram entitulados delegates e adicionou-se segurança de tipo a ele, sendo assim, para utilizar um delegate devemos especificar exatamente o tipo do resultado que o método apontado retorna, bem como os argumentos que o método espera receber.</p>
<p>Após satisfazer estas condições podemos "passar" o delegate como se fosse uma variável.</p>
<p>Nosso primeiro exemplo mostra o uso de delegate assim como era utilizado no .NET 1.0! Definimos um delegate e o tipo de argumento para o mesmo. Criamos o delegate e apontamos para o método de referência. Agora podemos<br />utilizar nosso delegate pelo código...</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/04/lambda1.png"><img alt="Lambda1" src="http://blob.vitormeriat.com.br/images/2011/04/lambda1.png" /></a></p>
<p>Dando um salto até o lançamento do .NET 2.0, teremos uma nova feature que irá facilitar o uso dos delegates em relação a maneira como eram escritos anteriormente. Este novo recurso eram os "Métodos Anônimos".</p>
<p>Os métodos anônimos suprimem a necessidade de se criar outros métodos para apontá-los com delegates!!! É isso mesmo! Agora podemos definir o método a ser apontado no mesmo instante em que criamos o delegate e o compilador fica com a responsabilidade da interpretação. Na prática houve aqui um grande evolução na escrita do código.</p>
<p>Vamos observar o funcionamento de um delegate tradicional comparado a sua utilização com um método anônimo: </p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/04/2.png"><img alt="2" src="http://blob.vitormeriat.com.br/images/2011/04/2.png" /></a></p>
<p>Podemos ver claramente a diferença aqui. Com os métodos anônimos, não precisamos criar outro método e um delegate que aponta para esse método. Dizemos apenas que queremos um delegate aqui e especificamos o corpo do método a ser chamado. É muito mais conveniente utilizar um método anônimo ao invés do modo com delegate tradicional. A definição do código a utilizar fica junto a sua utilização, tornando tudo mais intelegível. </p>
<p>Outra característica introduzida com os métodos anônimos é a possibilidade de usar variáveis definidas fora do método anônimo: Utilizando o exemplo acima, podemos ter uma variável e a utilizar na condição do método anônimo.</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/04/3.png"><img alt="3" src="http://blob.vitormeriat.com.br/images/2011/04/3.png" /></a></p>
<p>Neste exemplo vemos o uso da variável "procuraValor" dentro corpo do método do delegate embora tenhamos o definido fora dele. Neste caso, o compilador C# não somente cria o método como a própria classe (que contém o método) onde o valor que usaremos no corpo do delegate é passado como um membro dessa classe.</p>
<h3>Expressões Lambda</h3>
<p>Lambda expressions são expressões anônimas e métodos anônimos com uma sintaxe açucarada(syntatic sugar ou açucar sintático refere-se a maior legibilidade do código bem como maior facilidade na escrita) que tornará mais agradavel e elegante a forma de embarcar métodos anônimos ao código.</p>
<p>Nos dias de hoje, no C#3.0 (e no .NET 3.5) temos as expressões Lambda que são o próximo passo na "evolução do delegate". Agora, o compilador faz sumir o "delegate(...) {...}" (isso economiza um monte de digitação). Uma expressão lambda sempre consiste de duas partes (esquerda e direita) separadas por um "<strong>=&gt;</strong>". Este(<strong>=&gt;</strong>) por sua vez é o operador lambda que foi introduzido no C# 3.0 e é lido como "goes to" (vai para). A parte à esquerda do operador labmda contém uma lista de argumentos(não necessariamente tipados pois os tipos&nbsp; podem ser automáticamente indicados pelo compilador) a serem passados ao método. O lado direito contém o corpo do método. </p>
<h4>Vamos a prática:</h4>
<p>Em um determinado cenário temos um conjunto de regras que são alteradas com frequência. Para um melhor desing decidimos isolar este trecho de código. Criamos então um delegate que retorna um double. Em nossa aplicação percorremos uma lista de valores e aplicamos para cada item nossa regra, que em suma aplica o valor 0.0 quando o resultado retornado for menor que 300.00.</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/04/4.png"><img alt="4" src="http://blob.vitormeriat.com.br/images/2011/04/4.png" /></a></p>
<p>Notem que a expressão Lambda utilizada no método AplicaRegras é iniciado por um argumento de tipo implícito (<strong>i</strong>) que <u>vai para</u> o resultado de um calculo que neste caso e 15% do <strong>item</strong> em questão.</p>
<p>Agora fica muito mais fácil entender nossas consultas linq…</p>
<pre style="font-size: 1.2em !important">
    <code class="cs">
// Crio um objeto de contexto
ContextoDeDados contexto = new ContextoDeDados();
// Consulto os desenvolvedores que trabalhama na empresa Literatura e Cia
var consulta = contexto.desenvolvedores.Where(c => c.Empresa == "Literatura e Cia");
    </code>
</pre>

<pre><a href="http://cid-bd055aa47a388023.office.live.com/self.aspx/.Public/ExpressoesLambda.rar">Baixe o código dos Exemplos utilizados neste artigo.</a></pre>
