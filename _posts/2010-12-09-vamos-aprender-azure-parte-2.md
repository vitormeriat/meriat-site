---
layout: post
title: Vamos aprender azure! Parte 2
date: 2010-12-09
categories:
    - Cloud Computing
    - Microsoft Azure
---

<p>Continuando nossa série, agora chegou o momento de irmos para o código:</p>
<p>O primeiro passo é a inclusão dos Namespaces para utilizar as bibliotecas do Windows Azure.</p>
<pre style="font-size: 1.6em !important">
    <code class="cs">
// Referências ao Windows Azure.
using Microsoft.WindowsAzure;
// Este namespace fornece uma biblioteca de cliente
//para trabalhar com os serviços de armazenamento do
//Windows Azure.
using Microsoft.WindowsAzure.StorageClient;
    </code>
</pre>


<p>Agora iremos criar um método para realizar o upload da foto selecionada:</p>
<pre style="font-size: 1.6em !important">
    <code class="cs">
private void UploadFoto()
{
   openFileDialog1.InitialDirectory =
        Environment.GetFolderPath(Environment.SpecialFolder.CommonPictures);

   // Utilizo o filtro para permitir somente a extensão jpg
   openFileDialog1.Filter = "JPG Files (*.jpg)|*.jpg";
   openFileDialog1.FileName = "";
   openFileDialog1.ShowDialog(this);
   txFileName.Text = openFileDialog1.FileName;
}
    </code>
</pre>

<p>O próximo método irá realizar a publicação da foto selecionada:</p>
<pre style="font-size: 1.2em !important">
    <code class="cs">
private void PersistirFoto()
{
  // Verifico se todos os dados foram informados
  if (string.IsNullOrEmpty(txNomeConta.Text.Trim())
      || string.IsNullOrEmpty(txChave.Text.Trim())
      || string.IsNullOrEmpty(txFileName.Text.Trim()))
  {
      // Informo a nessecidade dos campos
      MessageBox.Show("Entre com a Conta/Chave (do Blob) e Arquivo a fazer upload");
      return;
  }

  // Crio um cursor
  Cursor actualCursor = this.Cursor;

  try
  {
     // Executo o cursor como espera(a ampulheta dos windows xp e anteriores),
     //para exibir ao usuário um feedback da execução do upload.
     this.Cursor = Cursors.WaitCursor;

     // Crio um CloudStorageAccount que representa uma conta do Windows Azure.
     // Utilizo o StorageCredentialsAccountAndKey para representar as credenciais para acessar os serviços do Windows Azure..
     // Informo false para representar o uso do protocolo HTTP.
     CloudStorageAccount storageAccount =
     new CloudStorageAccount(
     new StorageCredentialsAccountAndKey(txNomeConta.Text, txChave.Text),
     false
     );

     // Crio um CloudBlobClient para fornecer o acesso ao serviço de Blob. O cliente do serviço encapsula o URI de base para o serviço de Blob.
     // Utiliza as credenciais do usuário.
     CloudBlobClient blobStorage = storageAccount.CreateCloudBlobClient();

     // Crio um CloudBlobContainer para representar um contêiner no serviço Windows Azure Blob.
     CloudBlobContainer container = blobStorage.GetContainerReference("concursofotonuvem");
     container.CreateIfNotExist();

     // configura container para ter acesso público
     var permissions = container.GetPermissions();
     permissions.PublicAccess = BlobContainerPublicAccessType.Container;
     container.SetPermissions(permissions);

     // Nome do arquivo a ser publicado
     string uniqueBlobName = string.Format("foto_{0}.jpg", Guid.NewGuid().ToString());
     CloudBlockBlob blob = container.GetBlockBlobReference(uniqueBlobName);
     blob.Properties.ContentType = "jpg";
     blob.UploadFile(txFileName.Text);
     // Exibo o endereço do arquivo publicado
     txNomeDoBlob.Text = blob.Uri.AbsoluteUri;
  }
  catch (Exception err)
  {
     txNomeDoBlob.Text = "Erro!";

     this.Cursor = actualCursor;
     MessageBox.Show("Erro: " + err.Message);
     return;
  }
  this.Cursor = actualCursor;

  MessageBox.Show("Upload foi feito com Sucesso !!nATENÇÃO: Não se esqueça de copiar o nome final da sua foto para cadastrar no site do concurso !!!");
}
    </code>
</pre>

<p>Agora é só fazer a chamada dos métodos aos respectivos eventos.</p>
<p align="justify">O próximo passo será a criação do Storage account para que possamos publicar a foto. Acesse o portal do Azure, Clique em Hosted Services, Storage Accounts &amp; CDN, selecione Storage Accounts e crie um novo Storage account conforme a imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2010/12/tela-1.png"><img alt="Tela 1" src="http://blob.vitormeriat.com.br/images/2010/12/tela-1.png" /></a></p>
<p>Agora podemos publicar nossa foto. No campo <strong>Nome da Conta,</strong> devemos passar o nome do Storage account que foi criado, neste caso será meriat. O campo <strong>Chave da conta</strong> pode ser obtida nas Propriedades no campo Primary access key.</p>
<p>Sugiro a vossas senhorias utilizar o Debug durante o upload da foto. O processo de publicação no azure é muito interessante!</p>
<p>Seu resultado deve ficar como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2010/12/f2.png"><img alt="f2" src="http://blob.vitormeriat.com.br/images/2010/12/f2.png" /></a></p>
<p>Depois disto é só copiar o link gerado e testar sua publicação na Nuvem!!!</p>
<p>Galera, não esqueçam de me mandar o link gerado e seus nomes para o meu contato. Conto com a ajuda de vocês.</p>
