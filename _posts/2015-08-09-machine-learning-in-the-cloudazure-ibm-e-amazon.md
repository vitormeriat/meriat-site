---
layout: post
title: Machine Learning in the Cloud–Azure, IBM e Amazon
date: 2015-08-09
categories:
  - Amazon Web Service
  - Cloud Computing
  - IoT
  - Machine Learning
  - Microsoft Azure
---

<div align="center" class="image-content">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/capa-ml-in-the-cloud.png">
</div>

Um dos alicerces do que hoje chamamos de <strong>IoT</strong>, é a geração insumos por meio de inteligência nos dados gerados. O fluxo feliz são <strong>"coisas" "conectadas"</strong> gerando <strong>"dados"</strong> e <strong>"inteligência"</strong>. Neste post veremos 3 soluções de <a href="https://en.wikipedia.org/wiki/Machine_learning" target="_blank"><strong>Machine Learning</strong></a> in the <strong>Cloud</strong>, ambas iguais em essência, mas diferentes em propósito e execução. Vou apresentá-los aos serviços <a href="http://azure.microsoft.com/en-us/services/machine-learning/" target="_blank">Azure Machine Learning</a>, <a href="http://www.ibm.com/smarterplanet/us/en/ibmwatson/" target="_blank">IBM Watson</a> e <a href="https://aws.amazon.com/pt/machine-learning/details/" target="_blank">Amazon Machine Learning</a>.

<strong>IBM Watson</strong> visa abstrair a ciência de dados, transformando as consultas em linguagem natural com base no conteúdo dos conjuntos de dados enviados. Já o <strong>Microsoft Azure Machine Learning</strong> utiliza uma metodologia de mineração de dados existentes para resultados rápidos e integração com outros serviços de nuvem para a extração dos dados. Mais novo no mercado, o <strong>Amazon Machine Learning</strong> foca em uma solução automática de <strong>aprendizagem supervisionada</strong>.

<div align="center" class="image-content" style="background-color: #278ca8">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/ml-azure.png">
</div>

A solução de <strong>Machine Learning do Microsoft Azure</strong>, fornece uma interface gráfica <strong>drag-and-drop</strong> para conectar componentes e rotear o fluxo de dados por várias etapas, já que em back o <strong>Azure ML </strong>é uma ferramenta que automatiza algumas tarefas da aprendizagem de máquina, assumindo que o usuário já tem alguma familiaridade com pelo menos o básico da ciências de dados.

<div align="center" class="image-content" style="background-color: #278ca8">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/azureml-01.png">
</div>

Assim que você se conectar utilizando o portal do <a href="https://studio.azureml.net" target="_blank">Azure Machine Learning</a>, serão aprensetandas algumas opções. Você pode começar a utilizar o Azure ML criando um Experimento.</p>

<div align="center" class="image-content" style="background-color: #278ca8">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/azureml-02.png">
</div>

Criar um experimento é simples. Temos apenas que selecionar um conjunto de dados e o arrastar para a tela de edição canvas. Conjuntos de dados tem apenas portas ou ligações de saída, logo servem apenas para alimentar um módulo. Os módulos estão disponíveis no menu esquerdo e possuem duas portas, entrada e saída.

Módulos adicionais podem ser arrastados para a tela e ligados uns aos outros (a partir de uma porta de saída de um módulo para a porta de entrada de um outro). Módulos de pré-processamento de dados incluem entre outros recursos o tratamento de <strong>missing data scrubbing</strong>, seleção de recursos através de análise discriminante linear e detecção de colunas duplicadas.

Os algoritmos suportados incluem multi-class neural networks, logistic regression, boosted decision trees, support vector machines, e locally deep support vector machines.

<div align="center" class="image-content" style="background-color: #231A1E">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/ml-imb-watson.png">
</div>

Assim que você acessa e loga a página no <strong>IBM Watson Analytics</strong>, nos é apresentado um vídeo muito bem elaborado explicando o serviço de forma bem didática. Junto com a apresentação, temos um passo-a-passo que nos leva ao envio de dados que podem ser no formato <strong>CSV</strong> ou <strong>XLS</strong>. É importante pontuar que é possível seguir uma espécie de tutorial, que aponta inclusive, onde podemos obter dados de amostra para iniciar a análise.

Até o momento deste artigo, o <strong>Watson</strong> ainda estava público em beta-teste, e portanto limitado. Por exemplo, o envio de dados só ocorre para arquivos menores de <strong>12MB</strong> e com até <strong>50 colunas</strong>. É claro que isso é inviável quando falamos de ML em larga escala, porém ainda estamos em teste ok?

Trabalhar com o envio de dados nestes formatos é algo inviável, mas certamente ele vai seguir os mesmos passos que a <strong>Amazon </strong>e o <strong>Azure</strong>, onde poderemos informar bases já existentes. Porém existe um nicho aqui, a possibilidade de pessoas não técnicas fazendo upload de suas planilhas e realizando tratamentos e inteligência nos dados enviados.

O Watson oferece 4 recusos: <strong>Explore</strong>, <strong>Predict</strong>, <strong>Assemble </strong>e <strong>Refine</strong>. Vou abordar aqui os 3 primeiros disponíveis neste momento.

<div align="center" class="image-content" style="background-color: #000">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/watson-01.png">
</div>

<strong>Explore </strong>oferece uma ferramenta que permite a exploração dos dados. Um usuário pode selecionar a partir de um dos muitos exemplos de consultas, ou simplesmente&nbsp; digitando um em texto livre.

<div align="center" class="image-content" style="background-color: #000">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/watson-02.png">
</div>

<strong>Predict</strong> é a ferramenta que Watson fornece prever uma ou mais variáveis ​​alvo com base nos dados. Isto corresponde à classificação ou regressão dependendo se o alvo é variável categórica ou contínua.

<div align="center" class="image-content" style="background-color: #000">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/watson-03.png">
</div>

<strong>Assemble </strong>fornece uma interface para criar "pastas de trabalho de autoria própria". Estes contêm materiais de apresentação, visualizações de dados e relatórios.

<div align="center" class="image-content" style="background-color: #000">
  <img src="http://blob.vitormeriat.com.br/images/2015/08/ml-amazon.png">
</div>

Como já foi citado, o modelo adotado pela Amazon é o de aprendizado de máquina supervisionado, e refere-se a definir em que <strong>datapoint</strong> está associada a alguma variável-alvo. Quando o alvo é uma variável binária, o problema é chamado de <em>classificação binária</em>. Quando o alvo é uma variável categórica (com mais de 2 categorias), o problema é chamado <em>de classificação multi-classe</em>. Quando o alvo é de valor real (um número de ponto flutuante), o problema é chamado <em>de regressão</em> . Estes são os três serviços oferecidos pela Amazon Machine Learning. Embora existam muitos algoritmos, a Amazon coloca a responsabilidade mínima do algoritmo nas mãos dos usuários, oferecendo uma solução quase totalmente automatizada para o problema proposto.

O Amazon Machine Learning oferece ferramentas e assistentes de visualização que orientam você durante o processo de criação de modelos de aprendizagem de máquina (ML), sem necessidade de aprender tecnologias e algoritmos tecnologias complexos de ML. Após a conclusão dos modelos, o Amazon Machine Learning facilita a obtenção de previsões para sua aplicação usando APIs simples, sem necessidade de implementar um código de geração de previsões personalizado ou gerenciar qualquer infraestrutura.

<strong>A aquisição de Dados </strong>no Amazon ML inclui dados relacionais armazenados em <strong>RDS</strong>, arquivos <strong>CSV</strong> armazenados no <strong>S3</strong> ou dados no <strong>Redshift</strong> data warehouse da Amazon. Para quem quiser experimentar o serviço da Amazon, eles fornecem um conjunto de dados de amostra <strong>(bank.csv)</strong> que contém dados fictícios para os clientes dos bancos.

## Bons estudos e até a próxima pessoal ;)
