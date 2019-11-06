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

O método científico supõe que a observação dos fatos seja anterior ao
estabelecimento de uma hipótese e que os fatos observados sejam examinados sistematicamente mediante experimentação e uma teoria adequada.

Com isso em mente, se faz necessário o estudo de alguns pontos utilizados na disciplina de processamento de linguagem natural de forma  a obter a base necessária para uma correta exploração e aplicação das possibilidades.

Esse trabalho se propõe a trazer uma introdução ao estudo do `Processamento de Linguagem Natural` (`Natural Language Processing`). Minha intenção é olhar para sua base teórica enquanto disciplina. Sendo assim vamos passar por algumas definições e conceitos antes de avançar nas questões práticas. Vamos falar sobre a estrutura de uma linguagem, compiladores, árvores sintáticas e as complexidades da linguagem natural antes do famoso mão na massa, até por que `talk is cheap, show me the code`.

Antes de iniciar, se faz importante informar que alguns dos termos utilizados serão apresentados em inlgês e português. Para que não seja causada nenhuma estranheza ao leitor, vou priorizar os termos técnicos em inglês, e achando necessário realizo a explicação/tradução do mesmo. Para facilitar a leitura, algumas referências serão colocadas durante o texto. As demais estão todas na sessão de **Referências** ao final deste texto.

<div style="margin-bottom: 4em; margin-top: 4em; background-color: #35d648; color: #382d2d">
<p style="padding: 1.8em; font-family: courier; font-size: 1.4em;">
“Minha pátria é minha língua.” <b>Fernando Pessoa</b>
</p>
</div>

## Conceituação e história

Este tópico é de grande importância, visto que muito da problemática encontrada na linguagem natural e sua compreensão, fazem parte do domínio computacional. Sendo assim, nosso objetivo quanto pesquisadores em Processamento de Linguagem Natural também inclui a resolução desses desafios.

### Teoria da comunicação

Os seres humanos são considerados animais sociais e como tal, sabemos que a linguagem é nossa principal ferramenta de comunicação. Sabemos que a música é tão remota quanto o início da comunicação verbalizada, mas a principal diferença está nos papéis exercidos. Enquanto os sinais sonoros emitidos por instrumentos rudimentares foram seguindo o caminho da subjetividade, os sons cada vez mais coordenados dos seres humanos foram seguindo para se tornarem mais claros. Partimos dos grunidos para linguagens extramamente sofisticadas.

Mesmo após tanta evolução na comunicação falada e escrita, ainda vemos que a linguagem é um assunto complexo. A linguagem é cheia de abstrações, fluída, ambígua e muitas vezes confusa. Apesar das definições gramaticais, a linguagem é um organismo vivo e se renova muito rapidamente. Diversos termos novos surgem a cada dia, e termos conhecidos recebem uma nova significância da forma já habitual.

Quando falamos em teoria da comunicação, em termos básicos temos o papel do emissor, receptor, mensagem, código, contexto e canal. Cada um desses componentes é importante para determinar uma comunicação de sucesso. Se o emissor enviar uma mensagem para um receptor usando um código que não é conhecido pelo mesmo, ou se o contexto for desconhecido pelo receptor, ou se o canal de comunicação for insuficiente, a comunicação pode ser ruidosa e falha. Se tudo isso ainda for certeiro, temos de levar em conta que a mensagem vai ser interpretada por um receptor que vai levar em consideração sua perspectiva de mundo.

<div align="center" style="width: 100%;">
<img src="https://meriatblob.blob.core.windows.net/draft/theory_of_communications_2.png" style="margin-bottom: 0px !important;">
</div>
<div align="center" style="width: 100%;">
<img src="https://meriatblob.blob.core.windows.net/draft/theory_of_communications.png" style="margin-bottom: 0px !important;">
</div>

1. A fonte (**source**) produz uma mensagem. Uma mensagem pode ser um sinal de fumaça, telégrafo, rádio e etc.
2. Um transmissor (**transmitter**) traduz a mensagem em um sinal que possa ser enviado por um meio específico.
3. O canal (**medium**) é apenas o meio usado para transmitir o sinal do transmissor para o receptor. Pode ser um par de fios, um cabo coaxial, banda de radiofrequência, feixe de luz e etc.
4. O ruído (**noise**) é tudo aquilo que possa interferir no sinal.
5. O receptor (**receiver**) normalmente executa a operação inversa da realizada pelo transmissor, reconstruindo a mensagem a partir do sinal, para que o destino possa compreender.
6. O destino (**destination**) é a pessoa/coisa a quem a mensagem se destina.

### Linguística base

Se tratando em linguística, temos o estudo sobre o uso e funcionamento das línguas naturais, independentemente da sua especificidade e diversidade. Nesta ciência possuímos diversas nomenclaturas, para nosso objetivo, precisamos conhecer os itens abaixo:

* **Língua**: Podemos falar que a língua é, sobretudo, um instrumento de comunicação, e é essa a sua maior finalidade. Uma de suas riquezas e dificuldades, é que embora existam as normas gramaticais que regem um idioma, cada falante opta por uma forma de expressão que mais lhe convém, originando aquilo que chamamos de fala. A fala, embora possa ser criativa, deve ser regida por regras maiores e socialmente estabelecidas, caso contrário, cada um de nós criaria sua própria língua, o que impossibilitaria a comunicação. Na fala encontramos as variações linguísticas, visto que a língua é viva e dinâmica.

* **Idioma**: É uma língua própria de um povo. Está relacionado com a existência de um Estado político, sendo utilizado para identificar uma nação em relação às demais. Existem países, como o Canadá, por exemplo, em que dois idiomas são considerados como oficiais, nesse caso, o francês e o inglês.

* **Dialeto**: Variedade de uma língua própria de uma região ou território e está relacionado com as variações linguísticas encontradas na fala de determinados grupos sociais. As variações linguísticas podem ser compreendidas a partir da análise de três diferentes fenômenos: exposição aos saberes convencionais (diferentes grupos sociais com maior ou menor acesso à educação formal utilizam a língua de maneiras diferentes); situação de uso (os falantes adequam-se linguisticamente às situações comunicacionais de acordo com o nível de formalidade) e contexto sociocultural (gírias e jargões podem dizer muito sobre grupos específicos formados por algum tipo de “simbiose” cultural).

* **Fonética**: Estudo da realidade acústica, do funcionamento articulatório e anatómico e da interpretação percetiva dos sons de uma determinada língua natural.

* **Fonologia**: Estudo do sistema sonoro de uma língua, das regras subjacentes à combinação desses sons e do modo como esses sons exprimem distinções de significado.

* **Morfologia**: Estudo da formação e da estrutura interna das palavras na língua.

* **Sintaxe**: Estudo das regras subjacentes à organização das palavras numa frase gramaticalmente bem formada.

* **Semântica**: Estudo do significado da produção e interpretação de palavras e frases.

* **Pragmática**: Estudo do uso da língua em contexto por oposição ao estudo do sistema da língua.

### Influências e formação da linguagem

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/lusofonos.jpg" style="margin-bottom: 0px !important; width: 80%;">
<p>ilustração: Guilhere Lira/Mundo Estranho</p>
</div>

Vamos fazer um exercício olhando para nossa lingua natal. Quantos países têm a lingua portuguesa como sua lingua mater? Desses países, todos falam exatamente a mesma lingua? Se iniciarmos uma comparação básica entre o que é falado no Brasil, Portugal, Moçanbique e Angola, haverá muita diferença?

As grandes diferenças são as influências de línguas nativas e estrangeiras, que resultam em palavras e expressões particulares. O português brasileiro tem influência de línguas indígenas e de vários idiomas externos utilizados pelos os imigrantes, como árabes e italianos.

Em Angola, há 11 línguas e diversos dialetos que transformam o português incluindo diveras palavras ao vocabulário. Em Moçambique, o português é influenciado pelas 20 línguas locais. Apesar de ser o idioma oficial do país, em Moçambique ele é falado por apenas 40% da população. O português de Portugal possui grandes diferenças em relação ao portugês brasileiro. Em questões gramaticais, o português de Angola e Moçambique são mais próximos do português europeu do que o brasileiro.

> Por tudo isso, nos três países, há regionalismos que podem deixar o idioma incompreensível mesmo entre os lusófonos.

Por exemplo, aqui no Brasil nós adoramos abusar do tempo verbal gerúndio, muito pouco usado em outros países em questão. Por exemplo, usamos a frase **"estou fazendo isso"** no lugar de **"estou a fazer isso"**. Há também o gerundismo (uso desnecessário do gerúndio) como em **"vamos estar averiguando"**.

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/same-language.jpg" style="margin-bottom: 0px !important; width: 80%;">
<p> ilustração: Pilar Hernandez</p>
</div>

Em Moçambique, a língua portuguesa também sofre modificações baseadas nas regras gramaticais de línguas locais. É o caso do verbo "nascer", que lá é usado como na língua changana: "Meus pais nasceram minha irmã". O mesmo vale para "Nos disseram que hoje não há aula", que fica: "Nós fomos ditos que hoje não há aulas".

Essas estruturas são fundamentais para um correto entendimento e aplicação dos fundamentos em processamento de linguagem natural.

### História

Este é um 

* 1250...
* 1350...
* 1450...

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/imitation-game.png" style="margin-bottom: 0px !important;">
</div>

# Linguagem Natural e sua Complexidade

A complexidade envolvida na linguagem natural passa por sua estruturação formal (gramática), a questões mais subjetivas como interpretação. Adicione a isso o fato que temos diversas linguagens no mundo, todas com estruturas e significâncias diferentes. Ainda temos toda a problemática envolvendo as questões de engenharia, como por exemplo, processar grandes quantidades de texto, mas isso será abordado em outro momento. Para ilustração, vamos a um exemplo simples:

<div align="center" style="width: 100%; font-size: 0.8em; font-family: courier;">
<img src="https://meriatblob.blob.core.windows.net/draft/linguistics_club.png" style="margin-bottom: 0px !important;">
<p>ref: https://www.xkcd.com/1602/</p>
</div>

No exemplo acima, um dos personangens pergunta se o outro irá participar da convensão de linguística. A resposta é dizer que só uma pessoa que sabe o significado da palavra em inglês **sesquiannual** pode participar. Isso por que essa é uma palavra pouco usada, e portanto, se você a usar em uma conversação, é provável que a outra pessoa não entenda o seu propósito. A palavra em questão se refere a um período de 18 meses, ou um ano e meio.

sesquiannual: Occurring once every one and a half years (i.e. once every 18 months).

## Compreensão semântica

O estudo da semântica alude à parte da linguagem referente ao significado das palavras e expressões que a mesma pode gerar. Neste contexto, cada palavra possui uma semântica própria, que difere da sua classificação enquanto função sintática ou morfológica.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
A comunicação humana está essencialmente ligada à capacidade de utilizar meios <b>semióticos</b> (como a linguagem) para transmitir as <b>"intenções comunicativas"</b> de um indivíduo e a capacidade de reconhecer tais intenções. DASCAL, Marcelo. Interpretação e compreensão. 2006
</p>
</div>

Contudo, de maneira geral, a semântica não é tratada de forma isolada em cada palavra, mas sim generalizada a contextos mais amplos. Assim, em um diálogo, por exemplo, pode-se identificar um significado particular em cada frase e um significado mais geral pertinente ao assunto tratado pelas pessoas que promovem o diálogo. Da mesma forma, em um texto dissertativo, embora cada parágrafo possa expressar um sentido particular, é a união de todos os parágrafos que formarão o sentido do texto.

Como pode ser notado, a função básica de uma linguagem, ou seja, a comunicação, está centrada no significado das expressões linguísticas produzidas. Isto torna o estudo da semântica essencial para implementações computacionais que envolvam compreensão e produção de linguagem. Uma barreira porém a este objetivo gira em torno da necessidade da utilização da intuição na compreensão do sentido de um texto, atos dificilmente aplicáveis a máquinas inspiradas na arquitetura de `Von Neumman`.

Se utilizarmos um dos programas atuais de tradução de textos, vamos perceber ao final de todo o processamento que o resultado obtido apresenta em grande parte das vezes, inúmeras deficiências como falta de pronomes, erros de gênero e troca de palavras. Nos sistemas modernos, percebemos que essas falhas, mesmo não comprometendo a compreensão do contexto do documento traduzido, irá nos requerer uma revisão para a correta compreensão do assunto tratado.

O que destaco aqui, é que o processamento e tratamento computacional da linguagem natural, colide com enormes barreiras, as quais são típicas da comunicação humana. Essas dificuldades são tratadas pelo cérebro de forma natural, embora já conhecemos os ríscos que estão associados a comunicação humana.

# Natural Language Processing

Podemos conceituar `NLP` da seguinte maneira:

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
<b>Natural Language Processing</b> é a disciplina que consiste no desenvolvimento de modelos computacionais que utilizam informação expressa em uma determinada língua natural.
</p>
</div>

Como objetivo, podemos definir que em `NLP` queremos construir mecanismos artificiais que permitem o entedimento da linguagem natural para a realização de tarefas que visam simular um comportamento humano (e.g. tradução e interpretação de textos, busca de informações em documentos, detecção de tópicos).

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

# Garbage

---

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

# Gramática e análise sintática

Uma gramática é uma especiﬁcação formal da estrutura das sentenças permitidas numa linguagem. O modo mais simples de deﬁnir uma gramática é especiﬁcando um conjunto de símbolos terminais, denotando palavras da linguagem, um conjunto de símbolos não-terminais, denotando os componentes das sentenças, e um conjunto de regras de produção, que expandem símbolos não-terminais numa sequência de símbolos terminais e não-terminais [3]. Além disso, a gramática deve ter um símbolo não-terminal inicial. Por exemplo, a gramática a seguir deﬁne um fragmento da língua portuguesa:

#### Gramática 1. 

* frase ⇒ sujeito predicado
* sujeito ⇒ artigo substantivo
* predicado ⇒ verbo artigo substantivo
* artigo ⇒ o
* substantivo ⇒ gato > rato
* verbo ⇒ caçou

Nessa gramática, os símbolos terminais são o, gato e rato, sendo os demais símbolos não-terminais. A regra de produção frase ⇒ sujeito predicado estabelece que uma frase é composta de um sujeito seguido de um predicado; enquanto a regra substantivo ⇒ gato > rato estabelece que um substantivo pode ser a palavra “gato” ou “rato”. Além disso, para essa gramática, o símbolo não-terminal inicial será frase. Nas gramáticas livres de contexto (do tipo que consideramos nesse artigo), o lado esquerdo de uma regra de produção será sempre um único símbolo não terminal, enquanto o lado direito pode conter símbolos terminais e não terminais. Como veremos a seguir, uma gramática pode ser usada tanto para reconhecimento, ou seja, para decidir se essa frase pertence à linguagem deﬁnida pela gramática; quanto para geração, ou seja, para construir uma frase pertencente à linguagem deﬁnida pela gramática.

---

> Se a comunicação é algo complexo mesmo para nós os seres humanos, como podemos trabalhar isso em computação?

Bom, o primeiro passo é transformar a nossa linguagem natural em algo que possa ser trabalhado por máquina. Fazemos isso transformando nosso dado textual em algum padrão de representação numérica, algo que seja processável e compreendido por uma máquina. Somente realizando esse passo é possível iniciar o processo de examinar os dados para criação de modelos matemáticos.

---

## Conlusão

Existe muita confusão quanso se fala em NLP. Temos diversas terminologias e conceitos que são errôneamente relacionados a essa materia. NLP é um campo onde uma certa complexidade está associada, então um correto entendimento dos conceitos é fundamental para conseguir atingir um nível avançado de trabalho. 

Fora isso a pesquisa e desenvolviemnto explorando o estado da arte em NLP requer um forte conhecimento em áreas como a linguística, uma vez diversos dos problemas que hoje queremos resolver, extrapolam a engenharia para algo mais conceitual.

## Referências

* Computational Linguistics and Natural Language Processing, Jun’ichi Tsujii, University of Tokyo
* Introduction to Computational Linguistics, Jason Eisner, Johns Hopkins University
* Interpretação e compreensão. Marcelo DASCAL
* SILVA, M.C.S; KOCH, I.V. Linguística Aplicada ao Português: Morfologia. 18ª ed. – São Paulo: Cortez, 2012.
* Diferenças entre língua, idioma e dialeto; PEREZ, Luana Castro Alves, Brasil Escola.
* INTRODUÇÃO À LINGÜÍSTICA VOLUMES 1 E 2, José Luiz Fiorin
* A Mathematical Theory of Communication, C. E. SHANNON, harvard
* A Mind at Play: How Claude Shannon Invented the Information Age, Jimmy Soni and Rob Goodman
* COMPUTING MACHINERY AND INTELLIGENCE, A. M. Turing, [link](https://www.csee.umbc.edu/courses/471/papers/turing.pdf)
