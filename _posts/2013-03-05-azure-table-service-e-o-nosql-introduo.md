---
layout: post
title: Azure Table Service e o NoSQL – Introdução
date: 2013-03-05
categories:
- Cloud Computing
- Microsoft Azure
- Microsoft Azure Storage

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/03/nosql.gif"><img title="nosql" alt="nosql" align="left" src="http://blob.vitormeriat.com.br/images/nosql.gif" width="260" height="260" /></a>Bom, minha motivação nesta mini-série gira em torno de um problema comum que tenho: Dúvidas sobre o <strong>ATS (Azure Table Service)</strong>. <br />Geralmente o pessoal que visita o meu blog ou me conhece e lê ou sabe da experiência que tive com Azure, costuma me questionar sobre qual a diferença entre desenvolver &quot;para&quot; o <strong>Azure</strong> e da maneira convencional. Geralmente essa é uma dúvida simples de responder, já que a maioria do pessoal não faz nem ideia do que realmente seja Cloud Computing. Agora a dúvida que realmente complica o meio de campo é: Qual a diferença de desenvolvimento entre Azure Table Service e o <strong>MSQLS</strong> convencional? O problema aqui é mais conceitual.</p>
<p><!--more--><br />
<h2 align="justify">&#160;</h2>
<h2 align="justify">O Azure Table Service</h2>
<p align="justify">No primeiro momento é possível dar as respostas “comuns” como: O Azure Table Service é um serviço de armazenamento de dados não relacional que proporciona a persistência de entidades dentro de tabelas que por sua vez estão relacionadas a uma conta do Windows Azure.</p>
<p align="justify">Beleza, a galera estuda um pouco parte para a prática e novas dúvidas surgem sobre o ATS. Ai você já pode dizer que o ATS não é um banco de dados relacional como os já consagrados Microsoft SQL Server, Oracle ou DB2. Ele possui uma estrutura “frouxa” que proporciona em uma mesma tabela se ter linhas com estruturas de colunas distintas. Neste ponto o pessoal já começa a perceber algo de estranho. Deixa só esse povo precisar fazer um JOIN…</p>
<p align="justify">Primeiro falta o conhecimento do <strong>porquê </strong>se ter uma estrutura como a do ATS. Algumas pessoas questionam sua utilidade já que temos o SQL Azure. Outras iniciaram os estudos no Azure, optaram por utilizar o ATS pelas vantagens já citadas em diversos post, e diante das diferenças impostas pelo ATS acabaram migrando suas aplicações para o <strong>SQL Azure</strong>. É <strong>natural</strong> que em muitos casos, essas aplicações se utilizando do ATS sejam modeladas pensando no padrão convencional dos bancos de dados relacionais. Não é preciso dizer que em breve virão dificuldades… </p>
<p align="justify">O ponto principal é conhecer sobre os bancos de dados não relacionais, ou o comumente tão falado movimento NoSQL.</p>
<p align="justify">&#160;</p>
<h2 align="justify">O movimento NoSQL</h2>
<p align="justify">Chamado de movimento NoSQL por ser considerado um passo maior em relação a uma nova maneira de pensar do que na adoção de uma nova tecnologia. Novos modelos e estruturas de dados, desnormalização de dados, arquiteturas distribuídas e utilização intensiva de memória RAM, são algumas das características que o movimento tem proposto.</p>
<p align="justify">Como veremos nos próximos posts, os motivos e que levam a adoção do NoSQL envolvem problemas de <strong>flexibilidade</strong>, <strong>escalabilidade</strong>, <strong>taxa de transferência</strong>, <strong>latência</strong> e <strong>performance</strong>.</p>
<p align="justify">Vamos dar uma pequena volta em torno de alguns conceitos e entender melhor a necessidade de se buscar novas maneiras de encarar os problemas corriqueiros em relação a demanda de storage que as aplicações atuais tem requerido.</p>
<p align="justify">&#160;</p>
<h2 align="justify">Conclusão e próximos passos…</h2>
<p align="justify">Minha intenção nesta série e chegar aos pontos (iniciando pela infraestrutura) que justificam a estrutura do ATS, bem como mostrar o papel do NoSQL no cenário do desenvolvimento atual.</p>
