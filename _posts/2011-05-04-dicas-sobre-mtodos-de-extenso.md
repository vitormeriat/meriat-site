---
layout: post
title: Dicas sobre Métodos de Extensão
date: 2011-05-04
categories:
    - C#
---

No post anterior estive falando sobre os métodos de extensão. Como surgiram algumas dúvidas(minhas e de alguns colegas) sobre este tema, resolvi aprofundar um pouco mais e estou compartilhando agora algumas dicas do uso prático deste recurso.

### Métodos de Extensão em Resumo

Os Métodos de Extensão permitem que um tipo existente seja estendido com métodos novos, sem alterar a definação do tipo original. Ele é um <strong>método estático</strong> de uma classe estática, onde o modificador <strong>this</strong> é aplicado ao primeiro parâmetro. O tipo do primeiro parâmetro será o tipo estendido. <u><a href="http://vitormeriat.com.br/2011/04/24/mtodos-de-extenso/" target="_blank">Leia mais sobre este assunto.</a></u>

### Encadeamento do Método de Extensão

Os métodos de extensão, assim como os métodos de instância, oferecem uma forma ordenada de encadear funções. Observe as duas funções abaixo:

<pre style="font-size: 16pt !important">
<code class="cs">
public static class StringHelper
{
    public static string ParaPlural(this string termo)
    {
        return "...";
    }
    
    public static string PrimeiraLetraParaMaiusculo(this string termo)
    {
        return "...";
    }
}
</code>
</pre>


Agora que nossos métodos de extensão estão prontos, quero em uma determinada situação, que o meu termo seja pluralizado e que tenha apenas sua primeira letra maiúscula. Em outras palavras, que utilizar meus métodos de forma encadeada. Observe a figura abaixo:
<pre style="font-size: 16pt !important">
<code class="cs">
string termo1 = "vitor".ParaPlural().PrimeiraLetraParaMaiusculo();
string termo2 = StringHelper.ParaPlural(StringHelper.PrimeiraLetraParaMaiusculo("vitor"));
</code>
</pre>

Sabemos que os termos 1 e 2 são equivalentes porém o termo1 utiliza métodos de extensão , enquanto o termo2 utiliza métodos estáticos.

### Restrição aos métodos de extensão

Se você já está usando métodos de extensão, fatalmente você pode imaginar algo como manipular variáveis da classe a ser estendida. Pois é, isso não é possível.

O compilador do C# trata o método de extensão como se fosse um método estático da pertencente a classe, e isso nos restringe o acesso aos membros internos da classe.

### Métodos de Extensão para Download

Imagine um método ToInt32() disponível na classe String os invés do famoso Convert.ToInt32(“minhaString”). Isso pode ser bem útil, assim como inúmeros outros métodos.

Uma boa dica é o site <a href="http://www.extensionmethod.net/">http://www.extensionmethod.net/</a> onde temos inúmeros métodos de extensão comentados e disponíveis para download. Você pode criar uma classe utilitária com todos estes métodos selecionados especialmente para seu projeto.

### Métodos de extensão versus Métodos de instância

Durante uma implementação, percebi que tinha dois métodos com a mesma assinatura, sendo que um estava declarado na classe e o outro era meu método de extensão. Sei que isso parece sem propósito mas a dúvida ficou no ar… qual método teria prioridade? Vejamos a implementação abaixo:

<pre style="font-size: 16pt !important">
<code class="cs">
namespace MetodosExtensaoDicas
{
    class Program
    {
        static void Main(string[] args)
        {
            new Classe().Metodo();
        }
    }
    
    public class Classe
    {
        public void Metodo()
        {
            Console.WriteLine("Impressão do Método de Instância!");
        }
    }
    
    public static class Extensao
    {
        public static void Metodo(this Classe classe)
        {
            Console.WriteLine("Impressão do Método de Extensão!");
        }
    }
}
</code>
</pre>

A saída de nosso exemplo será: <strong>Impressão do Método de Instância!</strong>

Quando executarmos a chamada ao método da <strong>instância</strong> de nossa classe, o método de instância será executado. Você pode usar os métodos de extensão para estender uma classe ou interface, mas não para substituí-las.

Um método de extensão com o mesmo nome e assinatura de um método da instância nunca será chamado. No momento da <strong>Compilação</strong>, os métodos de instância sempre terão prioridade em relação aos métodos estendidos. Quando o compilador&nbsp; tem uma chamada a método, ele primeiro procura por repetições nos métodos de instância. Se não houver nenhuma ele irá pesquisar os métodos de extensão e se seus tipos são compatíveis.

### Método de Extensão versus Método de Extensão

O que acontece se tivermos dois métodos de extensão com a mesma assinatura? Considere o seguinte exemplo:

<pre style="font-size: 16pt !important">
<code class="cs">
public static class StringFunctions
{
    public static bool EhPermitido(this string termo)
    {
        return false;
    }
}

public static class ObjectFunctions
{
    public static bool EhPermitido(this object termo)
    {
        return false;
    }
}
</code>
</pre>


Se houver dois ou mais métodos com a mesma assinatura, devemos trabalhar utilizando-os como métodos estáticos para evitar a ambiguidade. Caso contrário, o compilador irá chamar o método que possui argumentos mais <strong>específicos</strong>.

<pre style="font-size: 16pt !important">
<code class="cs">
bool permissao = "meirat".EhPermitido();
</code>
</pre>


O código acima faz uso do método de extensão e irá chamar o método EhPermitido do StringFunctions. Caso você queira chamar o método EhPermitido do ObjectFunctions, será necessário especificá-lo explicitamente:
<pre style="font-size: 16pt !important">
<code class="cs">
ObjectFunctions.EhPermitido("meriat")
</code>
</pre>

Em nosso exemplo, o primeiro método tem como argumento um string e o segundo um object. A classe string herda de object e portanto é mais <strong>específica </strong>em suas funções.

<hr />
<strong>PS:</strong> Em geral, é recomendável implementar métodos de extensão com moderação e apenas quando necessário. Bom senso é algo fundamental para ser um bom programador!
