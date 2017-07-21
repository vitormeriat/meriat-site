---
layout: post
title: "Custom Vision in Cognitive Services"
date: 2017-06-07
categories:
    - AI
    - Cognitive Computing
image-full: "http://meriatblob.blob.core.windows.net/images/2017/06/07/13-custom-vision.png"
---

Os serviços cognitivos da Microsoft tem evoluído muito desde seu início. Como é sabido o mesmo se iniciou no Microsoft Research com o famoso **Project Oxford**, que já disponibilizava uma série de `API's` para se trabalhar especialmente com Visão Computacional e Processamento de Linguagem Natural.

Focando na Visão Computacional, quando a Microsoft lançou o **Cognitive Services**, as API's de serviços cognitivos já disponibilizavam uma grande capacidade e variedade, te posssibilitando trabalhar de uma simples análise de imagens a detecção de faces com análise de sentimentos. Algumas combinações de serviços nos proporcionam inúmeras possibilidades de uso, como por exemplo, uma análise de sentimento em texto que dava a possibilidade do usuário enviar uma imagem que era interpretada via OCR, e tinha sua analise de sentimento exatamente igual ao texto digitado.

Contudo não era possível trabalhar de forma específica. Imagine que você precisa identificar um determinado elemento. Você tem diversas possibilidades, porém não era possível realizar um treino para a obtenção de um resultado definido... até agora...

No Build deste ano (2017), a Microsoft lançou o Serviço de Visão Customizada. Este novo serviço possibilita que você trabalhe com seu próprio dataset de treino a fim de aprender e identificar estes mesmos padrões em outras imagens. 

Seu funcionamento é extremamente simples, basta enviar seu dataset de treino, definir um label para o mesmo, mandar treinar e verificar a acurácia do modelo. O próximo passo e gerar sua API de acesso para consumir seu modelo personalizado.

<div style="margin-bottom: 3em;"></div>

### Under the Hood

Existe uma série de conceitos por debaixo dos panos. Não vou entrar em questões mais específicas sobre visão computacional ou esse aprendizado, nem tão pouco dicutir os algorítmos em si. Entretando alguma base é necessária para se utilizar o Custom Vision.

De forma mais básica e genérica o possível, podemos pensar neste aprendizado e treino como o input de dados e extração de características para uma posterior classificação/reconhecimento de imagens.

Ok, como é possível usar o Cognitive Services que já está treinado para atividades específicas, e usá-lo para reconhecer um padrão meu?

Olhando mais a fundo estamos falando aqui do conceito de `Transfer Learning`, já que na realidade, temos os algorítimos de Deep Learning e modelos pré-treinados que são ensinados a procurar detalhes a recurso distintos em um novo dataset que é informado posteriormente.

Transferência de aprendizagem, é um campo de pesquisa na aprendizagem de máquinas que se concentra no armazenamento de conhecimento adquirido ao resolver um problema, e o usa para resolver um problema diferente, mas relacionados.

> Sendo assim, Transfer Learning se trata da capacidade de usar modelos pré-treinados para solucionar problemas relacionados com um treinamento reduzido. 

Em nosso caso o `serviço de visão computacional` do Azure já possui em amplo treinamento em diversos domínios, o que nos da a possibilidade de transferir essa aprendizagem a um domínio menor... e assim temos nosso **Custom Vision API**.

Para conseguirmos um resultado satisfatório, nosso objetivo deve ser o reconhecimento de padrões de algo específico. O melhor cenário aqui é trabalhar na detecção de algo único, com um bom dataset das diversas posições, perspectiva, iluminação e etc.

<hr style="margin-bottom: 4em;margin-top: 6em;"/>

## Show me the code - First Try

Uma vez que já temos uma base vamos aos passos necessários para realizar nosso primeiro treino com o **Microsoft Congnitive Service Vision Custom** e discutir um pouco sobre sua aplicação prática...

<div style="margin-bottom: 3em;"></div>

#### Criando um novo projeto

Primeiro você vai precisar acessar o site específico do Custom Vision em [customvision.ai](https://customvision.ai). Agora é só fazer o login com sua conta do Microsoft Azure. 

Assim que você estiver logado vai ver a tela com os seus projetos, e a opção para a criação de um novo projeto. Assim como segue abaixo:

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/01-custom-vision.png" class="absolute-bg"></p>

Crie um novo projeto informando o nome do mesmo, uma descrição e selecione a opção `General`. Você pode treinar um modelo usando um cenário específico, é bastante útil em caso de já utilizarmos uma **memória** de auxílio. No meu caso eu usei como nome do projeto **vehicles**, e como modo de treino a opção **General**.

<div style="margin-bottom: 3em;"></div>

#### Carregando nosso dataset

Com o projeto criado precisamos treinar nosso modelo. Isso só é possível se tivermos dados. Então vamos lá, clique no botão upload e envie suas fotos.

> Lembre-se da importância de um bom conjunto de dados, com fotos em diversos ângulos, tamanhos, variações de iluminação e etc. Quanto mais variado, mais caracteristicas serão aprendidas.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/02-custom-vision.png" class="absolute-bg"></p>

Para este teste estive procurando uma opção simples de treino. Eu utilizei conjunto de datasets disponibilizado pela [Caltech](http://www.caltech.edu/) com foco em visão computacional. Estou utilizando neste primeiro momento o dataset **CARS** de 2001.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/03-custom-vision.png" class="absolute-bg"></p>

Aqui eu tenho minha primeira surpresa: Existe uma limitação na quantidade de arquivos a serem enviados. No total, para cada projeto podemos enviar apenas 1000 imagens para o treino.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/04-custom-vision.png" class="absolute-bg"></p>

Quem já trabalhou com este tipo de treinamento, provavelmente pode cair na mesma cilada, já que geralmente temos grandes quantidades de imagens para este tipo de treino.

<div style="margin-bottom: 5em; margin-top: 4em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
É importa ler todas as limitações e cotas de utilização de um serviço antes de usá-lo. Por exemplo, temos limitação de 1000 imagens, imagens somente até 4MB, somente JPG, PNG e BMP e etc.
</p>
</div>

Sendo assim resolvi mudar minha estratégia: Dividir minhas imagens em grupos de 300, já que estou falando de 3 tipos de veículos que quero identificar:

* Cars
* Motorbikes
* Airplanes

O que eu fiz foi criar um simples script em python para selecionar 300 imagens aleatórias do meu dataset, para cada categoria.

<pre style="font-size: 1.2em !important">
    <code class="python">
import os
import random
import numpy as np
from sklearn.model_selection import train_test_split

dir_src = "C:\\Users\\vitor.meriat\\Desktop\\cars_brad\\"
dir_test = "C:\\Users\\vitor.meriat\\Desktop\\cars_brad\\test\\"
dir_train = "C:\\Users\\vitor.meriat\\Desktop\\cars_brad\\train\\"

print('\nDiretório\n')

print('-'*30)

def get_filepaths(directory):

	file_paths = [] 
	
	for root, directories, files in os.walk(directory):
		for filename in files:
			# Supported image formats: JPEG, PNG, GIF, BMP.
			if filename[-4::] == 'jpeg' or filename[-3::] == 'jpg' or filename[-3::] == 'png' or filename[-3::] == 'gif' or filename[-3::] == 'bmp':
			    file_paths.append(filename)

	return file_paths
	
full_file_paths = get_filepaths(dir_src)
	
result = random.sample(set(full_file_paths), 300)

print('\nNúmero de arquivos do dataset: ' + str(len(full_file_paths)))

print('\nItens selecionados randomicamente: ' +str(len(result)))

X = y = result

# use 1/4 data for testing
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=0)

for xt in X_test:
	os.rename(dir_src + xt, dir_test + xt)

for yt in X_train:
	os.rename(dir_src + yt, dir_train + yt)
	
print('\nQuantidade de arquivos no conjunto de treino: ' + str(len(X_train)))

print('\nQuantidade de arquivos no conjunto de teste: ' + str(len(X_test)))
    </code>
</pre>

Você pode fazer o download deste código direto no meu gist [diretamente neste link](https://gist.github.com/vitormeriat/98785f92763bcc775d0a49704a0d33fd). O output será como o descrito abaixo:

```
λ python split.py

Diretório

------------------------------

Número de arquivos do dataset: 526

Itens selecionados randomicamente: 300

Quantidade de arquivos no conjunto de treino: 225

Quantidade de arquivos no conjunto de teste: 75
```

Nosso diretório vai ficar parecido como o descrito na imagem abaixo:

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/cars-folder.png" class="absolute-bg"></p>

Não esqueça que esse procedimento deve ser realizado para cada uma das categorias de veículos que queremos testar.

Agora eu posso fazer o upload dessas imagens... Quando cada uma das categorias são carregadas, é necessário informar uma `tag`. A tag vai representar aquele recurso, logo ao executarmos um teste, teremos de resposta a porcentagem da mesma ser ou não correspondente ao conjunto representado pela tag.

<div style="margin-bottom: 3em;"></div>

#### Um pouquinho mais sobre o reconhecimento de objetos e o tagueamento

O serviço de visão computacional do Cognitive Service hoje, é treinado para o reconhecimento de mais de 2000 objetos, sendo eles seres vivos, cenários ou ações.

Este reconhecimento é classificado e categorizado seguindo a seguinte taxonomia:

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/analyze_categories.jpg" class="absolute-bg"></p>

Em nosso caso estamos criando um modelo simples com apenas 4 classes e que são distintas entre si. Como já vimos anteriormente temos carros, motos e aviões. Se passarmos um de nossos dados de treino para o serviço de análise de imagem do Cognitive Services teremos como resultado o que se segue abaixo:

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/car.jpg" class="absolute-bg"></p>

<pre>
    <code class="json">
 "categories": [
    {
      "name": "others_",
      "score": 0.00390625
    },
    {
      "name": "outdoor_road",
      "score": 0.296875
    },
    {
      "name": "trans_car",
      "score": 0.67578125
    }
  ],
 "description": {
    "captions": [
      {
        "confidence": 0.9560722703980943,
        "text": "a car parked on the side of a road"
      }
    ],
 "tags": [
    {
      "confidence": 0.9992092251777649,
      "name": "outdoor"
    },
    {
      "confidence": 0.9986016154289246,
      "name": "car"
    },
    {
      "confidence": 0.9985461235046387,
      "name": "sky"
    },
    {
      "confidence": 0.9938879609107971,
      "name": "road"
    },
    {
      "confidence": 0.9547197818756104,
      "name": "way"
    },
    {
      "confidence": 0.8574815392494202,
      "name": "scene"
    },
    {
      "confidence": 0.8200963139533997,
      "name": "street"
    },
    {
      "confidence": 0.6744081974029541,
      "name": "highway"
    },
    {
      "confidence": 0.37572911381721497,
      "name": "stopped"
    }
 ]
    </code>
</pre>

Observe que nossa imagem foi categorizada em 3 locais, onde as duas melhores classificações são realtivas a carros. Em relação ao tagueamento, vemos `car` na segunda posição. A descrição indica **a car parked on the side of a road**. 

Faça o mesmo teste com outras images, incluindo avião e moto. Você vai perceber que o serviço tem uma boa acurácia em relação ao reconhecimento dessas imagens.

Do nosso lado, o tagueamento é importante para representar corretamente as imagens, e ter um retorno claro, já que a ideia final é consumir esse modelo via `REST`.

<div style="margin-bottom: 3em;"></div>

#### Treinando o modelo

Agora vamos ao passo mais simples, clique no botão `Train`. No meu caso o treinamento levou `23.09` segundos. 

Com o modelo treinado, você pode ir na página `PERFORMANCE`, onde encontramos o seguinte gráfico:

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/06-custom-vision.png" class="absolute-bg"></p>

Este gráfico possui duas medidas, `Precision` e `Recall`, sendo que **Precision** representa a probabilidade de seu classificador conseguir identificar corretamente uma imagem. **Recall** representa a porcentagem de imagens contendo os itens que queremos identificar no conjunto enviado.

Em nosso caso temos uma presição de `99.7%`, o que indica que alguma imagem enviada não foi reconhecida e portanto foi descartada.

Para fazer o `double check`, acesse a guia **TRAINING IMAGES** e depois **Iteration History**. Agora podemos ver qual imagem confundiu nosso modelo.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/12-custom-vision.png" class="absolute-bg"></p>

<div style="margin-bottom: 3em;"></div>

#### Hora do Teste

Agora vamos aos testes. Podemos fazer isso de forma simples utilizando o próprio site. Vamos para a aba **Quick Test**, selecione a opção **Browse local files** e selecione uma imagem para teste.

No meu caso estou utilizando uma das imagens de teste que separei anteriormente. Você pode selecionar uma imagem da própria web.

Ao fazer o upload, note que você já terá a classificação da imagem segundo seu modelo.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/13-custom-vision.png" class="absolute-bg"></p>

Tente utilizar outras imagens de teste... temos os carros, aviões ou até mesmo coisas que não tenham nenhuma ligação com o modelo treinado.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/14-custom-vision.png" class="absolute-bg"></p>

Outra coisa interessante é que ao realizar estes testes, você pode acessar a guia **PREDICTIONS**. Lá você vai ver todas as imagens que foram enviadas para teste.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/15-custom-vision.png" class="absolute-bg"></p>

Note que aqui temos a classificação que foi realizada para cada imagem. Você pode deletar uma ou todas as imagens, como também realizar um novo treino com essas imagens sendo adicionadas ao dataset original. Isso pode ou não melhorar a precisão do nosso modelo.

<div style="margin-bottom: 5em; margin-top: 4em; background-color: #dcbc14; color: #382d2d">
<p style="padding: 1.6em; font-family: courier;">
Este artigo está fortemente baseado na utilização do portal. Lembre-se que podemos fazer da <b>ingestão</b> ao <b>treino</b> via código.
</p>
</div>

#### Gerando novos modelos

Durante os testes você pode verificar que seu modelo precisa melhor. Você já sabe que um bom modelo vai depender da qualidade de seus dados, e segundo essa linha você adiciona novas imagens com mais angulos, cores e perspectivas diferentes. 

Pronto, agora você só precisa realizar outro treino para verificar se o novo conjunto vai ou não melhorar sua classificação.

O resultado deste processo é que será gerado a cada treino um novo modelo que será chamado aqui de `Iteration`.

#### Gerando nosso Modelo as a Service

Já temos nosso modelo treinado, realizamos alguns testes e agora chegou o momento de usar consumir nosso modelo.

Para isso você só precisa clicar em **Prediction URL**. Com isso veremos o `endpoint` da nossa aplicação, que vamos usar para consumir o modelo. Aqui também temos nossa `Prediction-Key`, que deve ser informada no cabeçalho da requisição.

Um detalhe importante é que você pode definir qual **Iteration** você quer consumir. Sendo assim é possível usar o modelo padrão ou definir um modelo com melhor precisão.

Em relação ao código é tudo muito simples. Você pode enviar a url ou o binário. Para efeitos práticos realizei o primeiro teste utilizando o postman. 

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/custom-vision-postman.png" class="absolute-bg"></p>

```

```

A imagem utilizada segue abaixo. Você pode acessar a imagem no seguinte link: [car-train](http://meriatblob.blob.core.windows.net/images/2017/06/07/car-train.jpg). Essa foi uma imagem retirada da internet, você pode passar um link qualquer para realizar seu teste.

<p align="center"><img src="http://meriatblob.blob.core.windows.net/images/2017/06/07/car-train.jpg" class="absolute-bg"></p>

Neste caso estou utilizando a `API` de Custom Vision Prediction, que aponta diretamente para o nosso modelo.

<div style="margin-bottom: 6em;"></div>

# Conclusão
Esta é uma parte introdutória do assunto e do serviço, porém já é possível perceber todo o potencial oferecido pelo produto. Existem ainda algumas observações importantes a serem feitas, tanto na questão mais prática em relação ao desenvolvimento, quanto na questão mais teórica, a fim de entender os propósitos e assim construir modelos satisfatórios.

Estou roterizando um vídeo sobre o assunto, e creio que lá será mais simples expor todo o conteúdo e realizar melhor os testes. Assim que o mesmo estiver publicado, atualizo este artigo.

Por hora, é isso ai pessoal.


# Referências

* [Artificial Neural Networks, Wikipedia](https://en.wikipedia.org/wiki/Artificial_neural_network)
* [Artificial Neural Networks, by Saed Sayad](http://www.saedsayad.com/artificial_neural_network.htm)
* [Neural Networks Demystified, by Stephen Welch](https://www.youtube.com/watch?v=bxe2T-V8XRs)
* [Activation function, Wikipedia](https://en.wikipedia.org/wiki/Activation_function)
* [Transfer Learning](https://en.wikipedia.org/wiki/Transfer_learning)
* [Computer Vision, Cognitive Services](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/home)
* [Custom Vision Training](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3)
* [Custom Vision Prediction](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814)
 
