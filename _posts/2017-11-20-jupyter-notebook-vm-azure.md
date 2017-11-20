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



Acesse o seu servidor recém criado via SSH

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ ssh {seu-usuário}@{ip-vm}
    </code>
</pre>

Baixar o Anaconda installer bash script. Sempre utilizar a última versão

* [Anaconda]()

Vamos utilizar a pasta tmp.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ cd /tmp
    </code>
</pre>

Now it's time for downloading the bash script. Use curl to download the file.

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ curl -O https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
    </code>
</pre>



Agora vamos validar o script verificando seu hash 

<pre style="font-size: 1.6em !important">
    <code class="bash">
$ sha256sum Anaconda3-5.0.1-Linux-x86_64.sh
    </code>
</pre>

O resultado deste comando é o hash que vamos utilizar para fazer o double-check

Agora vamos ativar a instalação

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

Seu output deve ser a lista com todos os pacotes de forma ordenada.

<pre style="font-size: 1.6em !important">
    <code class="python">
 import psutil
 psutil.cpu_count()
    </code>
</pre>




## Referências

* [How to install Anaconda Python on Ubuntu](https://poweruphosting.com/blog/install-anaconda-python-ubuntu-16-04/)
* [How to create a Virtual Machine Linux on Azure]()


https://www.youtube.com/watch?v=5aWCxfHYhlg