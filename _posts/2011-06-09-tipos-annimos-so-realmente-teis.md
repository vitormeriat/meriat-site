---
layout: post
title: Tipos anônimos são realmente úteis?
date: 2011-06-09
categories:
  - C#
  - CLR
---

Os tipos anônimos (Anonymous Types) são uma característica da linguagem C# onde criamos diversas propriedades para um objeto sem ter que definir explicitamente seu tipo. Essa novidade surgiu na versão 3.0 junto com diversas outras tais como: propriedades automáticas, inferência de tipos, inicializadores de objetos, expressões lambda, métodos de extensão dentre outros.

A referência para tipos anônimos na MSDN diz que tipos anônimos fornecem uma maneira conveniente de encapsular um conjunto de propriedades apenas leitura em um simples objeto sem que seja necessário primeiro definir explicitamente um tipo. O nome do tipo é gerado pelo compilador e não está disponível no nível do código fonte. <strong>O tipo das propriedades é inferido pelo compilador</strong>.

Um tipo anônimo pode ser declarado da seguinte maneira:

<pre style="font-size: 16pt !important">
<code class="javascript">
static void Main(string[] args)
{
    // Criando um tipo anônimo
    var tipoAnonimo = new { Nome = "Meriat", Idade = 26, Altura = 1.78 };
}
</code>
</pre>

Neste caso a variável tipoAnonimo é um tipo anônimo que possui três propriedades:

* Nome do tipo System.String;
* Idade do tipo System.Int32;
* Altura do tipo System.Double.


Os tipo anônimos são muito úteis quando realizamos consultas usando o LINQ uma vez que normalmente temos que retornar um tipo com o conjunto de propriedades diferentes dos tipos já existentes. Vamos realizar algumas consultas para exemplificar esta assertiva:

<pre style="font-size: 16pt !important">
<code class="javascript">
static void Main(string[] args)
{
    // Cria um objeto de contexto
    ContextoDeDados contexto = new ContextoDeDados();
    
    // Consulta os desenvolvedores que trabalham em um empresa específica
    var consulta1 = contexto.desenvolvedores.Where(c => Empresa == "Meriat $ Cia");
    
    // Consulta desenvolvedores maiores de idade
    var consluta2 = from c in contexto.desenvolvedores
        where c.Idade > 18
        select new { c.Nome, c.Empresa, c.Linguagem };
    
    // Consulta desenvolvedores que programam em C#
    var consulta3 = from c in contexto.desenvolvedores
        where c.Linguagem = "C#"
        selec new { c.Empresa };
}
</code>
</pre>

A primeira consulta retorna um tipo que contém três propriedades(Nome, Empresa e Linguagem) e no segundo exemplo obtemos um tipo com apenas uma propriedade( Empresa). Sem o recuso dos tipos anônimos teríamos que definir explicitamente a classe para representar os tipos retornados.

Quando um tipo anônimo é atribuído a uma variável, a variável deve ser inicializada com a construção <a href="http://msdn.microsoft.com/pt-br/library/bb383973.aspx">var</a>. Isso ocorre porque apenas o compilador tem acesso ao nome base do tipo anônimo.


Quando criamos um tipo anônimo o compilador gera uma classe selada interna que modela o tipo . O tipo anônimo é imutável: todas as suas propriedades estão no modo somente leitura. Essa classe contém substituições de Equals() e GetHashCode() que implementam a semântica de valores. Além disso, o compilador gera uma substituição de ToString(), que exibe o valor de cada uma das propriedades públicas.

Tipos anônimo são tipos de referência, derivam diretamente de <strong>object</strong>. Durante sua criação o compilador lhe atribui um nome que é inacessível para a aplicação. Da perspectiva do CLR, um tipo anônimo não é diferente de qualquer outro tipo por referência, exceto pelo fato de não poder ser convertido para qualquer tipo.


## Limitações

Os tipos anônimos apresentam limitações que devem ser conhecidas para que seu uso possa ser mais consciente. Quando se opta por usar tipos anônimos é necessário saber que eles não são símbolos C# válidos, sua validade fica a nível de CLR. Isto implica na impossibilidade de definir métodos de extensão, de declarar métodos com tipos anônimos como parâmetros e retornar tipos anônimos a partir de métodos.


## Resposta

É certo que os tipos anônimos tem limitações, então qual sua real utilidade?

Penso que a utilização de tipos anônimos(sempre com o uso do bom senso) é muito vantajosa pelos seguintes pontos:

* O compilador escreve os códigos muito mais rápido que você! Ele cria um calhamaço de código para cada tipo anônimo que criamos;
* É uma ótima maneira de economizar tempo (Time is money);
* Não destroem o desing da aplicação. São uma excelente alternativa para valores locais desafogando a necessidade que muitas vezes se tinha de criar uma classe para se trabalhar com os retornos;
* Por serem anônimos podem seu utilizados para trazer um maior desacoplamento, separando lógicas específicas sem a dependência de tipos já definidos.
 

Existem algumas estratégias que possibilitam um uso mais apurado dos tipos anônimos. Mais isto fica para o próximo post.

<p>Baixo e código fonte do post <a href="httpcid-bd055aa47a388023.office.live.comself.aspx.PublicTiposAnonimos.rar" target="_blank">aqui</a>!</p>

### Um grande abraço e ótimo Estudo!
