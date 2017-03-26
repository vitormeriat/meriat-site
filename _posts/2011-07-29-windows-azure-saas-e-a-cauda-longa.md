---
layout: post
title: 'Windows Azure: SaaS e a Cauda Longa'
date: 2011-07-29
categories:
    - Cloud Computing
    - Microsoft Azure
---
Antes de prosseguir recomendo a leitura dos seguintes posts:

* <a href="http://vitormeriat.com.br/2011/07/08/modelos-de-servio-na-nuvem-iaas-paas-e-saas/" target="_blank">Modelos de Serviço na Nuvem: IaaS, PaaS e Saas</a>
* <a href="http://vitormeriat.com.br/2011/05/09/a-cauda-longa-da-ti-the-long-tail/" target="_blank">A cauda Longa da TI (The Long Tail)</a>


Como já vimos anteriormente <strong>SaaS</strong> ou Software como Serviço é um modelo de uso onde consumimos softwares através de aplicações web disponíveis online para os usuários. Simples, barato e flexível, este modelo já virou realidade dentro de muitas empresas.

Utilizando-se da internet como meio de consumo o modelo SaaS objetiva disponibilizar os mesmos recursos de software para um número ilimitado de clientes.

Pensando neste contexto é possível observar como os conceitos de <strong>“Cauda Longa”</strong> e “<strong>Multi-Inquilino</strong>”se completa dentro do modelo SaaS.

<h3>Cauda Longa</h3>
Basicamente neste conceito temos uma procura elevada para um conjunto pequeno de produtos [ofertas] e procura reduzida para um conjunto elevado de produtos.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/07/caudalonga.png"><img alt="CaudaLonga" src="http://blob.vitormeriat.com.br/images/2011/07/caudalonga.png"/></a></p>

Na economia tradicional, os custos fixos de manutenção de estoques, permitem calcular um valor para a procura que define a fronteira entre lucro e prejuízo.

Apostar na Cauda Longa torna-se economicamente interessante pois conforme diminuímos o custo de adoção, um número maior de clientes pode adotar nossa solução. A lógica é a seguinte:

* A capacidade de adoção tende ao infinito (a curva nunca toca o eixo “X”);</font> </div>
* Para explorar a Cauda Longa precisamos então pensar em soluções e infra-estruturas de baixo custo e alto aproveitamento de recursos;
* Estas soluções devem alcançar o maior número possível de clientes;</font></div>

Com isto iremos atingir um público não suportado hoje em dia, devido ao alto custo necessário para se trabalhar com determinadas ferramentas. Fica fácil abstrair isto se imaginarmos o cenário de uma pequena empresa. Se você decidir abrir uma pequena empresa de desenvolvimento de software com 5 funcionários, seus gastos serão muito menores consumindo os serviços em nuvem. É uma questão de matemática: Basta comparar o valor de uma licença para montar um único servidor e voilá, você paga por todos os serviços necessários na nuvem com um sorriso estampado na face (dramático não?)… isto sem falar em todos os recursos que as ofertas em nuvem disponibilizam.

> A TI não precisa mais ter a posse do software. Novas modalidades de cobrança nos permitem mais flexibilidade e menos custos.

Este é realmente um conceito muito apelativo, o modelo de "<em><strong>micro-pagamento</strong></em>" que explora na cauda longa, um número muito grande de usuários que podem adotar nossa solução pagando pelo uso, por demanda, o que gera um valor muito baixo de pagamento. Nesse cenário, estamos realmente buscando o chamado "milhões de mercados de poucos" ao invés dos atuais "poucos mercados de milhões", sendo o cerne do modelo baseada na Cauda Longa.

<h2>Multi-Inquilino</h2>

Utilizando o conceito da cauda longa mostrado a cima, o termo multi-inquilino ilustra bem a evolução natural que converge para a Cloud Computing, pois refere-se ao uso do mesmo software por vários clientes e empresas de forma simultânea.

A partir dos conceitos do SaaS, fica claro o impacto na construção de uma arquitetura baseada nesse modelo. Existem diversas necessidades de tecnologia e infra-estrutura que precisam ser atendidas para que essa visão seja suportada. Cito o artigo <a href="http://msdn.microsoft.com/en-us/library/bb507203.aspx" target="_blank">An Overview of Software as a Service in Retail</a> da MSDN.

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/07/multiinquilino.png"><img alt="MultiInquilino" src="http://blob.vitormeriat.com.br/images/2011/07/multiinquilino.png"/></a></p>

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/07/legendamultiinquilino.png"><img alt="LegendaMultiInquilino" src="http://blob.vitormeriat.com.br/images/2011/07/legendamultiinquilino.png"/></a></p>

A ilustração acima representa os quatro quadrantes que representam o conceito de Multi-Inquilino.


<strong>Primeiro quadrante: </strong>Aqui cada solução é direcionada para um determinado inquilino. Isso garante completo atendimento das demandas do inquilino (cliente), mas gera um custo elevado devido a grande customização e disponibilidade de recursos individuais.

<strong>Segundo quadrante: </strong>É possível observar uma única solução direcionada para todos os inquilinos separadamente. Não há nenhuma customização presente a nenhum dos inquilinos garantindo menor custo de manutenção já que a mesma solução atende a diversos clientes.

<strong>Terceiro quadrante: </strong>Temos uma única solução para todos os inquilinos e, diferente do quadrante dois, esse solução é única e <strong>disponível</strong> para todos. Assim, podemos identificar nesse quadrante, uma solução já multi-inquilino <em>(multi-tenant),</em>apresentando total compartilhamento de recursos.

<strong>Quarto quadrante: </strong>O atendimento é diferenciado para inquilinos que exigem elevada demanda de recursos, havendo uma carga balanceada na infra-estrutura do provedor da solução SaaS <em>(tenant load balancer).</em>

<h2>Alguns dos principais benefícios são:</h2>

<ul>
<li>Implementação imediata  </li>
<li>Baixos custos  </li>
<li>Não é necessário treinar pessoas  </li>
<li>Acesso móvel  </li>
<li>Suporte on-line  </li>
<li>Sistema completo  </li>
<li>Não requer servidor  </li>
<li>Backup automatizado  </li>
<li>ROI (Retorno Sobre o Investimento) mais rápido  </li>
<li>Blindagem de acesso  </li>
<li>Soluções personalizadas  </li>
<li>Não há licenciamento  </li>
<li>Não há necessidade de manutenção pelo usuário</li>
</ul>
<p><strong></strong>&nbsp;
<p><strong>Referências</strong>:
<ul>
<li>Frederick Chong and Gianpaolo Carraro – <strong>“Architecture Strategies for Catching the Long Tail”</strong>  </li>
<li>Blog MSDN <strong>-</strong> <a href="http://blogs.msdn.com/">http://blogs.msdn.com/</a></li>
</ul>
<p>&nbsp;</p>

#### Um grande abraço e ótimo estudo!
