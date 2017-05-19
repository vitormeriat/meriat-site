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


#### Presentation Translator
Certamente outro recurso que chamou atenção: A tradução em "em tempo real" de uma apresentação realizada no PowerPoint. Certamente temos aqui a utilização de um serviço cognitivo, porém já é possível notar o movimento da Microsoft integrando AI em seu famoso pacote Office.

Este serviço já está disponível para teste, basta apenas você se inscrever [neste formulário](https://www.aka.ms/PresentationTranslator) para ter a oportunidade de avaliar.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/ppt-translator.png" class="absolute-bg"></p>

#### Cortana speaker

<p align="center" style="background-color: black;"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/cortana.png" width="200"></p>

Em relação a Cortana o que vimos neste Build é sobre adoção. Foi anunciado oficialmente o uso da Cortana como assistente para o controle por voz do [Invoke](http://www.harmankardon.com/invoke.html), que até então iria utilizar o Alexa da Amazon. Este produto será lançado no quarto trimestre nos EUA, e por hora não tem nenhum detalhe em relação ao preço.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/invoke.png"></p>

Também tivemos o anúncio da parceria fechada com a HP para a construção do seu **smart speaker** utilizando a Cortana.

Apesar de a Microsoft já ter ficado bem próxima de Apple e Google no desenvolvimento de assistentes digitais, as iniciativas recentes da Amazon e do Google para extender sua participação para as casas de seus usuários deixaram a Microsoft um pouco para trás. Mesmo agora, o Invoke será lançado apenas no final do ano, bem depois de seus concorrentes.

#### New AI MVP Award Category

Firmando o compromisso da Microsoft com essas ações em AI, tivemos também o anúncio da nova categoria para o [programa MVP](https://mvp.microsoft.com/), a categoria de AI.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/05/17/award-mvp-ai.png"></p>

Como podemos ver acima essa área envolve do aprendizado de máquinas ao serviços cognitivos, ou seja, AI em toda a sua Glória ;)

<div style="margin-bottom: 3em;"></div>
<hr/>

Parte da estratégia da Microsoft é dar um "empurrão" a fim de trazer inteligência artificial para a computação mainstream. Em resumo, sobre o que vimos no Build, na visão da Microsoft é certo dizer:

> Artificial Intelligence está saindo do Research & Development para ficar mais próximo dos desenvolvedores

Resumindo o motivo de estamos ouvindo falar tanto sobre AI, podemos dizer que chegamos a esse ponto graças à convergência de três forças principais: O aumento da potência computacional que hoje está exponencial na nuvem, poderosos algoritmos que funcionam em redes neurais profundas e acesso a enormes quantidades de dados.

## Project Oxford
O investimento da Microsoft em AI não é novo. Como citado por Harry Shum, o departamento de Research & Development tem realizados pesquisas voltadas para AI nos últimos 20 anos, o que pode ser bem notado se olharmos para o histórico.

