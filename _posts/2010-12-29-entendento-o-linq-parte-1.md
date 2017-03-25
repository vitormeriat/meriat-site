---
layout: post
title: Entendento o LINQ (parte 1)
date: 2010-12-29
categories:
    - LINQ
    - ORM
image: "http://blob.vitormeriat.com.br/images/2010/12/linq.jpg"
---

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2010/12/linq.jpg"><img alt="linq" src="http://blob.vitormeriat.com.br/images/2010/12/linq.jpg" /></a></p>

O LINQ (Language Integrated Query ou Linguagem Integrada de Consulta), é uma nova função do C# 3.0 e .Net Framework 3.5. Ele permite escrever consultas estruturadas seguras em torno de coleções locais e objetos e fontes remotas de dados. </p>

Para iniciar nossos estudos no LINQ, devemos utilizar os namespaces "System.Linq" e "System.Linq.Expressions". Estarei utilizando o Visual C# 2010 Express.

O LINQ permite você consultar qualquer coleção de executando IEnumerable&lt;&gt;, no meio de um array, list, XML DOM, ou fonte remota de dados(como uma tabela no SQL Server). O LINQ oferece os benefícios de ambos os tipos de verificação do tempo de compilação e composição dinâmica de consultas.

O LINQ proporciona duas arquiteturas paralelas: consultas locais e consultas interpretadas. As consultas locais tratam de coleções locais de objetos, quanto às consultas interpretadas tratam de fontes remotas de dados.Neste momento, iremos nos ater somente as consultas locais, abordando as consultas interpretadas a partir do tópico LINQ para SQL.

As unidades básicas de dados no LINQ são sequências e elementos. Uma sequência é qualquer objeto que executa a interface IEnumerable.

<p align="justify">No exemplo seguinte, o array numeros é uma sequência e 1,2,3,4,5 são os elementos:</p>
<pre style="font-size: 1.6em !important">
    <code class="cs">
int[] numeros = {1,2,3,4,5};
    </code>
</pre>


> Este tipo de sequência é denominada "local", uma vez que representa uma coleção local de objetos na memória.

# Operadores de Consulta

São métodos que transformam uma sequência. Por padrão, um operador de consulta recebe uma sequência de entrada e retorna uma sequência de saída transformada. Há em torno de 40 operadores de consulta, executados como métodos estáticos de extensão e que são denominados operadores padrões de consulta.

# Consulta

É uma expressão que transforma sequências utilizando operadores de consulta. A estrutura mais simples de uma consulta engloba uma sequência de entrada e um operador; como no exemplo 1:

<pre style="font-size: 1.6em !important">
    <code class="cs">
// Sequência a ser consultada
int[] sequencia = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// Consulta que retorna os números pares
IEnumerable<int> filtro = System.Linq.Enumerable.
    </code>
</pre>

# Consultas Lambda

São as mais flexíveis e fundamentais. A maioria dos operadores de consulta aceita expressões Lambda como argumento. Estas expressões ajudam a direcionar e dar forma ao à consulta. No exemplo 1, utilizamos uma expressão Lambda:

<pre style="font-size: 1.6em !important">
    <code class="cs">
n => n % 2 == 0
    </code>
</pre>

O argumento de entrada <em><font size="2">n</font></em> representa cada um dos números no array e é do tipo int. O operador Where necessita que a expressão retorne um valor bool, indicando que o elemento deverá ser incluído na sequência de saída. 

No C# temos uma sintaxe especial para escrever consultas, denominada "sintaxe de compreensão de consultas". O exemplo 1 utilizando o esta sintaxe ficaria assim:

<pre style="font-size: 1.6em !important">
    <code class="cs">
int[] sequencia = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

IEnumerable<int> filtro = from n in sequencia
  where n % 2 == 0
  select n;
    </code>
</pre>

As sintaxes Lambda e de compreensão são complementares, então utilizaremos ambas durante os exemplos. Aproveitando o gancho, vamos diminuir nossa consulta "tipando implicitamente" o filtro, e chamando nosso operador diretamente de sequencia(nosso array de int), uma vez que os operadores são executados como métodos de extensão. O Exemplo 1 ficará assim: 

<pre style="font-size: 1.6em !important">
    <code class="cs">
int[] sequencia = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
var filtro = sequencia.Where(n => n % 2 == 0);
    </code>
</pre>


# Encadeamento de Operadores

Para realizar consultas mais complexas, nós podemos utilizar o encadeamento de operadores como no exemplo 2:

<pre style="font-size: 1.6em !important">
    <code class="cs">
// Crio a sequência a ser consultada
string[] sequencia = { "Vasco", "Fluminense", "Bota-Fogo", "Grêmio", "Santos", "Internacional", "Cruzeiro", "Figueirense" };

// Executo a consulta utilizando os operadores encadeados.
var filtro = sequencia
   .Where(n => n.Contains("a")) // Condição
   .OrderBy(n => n.Length)      // Ordenação
   .Select(n => n.ToUpper());   // Tudo em letras maiúsculas
    </code>
</pre>

Os operadores Where, OrderBy e Select separam os métodos de extensão na classe Enumerable. O operador Where, faz o primeiro filtro da sequência de entrada. O operador OrderBy retira uma versão ordenada da sequência de entrada e o método Select retorno uma sequência onde cada elemento é transformado por uma determinada expressão Lambda. Os dados fluem da esquerda para a direita, em nosso caso, a ordem de execussão é: Where, OrderBy, OrderBy e Select.

> É importante frisar que ao utilizar operadores não é alterada a sequência de entrada. O que acontece é o retorno de uma nova seuqência.

Quando utilizamos operadores de consulta encadeados, a sequência de saída do primeiro operadar é a sequência de entrada de outro. Podemos então, construir o exemplo 2 como no código abaixo:

<pre style="font-size: 1.6em !important">
    <code class="cs">
string[] sequencia = { "Vasco", "Fluminense", "Bota-Fogo", "Grêmio", "Santos", "Internacional", "Cruzeiro", "Figueirense" };

// Filtro
var filtro = sequencia.Where(n => n.Contains("a"));
// Ordenação
var sorted1 = filtro.OrderBy(n => n.Length);
// Transforma tudo em letras maiúsculas
var resultadoFinal = sorted2.Select(n => n.ToUpper());
    </code>
</pre>


# Subconsultas

Uma subconsulta é uma expressão Lambda de consulta obtida sobre o resultado da consulta anterior. No expemplo 3 utilizamos uma consulta n.Split() para converter cada uma das strings em uma coleção de palavras, logo após utilizamos nossa subconsulta .Last() para que a ordenação seja realizada pelo último elemento da coleção, neste caso o sobrenome do escritor.

<pre style="font-size: 1.6em !important">
    <code class="cs">
// Crio a sequência com os nomes dos escritores brasileiros
string[] nomes = { "Monteiro Lobato", "Cecilia Meireles", "Manuel Bandeira", "Mario Quintana", "Castro Alves" };

// Crio uma consulta pra ordenar os nomes pelos sobrenomes dos escritores
var resultado = nomes.OrderBy(n => n.Split().Last());
    </code>
</pre>

No exemplo 4 utilizamos uma subconsulta mais elaborada. Nesta subconsulta, retornamos todas os elementos químicos cujo a quantidade de letras for igual ao elemento menor.

<pre style="font-size: 1.6em !important">
    <code class="cs">
// Crio a sequência com alguns elementos da tabela periódica
string[] nomes = { "Urânio", "Rênio", "Ununquádio", "Sódio", "Copernício", "Bário" };

// Consulta para retornar todos os nomes cujo o tamanho seja igual ao menor nome.
var resultado = nomes
   .Where(n => n.Length ==
       nomes.OrderBy(n2 => n2.Length)
       .Select(n2 => n2.Length).First());
    </code>
</pre>

A variável externa de repetição (<i>n</i>) está no centro da subconsulta, portanto, não podemos reutilizar <i>n</i> como variável de iteração da subconsulta.

#### No próximo artigo iremos continuar explorando as funcionalidades do LINQ.