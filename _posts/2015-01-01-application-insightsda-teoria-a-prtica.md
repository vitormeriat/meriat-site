---
layout: post
title: Application Insights–Da teoria a prática
date: 2015-01-01
categories:
  - ALM
---
<p align="justify">O <strong>Application Insights</strong> é um serviço de nuvem (<strong>SaaS</strong>) distribuído como parte do <strong>Visual Studio Online </strong>e integrado ao <strong>Portal do Microsot Azure</strong> <strong><u>DevOps</u></strong>. Com ele e possível garantir que a <strong>aplicação ou serviço</strong> estão realmente rodando, além de identificar problemas de desempenho e se obter uma monitoração eficiente.</p>
<p align="justify">Basicamente, o <strong>Application Insigths</strong> tenta responder as seguintes perguntas: Sua aplicação está no ar neste momento? Está funcionando? Será que está com algum erro? E o desempenho?</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/capa1.png"><img title="CAPA" alt="CAPA" src="http://blob.vitormeriat.com.br/images/2014/12/capa.png" width="700" height="364" /></a></p>
<p align="justify">Neste post, além de uma introdução ao <strong>Application Insights</strong>, vou criar uma aplicação <strong>WEB</strong> utilizando os recurso de telemetria, testando e visualizando os resultados no portal do <strong><a href="http://channel9.msdn.com/Blogs/Windows-Azure/Azure-Preview-portal" target="_blank">Microsoft Azure DevOps</a></strong>.</p>
<p><!--more--><br />
<h1>Introdução</h1>
<p align="justify">Um problema comum ocorre devido ao desenvolvimento ágil e contínuo, onde aliado ao desenvolvimento da <strong>Cloud Computing</strong>, ampliamos a capacidade de entrega contínua de recursos. Com essa agilidade e frequência em publicar novas releases, os desenvolvedores tem pouca ou nenhuma telemetria ou visibilidade em produção. Não conseguem ter visibilidade do que está acontecendo em sua aplicação. </p>
<p align="justify">Então o que queremos é ter visibilidade. Para isso precisamos responder 3 perguntas:</p>
<ul>
<li>
<div align="justify"><strong>Minha aplicação está disponível?</strong> Ou seja, meus clientes conseguem realmente acessar meu produto? Não só rapidamente mas também em diferentes regiões do mundo... </div>
</li>
<li>
<div align="justify"><strong>Minha aplicação está performática?</strong> Ou seja, ela consegue responder rapidamente? O tempo de resposta é aceitável? Estou gerando erros para os clientes?</div>
</li>
<li>
<div align="justify"><strong>A minha aplicação está tendo sucesso?</strong> Estou convertendo as vendas? Meu produto está sendo efetivo?</div>
</li>
</ul>
<p align="justify">Neste mundo ágil, é extremamente importante se ter esta visibilidade da saúde da aplicação, a fim de não comprometer a experiência da usuário, sem falar na redução do tempo para se detectar os problemas e minimizar as paradas que impactam aos clientes.</p>
<p align="justify">E como fazemos isso utilizando o <strong>Application Insights</strong>? Primeiro é importante entender que o <strong>Application Insights</strong> é integrado ao <strong>Visual Studio</strong> e sendo assim, com alguns cliques é possível monitorar sua aplicação.</p>
<p align="justify">Para responder a primeira pergunta (disponibilidade), criamos o chamado <strong>PING TESTE</strong>. Com isso você pode monitorar um ou vários endpoints, consultando eles de uma ou várias partes do mundo e garantindo a monitoração tanto da disponibilidade quanto a velocidade de acesso. </p>
<p align="justify">Alguma vezes queremos saber porque nossa aplicação está lenta. Ou as vezes ela fica lenta e outras vezes está normal. Para isso precisamos monitorar o servidor. Isso é possível com a instalação de um agente no servidor, que irá monitorar a aplicação e transmitir a <strong>telimetria</strong> ao SaaS.</p>
<p align="justify">Quando você configura o <strong>Application Insights</strong> em seu aplicativo Web, você obtém informações básicas sobre o número de usuários que visitam o seu aplicativo e os tipos de navegadores que eles usam, além de informações de desempenho. Você pode adicionar informações de uso mais detalhadas, acompanhando eventos e métricas. A nível de código também temos acesso ao SDK que é muito simples de usar.</p>
<p align="justify">Com isso podemos obter até o stack trace das exceptions geradas pela aplicação.</p>
<p align="justify">&nbsp;</p>
<h2 align="justify">DEMO – Criando uma uma aplicação com Application Insights</h2>
<p align="justify">Primeiro é necessário instalar o <a href="https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a" target="_blank">Application Insights Tools</a>. Pode ser via extension ou nuget. Outro ponto é que você consegue trabalhar com o <strong>Application Insights </strong>em qualquer versão do Visual Studio, até mesmo na versão Express. Agora para nosso primeiro exemplo, crie um <strong>Novo Projeto</strong> e selecione o <strong>template Web</strong>. Observe na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/ai001.png"><img title="AI001" alt="AI001" src="http://blob.vitormeriat.com.br/images/2014/12/ai001.png" width="700" height="540" /></a>&nbsp;</p>
<p align="justify">O <strong>Application Insights Tools</strong> é independente. Não é necessário ter uma conta do VSO já criada. Você precisa apenas ter um <strong>LiveID</strong>.</p>
<p align="justify"><font color="#ff0000"><font size="5">Quando estiver escrito <strong>AI</strong> em negrito, lê-se <strong>Application Insights.</strong></font></font></p>
<p align="justify">Agora crie uma nova aplicação WEB, e selecione o checkbox <strong>'Add Application Insights to Project'</strong>. Com isso, caso você não tenha um AI criado, será criada uma.</p>
<p align="justify"><strong>Selecione a conta</strong>, caso queira usar uma conta diferente da atual, e a <strong>subscription</strong> em que será criada os recursos de monitoração.</p>
<p align="justify">Selecione a opção <strong>'Send Telemetry to'</strong> para indicar que os dados devem ser enviados para um <strong>AI</strong> já criado ou para criar um novo específico para esta aplicação. O nosso caso será o segundo. Agora é só clicar em <strong>OK</strong> e selecionar o tipo de <strong>aplicação WEB</strong> que será criada.</p>
<p>Com isso a nova aplicação já virá toda configurada para trabalhar com o <strong>AI</strong>. Vale notar que este suporte é para todos os <strong>templates WEB</strong>. Observe a imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img021.png"><img title="IMG02" alt="IMG02" src="http://blob.vitormeriat.com.br/images/2014/12/img021.png" width="700" height="458" /></a></p>
<p align="justify">Observe que é criado na aplicação um arquivo chamado <strong>ApplicationInsights.config</strong>. Ao expandir é possível observar um arquivo chamado <strong>WebApplicationInsights overview</strong>. Aqui temos as configurações relativas ao <strong>AI</strong>, módulos e contextos do que será monitorado e exibido via portal.</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/img022.png"><img title="IMG02" alt="IMG02" src="http://blob.vitormeriat.com.br/images/2014/12/img022.png" width="700" height="555" /></a></p>
<p align="justify">Para<strong> possibilitar a telemetria</strong> em sua aplicação, já temos por default a instalação dos scripts necessários em nossa <strong>“master page”</strong>, como o destacado na imagem abaixo:</p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2014/12/ai004.png"><img title="AI004" alt="AI004" src="http://blob.vitormeriat.com.br/images/2014/12/ai004.png" width="700" height="376" /></a></p>
<p align="justify">Agora volte ao arquivo <strong>WebApplicationInsights overview</strong> e clique duas vezes nele para que seja aberto o portal do <strong>Microsoft Azure</strong>, onde realizaremos a monitoração. Será aberto em seu navegador a página específica de monitoração da sua aplicação conforme a tela abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/ai003.png"><img title="AI003" alt="AI003" src="http://blob.vitormeriat.com.br/images/2014/12/ai003.png" width="700" height="408" /></a></p>
<p align="justify">Neste momento já temos tudo o que precisamos para monitorar nossa aplicação, configurado e rodando, porém não haverá nenhuma atividade monitorada. Isso faz muito sentido, até porque nossa aplicação ainda não está rodando.</p>
<p align="justify">Para testar nossa telemetria, você só precisa rodar sua aplicação. Não é necessário nem fazer o deploy. Rode sua aplicação localmente e abra duas instâncias do mesmo em navegadores distintos:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/ai005.png"><img title="AI005" alt="AI005" src="http://blob.vitormeriat.com.br/images/2014/12/ai005.png" width="700" height="379" /></a></p>
<p align="justify">Neste momento, já conseguimos observar a coleta de informações sobre nossa aplicação como na imagem abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2014/12/ai006.png"><img title="AI006" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="AI006" src="http://blob.vitormeriat.com.br/images/2014/12/ai006.png" width="700" height="414" /></a></p>
<p align="justify">Observe que são contabilizados os usuários, sessões, páginas visualizadas de maneira simples e organizada.</p>
<p align="justify">&nbsp;</p>
<h1 align="justify">Próximo passo</h1>
<p align="justify">Este post é apenas uma introdução. Nas referências tem alguns links para aprofundar os estudos e realizar as customizações necessárias. Minha ideia é gravar um vídeo mostrando mais detalhes e dicas para a inclusão de telemetria e monitoração com o <strong>AI</strong>.</p>
<p align="justify">&nbsp;</p>
<h1 align="justify">Referências</h1>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/dn481100.aspx" target="_blank">Track web service events and metrics</a></p>
<p align="justify"><a href="http://msdn.microsoft.com/en-us/library/dn481095.aspx" target="_blank">Application Insights for Visual Studio Online</a></p>
