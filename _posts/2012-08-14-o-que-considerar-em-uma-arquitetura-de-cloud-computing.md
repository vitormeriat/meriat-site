---
layout: post
title: O que considerar em uma arquitetura de cloud computing
date: 2012-08-14
categories:
- Cloud Computing

---
<p><a href="http://blob.vitormeriat.com.br/images/2012/08/8610-138172319_800.jpg"><img style="background-image:none;margin:0 20px 0 0;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border-width:0;" title="8610-138172319_800" src="http://blob.vitormeriat.com.br/images/8610-138172319_800.jpg" alt="8610-138172319_800" width="270" height="138" align="left"   /></a></p>
<p align="justify">O ponto mais relevante ao se falar em soluções de TI é a exata compreensão do problema ou necessidade a serem sanados. As organizações devem entender os requisitos que envolvem suas aplicações antes de decidirem as plataformas e soluções a serem abordadas, uma vez que muito do sucesso de um determinado projeto depende de se ter a arquitetura certa para a aplicação certa.</p>
<p><!--more--></p>
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2012/08/250px-ibm_pc_5150.jpg"><img style="background-image:none;margin:0 0 0 20px;padding-left:0;padding-right:0;display:inline;float:right;padding-top:0;border-width:0;" title="250px-IBM_PC_5150" src="http://blob.vitormeriat.com.br/images/250px-ibm_pc_5150.jpg" alt="250px-IBM_PC_5150" width="260" height="194" align="right"   /></a>Na década de 90, o computador pessoal (PC) toma conta de lares e escritórios, e o ambiente cliente/servidor com sistemas gráficos viabilizados pela interface Windows aproximou ainda mais a informática das pessoas, gerando ao contrário das expectativas uma utilização de grande escala. Nasce ali os sistemas de gestão integrados e o usuário começa a ganhar o poder da informação. Hoje grande parte dos softwares são desenvolvidos para a internet estando sempre disponíveis em qualquer lugar, onde e quando o usuário precisa, sem necessidade de instalações aqui e lá, tendo como requisitos o acesso e um navegador internet (browser). A grande disseminação do acesso de banda larga, e o crescente uso demandaram a criação de grandes centrais de processamento de dados, os data centers. Se você faz uma pesquisa no BING, acessa seu e-mail, constrói um texto ou planilha diretamente no Google, com certeza estará usando o processamento dos milhares de servidores destas empresas espalhados no mundo.</p>
<p align="justify">
<h2 align="justify">Entrando na Nuvem</h2>
<p align="justify">O primeiro passo é saber identificar uma legítima estrutura de cloud computing. Há muitas definições para computação em nuvem, mas uma das mais concisas e amplamente reconhecidas é a do <strong>National Institute of Standards and Technology</strong> <strong>(NIST)</strong>. O NIST define cinco características essenciais, três modelos de serviço e quatro modelos de implantação. As características essenciais formam a base da definição. As características necessárias para que qualquer solução possa ser chamada de uma verdadeira solução de “nuvem” incluem:</p>
<ul>
<ul>
<li>Autoatendimento sob demanda</li>
<li>Amplo acesso à rede</li>
<li>Pool de recursos</li>
<li>Elasticidade rápida</li>
<li>Serviço medido</li>
</ul>
</ul>
<p>O NIST também define três modelos de serviço, ou o que algumas vezes recebe o nome de camadas de arquitetura:</p>
<ul>
<ul>
<li>Infraestrutura como um serviço <strong>(IaaS)</strong></li>
<li>Software como um serviço <strong>(SaaS)</strong></li>
<li>Plataforma como um serviço <strong>(PaaS)</strong></li>
</ul>
</ul>
<p>Por fim, define quatro modelos de implantação:</p>
<ul>
<ul>
<li>Nuvem privada</li>
<li>Nuvem comunitária</li>
<li>Nuvem pública</li>
<li>Nuvem híbrida</li>
</ul>
</ul>
<p>&nbsp;</p>
<h2>Ponto de partida</h2>
<p align="justify">O ponto de partida para uma empresa que cogita implementar uma plataforma de cloud computing é fazer o exame de sua arquitetura atual de TI. A ideia é alinhar as aplicações a arquitetura(computadores, redes, data center, recursos de storage etc), para manter a empresa no caminho certo no qual será possível atingir ou manter a confiabilidade e performance necessárias a um ambiente de computação na nuvem.</p>
<p align="justify">Você deve entender os requisitos individuais de suas aplicações e, se já estiverem usando uma plataforma de nuvem, entender a arquitetura de cloud correspondente. Com esse conhecimento é possível tomar decisões sobre que plataforma de cloud responde melhor às necessidades de confiabilidade e de performance das suas aplicações.</p>
<p>Abaixo segue as principais considerações ao se avaliar arquiteturas de cloud computing:</p>
<p>&nbsp;</p>
<h2>Segurança</h2>
<p align="justify">A segurança continua a ser a principal preocupação para as organizações que almejam implementar a cloud. Entre as principais inquietações estão a perda de controle de dados sensíveis, os riscos associados a ambientes multiusuários, e como dar resposta aos vários padrões e compatibilidades necessárias. É necessário saber como um ambiente partilhado e multiusuário é segmentado, de forma a evitar a sobreposição dos clientes do serviço e a quebra das fronteiras que devem ser estabelecidas<br />
entre eles. Como está arquitetada a solução, e se a infraestrutura de Cloud do fornecedor do serviço (rede e plataformas de virtualização e armazenamento) é segura.</p>
<p>&nbsp;</p>
<h2>Disponibilidade</h2>
<p align="justify">Nem todas as aplicações são iguais, tal como nem todas as plataformas de cloud são iguais. As organizações têm de priorizar as suas aplicações, identificando as que precisam estar sempre disponíveis e as que podem ter quebras de serviço, e que quebras de serviço são aceitáveis.</p>
<p align="justify">Deve-se compreender os riscos associados à indisponibilidade dos seus dados. Para as aplicações que têm de estar sempre disponíveis, é necessário considerar tecnologias de alta qualidade e de classe empresarial que tenham sido rigorosamente testadas, em detrimento do desenvolvimento interno de uma solução. É também importante procurar por soluções multi-site e por planejamento de <strong>disaster recovery / business continuity*</strong>. Para a maioria das organizações, isto significa trabalhar com um integrador de serviços ou uma empresa de consultoria, que incluem estes serviços no seu <strong>core business</strong>.</p>
<p>&nbsp;</p>
<h2>Gestão</h2>
<p align="justify">As organizações devem compreender quais as suas obrigações, em vez de saberem apenas o que esperar de um fornecedor do serviço. A maioria dos fornecedores de soluções de Cloud pública não oferecem suporte de administração. Ou os potenciais clientes dessas soluções têm os conhecimentos técnicos para desenhar a solução certa dentro de casa, ou devem procurar os serviços de um fornecedor externo. Deve existir sempre uma compreensão do nível de gestão que as suas aplicações necessitam e a identificação de um processo de gestão de mudança.</p>
<p>&nbsp;</p>
<h2>Performance</h2>
<p align="justify">Tal como nos modelos de <strong>hosting</strong> tradicionais, é importante compreender as exigências de fluxo de trabalho que vão recair na infraestrutura. Deve-se compreender quais os seus problemas e como a arquitetura de cloud que têm, ou querem adquirir, pode eliminá-los. Devem realizar seus próprios testes para compreender como um ambiente de cloud pode afetar os recursos computacionais, de rede e de armazenamento.</p>
<p>&nbsp;</p>
<h2>Conformidade</h2>
<p align="justify">As organizações devem compreender onde estão os seus dados e quem interage com os mesmos, e como. Devem compreender as áreas de conformidade que o fornecedor do serviço controla e comparar com os padrões e regulamentos a que pretendem aderir.</p>
<p>&nbsp;</p>
<h2>*</h2>
<ul>
<ul>
<li><strong>Disaster recovery </strong>[recuperação de desastre]</li>
<li><strong>Business continuity</strong> [continuidade dos negócios] é a atividade realizada por uma organização para assegurar que as funções críticas do negócio estarão disponíveis para clientes.</li>
</ul>
</ul>