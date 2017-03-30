---
layout: post
title: SUT, Stubs, Mocks e os primeiros passos para o TDD
date: 2013-02-15 
categories:
- Agile
- Testes

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/02/tdd.png"><img title="tdd" style="border-top:0;border-right:0;background-image:none;border-bottom:0;float:left;padding-top:0;padding-left:0;margin:0 15px 0 0;border-left:0;display:inline;padding-right:0;"   alt="tdd" align="left" src="http://blob.vitormeriat.com.br/images/tdd.png" width="240" height="228" /></a>É consenso que os testes são de extrema importância para o desenvolvimento de um produto. Com o passar dos anos os testes foram galgando diferentes posições dentro deste mundo. Mesmo que você não seja um optante ou profundo conhecedor do <strong>TDD</strong>, é provável que já tenha escrito ou testado seu código de alguma forma. Sendo assim, é importante conhecer alguns dos mecanismos, artefatos e técnicas da disciplina de testes. </p>
<p align="justify">Existem discussões intermináveis sobre o valor dos testes em detrimento do tempo que usamos para codificá-los. O que não se discute é sobre sua importância. Podemos verificar se uma funcionalidade está corretamente implementada e garantir durante o desenvolvimento que esta implementação não será quebrada.</p>
<p align="justify">O problema é que trabalhar com testes no mundo real não é tão simples. Quando estamos desenvolvendo nossas aplicações, nos deparamos com a necessidade de testes que envolvem banco de dados, web services, componentes de terceiros e por ai vai. Tudo isso pode deixar a complexidade do teste extremamente alta tanto para escrita quanto para depuração, sem falar que isso pode tornar o seu teste falho. Imagine que você escreve um determinado teste usando um banco de dados compartilhado e durante sua rotina de execução de teste ele falha. No primeiro momento você não sabe se ocorreu alguma alteração em nível de código ou se simplesmente alteraram os valores no banco de dados levando o teste a falha.</p>
<p align="justify">É frequente ouvir equipes dizerem que não vão escrever determinados testes devido a dificuldade de traduzir certas partes do código. Ai entra um dos grandes desafios da disciplina de testes: <u>desenvolver estratégias para isolar a complexidade do código e facilitar a escrita dos testes</u>.</p>
<p align="justify">O que se segue abaixo são alguns dos termos, e dicas que para quem pretende iniciar no mundo dos testes.</p>
<p><!--more--><br />
<h2>&#160;</h2>
<h2>Conhecendo o SUT?</h2>
<p align="justify">Quando estamos estudando sobre testes é comum encontrar na literatura a sigla <strong>SUT</strong>. Geralmente ela aparece em expressões como &quot;o teste será realizado contra o SUT&quot; ou &quot;a <strong>Assert</strong> é contra o SUT&quot;. Mas o que é o SUT?</p>
<p align="justify">SUT vem do inglês<strong> System Under Test</strong> (sistema em teste) e se refere ao que estamos testando. É possível que em alguma literatura você encontre referência a <strong>CUT</strong> como sendo classe em teste ou código em teste, mas o mais usual é SUT. Quando testamos algo, nós nos referimos à ele como sendo o SUT.</p>
<p>&#160;</p>
<h2>Prevenindo contra dependências</h2>
<p align="justify">Quando escrevemos testes de unidade temos que ter em mente que eles devem executar em de maneira independente em relação ao ambiente onde está rodando. Não podemos escrever testes que rodem apenas em nossa máquina local. Nossos testes devem rodar seja na máquina do colega como no servidor de build. Para que isso ocorra devemos escrever testes independentes de infraestrutura, banco de dados, sistema operacional e qualquer coisa que não esteja sobre o domínio do desenvolvedor. Para prevenir estas situações temos objetos que nos ajudam a suprimir esta dependência e realizar o teste de maneira correta.</p>
<p align="justify">Uma das principais estratégias para ampliar a cobertura de testes nos cantos mais densos de nosso código, bem como zerar as dependências é o uso de objetos mock e stubs.</p>
<p>&#160;</p>
<h2>Conhecendo os objetos Mock e Stub?</h2>
<p align="justify">Bom iniciando meus estudos sobre testes e pondo a mão na massa, fiquei em dúvida sobre qual a diferença entre mocks e stubs (o que posteriormente observei ser uma dúvida comum).</p>
<p align="justify">Usando como base o artigo <strong>&quot;<em>Mocks Aren't Stubs</em>&quot;</strong> de <strong>Martin Fowler</strong>, temos a seguinte descrição sobre mocks e stubs:</p>
<ul>
<ul>
<li>
<div align="justify">Mocks: objetos pré-programados com informações que formam uma especificação das chamadas que esperam receber; </div>
</li>
<li>
<div align="justify">Stubs: providenciam respostas pré-configuradas para as chamadas feitas durante os testes, normalmente não respondem a nada que não esteja programado para o teste. Stubs também podem gravar informações sobre as chamadas, como um gateway que lembra as mensagens que 'enviou', ou talvez apenas quantas mensagens 'enviou'. </div>
</li>
</ul>
</ul>
<p align="justify">Conceitualmente são diferente embora na prática sejam parecidos. Inicialmente você pode pensar que diferença seja o fato de stubs serem classes estáticas e mocks serem classes dinâmicas geradas por algum tipo de ferramenta como<strong> Rhino Mocks</strong> ou <strong>NMock</strong>. Este é o ponto...</p>
<p align="justify">Stubs se diferem dos Mocks em seu uso. Stubs são usados ​​para representar e testar o estado de um objeto, enquanto Mocks testam suas interações.</p>
<p align="justify">Utilizando ainda o artigo de Martin Fowler sobre o assunto, podemos concluir que objetos Mock esperam a execução de determinados métodos e seu resultado remete a falha do teste caso a resposta não seja a esperada. </p>
<p align="justify">Já os objetos Stubs fornecem respostas &quot;enlatadas&quot; e não levam o teste de unidade a falha. Eles são usados ​​apenas para que o objeto que você está testando obtenha os dados de que necessita para realizar sua tarefa. Um &quot;stub&quot; é uma implementação de interface que existe para fornecer dados de algum tipo.</p>
<p align="justify">Um Stub é usado para substituir a dependência externa, fornecendo estado para que nossos testes sejam executados sem exceções. O Stub é adequado apenas para testar se o resultado de alguma função está correto ou não. Mock é mais complexo sendo usado para testar comportamentos, por exemplo, verificar se uma função foi chamada ou não.</p>
<p align="justify">Resumindo tudo segundo as palavras de <strong>Roy Osherove</strong> em seu livro <strong><em>&quot;The Art of Unit Testing&quot;</em></strong>, a diferença entre mocks e stubs é que mocks levam o teste a falha e stubs não.</p>
<p align="justify">Observe a ilustração abaixo:</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/02/mock-sut-stub.png"><img title="mock sut stub" style="background-image:none;float:none;padding-top:0;padding-left:0;margin-left:auto;display:block;padding-right:0;margin-right:auto;border-width:0;"   alt="mock sut stub" src="http://blob.vitormeriat.com.br/images/mock-sut-stub.png" width="560" height="412" /></a></p>
<p>&#160;</p>
<p align="justify">A setas vermelhas indicam que o caminho do Mock pode levar o teste ao erro, já no caso do Stub não deve haver falha.</p>
<p align="justify">Logo, usamos mocks para simular comportamentos, testar comunicação entre os objetos e caso as exigências do mesmo sejam contrariadas seu teste vai falhar. Sempre deve haver apenas um mock por teste e lembre-se: o Assert é contra o mock...</p>
<p align="justify">Os stubs fornecem dados, simulam resultados, suprimem as dependências e preparam o SUT para o teste. O stub é um auxílio, podem haver vários stubs em um teste e não causam a falha do mesmo.</p>
<p>&#160;</p>
<h2>Isolando os testes</h2>
<p align="justify">Isole os testes de unidade separando o código dos testes do SUT. O usual é ter projetos separados para o SUT e os testes. Com isso você pode manter seu projeto mais organizado e evita o trabalho e a preocupação sobre o que fazer com o código de teste na hora de colocar seu sistema em produção. </p>
<p align="justify">&#160;</p>
<h2>Testando unidades</h2>
<p align="justify">Testes unitários ou de unidade se referem a pequenos pedaços de código, comumente métodos ou partes ainda menores, como escopos dentro dos métodos. Escrever testes grandes demais ou que verifiquem muitos itens do código, geralmente, indica falha no design da aplicação. Lembre-se que quanto menor for seu teste, mais fácil será a manutenção no futuro e mais rápido será o entendimento do erro causado quando um teste falhar.</p>
<p>&#160;</p>
<h2>Quanto a dificuldade</h2>
<p align="justify">Levando em consideração as boas práticas e o Princípio da Responsabilidade Única ou SRP (Single Responsibility Principle), podemos afirmar que os testes devem ser feitos sem grandes dificuldades em relação ao desing da mesma. O teste deve ter apenas um objetivo e testar apenas uma funcionalidade por vez.</p>
<p>&#160;</p>
<h3><font style="font-weight:bold;">Referências</font></h3>
<p><a href="http://martinfowler.com/articles/mocksArentStubs.html" target="_blank">Mocks Aren't Stubs</a></p>

