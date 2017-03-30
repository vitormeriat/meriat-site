---
layout: post
title: TDC 2015 SP–Ciclo de vida de aplicões Universal Windows Platform
date: 2015-07-23
categories:
  - Comunidade
  - Modern APP
  - UWP
image-full: "http://blob.vitormeriat.com.br/images/2015/07/capatdc.png"
---

<p align="justify">No dia 22 de julho de 2015 tivemos a trilha <a href="http://www.thedevelopersconference.com.br/tdc/2015/saopaulo/trilha-universal-windows" target="_blank"><strong>Universal Windows</strong></a> do <a href="http://www.thedevelopersconference.com.br/tdc/2015/" target="_blank"><strong>TDC (The Developer’s Conference) 2015</strong></a>, edição São Paulo. Este ano tive o privilégio de palestrar sobre o <strong>cliclo de vida de aplicações</strong> <strong>UWP</strong> com <strong>Windows10</strong>, e como o prometido, segue o material utilizado na apresentação junto com as referências para quem quiser se aprofundar no assunto.</p>

<p align="justify"><img title="capatdc" alt="capatdc" src="http://blob.vitormeriat.com.br/images/2015/07/capatdc.png" width="100%" /></p>

<p><iframe style="margin-bottom: 5px; max-width: 100%; border-top: #ccc 1px solid; border-right: #ccc 1px solid; border-bottom: #ccc 1px solid; border-left: #ccc 1px solid" height="665" marginheight="0" src="//pt.slideshare.net/slideshow/embed_code/key/3dOx8cqKJvFAkC" frame  width="998" marginwidth="0" scrolling="no" allowfullscreen> </iframe><br />


<h2>Resumindo a apresentação</h2>
<p align="justify">Ao iniciar, suspender e retomar seu aplicativo de forma adequada, você assegura que o cliente tenha a melhor experiência possível com seu aplicativo.</p>
<p align="justify">O primeiro passo é a instalação do aplicativo. Isso acontece de duas maneiras:</p>
<ol>
<li>
<div align="justify">Quando o usuário instala a aplicação via STORE; </div>
</li>
<li>
<div align="justify">Quando fazemos uma instalação via Visual Studio, por meio de compilação, executando o aplicativo localmente durante o desenvolvimento ou teste.</div>
</li>
</ol>
<p align="justify">Assim que instalar sua APP, ela vai estar originalmente em estado <strong>NotRunning</strong>. Este estado siginifica que o aplicativo está unicamente armazenado em DISCO.</p>
<p align="justify">Uma App pode estar no estado <strong>NotRunning</strong> caso:</p>
<ul>
<li>
<div align="justify">Nunca tenha sido iniciada </div>
</li>
<li>
<div align="justify">Foi parada durante uma execução por erro </div>
</li>
<li>
<div align="justify">Foi suspensa</div>
</li>
</ul>
<p align="justify">Para que uma <strong>APP</strong> possa entrar no modo <strong>Running</strong>, ela deve primeiro ser <strong>ativada/iniciada</strong> pelo usuário.</p>
<p align="justify">Uma <strong>APP</strong> ao ser iniciada, ou entrar no modo <strong>Running</strong>, exibe a tela incial ou a mais famosa: <strong>splash screen</strong>. Neste estado dizemos que a <strong>APP</strong> está em primeiro plano.</p>
<p align="justify">No momento em que a <strong>APP</strong> inicia, temos o disparo dos manipuladores de evento <strong>(event handlers)</strong> e as configurações de interface do usuário (<strong>UI</strong>).</p>
<p align="justify">Este momento é chamado de <strong>Activation</strong>. Aqui neste momento já podemos realizar algumas ações de configuração ou obtenção de dados, porém se alguma dessas ações demorar mais que segundos, você deve remover esta operação para outro momento, fora do <strong>Activation</strong>.</p>
<p align="justify">Uma estratégia para situações que envolvem operações de longa duração seria uma&nbsp; tela inicial estendida.</p>
<p align="justify">Ao final do processo de <strong>Activation</strong>, a <strong>splash screen</strong> desaparece e a <strong>APP</strong> entre no estado de <strong>Running</strong>. Para que um aplicativo esteja rodando, ele deve ser <strong>ativado</strong> pelo usuário e seu estado anterior deve ser <strong>NotRunning</strong>.</p>
<p>&nbsp;</p>
<h2>Referências</h2>
<ul>
<li><a href="https://channel9.msdn.com/Events/Build/2015/3-626">https://channel9.msdn.com/Events/Build/2015/3-626</a>  </li>
<li><a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh464925.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/hh464925.aspx</a>  </li>
<li><a href="https://msdn.microsoft.com/pt-br/library/windows/apps/hh986966.aspx">https://msdn.microsoft.com/pt-br/library/windows/apps/hh986966.aspx</a>  </li>
<li><a title="http://www.microsoftvirtualacademy.com/training-courses/a-developers-guide-to-windows-10" href="http://www.microsoftvirtualacademy.com/training-courses/a-developers-guide-to-windows-10">http://www.microsoftvirtualacademy.com/training-courses/a-developers-guide-to-windows-10</a> </li>
</ul>
<p>&nbsp;</p>
<h2><font color="#f79646">Bons estudos e até a próxima pessoal&nbsp; ;)</font></h2>