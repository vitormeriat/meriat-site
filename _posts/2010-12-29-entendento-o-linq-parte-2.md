---
layout: post
title: Entendento o LINQ (parte 2)
date: 2010-12-29
categories:
    - LINQ
    - ORM
---

# LINQ para SQL

Até este momento tratamos apenas das consultas locais. Agora iremos abordar as consultas interpretadas que são descritivas e operam sequências que executam <strong>IQueryable&lt;T&gt;</strong> e se decompõem para operadores de consulta na classe Queryable, enviando árvores de expressão que serão interpretadas em tempo de execução.

Para entendermos seu funcionamento, vamos ao exemplo 5. O primeiro passo será a criação do Banco de dados. Neste exemplo, estarei utilizando um banco criado no próprio projeto. Crie o banco e uma tabela Desenvolvedores conforme a figura abaixo:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2010/12/figura-1.png"><img src="http://blob.vitormeriat.com.br/images/2010/12/figura-1.png" alt="figura 1" /></a></p>

Agora que temos nossa fonte de dados criada, é só inserir alguns valores, como no script abaixo, para efetuarmos nossos testes:

<pre style="font-size: 1.6em !important">
    <code class="sql">
INSERT INTO Desenvolvedores (Nome, Linguagem, Empresa, DataNascimento)
VALUES ('Vitor', 'C#', 'DevGeek', '10-11-1984')
    </code>
</pre>


O próximo passo será a criação de nosso contexto. Neste exemplo, utilizamos uma classe chamada Desenvolvedor para representar os dados. O LINQ para SQL nos permite utilizar este recurso, desde que decoremos os atributos corretamente utilizando o namespace <em><strong>System.Data.Linq.Mapping</strong></em>.
<pre style="font-size: 1.6em !important">
    <code class="cs">
[Table(Name = "Desenvolvedores")]
public class Desenvolvedor
{
   [Column(IsPrimaryKey = true)]
   public int ID;

   [Column]
   public string Nome;

   [Column]
   public string Linguagem;

   [Column]
   public string Empresa;

   [Column(Name = "DataNascimento")]
   public DateTime DataDeNascimento;
}
    </code>
</pre>

O atributo [Table] indica ao LINQ que um objeto deste tipo representa uma linha em uma tabela de um banco de dados. Seu padrão aponta que o nome da tabela é o mesmo da classe. Isso pode ser alterado caso necessário.

Esta classe decorada com os atributos de [Table], passa a ser chamada de entidade no LINQ para SQL. A melhores práticas indicam que sua estrutura deve ser idêntica à tabela do banco de dados, em uma construção de baixo nível.

O atributo [Column] indica que o campo ou propriedade representa uma coluna da tabela, e a propriedade <strong>IsPrimaryKey</strong> indica que a coluna é chave primaria na tabela. Caso haja necessidade, podemos utilizar nomes diferentes para a tabela e as colunas, desde que especifiquemos o nome correto com o atributo Name. A exemplo da tabela e da coluna DataDeNascimento.

Com nosso contexto criado, precisamos de uma “ponte” que nos ligue a fonte de dados externa. Esta ponte nós chamamos de <strong>DataContext</strong>.

# DataContext

Um objeto DataContext (do tipo <strong>System.Data.Linq.DataContext</strong>), age de duas maneiras. Primeiro como uma fábrica de geração de tabelas, e segundo, armazenando “vestígios” de qualquer alteração da entidade para que possamos escrever diretamente na memória de acesso rápido. O objeto DataContext monitora todas as entidades que ele intanciou.

Para termos acesso as tabelas, elas devem ser mapeadas e estar disponíveis em um objeto do tipo DataContext. O objeto DataContext suporta atualizações e manutenção do banco de dados para objetos conhecidos do LINQ e efetua o tratamento da conexão com o banco de dados. Vamos criar nosso DataContext como na listagem abaixo:

<pre style="font-size: 1.6em !important">
    <code class="cs">
DataContext contextoDeDados = new DataContext("string de conexão");
Table<Desenvolvedor> desenvolvedores = contextoDeDados.GetTable<Desenvolvedor>();
    </code>
</pre>

No código acima criamos um DataContext chamado contextoDeDados e uma coleção Table de nosso contexto. A classe 
<strong>Table&lt;TEntity&gt;</strong>, do namespace System.Data.Linq representa uma tabela do banco de dados. Ela implementa as interfaces <strong>IEnumerable&lt;T&gt;</strong> , <strong>IQueryable&lt;T&gt;</strong> e <strong>ITable</strong> que por sua vez implementa<strong> IEbumerable</strong> e <strong>IQueryable</strong>.

Utilizamos o método <strong>GetTable&lt;T&gt;</strong> do DataContext para criar um para criar um objeto Desenvovedor do tipo<strong> Table&lt;</strong><strong>Desenvovedor&gt;</strong> no contexto <strong>contextoDeDados</strong>. Notem que passamos como argumento do construtor DataContext a string de conexão. Agora nosso Banco de Dados passa a ser conhecido pelo LINQ.

Segue a listagem completa do Exemplo 5.
<pre style="font-size: 1.6em !important">
    <code class="cs">
// String de conexão com o banco
const string sc = @"String de Conexão";

// Crio o objeto de contexto e informo a conexão para o banco
DataContext contextoDeDados = new DataContext(sc);

Table<Desenvolvedor> desenvolvedores = contextoDeDados.GetTable<Desenvolvedor>();

var consulta = from c in desenvolvedores
            where c.Linguagem == "C#"
            orderby c.DataDeNascimento, c.Nome
            select new { c.Nome, c.Empresa, c.DataDeNascimento };
    </code>
</pre>

Estamos fazendo uma consulta simples, onde selecionamos o Nome a empresa e a data de nascimento de todos os desenvolvedores que programam em C#. Ordenamos primeiro pela data de nascimento e depois pelo nome.

Iremos abordar uma solução mais elegante e recomendada, iremos utilizar um DataContext fortemente tipado, como na listagem abaixo:

<pre style="font-size: 1.6em !important">
    <code class="cs">
public partial class ContextoDeDados : DataContext
{
   public Table<Desenvolvedor> desenvolvedores;

   public ContextoDeDados() : base(@"String")
   { }
}
    </code>
</pre>


Neste exemplo, declaro uma classe que herda de DataContext. Crio um campo desenvolvedor do tipo Table&lt;T&gt; para a tabela que será mapeada e chamo o construtor base de DataContext no construtor da classe, passando a string de conexão com o banco de dados. Agora para realizarmos uma consulta usando o contexto fortemente tipado, basta apenas criar uma instância do mesmo, como no exemplo abaixo.

<pre style="font-size: 1.6em !important">
    <code class="cs">
// Crio um objeto de contexto
ContextoDeDados contexto = new ContextoDeDados();
// Consulto os desenvolvedores que trabalhama na empresa Literatura e Cia
var consulta = contexto.desenvolvedores.Where(c => c.Empresa == "Literatura e Cia");
    </code>
</pre>


Neste exemplo estou utilizando o método <strong>GetCommand</strong> para visualizar o comando SQL gerado.

O arquivo com todos os exemplos pode ser baixado <a href="http://cid-f47ea42a37bff249.office.live.com/browse.aspx/Artigos" target="_blank">AQUI</a>

#### Espero que tenham gostado da dica e qualquer dúvida é só entrar em contato!
