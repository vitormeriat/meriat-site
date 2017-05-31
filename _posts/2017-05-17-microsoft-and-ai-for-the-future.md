---
layout: post
title: "Microsoft and Artificial Intelligence for the future"
date: 2017-05-17
categories:
    - IA
    - Cognitive Computing
    - Microsoft Azure
    - Deep Learning
description: "Microsoft and Artificial Intelligence in Build 2017"
image-full: "https://qzprod.files.wordpress.com/2016/03/microsoft_tai.png"
---

Aproveitando o famoso [Microsoft Build](https://build.microsoft.com/) que em 2017 ocorreu em Seattle, e juntando ao convite para resumir o que foi apresentando durante esta conferência em relação a AI no [Delivering Software meetup](https://www.meetup.com/DeliveringSoftware/events/239680578/), vou expor um pouco do histórico da Microsoft e conjecturar sobre sua visão de futuro no quesito Artificial Intelligence.

Segundo Harry Shum (Executive Vice President, Microsoft AI and Research), durante seu discurso no Build: 

> Alguns anos atrás, era difícil pensar em uma ferramenta de tecnologia popularmente usada que fazia uso do poder da AI. Em poucos anos, será difícil imaginar qualquer tecnologia que não aproveite o poder da AI. 

Isso nos mostra como as grandes companias como Microsoft, Google, Amazon e etc, estão focando em produtos que explorem o poder na inteligência artificial.

## Sobre o Build 2017

Sobre o que foi apresentado no Build 2017, temos algumas novidades interessantes. Se comparado com o Build passado (2016), podemos dizer que a Microsoft trouxe bastante coisa nova ao cenário.

#### Cognitive Services
E relação aos cognitive services, foram acrescentados 4 novos serviços aos 25 já existentes:

* [Bing Custom Search](https://azure.microsoft.com/pt-br/services/cognitive-services/bing-custom-search/)
* [Custom Vision Service](https://azure.microsoft.com/en-us/services/cognitive-services/custom-vision-service/)
* [Custom Decision Service](https://azure.microsoft.com/en-us/services/cognitive-services/custom-decision-service/)
* [Video Indexer](https://azure.microsoft.com/en-us/services/cognitive-services/video-indexer/)

O que vale salientar aqui é que agora temos outros 3 serviços customizáveis, o que traz uma outra linha de atuação aqui. Tirando o LUIS (Language Understanding Intelligent Service) e o Custom Speech Service, todos os demais serviços se tratam de aprendizado prévio e consumível via API. Como LUIS é possível haver uma customização e aprendizagem da intenção com base no que foi estipulado. Podemos utilizar o Custom Speech Service para aprender com um determinado conjunto de linguagem, seja técnica ou não, e adaptar esse vocabulário para seu usuário final. Na prática os novos serviços customizáveis dão mais poder aos usuários, permitindo aos mesmos realizar aprendizados e experiências direcionadas aos seus problemas específicos.

#### Cognitive Services Labs
O Cognitive Services Labs é um ambiente para testar e dar feedback sobre as novas tecnologias sobre serviços cognitivos que estão sendo desenvolvidos pela Microsoft. Sendo assim você pode se inscrever para testar o que provavelmente serão os novos serviços a serem disponibilizados na plataforma Azure. 

A Microsoft já havia feio o mesmo por meio do projeto Oxford, que é precessor do Cognitive Services.

Vale dar uma olhada nesse cara, aqui temos alguns serviços disruptivos na área, como por exemplo o Gesture API, doravante chamado de Project Prague, que cria experiências mais intuitivas e naturais, permitindo aos utilizadores controlar e interagir através de gestos.

Você pode acessar o [Cognitive Services Labs aqui!](https://labs.cognitive.microsoft.com/)

#### Azure Batch AI Training
O [Azure Batch AI Training](https://batchaitraining.azure.com/) é fenomenal. Este serviço possibilita que os desenvolvedores possam treinar suas próprias redes neurais profundas, utilizando as principais plataformas, incluindo o Microsoft Cognitive Toolkit, TensorFlow e etc. Outro ponto aqui é que você pode simplesmente enviar seu código em um container Docker e deixar a Microsoft lidar com isso.

O grande ganho aqui é poder utilizar a mesma infra-estrutura que a Microsoft usa para o seu desenvolvimento de AI por demanda. Na prática agora temos GPUs NVIDIA de ponta que serão utilizadas para o processamento. Agora não vamos mais ter que nos preocupar com a distribuição e paralelização deste processamento, jogando a responsabilidade para a nuvem. 

Vale notar que no Build, foi exibido que será bem simples levar esses modelos de aprendizagem profunda para onde estão os dados, usando o analytics integration fornecido pelo Azure Data Lake, Azure Cosmos DB ou SQL Server.

#### Bots
Usando os novos Adaptive Cards ​​suportados pelo Microsoft Bot Framework, os desenvolvedores podem gravar cartões que ficam ótimos em vários aplicativos e plataformas. Outra novidade foi a possibilidade de publicar em novos canais, incluindo Bing, Cortana e Skype for Business, fora o poder de implementar a API de solicitação de pagamento da Microsoft para verificação rápida e fácil em seus bots.

A Microsoft também atualizou o LUIS (Language Understanding Intelligent Service),a fim de oferecer um reconhecimento de fala mais preciso, sem falar no número crescente de entidades e intenções que o sistema pode reconhecer.

#### Cortana Skills Kit
O Cortana Skills Kit foi lançado em preview, e em suma oferece o poder de desenvolver habilidades para Cortana criando um bot e publicando-o no novo canal da Cortana Bot Framework. Isso está disponível no Windows 10, Android, iOS e no novo alto-falante Harman Kardon Invoke,que é powered by Cortana.

#### Presentation Translator
Certamente outro recurso que chamou atenção: A tradução em "em tempo real" de uma apresentação realizada no PowerPoint. Certamente temos aqui a utilização de um serviço cognitivo, porém já é possível notar o movimento da Microsoft integrando AI em seu famoso pacote Office.

Este serviço já está disponível para teste, basta apenas você se inscrever [neste formulário](https://www.aka.ms/PresentationTranslator) para ter a oportunidade de avaliar.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/ppt-translator.png" class="absolute-bg"></p>

#### Cortana speaker

<p align="center" style="background-color: black;"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/cortana.png" width="200"></p>

Em relação a Cortana o que vimos neste Build é sobre adoção. Foi anunciado oficialmente o uso da Cortana como assistente para o controle por voz do [Invoke](http://www.harmankardon.com/invoke.html), que até então iria utilizar o Alexa da Amazon. Este produto será lançado no quarto trimestre nos EUA, e por hora não tem nenhum detalhe em relação ao preço.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/invoke.png" class="absolute-bg"></p>

Também tivemos o anúncio da parceria fechada com a HP para a construção do seu **smart speaker** utilizando a Cortana.

Apesar de a Microsoft já ter ficado bem próxima de Apple e Google no desenvolvimento de assistentes digitais, as iniciativas recentes da Amazon e do Google para extender sua participação para as casas de seus usuários deixaram a Microsoft um pouco para trás. Mesmo agora, o Invoke será lançado apenas no final do ano, bem depois de seus concorrentes.

#### New AI MVP Award Category

Firmando o compromisso da Microsoft com essas ações em AI, tivemos também o anúncio da nova categoria para o [programa MVP](https://mvp.microsoft.com/), a categoria de AI.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/award-mvp-ai.png" class="absolute-bg"></p>

Como podemos ver acima essa área envolve do aprendizado de máquinas ao serviços cognitivos, ou seja, AI em toda a sua Glória ;)

<div style="margin-bottom: 3em;"></div>
<hr/>

Parte da estratégia da Microsoft é dar um "empurrão" a fim de trazer inteligência artificial para a computação mainstream. Em resumo, sobre o que vimos no Build, na visão da Microsoft é certo dizer:

> Artificial Intelligence está saindo do Research & Development para ficar mais próximo dos desenvolvedores

Resumindo o motivo de estamos ouvindo falar tanto sobre AI, podemos dizer que chegamos a esse ponto graças à convergência de três forças principais: O aumento da potência computacional que hoje está exponencial na nuvem, poderosos algoritmos que funcionam em redes neurais profundas e acesso a enormes quantidades de dados.

## Project Oxford
O investimento da Microsoft em AI não é novo. Como citado por Harry Shum, o departamento de Research & Development tem realizados pesquisas voltadas para AI nos últimos 20 anos, o que pode ser bem notado se olharmos para o histórico.

O projeto Oxford é a coleção da Microsoft de APIs para serviços de aprendizado de máquina. Antes de seu lançamento oficial, a Microsoft laçou o (que na época se tornou um viral) sua aplicação para "adivinhação de idade", o How-Old.net. Poucas horas depois de ser lançado, o site reuniu centenas de milhares de submissões de imagens em que os usuários brincaram com as tentativas do site de descobrir as idades e os gêneros das pessoas nas fotos submetidas. É claro que isso ajudou a treinar o modelo de reconhecimento e analise de sentimento, tornando o serviço mais confiável.

O projeto Oxfor iniciou com os seguintes serviços:

* Face recognition
* Speech processing
* Visual tools
* Language Understanding Intelligent Service (LUIS)

## Deep Learning
Apesar do termo datar como recente para a maioria das pessoas, as pesquisas envolvendo redes neurais de N camadas para problemas complexos está no campo de pesquisa da Microsoft há decadas, e mais especificamente no área do reconhecimento de fala, como podemos ver neste paper da IEEE, datado de 2013: [Recent advances in deep learning for speech research at Microsoft](http://ieeexplore.ieee.org/abstract/document/6639345/)

## Microsoft Research

Quando Bill Gates criou a Microsoft Research, em 1991, ele previa que os computadores um dia veriam, ouviriam e entenderiam os seres humanos – e essa perspectiva atraiu algumas das melhores mentes para os seus laboratórios, segundo a Microsoft.

Vários projetos desenvolvidos no Microsoft Resarch serviram de inovação e base para novas tendências que viraram projetos de grande sucesso para a empresa. O sucesso dos bots, serviços cognitivos, cortana, HoloLens e compania sevem como base para novos projetos que hoje já sabemos ser bem aguardados como por exemplo, o Skype Translator.

Em outubro de 2016, a Microsoft se tornou a primeira empresa do setor a chegar à paridade com humanos em reconhecimento de voz, segundo o anunciado por Harry Shum.

A visão da Microsoft é realmente expandir, tanto que vemos anuncios como o da colaboração entre a Microsoft Research e o grupo OpenAI, que é uma empresa de pesquisa de AI sem fins lucrativos, e que é destaque por sua atuação e produção.


## Referências
* [Resumo do anúncio realizado por Harry Shum](https://blogs.microsoft.com/blog/2017/05/10/microsoft-build-2017-microsoft-ai-amplify-human-ingenuity/)
* [Project Oxford](http://www.projectoxford.ai/)
* [Advancing our ambition to democratize artificial intelligence](https://blogs.microsoft.com/blog/2016/11/15/advancing-ambition-democratize-artificial-intelligence/)