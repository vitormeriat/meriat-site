---
layout: post
title: Como retornar um tipo anônimo por método
date: 2011-06-29
categories:
    - C#
---

Os tipos anônimos são muito uteis principalmente quando estamos trabalhando com LINQ. Podemos filtrar uma lista de campos para um resultado projetando um tipo personalizado. Usar um tipo anônimo pode ser muito mais rápido que criar um novo tipo.

No post <a href="http://vitormeriat.com.br/2011/06/09/tipos-annimos-so-realmente-teis/" target="_blank">Tipos anônimos são realmente úteis?</a>, falei sobre os tipos anônimos, suas limitações e como este recurso é útil. Um dos pontos abordados foi sobre as limitações dos tipos anônimos. Vou reproduzir o texto em questão:

> Os tipos anônimos apresentam limitações que devem ser conhecidas para que seu uso possa ser mais consciente. Quando se opta por usar tipos anônimos é necessário saber que eles não são símbolos C# válidos, sua validade fica a nível de CLR. Isto implica na impossibilidade de definir métodos de extensão, de declarar métodos com tipos anônimos como parâmetros e retornar tipos anônimos a partir de métodos.

Vamos analisar o código abaixo:

<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/06/tiposanonimos01.png"><img alt="tiposAnonimos01" src="http://blob.vitormeriat.com.br/images/2011/06/tiposanonimos01.png" /></a></p>


<p align="justify">Este código cria uma nova instância de um tipo anônimo. É possível notar que que o compilador C# é capaz de inferir os tipos como visto no <strong>Intellisense</strong>. Depois de ter declarado o tipo você pode usá-lo como se houvesse feito uma declaração de tipo normal. O compilador C# atribui o tipo adequado para cada propriedade. Esta atribuição não se limita a valores literais, pode ser uma expressão de valor ou tipos aninhados como no exemplo a seguir: </p>

<pre style="font-size: 16pt !important">
<code class="cs">
var Cliente = new
{
    Empresa = "Sr.Nimbus",
    Name = "Vitor Merat",
    Admissao = new DateTime(2011, 01, 01),
    Idade = 26,
    Contatos = new
    {
        Telefone = "61 3121-1211",
        Fax = "61 3231-1211",
        Email = "vitormeriat@srnimbus.com.br"
    }
};
</code>
</pre>

Dentro do escopo do método local, o compilador entende toda a semântica do tipo. Isto tudo é muito legal mas como já foi dito o tipo anônimo é desconhecido fora do método que o criou. Não há nada de tão especial sobre este tipo - é simplesmente uma instância de um tipo de referência. A única coisa diferente sobre esse tipo é que ele tem um nome que você não pode ver.

Esta é uma situação em que é necessário usar a palavra-chave var. Como não sabemos qual o nome do tipo, usamos a palavra-chave var, e deixamos com o compilador a missão de inferir o tipo.


Então se um tipo é anônimo, como podemos fazer para que um método possa retorná-lo?

<pre style="font-size: 16pt !important">
<code class="cs">
public ????? ListaDeClientes()
{
    var q1 = from c in contexto.Clientes
        where c.Cidade == "Brasília"
        select new { c.PrimeiroNome, c.UltimoNome, c.Cidade };
        
    return q1;
};
</code>
</pre>

Se você quiser retornar um objeto a partir de um método, você deve declarar o método para retornar um objeto deste tipo. Isto está bem claro na semântica do C#, para chegarmos ao fim desejado devemos tornar nosso tipo anônimo em um tipo nominal.

Não podemos retornar um <strong><font size="2">var</font></strong>, então para ser mais genérico o mais recomendado é utilizar um <strong><font size="2">object</font></strong> para o retorno. Se um um tipo anônimo é um tipo do .NET, então esse herda de <strong>System.Object</strong>, logo podemos retornar um object. Isto pode funcionar em alguns casos mais certamente você será surpreendido com impossibilidades nesta abordagem.

<pre style="font-size: 16pt !important">
<code class="cs">
public object ListaDeClientes()
{
    var q1 = from c in contexto.Clientes
        where c.Cidade == "Brasília"
        select new { c.PrimeiroNome, c.UltimoNome, c.Cidade };
        
    return q1;
};
</code>
</pre>

O raciocínio está correto, porém quando o tipo é transformado para object, perdemos a possibilidade de utilização das propriedades do tipo anônimo (<strong>strong typing</strong>).

> Strong Typing: É uma caracteristica das linguagens de programação, onde não é permitida a modificação do tipo de dados de uma variável durante a execução dos programas.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/06/tiposanonimos05.png"><img alt="tiposAnonimos05" src="http://blob.vitormeriat.com.br/images/2011/06/tiposanonimos05.png"/></a></p>

Este erro ocorre porque quando criamos um tipo anônimo, suas propriedades são <strong>READ ONLY</strong>. Isto significa que você pode criar o tipo anônimo, mas você não pode atribuir valores a ele após sua criação.

<p align="justify">Para resolver esse problema temos 3 estratégias possíveis:</p>
<ol>
<ol>
<li>
<div align="justify">Reflection; </div>
</li>
<li>
<div align="justify">Dynamic Programming; </div>
</li>
<li>
<div align="justify">Realizar um cast do object com o tipo anônimo.</div>
</li>
</ol>
</ol>

<p align="justify">Trabalhar com <strong>reflection</strong> é bastante pesaroso sem falar nas questões de desempenho, trabalhar com programação dinâmica é bem legal mais como ainda não postei sobre este tema vamos nos ater a terceira estratégia.</p>

<p align="justify">Vejamos o código abaixo:</p>

<p><a href="http://blob.vitormeriat.com.br/images/2011/06/tiposanonimos06.png"><img alt="tiposAnonimos06" src="http://blob.vitormeriat.com.br/images/2011/06/tiposanonimos06.png"/></a></p>

<script src="https://gist.github.com/vitormeriat/eb68005cc53f307068b3bf5b53b06cbd.js"></script>

Utilizando todo o poder dos <strong>Generics</strong>, conseguimos montar um método <strong>ConverteTiposPara</strong> que realiza o cas de um object para um tipo anônimo. Graças a “inferência de tipo” é possível fazer um cast sem conhecer o nome do tipo.

<p>&nbsp;</p>

Baixar o Código Fonte do Artigo <a href="https://skydrive.live.com/?wa=wsignin1.0&amp;cid=bd055aa47a388023&amp;sc=documents#cid=BD055AA47A388023&amp;id=BD055AA47A388023%21125" target="_blank">aqui!</a>

<p>&nbsp;</p>

<h3>Links de ajuda:</h3>
<p>Anonymous Types (C# Programming Guide)<strong>&nbsp;&nbsp; </strong><a href="http://bit.ly/69HYJd">http://bit.ly/69HYJd</a></p>
<p>&nbsp;</p>

### Um grande abraço e ótimo estudo!
