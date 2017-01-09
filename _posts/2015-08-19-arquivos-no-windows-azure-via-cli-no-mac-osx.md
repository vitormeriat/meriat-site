---
layout: page
title: Arquivos no Windows Azure via CLI no MAC OSX
date: 2015-08-19 02:08
author: jorgemaia
comments: true
categories: [.NET, azure, Blob, Cloud, Cloud, MAC OS, Terminal]
---
Como todos sabem eu mantenho um <a href="http://www.jorgecast.com.br" target="_blank">podcast</a> e recentemente, após algumas várias semanas sem gravar resolvi que era momento de retomar as falas. Com isso voltei a me perguntar sobre como automatizar mais o processo entre gravar, colocar a vinheta, gerar o post no site do podcast e disponibilizar aos ouvintes a boa nova. Neste insight me deparei com a mesma pergunta que outrora já havia me feito sobre qual a real necessidade de manter a minha assinatura do SoundCloud, pois tenho um site e um feed próprio!

Não tenho de maneira alguma a pretenção de fazer um trabalho melhor que o SoundCloud, mas, para minha necessidade ele está servindo somente como repositório de arquivos MP3. Se o negócio é só esse, por que não usar o blob storage do Windows Azure?

Então, depois de relutar por vários meses em manter o serviço, resolvi mudar, graças a isso, aproveitei também para retomar as escritas no Blog. (em breve colocarei todos os rascunhos no ar, preciso somente dar uma lida pois tem texto de mais de um ano).

Vamos ao que interessa! Para guardar arquivos no Storage do Azure e acessar/controlar via MAC OSX.

<strong>Passo 1 - Instalar o CLI no MAC (pode ser usado no Windows e no Linux também)</strong>

Primeiro verifique se o Node.js está instalado, se quiser usar um terminal basta digitar npm -v e ver o que acontece, se vier uma versão você tem senão você tem que fazer o <a href="https://nodejs.org/download/" target="_blank">download e instalar</a>.

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-7.50.05-PM.png"><img class="alignnone size-full wp-image-172" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-7.50.05-PM.png" alt="Screen Shot 2015-08-18 at 7.50.05 PM" width="718" height="114" /></a>

Após a instalação sabemos Node.js e podemos prosseguir.
<p style="text-align: center;"><a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-7.52.02-PM.png"><img class="alignnone size-full wp-image-173" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-7.52.02-PM.png" alt="Screen Shot 2015-08-18 at 7.52.02 PM" width="628" height="447" /></a></p>
<p style="text-align: left;">Com isso partimos para instalação do Azure Command-Line Interface (Azure CLI) que vai nos dar o poder via shell de manipular sites, serviços, vms e o Storage que é nosso foco hoje. Claro que tem muito mais coisa além disso, mas vamos focar no que nos propomos.</p>
<p style="text-align: left;">Instalando o Azure CLI</p>

<pre>sudo npm install -g azure-cli</pre>
Não se esqueça de elevar o comando para ser executado como administrador da máquina.

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.01.07-PM.png"><img class="alignnone size-full wp-image-175" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.01.07-PM.png" alt="Screen Shot 2015-08-18 at 8.01.07 PM" width="717" height="649" /></a>

E agora temos Azure CLI no MAC OSX! Então vamos ao que interessa.

Digite azure no seu terminal e bem vindo ao mundo!

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.08.03-PM.png"><img class="alignnone size-full wp-image-176" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.08.03-PM.png" alt="Screen Shot 2015-08-18 at 8.08.03 PM" width="712" height="761" /></a>

Agora para saber de todos os comandos você pode usar azure + comando e receberá uma ajuda específica.

<strong>Passo 2 - Conectar no Azure pela linha de comando </strong>

Para acessar sua conta você precisa do arquivo de publicação, para isso vamos ao invés de baixar do portal já usar o terminal e pegar o arquivo.

azure account download

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.16.28-PM.png"><img class="alignnone size-full wp-image-177" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.16.28-PM.png" alt="Screen Shot 2015-08-18 at 8.16.28 PM" width="713" height="160" /></a>

Uma janela de navegador se abrirá e após você estar logado o arquivo é baixado para sua máquina.

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.15.55-PM.png"><img class="alignnone size-medium wp-image-178" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.15.55-PM-300x247.png" alt="Screen Shot 2015-08-18 at 8.15.55 PM" width="300" height="247" /></a>

Com isso, temos o arquivo de publicação e vamos ter que importar ele para que possamos usar a conta.

azure account import /Caminho...

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.21.jpg"><img class="alignnone size-full wp-image-180" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.21.jpg" alt="Screen Shot 2015-08-18 at 8.21" width="713" height="169" /></a>

Agora vamos colocar arquivos.

Para partirmos para os arquivos, temos que entender que no Storage do Azure não temos diretórios, para separar arquivos em grupos usaremos os containers. O que precisamos então é de uma conta de armazenamento, containers e arquivos. Lembrando que você vai acessar suas imagens por uma URI, que deverá ser mais ou menos desta forma:
<p style="text-align: center;"><span style="color: #000080;"><em>"https://ContaArmazenamento.blob.core.windows.net/Container/(blob)Arquivo.extensão"</em></span></p>
<p style="text-align: center;"><a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/3482.00.png"><img class="alignnone size-full wp-image-181" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/3482.00.png" alt="3482.00" width="569" height="278" /></a></p>
Aproveito para lembrar que é possível criar um apontamento personalizado do seu domínio para este "link" de acesso.

Vamos então criar a nossa conta teste de armazenamento via comando.

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.51.25-PM.png"><img class="alignnone size-full wp-image-182" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-8.51.25-PM.png" alt="Screen Shot 2015-08-18 at 8.51.25 PM" width="734" height="268" /></a>

A solicitação do tipo da conta se refere a redundância e é dada por Locally redundant storage, Zone-redundant storage, Geo-redundant storage, Read-access geo-redundant storage o PLRS se refere a contas Premium para máquinas virtuais onde se precisa de alto desempenho e baixa latência.

Agora temos conta de armazenamento, vamos então criar um container e mandar arquivos.

Para qualquer operação em uma conta, precisamos da chave de acesso, para isso vamos listar as chaves de acesso

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-9.52.46-PM.png"><img class="alignnone size-full wp-image-183" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-9.52.46-PM.png" alt="Screen Shot 2015-08-18 at 9.52.46 PM" width="774" height="178" /></a>

se suas chaves estão suscetíveis a vazamento ou tiverem por algum motivo que serem substituídas, utilize o comando<em><span style="color: #000080;"> keys renew</span></em> para isso.

Para facilitar nossos comandos, vamos definir uma conta e sua chave para não termos que digitar sempre, para isso vamos salvar nessa sessão com uso do <em><span style="color: #000080;">export</span></em>, e as chaves de conta e chave.

<em><span style="color: #003366;"> export AZURE_STORAGE_ACCOUNT=jorgemaiateste
export AZURE_STORAGE_ACCESS_KEY=CHAVE</span></em>

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.08.11-PM.png"><img class="alignnone size-full wp-image-184" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.08.11-PM.png" alt="Screen Shot 2015-08-18 at 10.08.11 PM" width="774" height="143" /></a>

Para enviar arquivos precisamos de um container, para isso vamos criar um.

<span style="color: #000080;"><em>azure storage container create MeuContainer</em></span>

Para Listar os containers usamos

<em><span style="color: #000080;">azure storage container list</span></em>

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.14.12-PM.png"><img class="alignnone size-full wp-image-185" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.14.12-PM.png" alt="Screen Shot 2015-08-18 at 10.14.12 PM" width="777" height="513" /></a>

veja que o container não tem acesso público, o que não interessa nesse caso. Existem 3 níveis, o Off que é privado para tudo, o Blob que é publico para leitura do blob, mas não vê a listagem do container, nem os metadados e o Container que vê e lista tudo. Então vamos definir o container como Container, pois os metadados nos interessam.

<em><span style="color: #000080;">azure storage container set arquivos -p Container</span></em>

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.48.48-PM.png"><img class="alignnone size-full wp-image-187" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.48.48-PM.png" alt="Screen Shot 2015-08-18 at 10.48.48 PM" width="775" height="299" /></a>

Por fim, vamos subir um arquivo e acessar pelo navegador.

no meu caso aqui, o arquivo é uma logo minha que se chama jorge.png e está no diretório em que estou executando o comando.

<em><span style="color: #000080;">azure storage blob upload 'jorge.png' arquivos </span></em>

&nbsp;

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.52.48-PM.png"><img class="alignnone size-full wp-image-188" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.52.48-PM.png" alt="Screen Shot 2015-08-18 at 10.52.48 PM" width="775" height="283" /></a>

<a href="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.54.30-PM.png"><img class="alignnone size-full wp-image-190" src="http://www.jorgemaia.com.br/wp-content/uploads/2015/08/Screen-Shot-2015-08-18-at-10.54.30-PM.png" alt="Screen Shot 2015-08-18 at 10.54.30 PM" width="620" height="769" /></a>

&nbsp;

Para mais informações sobre os comandos use o Help do próprio CLI, digitando <em><span style="color: #000080;">azure e o comando</span></em> que quer saber.

Sempre bom usar definições sólidas, por isso recomendo uma lida no <a href="https://msdn.microsoft.com/en-us/library/dd135715.aspx" target="_blank">artigo de conceitos do MSDN sobre Naming and Referencing Containers, Blobs, and Metadata</a>.
