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

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2018/09/27/cpu-v-gpu-cap.png" style="width: 100%; margin-bottom: 0px !important;"></p>

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

Para uma comparação mais realista, a **NVIDIA GTX 670** - uma placa gráfica de uso geral - possui 1.344 núcleos CUDA trabalhando em 980 MHz, enquanto um processador Intel Sandybridge i7-2600 com 4 núcleos trabalha em 3,4 GHz.

Ainda em relação a questão de desempenho, no geral a GPU é instalada no barramento PCIe, que conhecidamente possui uma comunicação mais lenta se comparada com a comunicação da CPU e a memória do sistema.

<div style="margin-bottom: 2em; margin-top: 2em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
Este é outro ponto a se considerar, temos vantagens em usar a GPU somente quando a quantidade de cálculos a serem feitos, somado ao tempo de transferência do sistema-GPU se torna insignificante em relação ao tempo de cálculo em si.
</p>
</div>

Não existe uma proporção indicada. Neste momento estou me aprofundando no tema, revisando códigos e estudos que realizei tenando comparar o desempenho de determinadas implementações na CPU e na GPU. Particularmente, minha  tendência foi programar tudo o possível no **Tensorflow** para GPU, o que hoje, aprendi ser um erro.


## Frameworks para GPU

Em relação a programação para GPU, podemos elencar 2 frameworks como principais: 

* **OpenCL (solução open-source, uma API de baixo nível para programação paralela em diferentes tipos de processadores incluindo GPU, CPU e FPGA’s)** 
* **CUDA (Compute Unified Device Architecture)** da NVIDIA, que só pode ser usado em soluções da NVIDIA.

A principal diferença entre o **CUDA** e o **OpenCL** é que o CUDA é uma estrutura proprietária criada pela Nvidia e OpenCL é open source. Cada uma dessas abordagens traz suas próprias vantagens e desvantagens.

O consenso geral é que, se houver a possibilidade, prefira utilizar o CUDA, uma vez que os seus resultados em relação a desempenho hoje são considerados melhores. A razão deste ganho, é que a **NVIDIA**, proprietária do CUDA, fornece um grande suporte sem falar em todas as pesquisas e atualizações mantidas pela empresa.

Não estou elencado aqui **frameworks** como **Tensorflow**, **Keras**, **CNTK** e afins, uma vez que estes são frameworks criados com foco em **deep learning**, onde apenas existe suporte a utilização da GPU. Eles não são focados na programação efetiva da GPU.


## The Future

Neste texto introdutório estive abordando especificamente a ligação e importância do processamento de GPU para as técnicas de Deep Learning. Porém este é apenas o início da problemática. Da criação das primeiras GPUs até os dias atuais, diversar novas arquiteturas e outros componentes físicos foram entrando na jogada.

<p align="center"><img src="https://meriatblob.blob.core.windows.net/images/2018/09/27/the_future.png" style="width: 100%; margin-bottom: 0px !important;"></p>

Com a evolução constante da GPU, diversas novas técnicas estão sendo apresentadas, por meio de pesquisas e frentes levantadas por grandes empresas como o caso da Microsoft que está liderando as pesquisas em relação a programação com **FPGA (Field Programmable Gate Array)**.

Empresas como a Intel tem prometido melhorar o desempenho da própria CPU, enquanto um crescente número de pesquisas tem apontado a possibilidade da utilização de **ASICs (application-specific integrated circuit)**, componentes específicos para uma determinada ação, estão sendo considerados mais eficientes para processos como **Convoluções matemáticas**.

O importante é notar que além da evolução nos algorítmos e tecnicas, temos ainda um grande caminho a percorrer em relação a evolução do hardware.

## Testes

Este é um breve resumo dos testes realizados, toda a demonstração está no vídeo abaixo. Aqui vou apenas fazer um breve resumo e incluir alguns resultados que consegui. Todo o código fonte está no meu **github**, e pode ser baixado no seguinte link: [gpucpudemonstration](http://www.localhost/). 

A primeira parte do nosso teste é verificar se temos uma GPU disponível. Fazemos isso rodando alguns comandos do **Linux** e outros do próprio **Tensorflow**.

O código que eu utilizo é basicamente criar uma matriz de **N** por **N**, onde **N** é um número que vamos aumentando gradativamente para verificar a capacidade dos devices (**GPU, CPU**), para realizar esses cálculos.

Para verificar a importância dos **frameworks** especializados em **Deep Learning**, fiz o primeiro teste rodando sobre **Numpy**, depois as mesmas operações rodando sobre **Tensorflow**, tanto na CPU quanto na GPU. No caso do Tensorflow, isso é determinado pela variável **device_name**. O Numpy, como descrito no vídeo, não oferece suporte a GPU.

##### Numpy
<pre style="font-size: 1.4em !important">
    <code class="python">
  A=np.random.normal(size=(shapeMtx, shapeMtx))
  B=np.random.normal(size=(shapeMtx, shapeMtx))

  subtract = np.subtract(A, B)
  add = np.divide(A, B)
  multiply = np.multiply(A, B)
    </code>
</pre>

##### Tensorflow
<pre style="font-size: 1.4em !important">
    <code class="python">
  with tf.device(device_name):
    A = tf.random_uniform(shape=shape, minval=0, maxval=1)
    B = tf.random_uniform(shape=shape, minval=0, maxval=1)
    
    subtract_operation = tf.subtract(A, B)
    divide_operation = tf.divide(A, B)
    multiply_operation = tf.multiply(A, B)

  startTime = datetime.now()
  with tf.Session(config=tf.ConfigProto(allow_soft_placement=True, log_device_placement=True)) as session:
    session.run(subtract_operation)
    session.run(divide_operation)
    session.run(multiply_operation)
    </code>
</pre>

Como o exemplificado no vídeo, os tempos se alteram a medida em que aumentamos as dimensões de nossa matriz. Vemos que a CPU tem vantagem quando os cáculos são menores, enquando a GPU vai ganhando a medida em que os cálculos vão se tornando maiores.

Em relação a performance, podemos observar no segundo teste, que a GPU possui um aumento muito menor de tempo para realizar determinados cálculos se comparado a CPU. 

<p align="center"><img src="https://meriatblob.blob.core.windows.net/images/2018/09/27/graphic_test_performance.png" style="width: 100%; margin-bottom: 0px !important;"></p>

Neste teste especificamente, o tempo de execução na GPU tem um aumento tão pequeno em relação ao da CPU, que aparentemente temos a impressão que para o gráfico que estamos analisando apenas os tempos da CPU sofreram alteração. Como pode ser visto abaixo, ao imprimir os tempos, é possível realizar uma validação mais precisa. 

```
Output
...

GPU times [0.13785886764526367, 0.007532835006713867, 0.00854039192199707, 0.009807109832763672, 0.010930776596069336, 0.011966943740844727, 0.012804269790649414, 0.014283418655395508, 0.01694202423095703, 0.01774454116821289, 0.019214153289794922, 0.019917011260986328, 0.0216977596282959, 0.022628068923950195, 0.025137662887573242, 0.02427196502685547, 0.028975486755371094, 0.029575824737548828, 0.028879880905151367, 0.03321361541748047, 0.032982587814331055, 0.03345513343811035, 0.03653764724731445, 0.035642385482788086, 0.03930830955505371, 0.04390144348144531, 0.045243024826049805, 0.0432429313659668, 0.04667401313781738, 0.051265716552734375, 0.05484771728515625, 0.05348992347717285, 0.05866360664367676, 0.05812430381774902, 0.05793881416320801, 0.0610194206237793, 0.06328725814819336, 0.06955838203430176, 0.06947898864746094, 0.07118368148803711]

CPU times [0.28919482231140137, 0.36597657203674316, 0.4756290912628174, 0.6124699115753174, 0.7608673572540283, 0.9239287376403809, 1.092865228652954, 1.3050789833068848, 1.5583577156066895, 1.8389079570770264, 2.1097397804260254, 2.445690393447876, 2.819725275039673, 3.2182812690734863, 3.6523375511169434, 4.114335775375366, 4.665944337844849, 5.188570737838745, 5.789913654327393, 6.40700364112854, 7.094855308532715, 7.836256980895996, 8.639605522155762, 9.486554145812988, 10.296368837356567, 11.298496007919312, 12.23202109336853, 13.28882646560669, 14.383679151535034, 15.580460548400879, 16.79129123687744, 18.077450037002563, 19.419445753097534, 20.82856273651123, 22.34893012046814, 23.885477781295776, 25.47702121734619, 27.175251007080078, 28.97485899925232, 30.87795114517212] 
```
Abaixo segue o vídeo da demonstração completa...

<p align="center"><iframe height="506" src="https://www.youtube.com/embed/0qyZkh9OuaY?rel=0" width="100%" allowfullscreen style="border: 0px;"></iframe></p>


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