---
layout: post
title: Azure Table Service (ATS) e o suporte as consultas LINQ
date: 2011-05-20
categories:
    - Cloud Computing
    - LINQ
    - Microsoft Azure
    - Microsoft Azure Storage
---

O Azure Table Service é um serviço de armazenamento de dados não relacional que proporciona a persistência de entidades dentro de tabelas que por sua vez estão relacionadas a uma conta do Windows Azure.

O ATS não é um banco de dados relacional como os já consagrados Microsoft SQL Server, Oracle ou DB2. Ele possui uma estrutura “frouxa” que proporciona em uma mesma tabela se ter linhas com estruturas de colunas distintas.

Se você vai iniciar uma aplicação Azure e está pensando em usar LINQ para acesso a dados, ai vai a lista com os operadores que tem ou não suporte dentro do ATS.

### Operadores suportados
* **From**
* **Where**
* **First, FirstOrDefault**
* **Take**

**OBS:** Para o operador Take, o valor especificado deve ser menor ou igual a 1.000. No caso do valor ultrapassar este limite, o ATS irá retornar o famoso status code 400 (Bad Request). Se o operador Take não for especificado, o retorno trará somente os primeiros 1.000 registros.


### Operadores não suportados
<ul>
<li>
<div align="justify"><strong><font size="3">Select</font> </strong></div>
<p align="justify">OBS: Todas as propriedades de uma entidade são recuperadas em qualquer operação de leitura.</p>
</li>
<li>
<div align="justify"><strong><font size="3">GroupBy</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">OrderBy, OrderByDescending</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">ThenBy, ThenByDescending</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Average</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Min</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Max</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Last, LastOrDefault</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Skip<strong>Count, LongCount</strong></font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Sum</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">TakeWhile</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">SkipWhile</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Join, GroupJoin</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Single</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">OfType</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">SelectMany</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Concat</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">ElementAt, ElemenatAtOrDefault</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Distinct</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Except</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Intersect</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Union</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">All</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Any</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Contains</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">SequenceEqual</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Empty, Range, Repeat</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">SingleOrDefault</font></strong></div>
</li>
<li>
<div align="justify"><strong><font size="3">Reverse</font></strong></div>
</li>
</ul>

<p align="justify"><strong></strong>&nbsp;</p>
O Azure Table Service é uma ótima opção para o armazenamento de dados. Contudo é necessário conhecê-lo bem antes de fundamentar sua aplicação nele. Caso contrário você corre o risco de chegar no meio do projeto e se deparar com restrições que podem impossibilitar o desenvolvimento…
