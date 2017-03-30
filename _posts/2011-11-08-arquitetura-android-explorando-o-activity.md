---
layout: post
title: Arquitetura Android. Explorando o Activity
date: 2011-11-08 16:10:30.000000000 -02:00
type: post
published: true
status: publish
categories:
- Mobile
---
<p><a href="http://blob.vitormeriat.com.br/images/2011/11/android_head.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="android_head"   alt="android_head" src="http://blob.vitormeriat.com.br/images/android_head.png" width="560" height="186" /></a></p>
<p align="justify">Geralmente encontramos diversos artigos falando sobre a programação Android iniciando-se na instalação e configuração das ferramentas necessárias para o desenvolvimento. Entretanto, antes de despejar configurações e código sobre a tela, tenho aprendido o valor de se conhecer o terreno sobre o qual se anda. Neste caso, o primeiro passo para desenvolver aplicações Android é explorar um pouco da arquitetura do Activity, peça fundamental para o nosso objetivo.</p>
<p><!--more-->
<p>&#160;</p>
<h2>Visão geral</h2>
<p align="justify">Uma <strong>Activity</strong> (atividade) pode ser entendida como uma tarefa que a aplicação pode realizar. Quando me refiro a <strong>activity</strong>, estou falando de atividades que em sua maioria interagem com o usuário, logo cada tela que o usuário está vendo é uma <strong>activity</strong>. Todo aplicativo <strong>android</strong> tem pelo menos uma <strong>activity</strong>.</p>
<p align="justify">Ela é basicamente um Form onde é possível adicionar componentes (Views) e programar eventos. A <strong>activity</strong> como elemento de interface, é a classe responsável por prover a aplicação a tela que fornece a iteração ao usuário, como discar um número, tirar uma foto etc. As <strong>activities</strong> são normalmente apresentadas para o usuário como telas full-screen, elas também podem ser apresentadas de outra maneira: como janelas flutuantes (através de um tema com windosIsFloating configurado) ou embutido dentro de outra atividade (usando ActivityGroup).</p>
<p align="justify">Uma aplicação geralmente consiste de várias <strong>activities</strong> que são ligadas entre elas. Neste caso deve existir uma <strong>activity </strong>principal, que é executada quando a aplicação é iniciada e assim pode chamar outras <strong>activities</strong>.</p>
<blockquote><p><i>Uma Activity é basicamente uma classe gerenciadora de UI (Interface com o usuário). Todo aplicativo android começa por uma Activity.</i></p>
</blockquote>
<p>&#160;</p>
<h2>Ciclo de vida</h2>
<p align="justify">As Activities são gerenciadas em forma de pilha, então, quando uma nova activity é iniciada ela é colocada sobre o topo da pilha e se torna a atividade em execução, a activity anterior permanecerá sempre abaixo dela e não virá para o primeiro plano até a saída da activity em execução.</p>
<p align="justify">Vamos observar o plano de execução das atividades:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/11/ciclo-de-vida.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="ciclo de vida"   alt="ciclo de vida" src="http://blob.vitormeriat.com.br/images/ciclo-de-vida.png" width="545" height="711" /></a></p>
<p align="justify">O diagrama acima mostra os caminhos trilhados por uma activity. Os retângulos representam chamadas a métodos que você pode implementar para realizar as operações necessárias enquanto a atividade se move entre os estados. Os retângulos coloridos com cantos arredondados são os estados que a atividade esta sujeita.</p>
<p align="justify">Uma Activity tem alguns estados essenciais:</p>
<ul>
<li>
<div align="justify">Se a <strong>activity</strong> está em primeiro plano (no topo da pilha), ela está ativa ou em execução (active or running). </div>
</li>
<li>
<div align="justify">Se a <strong>activity</strong> não está mais em foco mas ainda está visível, por exemplo uma <strong>activity</strong> que não é executada em tela cheia, então a <strong>activity</strong> anterior está em pausa (Pause), ainda está em execução, mas pode ser finalizada pelo sistema em situações de baixa memória de execução. </div>
</li>
<li>
<div align="justify">Se a <strong>activity</strong> está totalmente escondida por outra <strong>activity</strong>, nesse caso ela está parada (<strong>Stopped</strong>). Ela ainda mantem todas as informações do estado, no entanto, não é mais visível para o usuário pois a janela está oculta, também, em alguns casos ela pode ser finalizada pelo sistema em situações de baixa memória. </div>
</li>
</ul>
<p>Conforme podemos ver abaixo, o plano de execução se baseia nestes estados.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/11/activity-android.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Activity Android"   alt="Activity Android" src="http://blob.vitormeriat.com.br/images/activity-android.png" width="540" height="428" /></a></p>
<p>&#160;</p>
<p align="justify">Sempre que outra activity é chamada, a activity anterior é parada, mas não descartada, o sistema à coloca em uma pilha para poder resgatá-la no futuro. Isso pode ser visto no uso de um sistema qualquer que tenha muitas telas, sempre que pressionarmos&#160; a tecla <strong>BACK</strong> vamos voltar para a tela anterior até o fechamento da aplicação.</p>
<p align="justify">Quando uma activity é interrompida porque outra é iniciada, o sistema é notificado dessa alteração através dos métodos da atividade chamada conforme vemos na imagem abaixo:</p>
<p><font size="1"><font size="1"><sup>(clique na imagem para ampliar)</sup></font></font></p>
<p><a href="http://blob.vitormeriat.com.br/images/2011/11/mtodos-android.png"><img style="background-image:none;padding-left:0;padding-right:0;display:block;float:none;margin-left:auto;margin-right:auto;padding-top:0;border-width:0;" title="Métodos Android"   alt="Métodos Android" src="http://blob.vitormeriat.com.br/images/mtodos-android.png" width="540" height="374" /></a></p>
<p>Como já ficou claro (assim espero), os métodos seguem uma sequencia lógica e estruturada. Cada chamada fica refém de uma sequencia tendo opções até a destruição dos recursos alocados.</p>
<p align="justify">Neste ciclo existem três laços extremamente importantes e devem ser monitorados dentro de sua atividade:</p>
<ol>
<li>
<div align="justify">Observando o ciclo de vida completo de uma atividade, notamos que ele acontece entre a primeira chamada do <strong>onCreate()</strong> até o <strong>onDestroy()</strong>. Esta atividade vai fazer toda a configuração do estado &quot;global&quot; da aplicação no <strong>onCreate()</strong> e liberar os recursos remanescentes em <strong>onDestroy()</strong>. </div>
</li>
<li>
<div align="justify">A atividade fica visível entre o <strong>onStart()</strong> até o <strong>onStop()</strong>. Durante esse tempo a atividade pode ser visualizada pelo usuário mesmo não estando totalmente disponível. Entre esses dois métodos você pode manter os recursos que são necessários para mostrar a atividade ao usuário. </div>
</li>
<li>
<div align="justify">Uma atividade está completamente visível para o usuário entre <strong>onResume()</strong> e <strong>onPause()</strong>. Durante esse tempo a atividade está na frente de outras atividades e interagindo com o usuário. Uma atividade pode frequentemente ir de status <i><strong>resumed</strong></i> para <i><strong>paused. </strong>P</i>or exemplo, quando o smartphone ou dispositivo onde o app roda entrar em modo <strong>sleep</strong> e por isso o código desses métodos deve ser mais simples. </div>
</li>
</ol>
<p>Espero que tenham gostado. No próximo post estarei concluindo mais algumas questões sobre o Activity.</p>
<h3>Um grande abraço e ótimo estudo.</h3>
<p><a href="http://blob.vitormeriat.com.br/images/2011/10/arquitetura.png"><img style="display:inline;float:left;margin:0 20px 0 0;" title="Arquitetura"   alt="Arquitetura" align="left" src="http://blob.vitormeriat.com.br/images/arquitetura.png?w=81&amp;h=130" width="81" height="130" /></a></p>
<p><strong>Twitter: <a href="http://twitter.com/vitormeriat">@vitormeriat</a></strong> <br /><i><strong>Microsoft MSP – Brasília</strong></i> <br /><a href="mailto:vitor.pereira@studentpartners.com.br">vitor.pereira@studentpartners.com.br</a> <br /><a href="mailto:vitor.meriat@srnimbus.com">vitor.meriat@srnimbus.com</a></p>