---
layout: post
title: C# 6.0 TIPS–Exception Filters
date: 2015-01-23
categories:
  - C#
---

<p align="justify">Esse é um post simples para explorar um ótimo recurso do <strong>C# 6.0</strong>: <strong>Exception Filters</strong>. Beleza, todo mundo que programa com C# já teve a necessidade trabalhar com o Exceptions. Meio que não há como fugir disso. Lógico que com tanto uso, alguma necessidades específicas aparecem, e para poder tratar melhor nossas exceção acabamos por utilizar estruturas condicionais, o que muitas vezes torna o código mais inteligível.</p>
<p align="justify">Com o <strong>Exception Filter</strong>, é possível aplicar um filtro direto na exceção. É claro que antes você já podia "tratar" isso dentro do bloco <strong>try/catch</strong>, porém teria de se executar o catch e em seguida filtrar a condição. Com este novo recurso podemos realizar a condição e aplicar o tratamento específico. Observe o código abaixo:</p>
<pre><code class="cs">
static void Main(string[] args)
{
    int numero = 12;

    try
    {
  
int resultado = numero % 0;
    Console.WriteLine(resultado);
    }
    catch (DivideByZeroException ex) when (ex.Source.Equals("Nome Errado"))
    {
  
Console.WriteLine("Condição falsa!!!");
    }
    catch (DivideByZeroException ex) when (ex.Message.Equals("Attempted to divide by zero."))
    {
   
Console.WriteLine("Condição verdadeiranMensagem: " + ex.Message);
    }

    Console.ReadKey(true);
}
</code></pre>
<p>Agora, um bloco o catch só será executado quando o filtro for verdadeiro.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2015/01/image.png"><img title="IMAGE" alt="IMAGE" src="http://blob.vitormeriat.com.br/images/2015/01/image.png" width="100%" /></a></p>
<p>O código fonte pode ser baixado aqui!!!</p>
<h2>Até a próxima e bons estudos pessoal :)</h2>
