---
layout: post
title: SQL Azure e o não suporte a tabelas sem clustered index
date: 2012-02-17
categories:
  - Microsoft Azure
  - Microsoft Azure Storage
  - SQL
image: "http://blob.vitormeriat.com.br/images/2012/02/errosqlazure.png"
---

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2012/02/errosqlazure.png"><img alt="ErroSqlAzure" src="http://blob.vitormeriat.com.br/images/2012/02/errosqlazure.png" /></a></p>
<p align="justifiy">Estava eu trabalhando feliz da vida em um sistema em Azure utilizando o ambiente local por meio do <strong>Compute Emulator</strong> e&#160; um banco de dados hospedado em um <strong>SQL Server 2008 R2</strong> padrão, e tudo corria perfeitamente bem. Com todos os testes passando decidi que era hora de testar com os dados no <strong>SQL Azure</strong> e tive uma surpresinha:</p>
<blockquote><p><font color="#ff0000"><strong>Msg 40054, Level 16, State 1, Line 3  <br /></strong>Tables without a clustered index are not supported in this version of SQL Server. Please create a clustered index and try again.</font></p>
</blockquote>
<p><!--more-->
<p>&#160;</p>
<h2>Explorando o motivo</h2>
<p>Bem, o motivo pelo qual me deparei com este “erro” se deve por que existem algumas limitações ou diferenças entre o SQL Server e o SQL Azure. Diferente do SQL Server padrão, o SQL Azure não permite inserções de dados em uma tabela sem um clustered index definido, dai a mensagem de erro dizendo que “esta versão” [SQL Azure] não suporta tabelas sem clustered index.</p>
<p>Para maiores detalhes e um guia completo das limitações do SQL Azure eu indico a leitura abaixo:</p>
<p><a href="http://msdn.microsoft.com/en-us/library/ee336245.aspx">General Guidelines and Limitations (SQL Azure Database)</a></p>
<p>&#160;</p>
<h2>Solução</h2>
<p align="justify">O primeiro passo foi identificar as tabelas sem um clustered index definido. É claro que no meu caso eu tinha muitas tabelas o que justifica o esforço, mas vamos simular isto criando um banco com quatro tabelas como segue na listagem abaixo. </p>
<pre style="font-size: 1.6em !important">
    <code class="sql">
CREATE DATABASE TesteSQLAzure
USE [TesteSQLAzure];
GO
CREATE TABLE [dbo].[Tabela01] (
  [PartitionKey] varchar(36)  NOT NULL,
  [RowKey] varchar(36)  NOT NULL,
  [PropriedadeA] varchar(50)  NULL
);
GO

CREATE TABLE [dbo].[Tabela02] (
  [PartitionKey] varchar(36)  NOT NULL,
  [RowKey] varchar(36)  NOT NULL,
  [PropriedadeA] varchar(50)  NULL
);
GO

CREATE TABLE [dbo].[Tabela03] (
  [PartitionKey] varchar(36)  NOT NULL,
  [RowKey] varchar(36)  NOT NULL,
  [PropriedadeA] varchar(50)  NULL
);
GO

CREATE TABLE [dbo].[Tabela04] (
  [PartitionKey] varchar(36)  NOT NULL,
  [RowKey] varchar(36)  NOT NULL,
  [PropriedadeA] varchar(50)  NULL
);
GO
    </code>
</pre>

<p align="justify">&#160;</p>
<p>Como próximo passo vamos criar os índices para as tabelas Tabela02 e Tabela04:</p>
<pre style="font-size: 1.6em !important">
    <code class="sql">
ALTER TABLE [dbo].[Tabela02]
ADD CONSTRAINT [PK_Tabela02]
PRIMARY KEY CLUSTERED ([PartitionKey], [RowKey] ASC);
GO

ALTER TABLE [dbo].[Tabela04]
ADD CONSTRAINT [PK_Tabela04]
PRIMARY KEY CLUSTERED ([PartitionKey], [RowKey] ASC);
GO
    </code>
</pre>

<p>&#160;</p>
<p align="justify">Neste exato momento, seria possível inserir dados nas tabelas Tabela02 e Tabela04, porém teríamos o referido problema quando fosse a vez de inserir dados nas tabelas Tabela01 e Tabela03 . Como ainda não sabemos disto, precisamos encontrar as tabelas “estragadas” no SQL Azure. Para isso, vamos dividir o script em 3 passos:</p>
<p>Passo 1: Contar a quantidade de tabelas do banco em questão;</p>
<pre style="font-size: 1.6em !important">
    <code class="sql">
SELECT COUNT (*)
FROM sys.objects
WHERE type = 'U'
    </code>
</pre>

<p>&#160;</p>
<p>Passo 2: Retornar a quantidade de tabelas com o clustered index definido;</p>
<pre style="font-size: 1.6em !important">
    <code class="sql">
SELECT COUNT (*) AS 'Quantidade'
FROM sys.indexes
WHERE object_id IN
  ( SELECT object_id FROM sys.objects WHERE type = 'U' )
  AND index_id = 1
    </code>
</pre>

<p>&#160;</p>
<p>Passo 3: Retornar o nome das tabelas sem um clustered index definido.</p>
<pre style="font-size: 1.6em !important">
    <code class="sql">
SELECT name AS 'Tabelas sem Clustered Index'
FROM sys.objects
WHERE type = 'U' AND object_id NOT IN
  (SELECT object_id FROM sys.indexes WHERE index_id = 1)
    </code>
</pre>

<p>&#160;</p>
<p>É claro que você poderia executar direto o 3º passo, mas assim fica mais claro como chegar até esta solução.</p>
<p>Agora que você já identificou as tabelas com problema, é só adicionar as constraints para que neste cenário, tudo funcione corretamente.</p>

<h3>Importante:</h3>
<p>** Esse exemplo não tem por objetivo entrar na discussão do que é uma boa chave para seu índice cluster, apenas mostra cuidados ao portar uma aplicação para o SQL Azure.</p>

<h4><strong>Um ótimo feriado a todos.</strong></h4>
