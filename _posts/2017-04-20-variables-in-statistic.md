---
layout: post
title: "Variáveis em Estatística e Macnhine Learning"
date: 2017-04-20
categories:
    - Statistics
    - Data Science
description: "Esta é minha primeira impressão utilizando a linguagem R, usada por programadores e cientistas de dados com ênfase em computação estatísticas. Para começar com o pé direito, nada como implementar uma regressão linear para iniciar."
image: "http://meriatblob.blob.core.windows.net/images/2017/04/20/variables.png"
---


Em Machine Lerning falamos em estática, e para ambos existe um elemento fundamental: dados. Quando olhamos para os dados precisamos notar o que há de mais especial, e geralmente conseguimos isso identificando nossas variáveis. Descobrir o porquê de uma determinada variação é um bom início para qualquer problema estatístico.

> Uma variável é como uma pergunta que pode ter várias respostas possíveis.

Observe a tabela abaixo:

<table class="table-fill">
  <tbody>
    <tr>
      <th>Nome</th>
      <th>Idade</th>
    </tr>
    <tr>
      <td>Machado de Assis</td>
      <td>69</td>
    </tr>
    <tr>
      <td>Carlos Drummond de Andrade</td>
      <td>85</td>
    </tr>
     <tr>
      <td>Graciliano Ramos</td>
      <td>61</td>
    </tr>
     <tr>
      <td>Mário Quintana</td>
      <td>38</td>
    </tr>
     <tr>
      <td>Guimarães Rosa</td>
      <td>59</td>
    </tr>
  </tbody>
</table>

Em nosso contexto, vamos considerar as linhas como observações/recursos, e as colunas vamos chamar de variáveis. As perguntas que nossas variáveis respondem são: "Qual o seu nome?" e "Qual a sua idade?".

> Primeira dica: Apenas o título da variável não representa toda sua história.

**Como assim? O que você quer dizer com isso?**

Se olharmos para a variável idade, não sabemos se ela se refere a idade do escritor hoje, a idade no momento de algum escrito famoso ou se foi a idade que ele tinha na época de seu falecimento. 

Uma de nossas tarefas é investigar nossa fonte de dados em busca de compreender o verdadeiro significado de cada variável.

Outro ponto importante é saber identificar uma variável. Se neste contexto você me perguntar meu nome, vou te responder **Vitor**. Não importa quantas pessoas diferentes me perguntarem eu vou continuar respondendo Vitor. Neste caso meu nome não é uma variável, e sim uma constante.

Seguindo essa linha vamos ver que uma variável depende da pergunta que está sendo feita. A resposta para <u>"Qual a ordem em que os dias da semana ocorrem"</u> será uma constante. Sempre teremos a mesma ordem, terça sempre virá após a segunda e etc. Agora se pergunto <u>"Que dia é hoje"</u>, vamos ter como resposta uma variável, já que a resposta tem relação direta com o dia em que a pergunta é feita. <u>"Que dia hoje"</u> pode ser, segunda, terça, quarta... ou seja, teremos **várias** possíveis respostas corretas.

## Variáveis numéricas e categóricas

Podemos diferenciar variáveis pelo tipo de dado. Em estatística consideramos dois tipos de variáveis: **Númericas** e **Categóricas**.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/04/20/variables.png"></p>

Variáveis podem ser classificadas da seguinte forma:

1. **Variáveis Numéricas**: são as características que podem ser medidas em uma escala quantitativa, ou seja, apresentam valores numéricos que fazem sentido. Podem ser contínuas ou discretas.
    * __Variáveis discretas__: características mensuráveis que podem assumir apenas um número finito ou infinito contável de valores e, assim, somente fazem sentido valores inteiros. Geralmente são o resultado de contagens. Exemplos: número de filhos, número de bactérias por litro de leite, número de cigarros fumados por dia.
    * __Variáveis contínuas__, características mensuráveis que assumem valores em uma escala contínua (na reta real), para as quais valores fracionais fazem sentido. Usualmente devem ser medidas através de algum instrumento. Exemplos: peso (balança), altura (régua), tempo (relógio), pressão arterial, idade.

2. **Variáveis Categóricas**: são as características que não possuem valores quantitativos, mas, ao contrário, são definidas por várias categorias, ou seja, representam uma classificação dos indivíduos. Podem ser nominais ou ordinais.
    * __Variáveis nominais__: não existe ordenação dentre as categorias. Exemplos: sexo, cor dos olhos, fumante/não fumante, doente/sadio.
    * __Variáveis ordinais__: existe uma ordenação entre as categorias. Exemplos: escolaridade (1o, 2o, 3o graus), estágio da doença (inicial, intermediário, terminal), mês de observação (janeiro, fevereiro,..., dezembro).

> As distinções são menos rígidas do que a descrição acima nos apresenta.

Sendo assim, podemos definir que se o resultado a pergunta for numérica <u>("Qual a sua idade?")</u>, então temos uma variável numérica. Se a reposta não pode ser representada de forma númerica <u>("Qual a raça do seu cachorro?")</u>, então temos uma variável categórica. 

Uma variável originalmente numérica pode ser coletada de forma categórica. 
Por exemplo, a variável idade, medida em anos completos, é quantitativa (contínua); mas, se for informada apenas a faixa etária (0 a 5 anos, 6 a 10 anos, etc...), é qualitativa (ordinal). Outro exemplo é o peso dos lutadores de boxe, uma variável quantitativa (contínua) se trabalhamos com o valor obtido na balança, mas qualitativa (ordinal) se o classificarmos nas categorias do boxe (peso-pena, peso-leve, peso-pesado, etc.).

Outro ponto importante é que nem sempre uma variável representada por números é quantitativa/numérica.

O número do telefone de uma pessoa, o número da casa, o número de sua identidade. Às vezes o sexo do indivíduo é registrado na planilha de dados como 1 se macho e 2 se fêmea, por exemplo. Isto não significa que a variável sexo passou a ser quantitativa!

## Variáveis Codificadas

Eu não posso analisar diretamente uma sentença como <u>"Hoje é terça-feira"</u> em termos estatísticos. Quando nossa variável não é númerica, precisamos transformar cada resposta à nossa pergunta em um número, para que o mesmo possa ser analisado. Este processo de conversão é chamado de "codificação". Como codificar uma variável vai depender do seu tipo de dado.


http://leg.ufpr.br/~silvia/CE055/node9.html

http://survivestatistics.com/variables/

<style>
div.table-title {
  display: block;
  margin: auto;
  max-width: 600px;
  padding:5px;
  width: 100%;
}

.table-title h3 {
   color: #fafafa;
   font-size: 30px;
   font-weight: 400;
   font-style:normal;
   font-family: "Roboto", helvetica, arial, sans-serif;
   text-shadow: -1px -1px 1px rgba(0, 0, 0, 0.1);
   text-transform:uppercase;
}


/*** Table Styles **/

.table-fill {
  background: white;
  border-radius:3px;
  border-collapse: collapse;
  height: 320px;
  margin: auto;
  max-width: 600px;
  padding:5px;
  width: 100%;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
  animation: float 5s infinite;
}
 
th {
  color:#D5DDE5;;
  background:#1b1e24;
  border-bottom:4px solid #9ea7af;
  border-right: 1px solid #343a45;
  font-size:23px;
  font-weight: 100;
  padding:24px;
  text-align:left;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  vertical-align:middle;
}

th:first-child {
  border-top-left-radius:3px;
}
 
th:last-child {
  border-top-right-radius:3px;
  border-right:none;
}
  
tr {
  border-top: 1px solid #C1C3D1;
  border-bottom-: 1px solid #C1C3D1;
  color:#666B85;
  font-size:16px;
  font-weight:normal;
  text-shadow: 0 1px 1px rgba(256, 256, 256, 0.1);
}
 
tr:hover td {
  background:#4E5066;
  color:#FFFFFF;
  border-top: 1px solid #22262e;
  border-bottom: 1px solid #22262e;
}
 
tr:first-child {
  border-top:none;
}

tr:last-child {
  border-bottom:none;
}
 
tr:nth-child(odd) td {
  background:#EBEBEB;
}
 
tr:nth-child(odd):hover td {
  background:#4E5066;
}

tr:last-child td:first-child {
  border-bottom-left-radius:3px;
}
 
tr:last-child td:last-child {
  border-bottom-right-radius:3px;
}
 
td {
  background:#FFFFFF;
  padding:20px;
  text-align:left;
  vertical-align:middle;
  font-weight:300;
  font-size:18px;
  text-shadow: -1px -1px 1px rgba(0, 0, 0, 0.1);
  border-right: 1px solid #C1C3D1;
}

td:last-child {
  border-right: 0px;
}

th.text-left {
  text-align: left;
}

th.text-center {
  text-align: center;
}

th.text-right {
  text-align: right;
}

td.text-left {
  text-align: left;
}

td.text-center {
  text-align: center;
}

td.text-right {
  text-align: right;
}

</style>