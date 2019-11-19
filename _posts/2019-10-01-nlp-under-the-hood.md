---
layout: post
title: "NLP under the hood"
date: 2019-10-01
categories:
    - IA
    - Machine Learning
    - Data Science
    - NLP
tags:
    - ai
    - deep learning
    - nlp
    - data science
image: "https://meriatblob.blob.core.windows.net/draft/capa.png"
description: Esse trabalho se propõe a trazer uma introdução ao estudo do Processamento de Linguagem Natural, (Natural Language Processing). Minha intenção é olhar para sua base teórica enquanto disciplina. Sendo assim vamos passar por algumas definições e conceitos antes de avançar nas questões práticas. Vamos falar sobre compiladores, árvores sintáticas e suas complexidades. 
---

<div align="center" style="width: 100%;"><img src="https://meriatblob.blob.core.windows.net/draft/capa.png" style="margin-bottom: 0px !important;"></div>

# Introdução

O método científico supõe que a observação dos fatos seja anterior ao estabelecimento de uma hipótese e que os fatos observados sejam examinados sistematicamente mediante experimentação e uma teoria adequada.

Com isso em mente, se faz necessário o estudo de alguns pontos utilizados na disciplina de processamento de linguagem natural de forma a obter a base necessária para uma correta exploração e aplicação das possibilidades.

Esse trabalho se propõe a trazer uma introdução ao estudo do `Processamento de Linguagem Natural` (`Natural Language Processing`). Minha intenção é olhar para sua base teórica enquanto disciplina. Sendo assim vamos passar por algumas definições e conceitos antes de avançar nas questões práticas. Vamos falar sobre a estrutura de uma linguagem, compiladores, árvores sintáticas e as complexidades da linguagem natural antes do famoso mão na massa, até por que `talk is cheap, show me the code`.

Antes de iniciar, se faz importante informar que alguns dos termos utilizados serão apresentados em inlgês e português. Para que não seja causada nenhuma estranheza ao leitor, vou priorizar os termos técnicos em inglês, e achando necessário realizo a explicação/tradução do mesmo. Para facilitar a leitura, algumas referências serão colocadas durante o texto. As demais estão todas na sessão de **Referências** ao final deste texto.

<div style="margin-bottom: 5em; margin-top: 5em; background-color: #35d648; color: #382d2d">
<p style="padding: 1.8em; font-family: courier; font-size: 1.4em;">"Minha pátria é minha língua." <b>Fernando Pessoa</b></p>
</div>

# Conceituação base

Este tópico é de grande importância, visto que muito da problemática encontrada na linguagem natural e sua compreensão, fazem parte do domínio computacional. Sendo assim, nosso objetivo quanto pesquisadores em Processamento de Linguagem Natural também inclui a resolução desses desafios, o que nos leva a procurar uma correta compreensão de seus conceitos base.

## Teoria da comunicação

Os seres humanos são considerados animais sociais e como tal, sabemos que a linguagem é nossa principal ferramenta de comunicação. Sabemos que a música é tão remota quanto o início da comunicação verbalizada, mas a principal diferença está nos papéis exercidos. Enquanto os sinais sonoros emitidos por instrumentos rudimentares foram seguindo o caminho da subjetividade, os sons cada vez mais coordenados dos seres humanos foram seguindo para se tornarem mais claros. Partimos dos grunidos para linguagens extramamente sofisticadas.

Mesmo após tanta evolução na comunicação falada e escrita, ainda vemos que a linguagem é um assunto complexo. A linguagem é cheia de abstrações, fluída, ambígua e muitas vezes confusa. Apesar das definições gramaticais, a linguagem é um organismo vivo e se renova muito rapidamente. Diversos termos novos surgem a cada dia, e termos conhecidos recebem uma nova significância da forma já habitual.

Quando falamos em teoria da comunicação, em termos básicos temos o papel do emissor, receptor, mensagem, código, contexto e canal. Cada um desses componentes é importante para determinar uma comunicação de sucesso. Se o emissor enviar uma mensagem para um receptor usando um código que não é conhecido pelo mesmo, ou se o contexto for desconhecido pelo receptor, ou se o canal de comunicação for insuficiente, a comunicação pode ser ruidosa e falha. Se tudo isso ainda for certeiro, temos de levar em conta que a mensagem vai ser interpretada por um receptor que vai levar em consideração sua perspectiva de mundo.

<div align="center" style="width: 100%;">
<img src="https://meriatblob.blob.core.windows.net/draft/theory_of_communications_2.png" style="margin-bottom: 0px !important;">
</div>
<div align="center" style="width: 100%;">
<img src="https://meriatblob.blob.core.windows.net/draft/theory_of_communications.jpg" style="margin-bottom: 0px !important;">
</div>

1. A fonte (**source**) produz uma mensagem. Uma mensagem pode ser um sinal de fumaça, telégrafo, rádio e etc.
2. Um transmissor (**transmitter**) traduz a mensagem em um sinal que possa ser enviado por um meio específico.
3. O canal (**medium**) é apenas o meio usado para transmitir o sinal do transmissor para o receptor. Pode ser um par de fios, um cabo coaxial, banda de radiofrequência, feixe de luz e etc.
4. O ruído (**noise**) é tudo aquilo que possa interferir no sinal.
5. O receptor (**receiver**) normalmente executa a operação inversa da realizada pelo transmissor, reconstruindo a mensagem a partir do sinal, para que o destino possa compreender.
6. O destino (**destination**) é a pessoa/coisa a quem a mensagem se destina.

## Linguística básica e nomenclaturas

Se tratando em linguística, temos o estudo sobre o uso e funcionamento das línguas naturais, independentemente da sua especificidade e diversidade. Nesta ciência possuímos diversas nomenclaturas, para nosso objetivo, precisamos conhecer os itens abaixo:

* **Língua**: Podemos definir que a língua é, sobretudo, um instrumento de comunicação, e é essa a sua maior finalidade. Uma de suas riquezas e dificuldades, é que embora existam as normas gramaticais que regem um idioma, cada falante opta por uma forma de expressão que mais lhe convém, originando aquilo que chamamos de fala. A fala, embora possa ser criativa, deve ser regida por regras maiores e socialmente estabelecidas, caso contrário, cada um de nós criaria sua própria língua, o que impossibilitaria a comunicação. Na fala encontramos as variações linguísticas, visto que a língua é viva e dinâmica.

* **Idioma**: É uma língua própria de um povo. Está relacionado com a existência de um Estado político, sendo utilizado para identificar uma nação em relação às demais. Existem países, como o Canadá, por exemplo, em que dois idiomas são considerados como oficiais, nesse caso, o francês e o inglês.

* **Dialeto**: Por dialeto, temos o estudo da variedade de uma língua própria de uma região ou território e está relacionado com as variações linguísticas encontradas na fala de determinados grupos sociais. As variações linguísticas podem ser compreendidas a partir da análise de três diferentes fenômenos: exposição aos saberes convencionais (diferentes grupos sociais com maior ou menor acesso à educação formal utilizam a língua de maneiras diferentes); situação de uso (os falantes adequam-se linguisticamente às situações comunicacionais de acordo com o nível de formalidade) e contexto sociocultural (gírias e jargões podem dizer muito sobre grupos específicos formados por algum tipo de “simbiose” cultural).

* **Fonética**: Podemos dizer que a fonética é o estudo da realidade acústica, do funcionamento articulatório e anatómico e da interpretação percetiva dos sons de uma determinada língua natural.

* **Fonologia**: É o estudo do sistema sonoro de uma língua, das regras subjacentes à combinação desses sons e do modo como esses sons exprimem distinções de significado.

* **Morfologia**: A morfologia é a área da linguística que faz o estudo da formação e da estrutura interna das palavras dada uma determinada língua.

* **Sintaxe**: Estudo das regras subjacentes à organização das palavras numa frase gramaticalmente bem formada. Refere-se à estrutura das frases. Regras pelas quais palavras podem ser combinadas em frases gramaticalmente aceitáveis.

* **Semântica**: Estudo do significado da produção e interpretação de palavras e frases. As regras definidas na semântica servem para definir os significados de morfemas, palavras e frases, indivíduos e sentenças. Reconhecimento de palavras e sentenças ambíguas, anômalas, paráfrases, etc.

* **Pragmática**: Estudo do uso da língua em contexto por oposição ao estudo do sistema da língua. Nela temos a percepção das regras que governam o uso da linguagem em contextos sociais, o que inclui o conhecimento de tipos de sentenças que são mais adequados para produzir resposta desejada, percepção da informação de fundo necessária para transmitir a mensagem visada e o entendimento dos princípios cooperativos que estão por trás das trocas na conversação.

* **Gramática**: A gramática formaliza a língua, seja realizando sua descrição, seja traçando as normas para o seu uso. A linguística analisa os fatos da língua na sua situação de uso e tenta explicá-los. Ambas tratam do mesmo assunto, mas sob ângulos diferentes.

* **Semiótica**: Por semiótica temos o estudo dos signos, o que abrange todos os elementos que representam algum significado e sentido para o ser humano, abarcando as linguagens verbais e não-verbais.

Com estes itens em mente, podemos prosseguir para nosso estudo visando nos aprofundar na teoria.

## Influências e formação da linguagem

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/lusofonos.jpg" style="margin-bottom: 0px !important; width: 80%;">
<p>ilustração: Guilhere Lira/Mundo Estranho</p>
</div>

Vamos fazer um exercício olhando para nossa lingua natal. Quantos países têm a lingua portuguesa como sua lingua mater? Desses países, todos falam exatamente a mesma lingua? Se iniciarmos uma comparação básica entre o que é falado no Brasil, Portugal, Moçanbique e Angola, haverá muita diferença?

As grandes diferenças são as influências de línguas nativas e estrangeiras, que resultam em palavras e expressões particulares. O português brasileiro tem influência de línguas indígenas e de vários idiomas externos utilizados pelos os imigrantes, como árabes e italianos.

Em Angola, há 11 línguas e diversos dialetos que transformam o português incluindo diveras palavras ao vocabulário. Em Moçambique, o português é influenciado pelas 20 línguas locais. Apesar de ser o idioma oficial do país, em Moçambique ele é falado por apenas 40% da população. O português de Portugal possui grandes diferenças em relação ao portugês brasileiro. Em questões gramaticais, o português de Angola e Moçambique são mais próximos do português europeu do que o brasileiro.

> Por tudo isso, nos três países, há regionalismos que podem deixar o idioma incompreensível mesmo entre os lusófonos.

Por exemplo, aqui no Brasil nós adoramos abusar do tempo verbal gerúndio, muito pouco usado em outros países em questão. Por exemplo, usamos a frase **"estou fazendo isso"** no lugar de **"estou a fazer isso"**. Há também o `gerundismo` (uso desnecessário do gerúndio) como em **"vamos estar averiguando"**.

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/same-language.jpg" style="margin-bottom: 0px !important; width: 80%;">
<p> ilustração: Pilar Hernandez</p>
</div>

Outro país onde a língua portuguesa sofre diversas alterações com base nas regras gramaticias das línguas locais é Moçambique. Como exemplo podemos usar o caso do verbo **"nascer"**, que lá é usado como na língua **changana**: **"Meus pais nasceram minha irmã"**. O mesmo vale para **"Nos disseram que hoje não há aula"**, que fica: **"Nós fomos ditos que hoje não há aulas"**.

Essas estruturas são fundamentais para um correto entendimento e aplicação dos fundamentos em processamento de linguagem natural.

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/luis_de_camoes.png" style="margin-bottom: 0px !important;">
<p>Luís de Camões, considerado um dos maiores escritores de língua portuguesa e ainda, um dos maiores representantes da literatura mundial.</p>
</div>

## História

Quando como seres humanos cientes de nossa colocação no mundo nos preocupamos com o estudo da linguagem? Mais ainda, por que isso seria interessante? Este é um bônus, um ponto importante para ilustrar não só a mutabilidade como o papel da linguagem na construção e identidade de uma sociedade. A curiosidade humana sobre a linguagem é remoto e pode ser percebido por meio de vários mitos, lendas e rituais antigos.

O início dessa jornada data do século IV a.c, onde os religiosos hindus iniciaram um estudo da língua a fim de preservar os textos sagrados do Veda. Esses estudos levaram a uma rápida evolução, e mais tarde o gramático Panini (século IV a.c.) em conjunto com outros estudiosos, produziram modelos de análise dado uma minunciosa descrição da própria língua. Estes modelos só foram descobertos pelo ocidente no final do século XVIII, quando principalmente os gregos se propuseram a definir as relações entre o conceito e a palavra que o designa.

Sendo assim os gregos levaram o estudo da linguagem a outro nível. Eles questionaram coisas como: existe relação necessária entre a palavra e o seu significado? Podemos ver Platão discutindo esse ponto específico no Crátilo. Aristóteles desenvolveu estudos em outro foco, tentando proceder a uma análise precisa da estrutura linguística, chegando a elaborar uma teoria sobre distinguir as partes do discurso e a enumerar as categorias gramaticais.

Entre estudiosos latinos, temos como destaque Varrão que, na esteira dos gregos, dedicou-se à gramática, em um esforço para defini-la como ciência e arte.

> No século XVI, a religiosidade ativada pela Reforma provoca a tradução dos livros sagrados em numerosas línguas, apesar de manter-se o prestígio do latim como língua universal. Viajantes, comerciantes e diplomatas trazem de suas experiências no estrangeiro o conhecimento de línguas até então desconhecidas. Em 1502 surge o mais antigo dicionário poliglota, do italiano Ambrosio Calepino. "Introdução à linguística Volumes 1 e 2, José Luiz Fiorin"

Em relação ao período moderno, podemos citar Franz Bopp como um dos principais criadores da gramática comparada. Sua obra publicada em 1816 se intitulava: `Über das Conjugationssystem der Sanskritsprache in Vergleichung mit jenem der griechischen, lateinischen, persischen und germanischen Sprache` **(Sobre o sistema de conjugação do sânscrito em comparação com o do grego, latim, persa e germânico)**. Esse trabalho evidenciou diversas semelhanças entre as línguas em questão.

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/indo-european-tree.jpeg" style="margin-bottom: 0px !important;">
<p>ilustração: Minna Sundberg</p>
</div>

Ao expor as semelhanças entre essas línguas, foi notório uma relação de parentesco que originou o que hoje chamamos de família `indo-européia`, em que existe uma origem comum, comprovada pelo método histórico-comparativo.

Somente no início do século XX a Linguística ganhou status de estudo científico. Como estudo ela sempre foi um anexo em estudos de lógica, filosofia, retórica, história ou crítica literária. O marco foi a divulgação dos trabalhos de Ferdinand de Saussure, professor da Universidade de Genebra. Em 1916, dois alunos de Saussure, a partir de anotações de aula, publicam o Curso de Lingüística geral, obra fundadora da nova ciência.

# Linguagem Natural e sua Complexidade

A complexidade envolvida na linguagem natural passa por sua estruturação formal (gramática), até as questões mais subjetivas como interpretação. Adicione a isso o fato que temos diversas linguagens no mundo, todas com estruturas e significâncias diferentes. Se isso ainda não for suficiente, ainda temos toda a problemática envolvendo as questões de engenharia, como por exemplo, processar grandes quantidades de texto.

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/linguistics_club.png" style="margin-bottom: 0px !important;">
<p>ref: https://www.xkcd.com/1602/</p>
</div>

No exemplo acima, temos uma anedota em torno da palavra **sesquiannual**, que representa um período de 18 meses. O punch aqui é que somente uma pessoa que conhece o significa dessa palavra sabe quando o encontro vai acontecer. Este é um exemplo simples onde temos uma palavra que pertence domínio geral da língua, está nos presente nos dicionários porém não é de uso comum da população.

## Compreensão semântica

O estudo da semântica alude à parte da linguagem referente ao significado das palavras e expressões que a mesma pode gerar. Neste contexto, cada palavra possui uma semântica própria, que difere da sua classificação enquanto função sintática ou morfológica.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
A comunicação humana está essencialmente ligada à capacidade de utilizar meios <b>semióticos</b> (como a linguagem) para transmitir as <b>"intenções comunicativas"</b> de um indivíduo e a capacidade de reconhecer tais intenções. DASCAL, Marcelo. Interpretação e compreensão. 2006
</p>
</div>

Contudo, de maneira geral, a semântica não é tratada de forma isolada em cada palavra, mas sim generalizada a contextos mais amplos. Sendo assim, ao considerar um diálogo, podemos identificar um significado particular em cada frase e um significado mais geral pertinente ao assunto tratado pelas pessoas que promovem o diálogo. Da mesma forma, em um texto dissertativo, mesmo considerando que cada parágrafo possa expressar um sentido particular, é somente com a junção de todas as sentenças que poderemos formar o sentido de um determinado texto.

Podemos concluir que a função base de uma linguagem é a comunicação, e esta está centrada na significância das expressões linguísticas produzidas. Como isto, o estudo da semântica ganha papel de fundamento para as implementações computacionais que envolvem compreensão e produção de linguagem. Isso dialóga diretamente com as dificuldades da envolvidas no processamento da linguagem natural, uma vez que nós utilizamos a intuição na compreensão do sentido de um determinado texto, algo que é discutível quando falamos de sua aplicação prática na computação.

<style>
.wrapper {
  display: flex;  
  flex-flow: row wrap;
  font-weight: bold;
  text-align: center;
  background: #9865d0;
  color: #ffffff;
  margin: 4em 0 4em 0;
}

.wrapper > * {
  padding: 10px;
  flex: 1 100%;
}

.main {
  font-size: 1.8em;
  display: -webkit-flex;
  display: flex;
  -webkit-align-items: center;
  align-items: center;
  -webkit-justify-content: center;
  justify-content: center;
}

.aside-1 {
  font-size: 0.8em;
}

@media all and (min-width: 600px) {
  .aside { flex: 1 0 0; }
}

@media all and (min-width: 800px) {
  .main    { flex: 3 0px; }
  .aside-1 { order: 1; } 
  .main    { order: 2; }
}
</style>

<div class="wrapper">
  <article class="main">
    <p>Como trabalhar o correto entendimento de um texto em uma máquina baseada na arquitetura de Von Neumman?</p>  
  </article>
  <aside class="aside aside-1">
	  <img src="https://meriatblob.blob.core.windows.net/draft/von-neumann.png" style="margin-bottom: 0px !important;">
	  <p>Von Neumman</p>
  </aside>
</div>

Um teste simples utilizando qualquer um dos grandes tradutores online da atualidade vai nos mostrar que a tradução obtida, na maioria dos casos apresenta diversas deficiências. Mesmo que isso não compremeta a compreensão geral do contexto da tradução, se faz necessário a revisão humana para uma correta compreensão do mesmo. 

> O que temos de pontuar aqui, é que o processamento e tratamento computacional da linguagem natural precisa transpassar diversas barreiras, as mesmas que são típicas da comunicação humana.

Essas dificuldades são tratadas pelo cérebro de forma natural, embora já conhecemos os ríscos que estão associados a comunicação humana, por mais eficiênte que ela possa se dar.

# Natural Language Processing

Partindo para a área computacional, podemos conceituar `NLP` da seguinte maneira:

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
<b>Natural Language Processing</b> é a disciplina que consiste no desenvolvimento de modelos computacionais que utilizam informação expressa em uma determinada língua natural.
</p>
</div>

Como objetivo, podemos definir que em `NLP`, queremos construir mecanismos artificiais que permitem o entedimento da linguagem natural para a realização de tarefas que visam simular um comportamento humano (e.g. tradução e interpretação de textos, busca de informações em documentos, detecção de tópicos).

`NLP` se encaixa no mundo da computação como uma subárea de Inteligência Artificial, e constantemente associada a Linguística Computacional, embora sejam matérias diferentes.

Quando comparamos as aplicações desenvolvidas nessas duas áreas, é fácil entender a confusão. Geralmente compartilham as mesmas conferências, colaboram em artigos, mas tem como essência, objetivos diferentes.

* **CL** – Computational Linguistics
  * **Profissional:** Linguistas
  * **Objetivo:** Uso da computação para o estudo da linguagem
* **NLP** – Natural Language Processing
  * **Profissional:** Cientistas da Computação
  * **Objetivo:** Aplicações envolvendo linguagem natural

## Computational Linguistics

Como matéria segue a linha das ciências naturais como à biologia computacional, e se propõem a desenvolver métodos computacionais a fim de responder às questões científicas sobre linguística.

As questões centrais da linguística envolvem a natureza das representações linguísticas e do conhecimento linguístico, e como o conhecimento linguístico é adquirido e implantado na produção e compreensão da linguagem. Responder a essas perguntas descreve a capacidade da linguagem humana e pode ajudar a explicar a distribuição de dados e comportamentos linguísticos que realmente observamos.

Na linguística computacional, são propostas respostas formais para essas questões. Os linguistas estão realmente perguntando o que e como os humanos estão associando. Por isso, definimos matematicamente classes de representações linguísticas e gramáticas formais (ou seja, modelos probabilísticos) que parecem adequadas para capturar a variedade de fenômenos presentes nas línguas humanas. São estudadas suas propriedades matemáticas a fim de guiar o desenvolvimento de algoritmos eficientes para o aprendizado, produção e compreensão da linguagem natural.

## NLP, uma questão de engenharia

Em comparação com o a linguística computacional, podemos perceber que enquando a `CL` foca na descoberta de fatos linguísticos, a `NLP` tem seu foco no desenvolvimento de tecnologias utilizando linguagem natural.

Em muitos casos isso é visto como uma questão de ciência versus engenharia. Não se trata de provar que as línguas X ou Y estão relacionadas historicamente. Tem mais ligação com as questões práticas e como produzir ferramentas que vão ajudar as pessoas a se comunicarem melhor (seja com o computar ou entre si), bem como trabalhar e extrair conhecimento da quantidade incomensurável de informação em linguagem natural que temos hoje.

Dado sua natureza prática, `NLP` é muito relacionada a questões comerciais embora tenha um papel importante em outras ciências possibilitando análises que hoje são consideradas fundamentas em áreas como política, medicina e econômia.

## E sobre Natrual Language Understanding?

Podemos enquadrar `NLU` como uma subárea em `NLP`. Para uma boa aplicação baseada em processamento de linguagem natural, um bom **entendimento da linguagem** é simplesmente fundamental.

## Linguagem de programação e sua relação com NLP

Quando falamos de NLP, existe uma correlação com a Linguagem de programação que é pouco explorada. Antes de entrar no aspecto técnico, podemos citar um exemplo emblemático.

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/imitation-game.png" style="margin-bottom: 0px !important;">
<p>ref: Computing Machinery and Intelligence, A. M. Turing</p>
</div>

Em meados de 1950, nos primordios da computação como conheçemos hoje, Alan Turing escreveu o famoso artigo que mais tarde ficou famoso como o teste de Turing. Basicamente ele sugere que um computador pode ser considerado inteligênte caso ele consiga por meio de uma interface conversacional, manter um diálogo com um ser humano sem que o mesmo consiga identificar que se trata de uma máquina. 

É nesta época, em conjunto com a evolução da linguagem de programação que temos os primeiros programadores experimentando entradas simples de linguagem escrita para executar tarefas computacionais. Uma década após, se inicia um movimento de pesquisas sobre a utilização de textos mais próximos da linguagem natural como input para tarefas computacionais.

Grande parte do interesse nessa atividade veio da possibilidade de dar ao usuário comum, o poder de interagir com a máquina a fim de realizar tarefas e obter informações sem a necessidade de programação explícita. Isso vai se tornar popular no imaginário mundial, por meio de obras SyFy (Science Fiction) como o grande clássico de Kubrick, 2001: A Space Odyssey. Esse filme de 1968 em particular, possui diversos diálogos entre homem e máquina. O nível de compreensão exibido pelo famoso computador HAL9000 é até hoje impensável.

<div align="center" style="font-size: 0.8em; font-family: courier;">
<img style="width: 100%;" src="https://ichef.bbci.co.uk/wwfeatures/wm/live/1600_640/images/live/p0/63/9f/p0639ffn.jpg">
<p>ref: 2001: A Space Odyssey. 1968, Stanley Kubrick</p>
</div>

Saindo da história para a engenharia, em grande parte o entendimento da estrutura interna de uma linguagem de programação traça um bom paralelo com a utilização da linguagem natural na computação. Em ambos os casos para um correto entendimento precisamos conhecer as regras que as formam. Novamente em ambos os casos, essas regras são definidas pelo que chamamos de gramática.

## Gramática

Já vimos que a gramática é o conjunto de regras que indicam o uso mais correto de uma língua. No início, a gramática tinha como função apenas estabelecer regras quanto à escrita e à leitura. É por isso que a palavra gramática, de origem grega (grámma), significa “letra”.

No estudo da língua podemos definir 4 tipos de gramáticas: normativa, descritiva, histórica e comparativa. Ao mesmo tempo, a gramática da língua portuguesa é dividida em fonologia, morfologia e sintaxe, sendo que muitos gramáticos ainda incluem nesse pacote a semântica.

Uma vez que enxergamos a gramática como uma especiﬁcação formal da estrutura geral de numa linguagem, podemos definir uma maneira simples de implementação que funciona para a criação de qualquer linguagem. Primeiro precisamos de um mecanismo que denote as palavras da linguagem, podemos chamar essa mecanismo de símbolos terminais. O próximo mecanismo será utilizado para denotar os componentes de uma sentença. Vamos chamá-los de símbolos não terminais. Para que isso possa ser aplicável, temos um conjunto de regras de produção, que expandem os símbolos não-terminais em uma sequência de símbolos terminais e não-terminais. Com isso a gramática de se iniciar com um símbolo não-terminal inicial. No exemplo abaixo, temos uma gramática que deﬁne um fragmento da língua portuguesa:

**Gramática 1.**

* frase ⇒ sujeito predicado
* sujeito ⇒ artigo substantivo
* predicado ⇒ verbo artigo substantivo
* artigo ⇒ o
* substantivo ⇒ gato > rato
* verbo ⇒ caçou

Nessa gramática, os símbolos terminais são o, gato e rato, sendo os demais símbolos não-terminais. A regra de produção frase ⇒ sujeito predicado estabelece que uma frase é composta de um sujeito seguido de um predicado; enquanto a regra substantivo ⇒ gato > rato estabelece que um substantivo pode ser a palavra “gato” ou “rato”. Além disso, para essa gramática, o símbolo não-terminal inicial será frase. Nas gramáticas livres de contexto (do tipo que consideramos nesse artigo), o lado esquerdo de uma regra de produção será sempre um único símbolo não terminal, enquanto o lado direito pode conter símbolos terminais e não terminais. Como veremos a seguir, uma gramática pode ser usada tanto para reconhecimento, ou seja, para decidir se essa frase pertence à linguagem deﬁnida pela gramática; quanto para geração, ou seja, para construir uma frase pertencente à linguagem deﬁnida pela gramática.

---

1. Normativa: A gramática normativa é sinônimo de norma culta. Ela estabelece os usos certos e errados em oposição ao uso popular. Isso porque, apesar de ser compreensível, no cotidiano, há sérias transgressões ao modelo estabelecido. Essa é a gramática oficial e, que portanto, é ensinada nas escolas.

2. Descritiva: A gramática descritiva analisa a língua com o objetivo de entender as suas alterações com o passar do tempo, especialmente em decorrência do seu uso oral.

3. Histórica: A gramática histórica trata justamente da história da língua, desde a sua origem às transformações.

4. Comparativa: A gramática comparativa estuda a gramática fazendo uma comparação com as gramáticas pertencentes às mesmas famílias linguísticas.

O português pertence à família das línguas indo-europeias, em que se inclui as línguas itálicas. São exemplos as línguas espanhola e francesa.

Trabalhar com NLP é um assunto como desafios complexos, como por exemplo, podemos pensar de forma intuítiva na criação de um sistema de perguntas simples e suas respostas. A forma ingenua seria construir um sistema baseado na busca de termos, palavras chave ou padrões de palavras. Essa é uma atividade relativamente fácil, principalmente pela capacidade computacional que temos hoje. Já se pensarmos no mesmo sistema construído para responder perguntas complexas, precisamos solucionar outros problemas com as inferências.

Conforme, a pesquisa em Pln está voltada, essencialmente, a três aspectos da comunicação em língua natural:

* som: fonologia
* estrutura: morfologia e sintaxe
* signiﬁcado: semântica e pragmática

A fonologia está relacionada ao reconhecimento dos sons que compõem as palavras de uma língua.

A morfologia reconhece as palavras em termos das unidades primitivas que a compõem (e.g. caçou → caç+ou).

A sintaxe deﬁne a estrutura de uma frase, com base na forma como as palavras se relacionam nessa frase (ﬁgura 1).

A semântica associa signiﬁcado a uma estrutura sintática, em termos dos signiﬁcados das palavras que a compõem (e.g. à estrutura da ﬁgura 1, podemos associar o signiﬁcado “um animal perseguiu/capturou outro animal”). Finalmente, a pragmática veriﬁca se o signiﬁcado associado à uma estrutura sintática é realmente o signiﬁcado mais apropriado no contexto considerado (e.g. no contexto predador-presa, “perseguiu/capturou” → “comeu”).

![0](https://meriatblob.blob.core.windows.net/draft/nlp-001.png)

Como podemos ver a PNL é uma área da pesquisa muito vasta, que envolve diversas disciplinas do conhecimento humano. Neste artigo vou abordar apenas a análise sintática de algumas frases em português. O objetivo é definir uma gramática capaz de gerar um conjunto finito de sentenças e decidir se uma determinada sentença pertence ou não à linguagem definida nesta gramática. Em seguida, vamos estender essa gramática para tratar concordância de gênero e número, bem como tempos verbais. Com isso conseguimos montar uma árvore sintática de uma sentença de forma automática.

> Se a comunicação é algo complexo mesmo para nós os seres humanos, como podemos trabalhar isso em computação?

Bom, o primeiro passo é transformar a nossa linguagem natural em algo que possa ser trabalhado por máquina. Fazemos isso transformando nosso dado textual em algum padrão de representação numérica, algo que seja processável e compreendido por uma máquina. Somente realizando esse passo é possível iniciar o processo de examinar os dados para criação de modelos matemáticos.

---

# Conlusão

Existe muita confusão quanso se fala em NLP. Temos diversas terminologias e conceitos que são errôneamente relacionados a essa materia. NLP é um campo onde uma certa complexidade está associada, então um correto entendimento dos conceitos é fundamental para conseguir atingir um nível avançado de trabalho. 

Fora isso a pesquisa e desenvolviemnto explorando o estado da arte em NLP requer um forte conhecimento em áreas como a linguística, uma vez diversos dos problemas que hoje queremos resolver, extrapolam a engenharia para algo mais conceitual.

# Referências

* Computational Linguistics and Natural Language Processing, Jun’ichi Tsujii, University of Tokyo
* Introduction to Computational Linguistics, Jason Eisner, Johns Hopkins University
* Interpretação e compreensão. Marcelo DASCAL
* SILVA, M.C.S; KOCH, I.V. Linguística Aplicada ao Português: Morfologia. 18ª ed. – São Paulo: Cortez, 2012.
* Diferenças entre língua, idioma e dialeto; PEREZ, Luana Castro Alves, Brasil Escola.
* Introdução à linguística Volumes 1 e 2, José Luiz Fiorin
* A Mathematical Theory of Communication, C. E. SHANNON, harvard
* A Mind at Play: How Claude Shannon Invented the Information Age, Jimmy Soni and Rob Goodman
* Computing Machinery and Intelligence, A. M. Turing, [link](https://www.csee.umbc.edu/courses/471/papers/turing.pdf)
* Introdução a semiótica, José David Campos Fernandes, [link](http://www.cchla.ufpb.br/clv/images/docs/modulos/p8/p8_4.pdf)
