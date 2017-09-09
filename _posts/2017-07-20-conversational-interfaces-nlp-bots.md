---
layout: post
title: "Conversational Interfaces, NLP and bots"
date: 2017-08-06
categories:
    - AI
    - NLP
    - Bot
image: "http://meriatblob.blob.core.windows.net/demos/new-bot.png"
lang: pt
color: "#202020"
description: "Este é um breve tratado sobre o processamento de linguagem natural, interfaces conversacionais e diálogos com foco em bots."
---

<p align="center" style="background-color: #202020; width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/new-bot.png" style="margin-bottom: 0px !important;"></p>


## Agenda

* Introdução
* A origem do problema
* A arte da compreensão semântica
* Geração de significado
* Analisando um Diálogo - Under the hood
* Evolução tecnológica
* Dos serviços de NLP
	* Api.ai
	* Luis.ai
	* Wit.ai
	* IBM Watson
	* Google Cloud Natural Language
	* Amazon Alexa Skill
	* Amazon Lex 	
* Conclusão
* Referências

<div style="margin-bottom: 4em;"></div>

**O objetivo** neste post é passar por uma leve introdução ao `NLP`, `Interfaces Conversacionais`, `bots` e suas significancias, e em conjunto analisar o seu funcionamento adaptando todos os conceitos de forma que seja possível ao fim do mesmo, melhorar suas habilidades em criação de diálogos, bem como o fazê-lo utilizando o serviço de sua preferência.

## Intodução

Um dos assuntos do momento tem sido a construção de interfaces conversacionais, tanto para `bots` quanto `assitentes de voz`.

Uma interface conversacional é qualquer `UI` que simula uma conversa real junto a um ser humano. A idéia aqui é que, em vez de se comunicar com um computador em seus próprios termos, seja usando sua tradução gráfica, seja inserindo comandos específicos de sintaxe, nós possamos utilizar a linguagem diária tal qual falamos com outros seres humanos.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
O objetivo das interfaces de conversacionais é chegar ao ponto em que permitirão aos os humanos que conversem com os computadores de uma maneira na qual a responsabilidade da interpretação e de descobrir o que deve ser feito seja do software, e não no usuário. Esse é o objetivo na evolução do NLP, e certamente tende a influenciar a maneira como interagimos com os computadores.
</p>
</div>

Apesar desta não ser uma disciplina moderna (se assim posso dizer), alguns problemas de ordem linguistica tem colocado as implementações atuais de **bots** em um patamar ainda amador. Deixe-me explicar melhor isso...

## A origem do problema

O primeiro e maior problema quando falamos na construção de **interfaces de conversação**, é ter um diálogo que possa parecer o mais perto o possível da linguagem natural e fluida falada por duas pessoas.

Para conseguir construir uma boa interface conversacional, é necessário ir além das expressões regulares, é necessário entender a estrutura da linguagem falada a fim de conseguir abstrair o sentido dado o contexto.

## A arte da compreensão semântica

> A comunicação humana está essencialmente ligada à capacidade de utilizar meios semióticos (como a linguagem) para transmitir as "intenções comunicativas" de um indivíduo e a capacidade de reconhecer tais intenções. *DASCAL, Marcelo. Interpretação e compreensão. 2006*

O estudo da semântica alude à parte da linguagem referente ao significado das palavras e expressões que a mesma pode gerar. Neste contexto, cada palavra possui uma semântica própria, que difere da sua classificação enquanto função sintática ou morfológica. 

Contudo, de maneira geral, a semântica não é tratada de forma isolada em cada palavra, mas sim generalizada a contextos mais amplos. Assim, em um diálogo, por exemplo, pode-se identificar um significado particular em cada frase e um significado mais geral pertinente ao assunto tratado pelas pessoas que promovem o diálogo. Da mesma forma, em um texto dissertativo, embora cada parágrafo possa expressar um sentido particular, é a união de todos os parágrafos que formarão o sentido do texto. 
    
Como pode ser notado, a função básica de uma linguagem, ou seja, a comunicação, está centrada no significado das expressões lingüísticas produzidas. Isto torna o estudo da semântica essencial para implementações computacionais que envolvam compreensão e produção de linguagem. Uma barreira porém a este objetivo gira em torno da necessidade da utilização da intuição na compreensão do sentido de um texto, atos dificilmente aplicáveis a máquinas inspiradas na arquitetura de Von Neumman.

O fato é que quando um usuário comum utiliza um programa de tradução de textos e percebe que ao final de todo o processamento - que geralmente requer um tempo considerável se analisado sob parâmetros computacionais - o texto resultante da tradução apresenta inúmeras deficiências, como faltam de pronomes, erros nos gêneros das palavras, bem como outros detalhes que embora não comprometam - ao menos nos sistemas atuais - a compreensão do contexto do documento, exigem sua revisão, pode ocorrer que aquele se sinta enganado pelo sistema. 

Ocorre que o processo de tratamento computacional da linguagem natural esbarra em enormes dificuldades, as quais são típicas da comunicação entre os seres humanos e que são tratadas pelo cérebro de uma forma tão normal e aparentemente simples que passam desapercebidas por exemplo a um usuário de computador que imagina que sua máquina possua as mesmas capacidades de seu cérebro no processamento de informações. 

## Geração de significado

**Entender** um texto significa reconhecer o contexto, fazer análise sintática, semântica, léxica e morfológica, criar resumos, extrair informação, interpretar os sentidos, analisar sentimentos e até aprender conceitos com os textos processados.

No próximo tópico vamos analizar uma possível estrutura de diálogo com o objetivo de entender os conceitos por trás das ferramentas de processamento de linguagem natural, focando nos serviços comumente utilizados hoje. 

## Analisando um Diálogo - Under the hood

Vamos pensar na estrutura de um diálogo step-by-setp. Aproveitando a brincadeira da pizza, vamos tentar pedir uma pizza utilizando um bot imaginário.

> desenho de uma pessoa falando com o bot e perguntando onde comprar uma pizza em vila mariana.

Olhando para o exemplo acima, podemos imaginar uma variedade de significados e formas diferentes de realizar a mesma pergunta:

* Lugares com pizza
* Pizzarias nas proximidades
* Pizzas na região de Vila Mariana
* Quero comprar pizza aqui perto de casa
* Me lista as pizzarias no meu bairro, por favor
* Onde tem pizza para entrega perto da minha localidade?
* etc.

Se olharmos para o cerne da questão, todas as perguntas estão relacionadas ao que chamamos de `intenção`, que neste caso é a busca por uma pizzaria em Vila Mariana. Para fins de classificação vamos atribuir uma `label` a nossa intenção. Para este caso vamos chamar de **localizar-pizzaria**

Ao definir uma determinada intenção, geramos um conjunto de sentenças, ou `enunciados` que no geral denotam um sentido comum. 

Sendo assim se pergunto ao bot **"onde acho pizzarias em Vila Mariana"**, posso `classificar` essa nova sentença como sendo pertencente a intenção **localizar-pizzaria**.

> desenho de uma pessoa perguntando o texto acima e uma engine procurando em qual intenção classificar a sentença

Podemos perceber com base neste exemplo simples, que toda `comunicação` dos usuários tem uma intenção que leva a alguma ação. Logo concluimos que a `intenção` é o conceito central na construção de uma interface conversacional. Sendo assim a primeira coisa que podemos fazer com a mensagem enviada pelo usuário é entender sua intenção, ou seja, devemos mapear a sentença para uma ação específica.

Junto com o intenção, é necessário identificar e extrair parâmetros, ou que na literatura clássica chamamos como `entidades`, que são a base para a tomada de ações na frase. Se olharmos para o nosso exemplo **"localizar pizzaria"**, as palavras **"próximo"**, **"na minha região"** correspondem à localização atual do usuário.

O reconhecimento de entidades nomeadas é uma técnica amplamente utilizada em Processamento da Linguagem Natural e consiste na identificação de nomes de entidades-chave, presentes na forma livre de dados textuais. Nesse sentido, a entrada para um sistema de extração de entidades nomeadas e um texto em sua forma livre, e sua saída é um conjunto de textos anotados, ou seja, uma representação estruturada a partir da entrada de um texto não estruturado. Vamos ao exemplo:


> desenho **"Vitor Meriat mora em Vila Mariana e trabalha na ESX."**


Ao efetuar a extração das entidades nomeadas, temos **[Vitor Meriat]**, **[Vila Mariana]** e **[ESX]**. Olhando para as entidades podemos atribuir para cada uma delas uma categoria apropriada, neste caso temos, **pessoa**, **localização** e **organização**.

Reconhecer e classificar categorias a entidades nomeadas presentes em um texto não é uma tarefa fácil. Isso fica evidente quando o assunto são nomes próprios e organizações. Este caso pode remeter a mais de uma categoria, ou simplesmente não possuir um contexto mais determinístico, em nível suficiente para auxiliar a tarefa de desambiguação. Vamos ao exemplo:

> desenho **"A Mercedes esteve em crise nos últimos meses. A empresa afirma que..."**

> desenho **"Hoje foi um ótimo dia para Mercedes."**

Para o primeiro exemplo, o contexto poderia auxiliar na desambiguação. Ou seja, havendo uma relação entre os sintagmas [a Mercedes] e [a empresa], podemos aferir a categoria "Organização" a entidade “Mercedes”, uma vez que o sintagma nominal [a empresa] identifica uma organização.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
O termo <b>"sintagma"</b> designa uma sequência hierarquizada de elementos linguísticos, que compõem uma unidade na sentença.
</p>
</div>

Isso ajuda a ilustrar o processo, bem como as dificuldades  

Até agora já vimos a representação das intenções e entidades. Um outro fator complicador é a questão do `contexto` conversacional. 

Um exemplo disto é quando eu pergunto **"onde compro pizza na minha região?"**. O contexto compreende o período do início da conversação, as interações (perguntas e respostas) até chegar na conclusão, que é **localizar uma pizzaria** na sua atual localidade.

> desenho da conversação completa até o resultado final. Usuário com cara de feliz.

Notem que no processo temos um estado intermediário, que é em muitas vezes essencial para a tomada de decisão final. É ai que entra o contexto conversacional. Para armazenar o estado intermediário usamos o contexto.

Podemos pensar no contexto como uma memória de curto prazo. Por exemplo, durante o bate-papo a procura de uma pizzaria, podemos armazenar a intenção **"comprar pizza"** e posteriormente adicionar outros parâmetros como localidade e hora (que podem já ter sido informados), e assim tomar uma decisão que pode dar início a uma `ramificação` do diálogo original.

No geral podemos ter mais de um contexto conversacional dentro do mesmo diálogo. Contudo isso faz sentido se em algum momento eles convergirem para o resultado que o final seja uma resposta mais completa e assim leve o usuário a ideia de uma conversação fluída.

Sendo assim, após identificar que o usuário quer comprar uma pizza, eu posso iniciar um novo contexto com o objetivo de obter as informações necessárias para um pedido.

Lógico que isso é uma visão genérica levando em consideração disciplinas de linguagem natural, linguagem formal e que já foi traduzido como serviços focando nas habilidades necessárias para a montagem de diálogos para interfaces conversacionais.


## Evolução tecnológica

Já é algo bem consolidado mais vale notar que `AI` é um campo amplamente explorado nas últimas 5 décadas. Alguns fatores influenciaram o **boom** que vivemos hoje, porém o mais importante para o nosso assunto é que recentemente tanto a maturidade quanto a disponibilidade de AI como serviço fornecida por grandes players de mercado como Microsoft, Google, IBM e Amazon, tem levado ao grande público as ferramentas necessárias para a criação de interfaces conversacionais robustas.

Ferramentas de processamento de linguagem natural (NLP), com capacidade de entender as intenções e  expressas em uma frase e extrair suas entidades estão se tornando amplamente disponíveis e a custo acessível. 

Outro fator é a quantidade de ferramentas.

Além disso, os frameworks focados na criação de ChatBots já pensando em toda a estrutura para integração com diversos `canais` de comunicação vem crescendo e se tornando mais completos.

A conclusão é que a tecnologia necessária para construir bots inteligentes já está disponível para desenvolvedores e corporações de forma satisfatória.

## Dos serviços de NLP

Na data em que escrevo este texto, seja por pesquisa ou por experiência, resolvi classificar as ferramentas citadas abaixo como os principais serviços para ser consumir **NLP** de forma simples e confiável focados em interfaces conversacionais. Todas as ferramentas listadas neste texto seguem os princípios listados no tópico sobre analise de diálogos.

<hr style="border: 1px dashed #f00; margin-top: 5em;" />

### Api.ai
<p align="center" style="width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/api.png" style="margin-bottom: 0px !important;"></p>

O **Api.ai** é um serviço diferenciado. Recentemente adquirido pela Google, ele surgiu como um serviço de NLP para suportar um assistente pessoal em app e evoluiu rapidamente dado seu uso e adoção. O Api.ai fornece todos os recursos que já vimos inclusive uma habilidade ainda não citada, `speech to text` e `text to speech`.

Até o momento deste post, o Api.ai tem uma oferta free com limitação de banda e no reconhecimento de voz.

**SITE:** [api.ai](https://www.api.ai)

<hr style="border: 1px dashed #f00; margin-top: 4em;" />

### Luis.ai
<p align="center" style="background-color: #219680; width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/luis.jpg" style="margin-bottom: 0px !important;"></p>

O **Microsoft Language Understanding Intelligent Service**, ou como é mais citado LUIS, é a plataforma da Microsoft que compoem dentre outras o chamado `Bot Framework`.

No LUIS é possível de forma simples e intuitiva treinar seus modelos, criar e selecionar suas entidades, visualizar os gráficos de utilização e tudo que temos na web conseguimos fazer via API. Após nosso modelo devidamente treinado é só consumir tudo via API.

Até o momento deste post, o LUIS encontra-se free para testes e em modo preview.

**SITE:** [wuis.ai](https://www.luis.ai)

<hr style="border: 1px dashed #f00; margin-top: 4em;" />

### Wit.ai
<p align="center" style="width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/wit.png" style="margin-bottom: 0px !important;"></p>

O **Wit.ai** assim como seu concorrente Api.ai veio como foco de auxiliar os desenvolvedores nas capacidades de linguagem natural. Seu bom trabalho e plataforma brilharam os olhos do **Facebook** que em 2015 fez a aquisição da mesma. Durante o próximo ano o Facebook realizou algumas alterações levando a ferramenta a compor seu `Bot Engine`, o que mudou a orientação principal do Wit.ai de uma ferramenta guiada por intenções, para uma ferramenta guiada por `história`.

Construir uma interface de conversação guiada pela "história" pode ser mais natural e mais fácil do que se basear em intenção, já que vamos trabalhado o todo. No geral o mecanismo não se altera já que continuamos defindo nossas intenções, entidades e etc.

Até o momento deste post, o Wit.ai encontra-se free.

**SITE:** [wit.ai](https://wit.ai)

<hr style="border: 1px dashed #f00; margin-top: 4em;" />
  

### IBM Watson
<p align="center" style="width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/watson.jpg" style="margin-bottom: 0px !important;"></p>

Talvez o **IBM Watson** seja o mais famoso da lista. Isto se dá pela IBM ser um dos primeiros players de mercado a investir tanto na tecnologia quanto no marketing de suas soluções, tanto no poder de processamento, quanto no quesito IA.

Temos a participação do Watson no famoso jogo da TV "Jeopardy" em 2011. Essa foi uma vitória memorável por vários motivos, mas o que importa agora é que temos todo este poder em nossas mãos, ou melhor, em uam API.

Seguindo nossa listagem temos **Watson Conversation**, que é a ferramenta direcionada para a construção de bots. Ele trabalha em um esquema direcional, onde você constroi um diálogo estruturado baseado em perguntas e respostas. 

A IBM também nos oferece o seu **Watson Natural Language Understanding**, que permite ao usuário extrair metadados chave de seus textos, incluindo entidades, relações, conceitos, sentimentos e emoções.

**SITE:** [watson conversation](https://www.ibm.com/watson/services/conversation/)


<hr style="border: 1px dashed #f00; margin-top: 4em;" />

### Google Cloud Natural Language
<p align="center" style="width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/google-cloud.jpg" style="margin-bottom: 0px !important;"></p>

O **Google Cloud Natural Language** oferece aos desenvolvedores acesso à análise de sentimentos, ao reconhecimento de entidades e análises de sintaxe.

**SITE:** [cloud.google.com/natural-language](https://cloud.google.com/natural-language/)

<hr style="border: 1px dashed #f00; margin-top: 4em;" />

### Amazon Alexa Skill
<p align="center" style="background-color: #009ad4; width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/07/20/alexa.png" style="margin-bottom: 0px !important;"></p>

Primeiro ponto a ser notado é que este serviço só é utilizado para o device Alexa. Fora isso o mecanismo é o mesmo, definimos intenções, entidades e ações. O grande ponto do Alexa Skill é o seu foco na linguagem falada.

O treino é mais complexo já que você necessita informar um conjunto maior de "dados" para que as expressões possam ser reconhecidas e classificadas em uma determinada intenção.

Outro ponto interessante é a integração do Alexa Skills Kit e o Amazon Lambda, que traz uma grande facilidade no desenvolvimento.

**SITE:** [developer.amazon.com/alexa-skills-kit](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit)

<hr style="border: 1px dashed #f00; margin-top: 4em;" />

### Amazon Lex
<p align="center" style="background-color: #FFFFFF; width: 100%;"><img src="https://d0.awsstatic.com/Digital%20Marketing/House/Editorial/products/ai/AI-380x186.png" style="margin-bottom: 0px !important;"></p>

O **Amazon Lex** é a solução da Amazon para a construção de interfaces conversacionais se utilizando dos recursos de NLP e integração com outros serviços da Amazon, como Lambda, Dynamo DB entre outros. 

**SITE:** [aws.amazon.com/lex](https://aws.amazon.com/pt/lex/)

<hr style="border: 1px dashed #f00; margin-top: 4em;" />

### Menção honrosa
Vou deixar aqui registrado alguns serviços que não consegui testar ainda, mas que são utilizados pela comunidade e também devem ter sua consideração. São eles:

* [Recast.ai](https://recast.ai/)
* [Kueri.me](http://kueri.me/)
* [Thomson Reuters Open Calais](http://www.opencalais.com/)

<div style="margin-bottom: 6em;"></div>

**Disclaimer:** Até este momento não testei de forma massiva todos os serviços, logo, se houver algum erro por favor me informe. Todos os comentários são bem-vindos. Se houver mais algum serviço não mencionado, sinta-se convidade o colaborar ;)


# Conclusão
Espero que esta pequena jornada seja útil para te ajudar a encontrar um melhor caminho na construção de diálogos inteligentes e cada vez mais naturais. Entender um pouco da problemática é importante para este fim.

Outro ponto que abordei aqui foram as plataformas que temos hoje para iniciar de maneira rápida e barata no mundo das interfaces conversacionais. No geral mesmo as APIs citadas sendo projetadas para trabalhar em resposta a uma única intenção ou ação, elas possuem todos os requisitos para que você consiga montar um bom diálogo.

Ainda falta uma melhora no quesito do conhecimento especializado, já que o único ponto de aprendizado é por meio das sentenças que informamos as APIs, sem um aprendizado coletivo das intenções.

Este é apenas uma introdução ao tema. Espero em breve poder trazer mais conteúdo sobre este tema que tem tudo para evoluir a maneira como interagimos quanto sociedade.


# Referências

* DASCAL, Marcelo. Interpretação e compreensão. Tradução de Márcia Heloisa Lima da Rocha. São Leopoldo: Editora Unisinos, 2006, p.729.
* [Advanced NLP tools for bot makers](https://stanfy.com/blog/advanced-natural-language-processing-tools-for-bot-makers/)