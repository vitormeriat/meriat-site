---
layout: post
title: 'Windows Azure Storage: Infra-estrutura de armazenamento'
date: 2011-10-26
categories:
    - Cloud Computing
    - Microsoft Azure
    - Microsoft Azure Storage
image: "http://blob.vitormeriat.com.br/images/2011/10/image_4.png"
---

Vamos falar um pouco sobre alguns dos conceitos básicos do <strong>Windows Azure Storage</strong> explorando mais um pouco da arquitetura do sistema de armazenamento.

<p><a href="http://blob.vitormeriat.com.br/images/2011/10/image_4.png"><img alt="image_4" src="http://blob.vitormeriat.com.br/images/2011/10/image_4.png"/></a></p>

Como já vimos anteriormente, o <strong>Windows Azure Storage</strong> inclui um conjunto de serviços robustos. Estes serviços estão sempre disponíveis, são duráveis e altamente escaláveis. Eles fazem parte integrante de uma aplicação de <strong>cloud-enabled</strong>. Esses benefícios são o resultado de uma complexa arquitetura que oferece muitas opções. Compreender esta arquitetura pode ser assustador, e você pode se perguntar por onde começar.

Aqui iremos explorar conceitos básicos e tecnologias que compõem o sistema de armazenamento do Windows Azure. Aconselho que você dê uma lida nos demais artigos desta série:

<ul>
<li>
<div align="justify"><a href="http://vitormeriat.wordpress.com/2011/08/03/windows-azure-storage-decolando-com-armazenamento-na-nuvem/" target="_blank">Windows Azure Storage: Decolando com armazenamento na Nuvem!</a></div>
</li>
<li>
<div align="justify"><a href="http://vitormeriat.wordpress.com/2011/08/10/windows-azure-storage-azure-storage-emulator-e-armazenamento-na-nuvem/" target="_blank">Windows Azure Storage: Azure Storage Emulator e Armazenamento na Nuvem</a></div>
</li>
</ul>

## Estrutura de armazenamento

A infra-estrutura de armazenamento para o Windows Azure é composto de assinaturas, contas, armazenamento e serviços de armazenamento. As subscrições são os pontos de entrada para o Windows Azure em si. Sem ele, você não pode acessar as ferramentas de gerenciamento que você precisa para criar as contas e serviços. Assinaturas estão associadas a um ID do Windows Live. Para adquirir uma assinatura, explore as várias ofertas e modelos e preços.

> Veja <a href="http://www.microsoft.com/windowsazure/offers/">http://www.microsoft.com/windowsazure/offers/</a> para mais informações.

Depois de criar uma assinatura, você pode acessar o portal do <strong>Windows Azure (</strong><a href="https://windows.azure.com">https://windows.azure.com</a><strong>)</strong>. A partir daqui, você pode criar contas de armazenamento, bem como outras contas, tais como contas de hospedagem para seus serviços de computação.

## Conta de Armazenamento

Cada assinatura pode ter zero ou mais contas de armazenamento. Contas de armazenamento são os pontos de entrada em serviços de armazenamento. Cada conta tem a capacidade para um <strong>terabyte de armazenamento</strong>.

Para criar uma conta de armazenamento, entre no <strong>Windows Azure Management Portal</strong> e navegue até <strong>Hosted Services</strong>, <strong>Contas de armazenamento</strong> &amp; <strong>view CDN</strong>. Clique em <strong>nova conta de Armazenamento</strong> e será exibido a seguinte caixa de diálogo.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/10/conta.png"><img alt="conta" src="http://blob.vitormeriat.com.br/images/2011/10/conta.png"/></a></p>

O valor que você digitar no campo URL é o nome da sua conta de armazenamento. Esse nome deve ser único entre todos os serviços de armazenamento existentes, porque ela forma a primeira parte do hostname dos serviços. A segunda parte do nome do host indica o tipo de serviço que é. Por exemplo, se o nome da conta de armazenamento é <strong>&quot;<font color="#004080">vitormeriat</font>&quot;</strong>, ao usar o serviço de <strong>blob</strong> o <strong>hostname</strong> será<strong> <font color="#004080">vitormeriat.blob.core.windows.net</font></strong>.

Em seguida, você precisa especificar a região a partir do qual a conta de armazenamento será atendida. A região indica a localização geográfica do centro de dados que irá hospedar seus serviços. Você deve escolher a região com base em onde seus usuários estão localizados. Se você planeja implantar um aplicativo do Windows Azure que vai usar sua conta de armazenamento, a região tanto para o armazenamento de contas como do serviço hospedado deve ser o mesmo. Escolher a mesma região proporciona benefícios de custo. Por exemplo, a largura de banda entre os serviços de armazenamento e os serviços hospedados é gratuita, e haverá ampla largura de banda, e períodos de baixa latência. 

Estas são as diferentes regiões que atualmente você pode escolher:

<ul>
<li>
<div align="justify">Norte dos EUA </div>
</li>
<li>
<div align="justify">Sul dos EUA </div>
</li>
<li>
<div align="justify">Europa do Norte </div>
</li>
<li>
<div align="justify">Europa Ocidental </div>
</li>
<li>
<div align="justify">Oeste da Ásia </div>
</li>
<li>
<div align="justify">Sudeste da Ásia </div>
</li>
</ul>

Localização das regiões citadas acima:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/10/ic525308.png"><img alt="IC525308" src="http://blob.vitormeriat.com.br/images/2011/10/ic525308.png"/></a></p>

## Emulando o armazenamento

Quando você constrói um aplicativo que usa um ou mais serviços de armazenamento, você pode desenvolver utilizando instâncias locais desses serviços. O emulador de armazenamento (storage emulator) é um aplicativo que fornece os serviços locais de tabela blob, e fila em seu ambiente de desenvolvimento.

O storage emulator faz parte do Windows Azure Software Development Kit (SDK), e que o ajuda dentre outras formas, reduzindo o custo de desenvolvimento.

> Lembre-se que uma premissa da cloud computing é que pagamos o que usarmos, sendo assim não há a necessidade de utilizar os serviços reais da nuvem a todo o momento.

Ao contrário dos serviços de armazenamento do Windows Azure, que usam um nome de domínio, os serviços locais que são hospedados pelo emulador de armazenamento e são abordados com o seu endereço IP local 127.0.0.1 e portas que vão 10000-10002. Aqui estão os serviços e os respectivos endereços:

<ul>
<li>
<div align="justify">Blob - <a href="http://127.0.0.1:10000/devstoreaccount1/">http://127.0.0.1:10000/devstoreaccount1/</a> </div>
</li>
<li>
<div align="justify">Fila - <a href="http://127.0.0.1:10001/devstoreaccount1/">http://127.0.0.1:10001/devstoreaccount1/</a></div>
</li>
<li>
<div align="justify">Tabela - <a href="http://127.0.0.1:10002/devstoreaccount1/">http://127.0.0.1:10002/devstoreaccount1/</a></div>
</li>
</ul>

Você vai notar que o caminho no endereço inclui &quot;devstoreaccount1&quot;. Este é o nome da conta para o serviço de armazenamento local. O emulador de armazenamento suporta apenas uma conta, tendo apenas um nome e uma chave o que nos dá a possibilidade de utilizarmos um atalho para a conta de armazenamento local. Isto foi abordado com mais detalhes em <a href="http://vitormeriat.com.br/2011/08/10/windows-azure-storage-azure-storage-emulator-e-armazenamento-na-nuvem/" target="_blank">Windows Azure Storage: Azure Storage Emulator e Armazenamento na Nuvem.</a>

Você pode iniciar o emulador de armazenamento através da barra de tarefas clicando em <strong>Iniciar</strong> , <strong>Todos os Programas</strong> , <strong>Windows Azure SDK v1.4 ou v1.5</strong> e clicando em <strong>Storage Emulator</strong>. Isso inicia o emulador, tanto o serviço de armazenamento como a aplicação de monitoramento para que você possa acessar a interface gráfica do usuário como na imagem abaixo:

<p><a href="http://blob.vitormeriat.com.br/images/2011/10/sem-ttulo.png"><img alt="Sem título" src="http://blob.vitormeriat.com.br/images/2011/10/sem-ttulo.png"/></a></p>

Interface gráfica para os serviços de armazenamento local.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/10/interface.png"><img alt="interface" src="http://blob.vitormeriat.com.br/images/2011/10/interface.png"/></a></p>

Outra maneira de iniciar o emulador de armazenamento é utilizando o comando <strong>DSInit</strong> na ferramenta de linha de comando fornecida no SDK do Azure. Na barra de tarefas, clique em <strong>Iniciar</strong> , <strong>Todos os Programas</strong> , <strong>Windows Azure SDK v1.4 ou v1.5</strong> e clique em <strong>Windows Azure SDK Command Prompt</strong> . O comando DSInit aceita os seguintes parâmetros:

<ul>
<li><strong>sqlInstance</strong> - Este parâmetro fornece o nome da instância do SQL Server. Você pode usar &quot;.&quot; para indicar que você deseja usar a instância padrão. Quando você usa o SQL Express como seu banco de dados, você deve fornecer o nome da instância, como &quot;SQLEXPRESS&quot;. </li>
<li><strong>forceCreate</strong> - Este parâmetro reinicializa o banco de dados. </li>
</ul>

Executando o DSInit:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/10/002.png"><img alt="002" src="http://blob.vitormeriat.com.br/images/2011/10/002.png"/></a></p>

Se tudo correr da maneira esperada, você vai ver a tela abaixo que exibe o resultado da inicialização dos serviços bem como da criação do bando de dados local que vai armazenar estas informações.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/10/001.png"><img alt="001" src="http://blob.vitormeriat.com.br/images/2011/10/001.png" /></a></p>


### Um ótimo estudo a todos.
