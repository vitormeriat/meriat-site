---
layout: post
title: 'SetConfigurationSettingPublisher: Estratégias para múltiplas conexões no Azure'
date: 2011-06-21
categories:
  - Cloud Computing
  - Microsoft Azure
  - Microsoft Azure Storage
---
<p><span style="font-size:x-small;"><span style="font-size:x-small;">Duas das minhas últimas postagens sobre Azure se dedicaram a explorar um dos mais comuns problemas que ocorrem no início da utilização do mesmo:</span></span></p>
<ol>
<ol>
<li><span style="color:#555555;"><a href="http://vitormeriat.wordpress.com/2011/05/25/cloudstorageaccount-e-o-mtodo-setconfigurationsettingpublisher/" target="_blank">CloudStorageAccount e o método SetConfigurationSettingPublisher</a></span>  </li>
<li><span style="color:#555555;"><a href="http://vitormeriat.wordpress.com/2011/06/07/porque-setconfigurationsettingpublisher-precisa-ser-chamado-antes-de-fromconfigurationsetting/" target="_blank">Porque SetConfigurationSettingPublisher precisa ser chamado antes de FromConfigurationSetting?</a></span> </li>
</ol>
</ol>
<p align="justify">Estes erros são muito comuns pois na maioria dos casos não é realizado um planejamento eficaz pensando nos ambientes para teste e desenvolvimento.</p>
<p align="justify">Imagine que você está desenvolvendo uma aplicação e naturalmente resolve armazenar a configuração da conta em um arquivo <strong>.config</strong> para recuperar esta informação em tempo de execução. Utilizando a solução conforme já estudamos anteriormente, conseguimos isto sem problemas após iniciar o delegate chamado por <strong>SetConfigurationSettingPublisher</strong> como na imagem abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/06/012.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="01"   alt="01" src="http://blob.vitormeriat.com.br/images/01.png" width="660" height="321" /></a></p>
<p align="justify"><em>Estou utilizando o exemplo do artigo 1 citado anterior (baixe o <a href="http://cid-bd055aa47a388023.office.live.com/self.aspx/.Public/CredenciaisAzure.rar">Código fonte do Artigo</a>).</em></p>
<p><!--more-->
<p align="justify"><em></em></p>
<p align="justify">Tudo corre perfeitamente pois você está rodando sua aplicação dentro do ambiente de desenvolvimento do Azure. Agora vamos levar em conta que durante os testes ou desenvolvimento da aplicação você executou seu projeto e por ventura ele está sendo executado como um projeto Web local e fora do ambiente Azure. O que vai acontecer???</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/06/02.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="02"   alt="02" src="http://blob.vitormeriat.com.br/images/02.png" width="656" height="500" /></a></p>
<p align="justify">O erro aconteceu quando a aplicação estava tentando ler a "configuração" da conta (que utiliza bibliotecas da classe 'RoleEnvironment') com o método RoleEnvironment.GetConfigurationSettingValue. Nosso código já está estruturado e conforme vimos nos artigos anteriores e na figura 1, ele está funcionando perfeitamente, entretanto quando executamos a busca de nossas credenciais temos um <strong>SEHException</strong>de presente.</p>
<p align="justify">Quando estamos executando nossa aplicação dentro do ambiente de desenvolvimento do Azure, ela irá executar utilizando a porta 81 como padrão, exatamente como na imagem abaixo. Caso a aplicação esteja fora do ambiente, teríamos um número aleatório como é comum as execuções ASP.NET.</p>
<p align="justify">&nbsp;<a href="http://blob.vitormeriat.com.br/images/2011/06/03.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="03"   alt="03" src="http://blob.vitormeriat.com.br/images/03.png" width="498" height="348" /></a></p>
<p align="justify">Um primeiro conceito que podemos abstrair aqui é verificar se estamos no ambiente de desenvolvimento do Azure. Isto pode ser feito utilizando o método IsAvailable da classe&nbsp; RoleEnvironment. Quando utilizamos <code><span style="color:#333333;"><strong>RoleEnvironment.IsAvailable(), </strong></span></code>recebemos um <strong>true or false</strong> indicando se o mesmo encontra-se no ambiente Azure. Quando executamos nossa aplicação fora do contexto, recebemos um <strong>false</strong> indicando isto.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/06/04.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="04"   alt="04" src="http://blob.vitormeriat.com.br/images/04.png" width="710" height="191" /></a></p>
<p>Agora que já sabemos como identificar em qual ambiente estamos executando e de acordo com o que já estudamos anteriormente, podemos definir uma estratégia para garantir que nossa aplicação possa executar em ambientes distintos.</p>
<p>Vamos alterar o método “<em>MeuEditorDeConfiguracao</em>” conforme o código abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/06/05.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="05"   alt="05" src="http://blob.vitormeriat.com.br/images/05.png" width="710" height="132" /></a></p>
<p align="justify">Notem que se o ambiente estiver disponível nós utilizamos o método <strong>GetConfigurationSettingValue</strong> para obter o valor da configuração no arquivo <strong>.cscfg</strong>, caso contrário, utilizamos o famoso <strong>WebConfigurationManager</strong> para obter a configuração que neste caso está no arquivo <strong>Web.config</strong>.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2011/06/06.png"><img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="06"   alt="06" src="http://blob.vitormeriat.com.br/images/06.png" width="660" height="63" /></a></p>
<p align="justify">Este é um exemplo básico mas abre caminho para inúmeras possibilidades. Como desenvolvedores nos deparamos com incontáveis situações e cenários que vão exigir adaptação e flexibilidade em nossas soluções.</p>
<p align="justify">Código fonte do artigo <a href="https://skydrive.live.com/?cid=bd055aa47a388023&amp;id=BD055AA47A388023%21216#">aqui.</a></p>
<p align="justify">
<h3>&nbsp;</h3>
<h3>&nbsp;</h3>
<h3>Um grande abraço e ótimo estudo!</h3>
<p><a href="http://blob.vitormeriat.com.br/images/2011/03/logo.jpg"><img style="display:inline;float:left;" title="logo"   alt="logo" align="left" src="http://blob.vitormeriat.com.br/images/logo.jpg?w=50&amp;h=98&amp;h=98" width="50" height="98" /></a></p>
<p><strong>&nbsp;&nbsp;&nbsp;&nbsp; Twitter: <a href="http://twitter.com/vitormeriat">@vitormeriat</a></strong><br />&nbsp;&nbsp;&nbsp;&nbsp; <a href="mailto:vitormeriat@gmail.com">vitormeriat@gmail.com</a><br />&nbsp;&nbsp;&nbsp;&nbsp; <a href="mailto:vitor.pereira@studentpartners.com.br">vitor.pereira@studentpartners.com.br</a></p></p>