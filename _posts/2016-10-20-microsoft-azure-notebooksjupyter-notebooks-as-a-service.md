---
layout: post
title: "Microsoft Azure Notebooks–Jupyter Notebooks as a Service"
date: 2016-10-20
categories:
  - Data Science
  - Machine Learning
  - Python
description:
image-full: "https://meriatsite.blob.core.windows.net/images/2016/10/capa.jpg"
---

Essa é uma dica para a galera (que como eu), utiliza o Jupyter Notebooks como ferramenta de estudo ou trabalho.

<p style="background-color: #35424a"><img title="capa" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="capa" src="https://meriatsite.blob.core.windows.net/images/2016/10/capa.jpg" width="752" height="412" /></p>

Provavelmente se você está lendo isto, é por que já conhece o Jupyter Notebooks ou antigo IPython, e tem interesse em usar ou entender esta oferta. Caso você não conheça esta ferramenta, basta saber que o Jupyter Notebooks oferece um environment com suporte a várias linguagens de programação, incluindo Python, R, MATLAB e etc. Esta é uma ferramenta que caiu nas graças dos programadores por proporcionar um meio simples de programar, visualizar e documentar de maneira eficientes seus experimentos. Em breve escrevo algo específico sobre essa ferramenta aqui no blog.

Por hora vamos analisar este serviço, que no momento em que escrevo este texto, está em PREVIEW.

Creio que o primeiro passo é entregar algumas informações sobre o serviço. Até este momento os Notebooks estão rodando sobre environment Anaconda para o Python e Microsoft R Open para R. Sendo assim temos suporte aos pacotes já conhecidos no Anaconda. Algo muito importante de ressaltar é que temos a possibilidade de instalar pacotes de maneira normal (pip install), ou usando Conda (conda install). O mesmo vale para R.

## Environments

* Anaconda 4.1.0 para Python 2.7.11
* Anaconda 4.1 para Python 3.5.1
* MRO 3.3.0 para R

## Restrictions

* É possível acessar o github, PyPI, CRAN, OneDrive, DropBox, Google Drive e é claro, o Azure;
* A memória é limitado a 4 GB;
* Seus dados pode ter removido após 60 dias de inatividade;
* Uso deve ser limitado a aprendizagem, investigação, computação em geral e etc. O que é meio lógico, já que o serviço (por hora gratuito), tem algumas limitações de processamento e privacidade.


## Start
Para utilizar o serviço é algo tão simples quanto acessar o serviço e se autenticar no serviço.

<p style="background-color: #35424a"><img title="azure-notebook-1" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; border-left: 0px; display: block; padding-right: 0px; margin-right: auto" border="0" alt="azure-notebook-1" src="https://meriatsite.blob.core.windows.net/images/2016/10/azure-notebook-1.jpg" width="100%" /></p>

Assim que você informar sua credencial, o serviço vai te solicitar a permissão para criar uma ID para sua conta no serviço. Diga sim e siga em frente…

Assim que tudo estiver pronto, você deve ver uma tela como abaixo:

<p><img title="azure-notebook-2" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; border-left: 0px; display: block; padding-right: 0px; margin-right: auto" border="0" alt="azure-notebook-2" src="https://meriatsite.blob.core.windows.net/images/2016/10/azure-notebook-2.jpg" width="100%" /></p>

Done. Você já um ambiente pronto, e inclusive alguns exemplos para testar. De cara, uma coisa interessante notar é que podemos importar notebooks direto de nosso computador ou de uma URL.

<p><img title="azure-notebook-3" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; border-left: 0px; display: block; padding-right: 0px; margin-right: auto" border="0" alt="azure-notebook-3" src="https://meriatsite.blob.core.windows.net/images/2016/10/azure-notebook-3.jpg" width="100%" /></p>

Agora perceba que todos os nossos cadernos estão vinculados a uma biblioteca chamada <strong>Sample notebooks</strong>. Sendo assim vamos criar uma biblioteca.&nbsp; </p>

<p align="justify">Clique em <strong>My libraries</strong>. Na página que se segue clique em <strong>New Library</strong> e informe o nome, descrição e url personalizada.</p>

<p><img title="azure-notebook-4" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; border-left: 0px; display: block; padding-right: 0px; margin-right: auto" border="0" alt="azure-notebook-4" src="https://meriatsite.blob.core.windows.net/images/2016/10/azure-notebook-4.jpg" width="100%" /></p>

Assim que sua biblioteca estiver criada você pode optar por importar um caderno ou abrir seu Jupyter Notebooks.

<p><img title="azure-notebook-5" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; border-left: 0px; display: block; padding-right: 0px; margin-right: auto" border="0" alt="azure-notebook-5" src="https://meriatsite.blob.core.windows.net/images/2016/10/azure-notebook-5.jpg" width="100%" /></p>

Agora estamos em terreno conhecido. É só criar um novo Notebook usando Py2, Py3 ou R.

No próximo post vou mostrar como instalar pacotes de Python, R e como compartilhar sua biblioteca de forma pública.

## Conclusion
A princípio vale notar que esta é uma ferramenta em preview. Sendo assim está em desenvolvimento ativo. Acho que hoje é uma maneira muito válida de compartilhar seus cadernos em um ambiente pronto para execução. Vejo uma ótima oportunidade para ensino aqui. Creio que em breve o serviço deve evoluir para ofertas com alto poder de processamento e armazenamento. Digo isso por que hoje já conseguimos utilizar e integrar nossos cadernos com o Azure Machine Learning, logo, creio que a intenção da Microsoft seja mais que apenas oferecer um local para treinar e repositar experimentos na nuvem… espero ;)
