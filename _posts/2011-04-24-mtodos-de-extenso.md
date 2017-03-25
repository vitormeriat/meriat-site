---
layout: post
title: Métodos de extensão
date: 2011-04-24
categories:
    - C#
    - LINQ
---

Dentre as muitas novidades advindas do .Net 3.5 gostaria de destacar a possibilidade de criar métodos de extenção.

Os método de extesão nos permitem “Adicionar” métodos para <strong>tipos</strong> existentes sem a necessidade de criar classes derivadas, recompilar ou modificar o tipo original. Os Métodos de extensão são um tipo especial de método estático com a sintaxe açucarada.

> Açucar Sintático para as linguagens de programação refere-se a sintaxe projetada para faliclitar a compreensão e escrita, tornando o código cada vez mais legível.

### A motivação

Geralmente é dificultoso realizar alguma alteração nos tipos padrão sem quebrar o código existente. Sempre deve se ter a preocupação de ao se tentar estender estes tipos com novas funcionalidades, não alterar o contrato existente.

Este recurso, entretanto, permite a extensão das funcionalidades de tipo existentes, mesmo quando um tipo não é hereditário. E estes métodos de exibição têm uma função crucial na implementação do LINQ. Um exemplo disso é a interface IEnumerable&lt;T&gt;. Para oferecer suporte ao LINQ, novos métodos tiveram que ser adicionados a esta interface. Contudo, a alteração da interface adicionando novos métodos a deixaria incompatível com as versões dos consumidores existentes. A adição de uma nova interface era uma possibilidade, mas a criação de uma nova interface para complementar a interface IEnumerable&lt;T&gt; existente seria um projeto um tanto estranho.(*)

### Mão na massa

Vamos ao nosso exemplo:

<pre style="font-size: 16pt !important">
<code class="cs">
static void Man(string[] args)
{
    // Declara uma pessoa
    Pessoa pessoa;
    // Informa o nome inicial e final da pessoa
    pessoa.PrimeiroNome = "Vitor";
    pessoa.UltimoNome = "Meriat";
    
    // Valida os nomes informados...
    if(pessoa.PrimeiroNome.ValidaNome() && pessoa.UltimoNome.ValidaNome())
    {
        // Exibe o nome da pessoa.
        Console.WriteLine(pessoa.QualMeuNome());
    }
}
</code>
</pre>

Declaramos um objeto Pessoa que é uma <strong>Struct</strong>(estrutura), e estruturas no C# são tipos de valor e diferente dos tipos por referência ele sempre tem um valor padrão. Logo após informamos os valores para primeiro e último nome. Dentro da nossa estrutura de verificação(nome chique para meu if) temos a variável pessoa do tipo struct. Ela possui uma propriedade <strong>PrimeiroNome</strong> do tipo <strong>string</strong>. O método <strong>ValidaNome</strong> é <strong>estendido</strong> do tipo string. Já após a validação dos nomes imprimimos o resultado. Agora nosso método é uma <strong>extenção</strong> da estrutura pessoa. Vamos ver como isso é possível.

<pre style="font-size: 16pt !important">
<code class="cs">
struct Pessoa
{
    public string PrimeiroNome;
    public string UltimoNome;
}

static class MetodosExtensao
{
    public static string QualMeuNome(this Pessoa pessoa)
    {
        return "Meu nome é: " + pessoa.PrimeiroNome + " " + pessoa.UltimoNome;
    }
    
    public static bool ValidaNome(this string nome)
    {
        return Char.IsUpper(nome[0]);
    }
}
</code>
</pre>

Temos uma classe Pessoa.cs e nela nossa estrutura Pessoa com suas propriedades. Notem que abaixo temos nossos métodos de extensão.

A declaração do método contém o atributo que identifica este método como um método de extensão. Este atributo é o <strong>"this"</strong> que está antes dos tipos dos parâmetros. Os métodos de extensão são definidos pela aplicação do atributo de extensão encontrado no namespace System.Runtime.CompilerServices encontrado em System.Core.Dll. Para aqueles que não estão familiarizados com atributos, eles podem ser usados para fornecer metadados que são usados pelo compilador para disparar uma funcionalidade adicional. Nesse caso, o atributo de extensão oferece informações que mostram ao compilador que aquele método poderá ser chamado no tipo identificado como o primeiro argumento para o método de extensão — A Struct Pessoa e a string nome, no meu exemplo.

<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/04/03.png"><img src="http://blob.vitormeriat.com.br/images/2011/04/03.png" alt="03" /></a></p>

Esta imagem ilustra muito bem o que aprendemos aqui. Agora que criamos nossos métodos e os estendemos nos tipos que precisamos, eles estão disponíveis no Intellisense, assim como alguns métodos especialmente estendidos para nossas consultas Linq. Notem que estes métodos estão sinalizados com (extension).

<a href="http://cid-bd055aa47a388023.office.live.com/self.aspx/.Public/M%c3%a9todos%20de%20Extens%c3%a3o.rar">Baixe aqui o Código Fonte do artigo</a>

<hr />

*fonte <a href="http://msdn.microsoft.com">http://msdn.microsoft.com</a>

PS: <strong>EXTENDER</strong>", com "<strong>x</strong>", <strong>NÃO EXISTE!</strong>
<p></p>
<strong>ESTENDER</strong>: (usado como vtd - verbo transitivo direto) Dar maior superfície a; Desdobrar, estirar; Alongar, distender; Prolongar; (usado como vtdi - verbo transitivo direto e indireto) Oferecer, apresentando; (usado como vi - verbo intransitivo);

<strong>EXTENSÃO: </strong>Efeito de estender(-se), ampliação; Dimensão; Duração; Importância, alcance; Desenvolvimento; Aplicação extensiva do sentido de palavra ou frase; Instalação telefônica ligada à mesma linha que outro(s) aparelho(s), em local diverso; Seqüência de caracteres adicionada ao final do nome de um arquivo, e que indica o tipo do arquivo, segundo sua função ou formato.


<strong>ESTENSÃO</strong>, com "<strong>s</strong>", <strong>NÃO EXISTE!</strong></p>
