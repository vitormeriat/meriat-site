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
---

<p align="center" style="background-color: #202020; width: 100%;"><img src="http://meriatblob.blob.core.windows.net/demos/new-bot.png" style="margin-bottom: 0px !important;"></p>

conversational-interfaces-explained

## Agenda

* Introdução
* A origem do problema
* Geração de significado
* Analisando um Diálogo
* Principais serviços de NLP
* Conclusão
* Referências

**O objetivo** neste post é passar por uma leve introdução ao `NLP`, `Interfaces Conversacionais`, `bots` e suas significancias, e em conjunto analisar o seu funcionamento adaptando todos os conceitos de forma que seja possível ao fim do mesmo, melhorar suas habilidades em criação de diálogos, bem como o fazê-lo utilizando o serviço de sua preferência.

## Intodução

Um dos assuntos do momento tem sido a construção de interfaces conversacionais, ou para ficar mais específicos, `bots`.

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

## Analisando um Diálogo

## Evolução tecnológica

Recentemente, a maturidade e a disponibilidade da tecnologia AI fornecida pela Google, IBM, Amazon e outras corporações tornaram a AI acessível para desenvolvedores e empresas de médio porte. Estruturas para processar a linguagem natural (NLP), para entender as intenções expressadas em uma frase, extrair entidades do texto, etc. estão se tornando amplamente disponíveis. Soluções de aprendizado profundo e de aprendizagem de máquinas estão disponíveis nas principais plataformas de nuvem. Além disso, as ferramentas dedicadas a projetar ChatBots e conversas de modelo estão florescendo. A tecnologia necessária para construir bots inteligentes e inteligentes tornou-se disponível para desenvolvedores e corporações.

## Principais serviços de NLP

Nós também nos concentramos nas plataformas que podemos usar para nossos bots hoje, incluindo a API - LUIS da Microsoft, Wit.ai do Facebook, Api.ai deEquipe assistente Google, Watson da IBM e Alexa Skill Set, e Lex da Amazon.




<div style="margin-bottom: 6em;"></div>

**Disclaimer:** Não sou um especialista na área de NLP ou linguística, logo, se houver algum erro por favor me informe. Todos os comentários são bem-vindos.

# Conclusão



# Referências

* DASCAL, Marcelo. Interpretação e compreensão. Tradução de Márcia Heloisa Lima da Rocha. São Leopoldo: Editora Unisinos, 2006, p.729.
* [Artificial Neural Networks, by Saed Sayad](http://www.saedsayad.com/artificial_neural_network.htm)
* [Neural Networks Demystified, by Stephen Welch](https://www.youtube.com/watch?v=bxe2T-V8XRs)
* [Activation function, Wikipedia](https://en.wikipedia.org/wiki/Activation_function)
* [Transfer Learning](https://en.wikipedia.org/wiki/Transfer_learning)
* [Computer Vision, Cognitive Services](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/home)
* [Custom Vision Training](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3)
* [Custom Vision Prediction](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814)
 
https://stanfy.com/blog/advanced-natural-language-processing-tools-for-bot-makers/

Amazon Lex
https://aws.amazon.com/pt/lex/

Wit.ai - facebook
https://wit.ai/

Api.ai - google
https://api.ai/

LUIS - microsoft
https://www.luis.ai/

Natural Language - google
https://cloud.google.com/natural-language/