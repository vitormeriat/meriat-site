---
layout: post
title: "Provision the Jupyter Notebook in Azure VM for Linux"
date: 2017-11-20
categories:
    - AI
    - Machine Learning
    - Data Science
tags:
    - ai
    - machine learning
    - data science
image-full: "http://meriatblob.blob.core.windows.net/images/2017/11/20/capa-jupyter-azure.png"
lang: pt
description: "Neste post vamos passo a passo criar uma máquina virtual Linux no Azure, instalar o Jupyter Notebook via Anaconda. Também vamos conectar em nossa VM via um túnel SSH para conseguir utilinar nossos Notebooks como se estevessem rodando local.\nEm poucos passos vamos ter a disposição todo o poder da Cloud Computing para rodar nossos algorítimos com muito mais robustez."
---

<p align="center" style="background-color: #f2f2f2; width: 100%;"><img src="http://meriatblob.blob.core.windows.net/images/2017/11/20/capa-jupyter-azure.png" style="margin-bottom: 0px !important;"></p>

Neste post vamos passo a passo criar uma máquina virtual Linux no Azure, instalar o Jupyter Notebook via Anaconda. Também vamos conectar em nossa VM via um túnel SSH para conseguir utilinar nossos Notebooks como se estevessem rodando local.

## Justificativa

Para facilatar deixe-me explicar o motivo deste texto: Estes são os passos que executei em algumas demonstrações que fiz abordando o quanto a `Cloud Computing` é importante para o avanço da inteligência artificial. Estamos falando de uma área da computação que é estudada desde a década de 40. 

Os grande avanços nessa área se dão basicamente por que hoje (em grande parte graças a Cloud Computing), temos um grande `poder computacional` bem como `poder de armazenamento` de dados, isso de forma acessível. Já preparei um vídeo apenas sobre este assunto que vai estar disponível em breve no meu canal.

Sendo assim nada mais justo do que usar todo este poder computacional ao nosso favor, utilizando os grande players de mercado para provisionar em minutos a infra necessária para treinar nossos modelos de manira rápida. Assim conseguimos nos concetrar em atividades mais importantes.

## Demonstração da instalação

<p align="center"><iframe height="506" src="https://www.youtube.com/embed/5aWCxfHYhlg?rel=0" width="900" allowfullscreen style="border: 0px;"></iframe></p>

## Requisitos

Para finalizar este tutorial, você vai precisar de uma conta ativa no Microsoft Azure, e caso sua máquina seja Windows, de acesso ao `bash` ou utilizar o `cmd` com ajuda do `putty`. Abaixo segue as referências.

* [Como criar uma conta gratuita no Microsoft Azure](https://azure.microsoft.com/pt-br/free/)
* [Como habilitar o bash no Windows 10](http://www.techtudo.com.br/dicas-e-tutoriais/noticia/2016/04/como-instalar-e-usar-o-shell-bash-do-linux-no-windows-10.html)
* [Como conectar via SSH no Windows utilizando o Putty](https://technet.microsoft.com/pt-br/library/hh225041(v=sc.12).aspx)

## Hands on

Acesse o portal do Microsoft Azure: [portal.azure.com](https://portal.azure.com/). Após o login execute os seguintes passo como o exemplificado no vídeo:

1. Clique em `+ New` no menu a esquerda;
2. Em `Search the Market Place` pesquise por **Ubuntu Server 17.10**;
3. Clique em `Create`;
4. Informe o nome da sua VM. Insira um Username e um Password. Crie um Resource Group e clique em **OK**;
5. Escolha o Size da sua máquina virtual e clique em **OK**;
6. No próximo passo acesso o `Network security group` e adicione uma nova `inbound rule` para a porta **8888**, que é onde vamos acessar nosso **Notebook**;
7. Em `Public ip address` selecione **um ip estático** e prossiga para a confirmação;
8. Finalize a instalação, aguarde o provisionamento e na tela que se seguirá, copie o `IP` que será criado para sua nova VM.

Agora que temos nossa VM criada no Azure, vamos executar os passos para a instalação do Jupyter Notebook.

O primeiro passo será acessar o servidor recém criado via SSH. Informe o usuário e o ip conforme o exemplo abaixo:

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ ssh {seu-usuário}@{ip-vm}
    </code>
</pre>

Assim que você realizar o acesso, informe sua senha e pronto. Você já vai estar conectado em sua VM. Agora vamos baixar o `Anaconda installer bash script`. Neste ponto acesso o site abaixo e verifique qual a última versão do **Anaconda**.

No momento deste post, a versão da última distribuição do Anaconda é a `5.0.1 For Linux`. Todos os exemplos vão utilizar essa versão, então lembre-se de trocar caso necessário.

* [Anaconda](https://www.anaconda.com/download/#linux)

Por questões de boas práticas, vamos acessar nossa pasta `tmp` para realizar o donwload do script acima.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ cd /tmp
    </code>
</pre>

Agora vamos utilizar o comando `curl` para fazer o download do arquivo.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ curl -O https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
    </code>
</pre>

Outra boa prática é validar a integridade do download antes da instalação. Neste caso específico vamos executar o script abaixo para fazer o double-check junto ao site do **Anaconda**.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ sha256sum Anaconda3-5.0.1-Linux-x86_64.sh
    </code>
</pre>

Acesse [esse link](https://docs.anaconda.com/anaconda/install/hashes/Anaconda3-5.0.1-Linux-x86_64.sh-hash) para verificar se os `hashes` correspondem. 

Com as informações validadas, execute o comando abaixo para inicializar a instalação.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ bash Anaconda3-5.0.1-Linux-x86_64.sh
    </code>
</pre>

Neste ponto você vai receber algumas mensagens, para confirmar a instalação, para confirmar que leu e concorda com os termos da instalação e posteriormente para confirmar qual o caminho onde a instalação será realizada. 

Confirme todos os passos e por último, após a instalação ser realizada com sucesso você vai receber a mensagem abaixo:

```
Output
...
installation finished.
Do you wish the installer to prepend the Anaconda3     install location
to PATH in your /home/vitormeriat/.bashrc ? [yes|no]
[no] >>> 
```

Esta é uma confirmação necessária para utilizarmos o `conda command utility`, que devo explicar melhor em um próximo vídeo. Inform **yes** e finalize o procedimento.

Agora é só executar o comando abaixo para ativar a instalação e vamos estar prontos para testar nosso **Jupyter Notebook**.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ source ~/.bashrc
    </code>
</pre>

Para verficar se a instalação ocorreu como o esperado, vamos listar todos os pacotes instalados pelo Conda utilizando o comando abaixo:

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ conda list
    </code>
</pre>



## Referências

* [How to install Anaconda Python on Ubuntu](https://poweruphosting.com/blog/install-anaconda-python-ubuntu-16-04/)
* [How to create a Virtual Machine Linux on Azure]()


https://www.youtube.com/watch?v=5aWCxfHYhlg