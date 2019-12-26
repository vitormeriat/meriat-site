---
layout: post
title: "Microsoft Azure Notebooks–Jupyter Notebooks as a Service"
date: 2016-10-20
categories:
    - Data Science
    - Machine Learning
    - Python
description:
image: "http://blob.vitormeriat.com.br/images/2016/10/capa.jpg"
---

Essa é uma dica para a galera (que como eu), utiliza o Jupyter Notebooks como ferramenta de estudo ou trabalho.

<div align="center" class="image-content" style="background-color: #35424a">
  <img src="http://blob.vitormeriat.com.br/images/2016/10/capa.jpg">
</div>

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

<div align="center" class="image-content" style="background-color: #35424a">
  <img src="http://blob.vitormeriat.com.br/images/2016/10/azure-notebook-1.jpg">
</div>

Assim que você informar sua credencial, o serviço vai te solicitar a permissão para criar uma ID para sua conta no serviço. Diga sim e siga em frente…

Assim que tudo estiver pronto, você deve ver uma tela como abaixo:

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2016/10/azure-notebook-2.jpg">
</div>

Done. Você já um ambiente pronto, e inclusive alguns exemplos para testar. De cara, uma coisa interessante notar é que podemos importar notebooks direto de nosso computador ou de uma URL.

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2016/10/azure-notebook-3.jpg">
</div>

Agora perceba que todos os nossos cadernos estão vinculados a uma biblioteca chamada <strong>Sample notebooks</strong>. Sendo assim vamos criar uma biblioteca.

Clique em <strong>My libraries</strong>. Na página que se segue clique em <strong>New Library</strong> e informe o nome, descrição e url personalizada.

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2016/10/azure-notebook-4.jpg">
</div>

Assim que sua biblioteca estiver criada você pode optar por importar um caderno ou abrir seu Jupyter Notebooks.

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2016/10/azure-notebook-5.jpg">
</div>

Agora estamos em terreno conhecido. É só criar um novo Notebook usando Py2, Py3 ou R.

No próximo post vou mostrar como instalar pacotes de Python, R e como compartilhar sua biblioteca de forma pública.

<div style="margin-bottom: 5em;"></div>

## Conclusion
A princípio vale notar que esta é uma ferramenta em preview. Sendo assim está em desenvolvimento ativo. Acho que hoje é uma maneira muito válida de compartilhar seus cadernos em um ambiente pronto para execução. Vejo uma ótima oportunidade para ensino aqui. Creio que em breve o serviço deve evoluir para ofertas com alto poder de processamento e armazenamento. Digo isso por que hoje já conseguimos utilizar e integrar nossos cadernos com o Azure Machine Learning, logo, creio que a intenção da Microsoft seja mais que apenas oferecer um local para treinar e repositar experimentos na nuvem… espero ;)
