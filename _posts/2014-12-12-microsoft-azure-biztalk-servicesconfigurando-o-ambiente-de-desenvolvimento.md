---
layout: post
title: Microsoft Azure BizTalk Services–Configurando o ambiente de desenvolvimento
date: 2014-12-12
categories:
  - BizTalk
  - Enterprise Integration
  - SOA

---
<p align="justify">Esta é a continuação do artigo <a href="http://vitormeriat.com.br/2014/12/01/microsoft-azure-biztalk-servicescriando-seu-primeiro-servio-biztalk/" target="_blank">Microsoft Azure BizTalk Services–Criando seu primeiro serviço BizTalk</a>. O que vimos anteriormente foi a criação do serviço, cobrindo os números 1 e 2 da agenda. Nesta parte vou concluir com as configurações do&nbsp; ambiente de desenvolvimento completando o passo 3.</p>
<p align="center"><a href="http://blob.vitormeriat.com.br/images/2014/12/capa02.png"><img alt="CAPA02" src="http://blob.vitormeriat.com.br/images/2014/12/capa02.png" /></a></p>
<h1>Agenda</h1>
<ol>
<li><font color="#cccccc">Pré-requisitos </font>
<ol>
<li><font color="#cccccc">Subscription ativa no Azure </font> </li>
<li><font color="#cccccc">Dependências no Azure </font> </li>
<li><font color="#cccccc">Dependências On-premisse</font></li>
</ol>
</li>
<li><font color="#cccccc">Provisionando o serviço </font>
<ol>
<li><font color="#cccccc">Criando o Banco de Dados </font> </li>
<li><font color="#cccccc">Criando uma Conta de Armazenamento&nbsp;&nbsp;&nbsp; </font> </li>
<li><font color="#cccccc">Criando o MABS (Microsoft Azure BizTalk Services) </font> </li>
<li><font color="#cccccc">Obtendo o Controle de Acesso </font> </li>
<li><font color="#cccccc">Configurando o Azure BizTalk Services Portal</font> </li>
</ol>
</li>
<li>Configurando o ambiente de desenvolvimento
<ol>
<li>Instalando o certificado  </li>
<li>Criando um certificado para o BizTalk Adapter Service  </li>
<li>Instalando o Azure SDK BizTalk Services  </li>
<li>Instalando o BizTalk Adapter Service (BAS)</li>
</ol>
</li>
<li><font color="#cccccc">Configurando o BizTalk Adapter Service </font> </li>
<li><font color="#cccccc">Considerações </font> </li>
<li><font color="#cccccc">Referências</font></li>
</ol>
<p><!--more--><br />
<h1>3 – Configurando o ambiente de desenvolvimento</h1>
<p align="justify">Nesta parte vou abortar sobre a configuração do ambiente de desenvolvimento, bem com algumas dicas importantes que podem te poupar o tempo que eu gastei tentando realizar este mesmo procedimentos.</p>
<p>&nbsp;</p>
<h3>Instalando o certificado</h3>
<p align="justify">Assim que criamos o serviço, é gerado um <strong>endpoint</strong> que será exatamente como o descrito abaixo, apenas substituindo o nome do serviço:</p>
<ul>
<li>
<div align="justify">&nbsp;<strong>&lt;<u>SeuBiztalkServiceName</u>&gt;.biztalk.windows.net</strong></div>
</li>
</ul>
<p align="justify">O que deve ser notado aqui é que para existir uma integração entre o serviço e os clientes, será necessário criar uma conexão segura. </p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/certificate.png"><img alt="certificate" src="http://blob.vitormeriat.com.br/images/2014/12/certificate.png" /></a>Para este exemplo vamos utilizar o certificado self-signed gerado pelo próprio Azure quando criamos o serviço.</p>
<p align="justify">Para isso vamos precisar fazer o download do certificado e realizar a instalação do mesmo na <font size="3"><font style="font-weight:normal;">Raiz de <font size="3"><font style="font-weight:normal;">Certificados</font></font> Confiáveis em cada máquina que requerer conexão para o deploy do serviço Biztalk que estiver sendo trabalhado. Este procedimento vai permitir a máquina local aceitar as credenciais certificadas do servidor, e estabelecer a conexão SSL. O que é válido reforçar que aqui estamos falando de um exmplo. <strong><font color="#ff0000">Para um serviço em produção é fortemente indicado que você utilize um certificado fornecido por uma entidade com</font> </strong><a href="http://en.wikipedia.org/wiki/Certificate_authority" target="_blank"><strong>certificate authority (CA).</strong></a></font></font></p>
<p align="justify">Com o serviço Biztalk que criamos anteriormente selecionado, clique em <strong>Download SSL Certificate</strong> como na imagem abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/bz011.png"><img alt="bz011" src="http://blob.vitormeriat.com.br/images/2014/12/bz011.png" /></a></p>
<p align="justify">Assim que o download do <strong>self-signed public certificate (.cer)</strong> terminar, acesse o Console de Gerenciamento Microsoft, que exibe algumas ferramentas administrativas criadas pela Microsoft e parceiros. Para isso pressione a tecla do logotipo do Windows e R. Na tela <strong>Executar</strong> ou <strong>Run</strong> apenas digite <strong>mmc</strong> e clique em <strong>OK</strong>.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/bz012.png"><img alt="bz012" src="http://blob.vitormeriat.com.br/images/2014/12/bz012.png" /></a></p>
<p align="justify">Na próxima tela clique em <strong>File</strong>, <strong>Add/Remove Snap-in</strong>. O resultado será a próxima tela.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/bz013.png"><img alt="bz013" src="http://blob.vitormeriat.com.br/images/2014/12/bz013.png"  /></a></p>
<p align="justify">No próximo passo selecione a opção <strong>Computer account</strong> e logo após <strong>Local computer</strong>, uma vez que estamos instalando o certificado para o desenvolvimento na máquina local.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/bz014.png"><img alt="bz014" src="http://blob.vitormeriat.com.br/images/2014/12/bz014.png" /></a></p>
<p align="justify">Agora navegue para a raiz da pasta <strong>Trusted Root Certification Authorities</strong> e importe o certificado que fizemos o download.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/bz016.png"><img alt="bz016" src="http://blob.vitormeriat.com.br/images/2014/12/bz016.png" /></a></p>
<p align="justify">Agora nosso certificado já está instalado.</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/bz017.png"><img alt="bz017" src="http://blob.vitormeriat.com.br/images/2014/12/bz017.png" /></a></p>
<p align="justify">&nbsp;</p>
<h2>Instalando o Azure SDK BizTalk Services</h2>
<p align="justify">Este SDK contém todos os ativos necessários para a criação de um projeto BizTalk no Visual Studio. Podemos separar os componentes do SDK em três grandes focos:</p>
<ul>
<li>
<div align="justify">O Tempo de Execução – Gerencia a conectividade entre as aplicações On-Premise, Line-Of-Business e o Serviço BizTalk no Azure;</div>
</li>
<li>
<div align="justify">O Núcleo de desenvolvimento – Contém os ativos para desenvolver as aplicações em BizTalk, como os Templates para os projetos BizTalk no Visual Studio e os modelos de artefatos;</div>
</li>
<li>
<div align="justify">As Ferramentas – Onde estão incluídos os cmdlets do PowerShell para a gestão de componentes tanto no servidor quanto no ambiente de desenvolvimento.</div>
</li>
</ul>
<p>&nbsp;</p>
<p align="justify">Estou levando em conta que você já avaliou todas as dependências de ambiente que apontei na primeira parte. Sendo assim, primeiro verifique que você está mesmo rodando o .Net Framework 4.5. Para isso pressione a tecla do logotipo do Windows e R. Na tela <strong>Executar</strong> ou <strong>Run</strong> apenas digite o comando <strong>regedit</strong>. Navegue para <strong>ComputerHKEY_LOCAL_MACHINESOFTWAREMicrosoftNET Framework SetupNDPv4Client </strong>e verifique no registro <strong>Version</strong>, como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz019.png"><img alt="bz019" src="http://blob.vitormeriat.com.br/images/2014/12/bz019.png" /></a></p>
<p>Para verificar versão do seu <strong>PowerShell</strong>, execute o comando <strong>$PSVersionTable</strong>:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz020.png"><img alt="bz020" src="http://blob.vitormeriat.com.br/images/2014/12/bz020.png" /></a></p>
<p>Com todos os requisitos supridos, faça o download do <font size="3"><a href="http://www.microsoft.com/en-us/download/details.aspx?id=39087" target="_blank">Microsoft Azure BizTalk Services SDK Setup</a>. Fique atento para baixar somente a versão correspondente ao seu SO (23 ou 64 bits). </font></p>
<p>Não esqueça de executar como Administrador. Agora aceite os termos e clique em Avançar.</p>
<p>Na tela de <strong>Features</strong>, selecionamos os recursos que serão instalados. Para o ambiente de desenvolvimento vamos instalar todos os recursos.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz021.png"><img alt="bz021" src="http://blob.vitormeriat.com.br/images/2014/12/bz021.png"/></a></p>
<p>A próxima tela, <strong>Summary</strong>, exibe tanto os componentes como o status da instalação.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz022.png"><img alt="bz022" src="http://blob.vitormeriat.com.br/images/2014/12/bz022.png" /></a></p>
<p align="justify">Durante a instalação dos componentes, será iniciado o processo para a instalação do BizTalk Adapter Service (BAS).</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz023.png"><img alt="bz023" src="http://blob.vitormeriat.com.br/images/2014/12/bz023.png" /></a></p>
<p>&nbsp;</p>
<h2>Instalando o BizTalk Adapter Service (BAS)</h2>
<p>O BizTalk Adapter Service, faz parte do recurso de comunicação que permite a integração entre o serviço na nuvem e o ambiente on-premise de desenvolvimento. Tendo isso mente, clique em Next. Aceite os termos de licença e novamente clique em Next.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz024.png"><img alt="bz024" src="http://blob.vitormeriat.com.br/images/bz024.png" /></a></p>
<p>Na próxima tela Management Service Application Pool, é onde fornecemos a conta de serviço que vai executar o IIS APPLICATION POOL do BAS. Para futura referência, o nome do pool é BizTalk Adapter AppPool. </p>
<blockquote><p>Vale notar que essa conta deve ter função de Administrador na máquina local.</p>
</blockquote>
<p align="justify">Como estamos utilizando uma máquina local, não é necessário informar o Domínio. Fora isso é só clicar em Next. </p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz025.png"><img alt="bz025" src="http://blob.vitormeriat.com.br/images/bz025.png" /></a></p>
<p align="justify">Na tela de<strong> Windows Azure BizTalk Services Deployment Details</strong>, devemos informar a <strong>URL</strong> da instância para o deploy. Você vai perceber que de fato só devemos substituir o campo <strong>&lt;deployment name&gt;</strong> pelo nome do nosso serviço.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz026.png"><img alt="bz026" src="http://blob.vitormeriat.com.br/images/bz026.png" /></a></p>
<p align="justify">Na tela de <strong>Management Service Site Binding</strong>, vamos utilizar o certificado que importamos para o IIS. Faremos isso pois em um ambiente coorporativo é necessário proteger nosso serviço e criptografar a comunicação HTTP estabelecendo uma comunicação segura. <strong>Lembre-se que para o ambiente de produção, devemos usar um certificado fornecido por uma autoridade de certificação confiável.</strong></p>
<p>Especifique o número da porta em que o Web Service BizTalk Adapter será executado. Lembre que este serviço em questão está instalado no IIS em sua máquina local. Vou deixar o valor padrão que é 8080. Agora clique em Next até concluir a instalação.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz027.png"><img alt="bz027" src="http://blob.vitormeriat.com.br/images/bz027.png" /></a></p>
<p>Quando isso ocorrer, este instalador será fechado e veremos a tela abaixo.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz028.png"><img alt="bz028" src="http://blob.vitormeriat.com.br/images/2014/12/bz028.png" /></a></p>
<p align="justify">Instalação concluída e como vemos abaixo o <strong>BizTalk Adapter AppPool</strong> foi criado com sucesso.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/bz029.png"><img alt="bz029" src="http://blob.vitormeriat.com.br/images/2014/12/bz029.png" /></a></p>
<h2>&nbsp;</h2>
<p align="justify">No próximo post finalizamos com a configuração do BAS, algumas considerações e as referências utilizadas na construção deste artigo.</p>
<p>&nbsp;</p>
<h4>Bons estudos e até a próxima pessoal&nbsp; ;)</h4>
