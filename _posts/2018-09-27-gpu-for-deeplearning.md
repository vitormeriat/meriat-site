---
layout: post
title: "GPU for Deep Learning"
date: 2018-09-27
categories:
    - AI
    - Deep Learning
tags:
    - ai
    - deep learning
    - hpc
    - gpu
image: "http://meriatblob.blob.core.windows.net/images/2018/09/27/capa.png"
lang: pt
description: "Chegamos a um tópico importante dentro do campo de estudo da Deep Learning, a programação em GPU. Minha intenção com este artigo é demonstrar qual a relação entre Deep Learning e GPU, e a importância deste hardware especializado nas atividade de programação em redes neurais artificiais profundas."
---

<p align="center" style="width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2018/09/27/capa.png" style="margin-bottom: 0px !important;"></p>

## Introdução

Chegamos a um tópico importante dentro do campo de estudo da Deep Learning, a programação em **GPU**. Minha intenção com este artigo é demonstrar qual a relação entre **Deep Learning** e GPU, e a importância deste hardware especializado nas atividades de programação em redes neurais artificiais profundas.

Todas as referências utilizadas neste artigo se seguem ao final do texto. Por hora, nos serve como introdução ao assunto o fato que Deep Learning é em sua essência, um apanhado de técnicas baseadas em multiplicações matriciais. Este é o ponto de insterseção entre Deep Learning e as técnicas de programação para GPU. O primeiro passo entretanto é olharmos para a evolução do hardware, o que torna visível sua importância dentro do tema.

## GPU e suas origens

Em meados dos anos 90, já havia uma vasta utilização dos computadores, mas pouco se conhecia sobre processamento gráfico. Já havia a utilização do **VGA (Video Graphics Array)**, componente usado como um "vetor de imagens gráficas", uma área contínua de dados que podem ser lidos e representados em uma tela. Dentro desta arquitetura, a responsabilidade de processar essa memória vinha inteiramente da **CPU**. Esse processamento devia acontecer várias vezes por segundo, exatamente como fazemos para simularmos a noção de movimento.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
A CPU (Central Processing Unit) é a unidade de processamento central do computador.
</p>
</div>

Estamos falando de uma época onde computadores ainda não eram populares. Com isso a utilização das aplicações gráficas ainda não eram um problema. A questão é que a medida em que os computadores foram se tornando populares, as aplicações que antes só trabalhavam com gráficos simples, bidimensionais e de baixa resolução baixa, partiram para aplicações mais elaboradas como jogos, aplicações para manipulação de imagens, **CAD (Computer-Aided Design)** e outras tantas.

Com essa crescente evolução, a demanda por mais poder de processamento fez com que os engenheiros de hardware, desenvolvessem um novo processamento para abarcar algumas das atividades que antes ocorriam na CPU, o que dava início as primeiras placas gráficas.

O que se percebeu é que algumas das atividades do processamento gráfico são extremamente intensivas, como o processo de rasterização, que converte vetores e elementos geométricos em pixels. Este é literalmente o primeiro processamento gráfico que foi implementado nestes novos hardwares.

Como segundo passo, foi realizado a implementação dos **shaders**, responsáveis pela renderização de sombras. As sombras são necessárias para que o usuário possa ter a impressão de profundidade. Aqui temos um ponto muito importante nesta história. Diferente da técnica de raterização, a técnica de shader possui uma grande diversidade de algoritmos, dado a diversidade de utilizações. Isso tornava a programação em hardware muito inviável, já que abarcar todas as implementações seria muito "pesado". A solução para este problema foi a criação de shaders configuráveis, o que tornava estes novos hardwares configuráveis. Um exemplo disso é o famoso **OpenGL**, que foi a mais famosa biblioteca para programação de shaders.

Agora havia um hardware configurável, e se se ele era configurável, implica dizer que havia um conjunto de instruções. Se eu posso realizar um conjunto de instruções em um hardware especializado, por que cargas d'água não incluir comandos mais complexos? E se este novo processador também realizase algumas outras atividades para aliviar a utilização da CPU?

Essas foram algumas das perguntas e necessidade que nos levaram a criação da GPU, do inglês **Graphics Processing Units**, ou unidades de processamento gráﬁcos.

Com este novo hardware, os engenheiros foram migrando aos poucos as atividades específicas do processamento gráfico da CPU para a GPU.

## Under the hood

Inicialmente a GPU era um processador bem mais simples do que as GPUs atuais. Sua arquitetura era construída com foco no processamento gráfico. Já as GPUs modernas tem focado no aspecto programável, tornando o hardware em um processador com grande capacidade aritmética e de uso geral, não mais restrita as operações gráficas.

Atualmente, as GPUs são processadores dedicados para processamento gráfico da classe **SIMD (Single Instruction Multiple Data)**. GPUs são desenvolvidas especificamente para cálculos de ponto flutuante, essenciais para os trabalhos de computação gráfica. Suas principais características são sua alta capacidade de processamento massivo paralelo e sua total programabilidade e desempenho em cálculos que exigem um volume grande de dados, resultando em um grande **throughput**.

Arquiteturalmente a GPU possui um número muito superior de unidades de processamento comparado a CPU. Observe a figura abaixo:

<p align="center"><img src="https://meriatblob.blob.core.windows.net/images/2018/09/27/01.png" style="width: 100%; margin-bottom: 0px !important;"></p>

O primeiro ponto a ser observado é que as unidades de processamento de uma GPU são mais simples e mais lentas que as unidades de processamento de uma CPU. Em relação ao barramento de comunicação, o usual é termos uma desvantagem na utilização da GPU. 

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
De fato, vamos ver nos testes que é necessário calcular se nossa empreitada é algo que vale ser processado na <b>GPU</b>. Descobri que às vezes a sobrecarga de transferência de dados para e da <b>GPU</b> elimina completamente o ganho de velocidade do paralelismo que temos na <b>GPU</b>. Nem sempre é uma boa ideia ir para a <b>GPU</b>. 
</p>
</div>

A maioria das CPUs multicore atuais usam o paradigma de memória compartilhada para comunicação com sincronização através de cache compartilhada. Cada núcleo tem uma thread de processamento por vez, com um conjunto de registradores contendo o estado da thread, uma **ULA (Unidade Logica Aritmética)** dedicada para a thread atual e uma unidade grande dedicada ao gerenciamento e escalonamento de tarefas.

Enquanto as CPUs dedicam uma grande quantidade de seus circuitos para o uso geral e de controle, a GPU foca mais nas ULAs ou **ALUs (Arithmetic Logical Units)**. Isso torna a GPU mais eficiente em termos de custo quando executam um software paralelo. Consequentemente, a GPU é construída para aplicações com demandas diferentes da CPU: cálculos paralelos grandes com mais ênfase no **throughput que na latência**.

Dado essa arquitetura, aplicações muito iterativas, tais como editores de texto ou players de áudio, não se beneﬁciariam do poder de processamento das GPUs. Por outro lado, aplicações em que exista muito paralelismo de dados tem um ganho nítido. 

Como vimos, a GPU, em seu core implementa um modelo computacional SIMD, que podemos traduzir como “instrução única, dados múltiplos". Neste modelo temos vários processadores, mais somente uma unidade de processamento. Isso implica em dizer que uma máquina SIMD faz muitas coisas em paralelo, mas sempre as mesmas coisas.

## GPU & Deep Learning. Uma questão de desempenho

Já vimos sobre o poder de paralelismo presente na GPU. A grande questão é que o ganho de desempenho não é necessariamente apenas fruto do paralelismo.

Como vimos, a CPU é otimizada para latência enquanto a GPU é otimizada para largura de banda.

A CPU é muito rápida porém lida com uma quantidade pequena de informação. Já a GPU é mais lenta porém lida com uma enorme quantidade de informação.

Para ambos os hardwares, existe a necessidade do tráfego de pacotes de dados. A CPU pode buscar alguns pacotes da memória RAM de forma muito veloz, enquanto a GPU para a mesma tarefa vai enfrentar uma latência maior. O ponto aqui é que a CPU precisa ir muitas vezes na memória para buscar as informações enquanto a GPU pode trabalhar uma quantidade muito superior.

Em outras palavras, a CPU é boa em buscar pequenas quantidades de memória de forma extremamente rápida, enquanto a GPU consegue buscar grandes quantidades de memória por vez.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
Hoje temos boas <b>CPUs</b> com cerca de <b>50GB/s</b> para a largura de banda de memória, enquanto boas <b>GPUs</b> trabalham com <b>750GB/s</b>.
</p>
</div>

Quando falamos de desempenho, quanto mais memória suas operações computacionais exigirem, maior será a vantagem de se utilizar a GPU em detrimento da CPU.

A GPU é um magnífico exemplo de hardware paralelo. Parafraseando o Manual de Boas Práticas da Nvidia: **“As GPUs da Nvidia suportam até 768 threads ativas por multiprocessador; algumas GPUs elevando este número a 1.024. Em dispositivos que possuem 30 multiprocessadores, tais como a GeForce GTX 280, isto faz com que 30,000 threads possam estar ativas simultaneamente"**. Este hardware poderosíssimo tem permitido que algumas aplicações pudessem executar até 100 vezes mais rapidamente que suas rivais restritas à CPU. 

<p align="center"><img src="https://meriatblob.blob.core.windows.net/images/2018/09/27/geforce-gtx-670.png" style="width: 100%; margin-bottom: 0px !important;"></p>

A GPU separa uma porção muito grande de sua área útil para tarefas de processamento, ao passo que a CPU usa bastante desta área para implementar a sua memória de cache.

Para uma comparação mais realista, a **NVIDIA GTX 670** - uma placa gráfica de uso geral - possui 1344 núcleos CUDA de 980 MHz cada, enquanto um processador Intel Sandybridge i7-2600 com 4 núcleos trabalha em 3,4 GHz.


## Frameworks para GPU

Em relação a programação para GPU, podemos elencar 2 frameworks como principais: 

* **OpenCL (solução open-source, uma API de baixo nível para programação paralela em diferentes tipos de processadores incluindo GPU, CPU e FPGA’s)** 
* **CUDA (Compute Unified Device Architecture)** da NVIDIA, que só pode ser usado em soluções da NVIDIA.

A principal diferença entre o **CUDA** e o **OpenCL** é que o CUDA é uma estrutura proprietária criada pela Nvidia e OpenCL é open source. Cada uma dessas abordagens traz suas próprias vantagens e desvantagens.

O consenso geral é que, se houver a possibilidade, prefira utilizar o CUDA, uma vez que os seus resultados em relação a desempenho hoje são considerados melhores. A razão deste ganho, é que a **NVIDIA**, proprietária do CUDA, fornece um grande suporte sem falar em todas as pesquisas e atualizações mantidas pela empresa.

## The Future

Neste texto introdutório estive abordando especificamente a ligação e importância do processamento de GPU para as técnicas de Deep Learning. Porém este é apenas o início da problemática. Da criação das primeiras GPUs até os dias atuais, diversar novas arquiteturas e outros componentes físicos foram entrando na jogada.

<p align="center"><img src="https://meriatblob.blob.core.windows.net/images/2018/09/27/the_future.png" style="width: 100%; margin-bottom: 0px !important;"></p>

Com a evolução constante da GPU, diversas novas técnicas estão sendo apresentadas, por meio de pesquisas e frentes levantadas por grandes empresas como o caso da Microsoft que está liderando as pesquisas em relação a programação com **FPGA (Field Programmable Gate Array)**.

Empresas como a Intel tem prometido melhorar o desempenho da própria CPU, enquanto um crescente número de pesquisas tem apontado a possibilidade da utilização de **ASICs (application-specific integrated circuit)**, componentes específicos para uma determinada ação, estão sendo considerados mais eficientes para processos como **Convoluções matemáticas**.

O importante é notar que além da evolução nos algorítmos e tecnicas, temos ainda um grande caminho a percorrer em relação a evolução do hardware.

## Testes

Estou gravando um vídeo para demonstrar o ganho na utilização de GPU x CPU para cálculos matriciais. O vídeo será uma comparação de diversos cálculos sendo processados na CPU e na GPU.

Assim que o vídeo estiver pronto, posto o link aqui... 


## Conlusão

Minha ideia neste texto foi trazer uma introdução a questão da grande adoção e utilização de GPUs no processo de Deep Learning.

Este é um assunto extenso, existem diversas novas arquiteturas computacionais visando diminuir os contras do processamento e GPU. Diversas pesquisas tem mostrado que ainda existe muito espaço para evolução deste tema.

Sendo assim em um segundo texto, devo ir mais especificamente nas questões de arquitetura, focando mais na questão do **HPC (High Performance Computing)**.

## Referências

* Vários autores. NVIDIA CUDA Compute Unfied Device Architecture – Programming Guide. NVIDIA, 1.0 edition, 2007.
* Daniel Cederman and Philippas Tsigas. GPU-quicksort: A practical quicksort algorithm for graphics processors. Jour- nal of Experimental Algorithmics, 14(1):4–24, 2009.
* Victor W Lee, Changkyu Kim, Jatin Chhugani, Michael Deisher, Daehyun Kim, Anthony D Nguyen, Nadathur Sa- tish, Mikhail Smelyanskiy, Srinivas Chennupaty, Per Ham- marlund, Ronak Singhal, and Pradeep Dubey. Debunking the 100X GPU vs. CPU myth: an evaluation of throughput computing on CPU and GPU. In ISCA, pages 451–460. ACM, 2010.
* Fernando Pereira. Técnicas de Otimização de Código para Placas de Processamento Gráfico.
* [NVIDIA Corporation. GeForce 256- The world’s first GPU](http://www.nvidia.com/page/geforce256.html).