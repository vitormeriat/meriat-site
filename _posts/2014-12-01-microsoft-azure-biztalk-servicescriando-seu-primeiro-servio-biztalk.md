---
layout: post
title: Microsoft Azure BizTalk Services–Criando seu primeiro serviço BizTalk
date: 2014-12-01
categories:
  - BizTalk
  - Enterprise Integration
image: "http://blob.vitormeriat.com.br/images/2014/12/capa01.png"
---
<p align="justify">Este artigo é dedicado a inicialização ao <strong>Microsoft Azure Biztalk Services</strong>. A ideia é criar um serviço do Biztalk <strong>PaaS</strong>, instalar o <strong>SDK</strong> na máquina de desenvolvimento e criar um projeto utilizando o <strong>Visual Studio</strong>.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/capa01.png"><img style="background-image: none; padding-top: 0; padding-left: 0; display: inline; padding-right: 0; border-width: 0;" title="CAPA01" src="http://blob.vitormeriat.com.br/images/2014/12/capa01.png" alt="CAPA01" width="700" height="363"   /></a></p>
<p align="justify">A primeira motivação para a criação deste artigo foi a quantidade de erros que tive de solucionar em conjunto com a falta de material atual sobre o assunto (e em português nem se fala). Neste artigo minha intenção é fornecer um guia completo para se iniciar no <strong>Azure BizTalk Services</strong> abrangendo tanto a criação do serviço no <strong>Portal do Azure</strong>, quanto a configuração e instalação do <strong>SDK</strong> para o desenvolvimento.</p>
<blockquote><p>“Vale notar que estamos falando do Azure BizTalk Services que é uma solução PaaS.”</p></blockquote>
<p align="justify">Se você não estiver familiarizado com o conceito de <strong>PaaS</strong>, sugiro a leitura do seguinte artigo: <span style="font-size: medium;"><span style="font-weight: normal;"><a href="http://vitormeriat.com.br/2011/07/08/modelos-de-servio-na-nuvem-iaas-paas-e-saas/" target="_blank">Modelos de Serviço na Nuvem: IaaS, PaaS e Saas</a>.</span></span></p>
<p>Também vou dividir este post em duas partes: A criação do serviço e a instalação do SDK.</p>
<p><!--more--></p>
<h1>Agenda</h1>
<ol>
<li><span style="color: #666666;">Pré-requisitos </span>
<ol>
<li><span style="color: #666666;">Subscription ativa no Azure </span></li>
<li><span style="color: #666666;">Dependências no Azure </span></li>
<li><span style="color: #666666;">Dependências On-premisse</span></li>
</ol>
</li>
<li><span style="color: #666666;">Provisionando o serviço </span>
<ol>
<li><span style="color: #666666;">Criando o Banco de Dados </span></li>
<li><span style="color: #666666;">Criando uma Conta de Armazenamento    </span></li>
<li><span style="color: #666666;">Criando o MABS (Microsoft Azure BizTalk Services) </span></li>
<li><span style="color: #666666;">Obtendo o Controle de Acesso </span></li>
<li><span style="color: #666666;">Configurando o Azure BizTalk Services Portal </span></li>
</ol>
</li>
<li><span style="color: #a5a5a5;">Configurando o ambiente de desenvolvimento </span>
<ol>
<li><span style="color: #a5a5a5;">Instalando o certificado </span></li>
<li><span style="color: #a5a5a5;">Criando um certificado para o BizTalk Adapter Service </span></li>
<li><span style="color: #a5a5a5;">Instalando o Azure SDK BizTalk Services </span></li>
<li><span style="color: #a5a5a5;">Instalando o BizTalk Adapter Service (BAS)</span></li>
</ol>
</li>
<li><span style="color: #a5a5a5;">Configurando o BizTalk Adapter Service </span></li>
<li><span style="color: #a5a5a5;">Considerações </span></li>
<li><span style="color: #a5a5a5;">Referências</span></li>
</ol>
<p>Nesta parte vou cobrir os pontos 1 e 2 da agenda.</p>
<p>&nbsp;</p>
<h1>1 - Pré-requisitos</h1>
<h3>Subscription ativa no Azure</h3>
<p align="justify">Primeiro você vai precisar de uma conta ativa no Microsoft Azure. Se você não tiver uma conta, será possível criar uma conta de avaliação gratuita em questão de minutos. Consulte o post <a href="http://go.microsoft.com/fwlink/p/?linkid=239738&amp;clcid=0x416">Avaliação gratuita do Azure</a>.</p>
<p>&nbsp;</p>
<h3>Dependências no Azure</h3>
<p>Para a criação do BizTalk Services será necessário primeiro dispor de alguns recursos criados no próprio <strong>Microsoft Azure</strong>. Você vai precisar criar:</p>
<ul>
<li>
<div align="justify"><strong>SQL DataBase -</strong> Necessário para a gravação dos dados de <strong>Tracking</strong>. Armazena as tabelas, exibições e os procedimentos armazenados usados pelo Serviço do BizTalk, incluindo os dados de Acompanhamento. Quando você cria um serviço do BizTalk, você pode usar um Servidor SQL do Azure existente, Banco de dados SQL do Azure, ou criar automaticamente um Servidor ou Banco de dados novo. A escala do Banco de dados SQL é configurada automaticamente. Tipicamente a escala padrão é suficiente para um Serviço BizTalk. Uma dica importante em relação a este ponto é que por questões de performance você deve criar o seu Banco de Dados na mesma Região (<strong>DataCenter</strong>) em que você pretende criar o BizTalk Service;</div>
</li>
<li>
<div align="justify"><strong>Storage -</strong> Necessário para o acesso às tabelas, aos blobs e às filas usadas pelos Serviços do BizTalk para fazer o seguinte: Arquivos de log que monitoram o Serviço do BizTalk. A saída do monitoramento também é exibida na guia Monitoramento no Portal de Gerenciamento do Azure;</div>
</li>
<li>
<div align="justify"><strong>Access Control -</strong> É criado um <strong>Namespace</strong> para o controle de acesso, que será utilizado pelo Visual Studio para realizar o deploy do serviço no BizTalk.</div>
</li>
</ul>
<p>&nbsp;</p>
<h3>Dependências On-premisse</h3>
<ul>
<li>Visual Studio 2012 - Pois é... o SDK ainda não tem suporte para o VS2013 :(</li>
<li>SQL Server - Pode ser a versão Express, contanto que nas versões 2008 ou superiores</li>
<li>.Net Framework 3.5.1 e 4.5</li>
<li>IIS - Internet Information Services</li>
<li>Windows PowerShell 3.0 ou superior</li>
</ul>
<h1>2 - Provisionando o serviço</h1>
<p align="justify">Neste ponto, vamos a criação do serviço cumprindo primeiro as exigências postadas de pré-requisito. Vale notar que para a criação do serviço você deve primeiro provisionar todo o seu storage na mesma região (Datacenter). Neste exemplo eu estou utilizando a região <strong>Brazil South</strong>.</p>
<p>&nbsp;</p>
<h2>Criando um Storage</h2>
<p align="justify">É tão simples quanto acessar a aba de <strong>STORAGE</strong> e clicar em <strong>+NEW</strong> no canto inferior esquerdo. Depois é só definir a URL (que deve ser única), o  <strong>LOCATION</strong> e a <strong>SUBSCRIPTION</strong> que serão as mesmas nos outros passos.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/createstorage.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/createstorage.png" alt="createstorage" /></a></p>
<p>&nbsp;</p>
<h2>Criando um SQL Database</h2>
<p align="justify">Em relação ao banco de dados temos uma série de opções a serem consideradas. No caso deste post eu estou utilizando uma versão <strong>WEB</strong>  com <strong>MAX SIZE</strong> de <strong>100MB</strong>. Isso porque a criação deste ambiente é apenas para demonstração.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/createdatabase.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/createdatabase.png" alt="createdatabase" /></a></p>
<p align="justify">Como o BizTalk Services não é um serviço que possa ser considerado dos mais baratos, faz sentido economizar ao máximo durante os testes.</p>
<p align="justify">Outro ponto importante: Caso você queira consultar seu banco, lembre que o serviço do Banco de dados SQL do Microsoft Azure está disponível somente com a porta <strong>TCP 1433</strong>. Para acessar um banco de dados do Banco de dados SQL do Azure em seu computador, <u>verifique se o firewall permite a comunicação TCP</u> de saída na porta TCP 1433.</p>
<p>&nbsp;</p>
<h2>Criando  o Serviço</h2>
<p align="justify">Agora chegamos ao serviço em si. Essa será a tela que você vai ver se não houver nenhum serviço já criado. Para a criação do serviço, acesse a aba <strong>BIZTALK SERVICES</strong> e clique em <strong>+NEW </strong>no canto inferior esquerdo  da tela.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz01.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz01.png" alt="bz01" /></a></p>
<p align="justify">Na tela que se segue devemos preencher as informações necessárias ao serviço.</p>
<ul>
<li>
<div align="justify"><strong>BIZTALK SERVICE NAME:</strong> Informe um nome para o serviço. Lembre-se que estamos falando de uma URI, que deve ser um valor único. De qualquer maneira, o valor será validado.</div>
</li>
<li>
<div align="justify"><strong>EDITION:</strong> Aqui selecionamos qual implementação será feita. Neste exemplo vou utilizar a edição <strong>Developer</strong>. Para mais informações vide a sessão referências.</div>
</li>
<li>
<div align="justify"><strong>REGION:</strong> Aqui estamos falando do Datacenter onde a solução será hospedada.</div>
</li>
<li>
<div align="justify"><strong>SUBSCRIPTION:</strong> Aponta para qual conta o serviço deve ser criado.</div>
</li>
<li>
<div align="justify"><strong>DOMAIN URL:</strong> É possível definir um domínio personalizado. Para mais informações vide a sessão referências.</div>
</li>
</ul>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz02.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz02.png" alt="bz02" /></a></p>
<p align="justify">O próximo passo será informar as contas de armazenamento e banco de dados que criamos anteriormente. Caso você ainda não tenha feito isso, é possível realizar tanto a criação do <strong>Banco de Dados</strong>, quanto do <strong>Storage</strong> neste <strong>Wizard</strong>. Contudo um novo passo será adicionado.</p>
<p align="justify">Levando em conta que você está seguindo exatamente como neste post, informe os dados e passe para o próximo passo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz03.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz03.png" alt="bz03" /></a></p>
<p align="justify">Confirmando todas as informações, o que se segue será o provisionamento do ambiente. Este processo é demorado, algo em torno de 20 a 30 minutos.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz04.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz04.png" alt="bz04" /></a></p>
<p align="justify">Depois de jogar um pouquinho, o portal do Microsoft Azure vai exibir o status de criado. Notem que existem algumas informações preciosas…</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz05.png"><img src="http://blob.vitormeriat.com.br/image/2014/12s/bz05.png" alt="bz05" /></a></p>
<p align="justify">Assim que o serviço estiver devidamente provisionado, será gerado também um certificado auto assinado e um controle de acesso.</p>
<p align="justify"><strong><span style="color: #666666; font-size: large;">Quando criamos um Serviço do BizTalk do Azure, também é criada uma URL HTTPS constituída com o nome do seu Serviço BizTalk. Esta URL é configurada automaticamente para usar um certificado auto-assinado, funcional apenas para desenvolvimento. Quando falamos de ambiente de produção, é necessário um certificado SSL privado.</span></strong></p>
<p>&nbsp;</p>
<h2>Obtendo as Credenciais de Acesso</h2>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/access-control.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/access-control.png" alt="Access Control" /></a>A ideia ao se criar um serviço <strong>PaaS</strong> do BizTalk, é conseguir a capacidade de integração com nosso ambiente local para o desenvolvimento. Para isso é necessário obter as credenciais para isso. Sendo assim, com o serviço selecionado, clique em <strong>CONNECTION INFORMATION</strong> na barra inferior como o indicado na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz06.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz06.png" alt="bz06"  /></a></p>
<p align="justify">Ao clicar será exibido a tela com as informações de credencial relativas a sua conta. Estes valores vão nos permitir registrar e configurar o portal do nosso serviço.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz07.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz07.png" alt="bz07" /></a></p>
<p align="justify">A identidade do serviço do Controle de Acesso é um conjunto de credenciais que permitem que aplicativos ou clientes façam autenticação diretamente com o <strong>Controle de Acesso</strong> e recebam de retorno um <strong>token</strong>.</p>
<p>&nbsp;</p>
<h2>Configurando o Azure BizTalk Services Portal</h2>
<p align="justify">O portal de serviços do <strong>Azure BizTalk</strong> oferece gestão a operações <strong>B2B</strong> (<strong>EDI</strong>), dos ativos criados (schemas, transforms) e integração com o BizTalk Server (on-premisse ou IaaS).</p>
<p align="justify">Para realizar o registro e configuração do serviço ao portal, selecione seu serviço e clique na opção <strong>MANAGE</strong> como o indicado na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz08.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz08.png" alt="bz08" /></a></p>
<p align="justify">Você vai notar que uma nova aba ou janela vai se abrir com o site do portal de gestão do seu serviço <strong>BizTalk PaaS no Azure</strong>. Agora é só informar as suas credencias e clicar em <strong>REGISTER</strong> para finalizar este passo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz09.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz09.png" alt="bz09" /></a></p>
<p align="justify">Após registrado você terá acesso ao portal. Vou voltar neste passo em um próximo post, quando fizer o <strong>deploy</strong> de nossa aplicação.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz010.png"><img src="http://blob.vitormeriat.com.br/images/2014/12/bz010.png" alt="bz010" /></a></p>
<p>&nbsp;</p>
<h3 align="justify">Na próxima parte iremos cobrir os tópicos 3, 4, 5 e 6. Todos os ativos e referências estarão nos próximos posts.</h3>
<p>&nbsp;</p>
<h2>Bons estudos e até a próxima pessoal  ;)</h2>