---
layout: post
title: Erro na criação de Fila no Azure
date: 2011-03-22
categories:
    - Cloud Computing
    - Microsoft Azure
---

### O PROBLEMA

Estava eu trabalhando tranquilamente em uma aplicação de teste para o Windows Azure quando tive a necessidade de criar uma Queue(fila).

Tudo corria na mais perfeita harmonia, já tinha criado algumas filas neste mesmo projeto sem nenhum tipo de problema. O código usado foi copy and paste dos demais e quando compilei o projeto e o resultado foi a tela amarela da morte como na imagem aseguir:

<p><a href="http://blob.vitormeriat.com.br/images/2011/03/01.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="01"   alt="01" src="http://blob.vitormeriat.com.br/images/2011/03/01.png" width="476" height="139" /></a></p>

Reparem as mensagens de erro retornadas:

* [WebException: The remote server returned an error: (400) Bad Request.]
* [StorageClientException: One of the request inputs is out of range.]


Esta exceção ocorre no método CreateIfNotExist(), que cria a fila caso a mesma não exista. O trecho de código é o seguinte:

<p><a href="http://blob.vitormeriat.com.br/images/2011/03/2.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="2"   alt="2" src="http://blob.vitormeriat.com.br/images/2011/03/2.png" width="471" height="56" /></a></p>

Quando crio a fila, passo uma string para referenciar seu nome. O grande problema é que não pode ser qualquer string...

### A SOLUÇÃO

Existem algumas "limitações" na criação de Blobs, Tables e Queues no Azure. Neste caso, o nome referenciado para a fila desobedecia uma das regras de nomeação.

Na versão atual do SDK(1.4), os nomes de Fila devem seguir as seguintes regras:


* começar com uma letra ou número; 
* conter apenas letras, números e hífen(-);  
* primeira e a última letra deve ser alfanumérico;  
* não deve conter espaços;  
* o hífen não pode ser a primeira ou última letra do nome;  
* não é possível ter dois hífens consecultivos;  
* todas as letras devem ser minúsculas;  
* o nome da fila deve ter de 3 a 63 caracteres.

<p>&nbsp;</p>

<p align="justify">Se o nome da fila especificada não é um nome válido, o método Criar Fila retorna o código de status 400(Bad Request), juntamente com informações de erro adicionais.</p>
<p align="justify">Segue a lista com os Códigos de Erro nos Serviços de Fila:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/03/3.png"><img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="3"   alt="3" src="http://blob.vitormeriat.com.br/images/2011/03/3.png" width="485" height="333" /></a></p>
<p align="justify"><font size="3">Para solucionar</font> o erro da minha aplicação, eu simplesmente coloquei o nome da fila como <strong>All Lowercase </strong>(tudo em minúsculo)! </p>
<p align="justify">PS: A grande questão aqui é a mensagem de erro que não deixa claro o motivo da exceção. Não há sinalização de que o nome da fila é o reponsável pelo erro, logo há uma “curva maior” para identificar e tratar o erro.</p>
<p>Um grande abraço e ótimo estudo!
