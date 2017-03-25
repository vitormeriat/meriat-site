---
layout: post
title: Onde usar o Windows Azure?
date: 2011-05-30
categories:
    - Cloud Computing
    - Microsoft Azure
---

Durante uma apresentação(Webcast) do arquiteto e evangelista da Microsoft <strong>Bill Zack</strong> sobre Windows Azure Design Patterns, ele disse algo que me chamou a atenção: “como arquitetos, estamos mais interessados ​​em resolver os problemas de negócios que podem ser solucionados utilizando esses recursos(do Windows Azure neste caso) onde eles são adequados”.

A Cloud computing foi desenvolvida para alguns cenários específicos e determinadas aplicações possuem um padrão de uso que as torna adequadas para a nuvem. O contrário também é verdade.

Durante seu Webcast, foi apresentado uma série de soluções e cenários cujo os recursos e componentes do Windows Azure são recomendados. Segue o resumo e logo após o link para o download do webcast.

**Workloads**
* <strong>On e Off</strong> – aplicações que são usadas esporadicamente durante determinados períodos de tempo durante o dia ou ano. Muitos serviços que rodam no final do dia ou do mês caem nessa categoria. Proporcionar a capacidade necessária para essas aplicações é mais caro que rodá-las em um cloud porque a maior parte do tempo a capacidade não é usada. 
* <strong>Crescimento rápido ou não rápido</strong> – um padrão de trabalho encontrado pelos iniciantes que não podem prever com exatidão o nível de sucesso de seu novo negócio e, consequentemente, a verdadeira capacidade que precisam. Iniciantes geralmente começam com pequenos aumentos de capacidade quando a demanda aumenta. Tais aplicações são adequadas para o cloud por que o cloud pode suportar o crescimento das necessidades rapidamente.
* <strong>Crescimento imprevisível</strong> – isso acontece, por exemplo, quando a carga normal em um web server é temporariamente aumentada por uma valor muito alto, tão grande que o sistema não consegue lidar com o tráfego passageiro. Os proprietários devem fornecer capacidade suficiente para suportar essas cargas, mas eles não esperam esses picos de tráfego. Mesmo se eles antecipá-las, a capacidade adicional ficaria a maior parte do tempo sem uso. Este é um outro bom candidato ao cloud.
* <strong>Crescimento previsível</strong> – a carga constatemente varia de uma maneira previsível ao longo do tempo. O proprietário pode comprar o equipamente e software necessário sem ter que depender de uma fornecedor de cloud.
* Zack continua descrevendo cenários para computação, armazenagem, comunicações, deploy e administração com soluções fornecidas pelo Windows Azure.

**Computation**
<ul>
<li>
<div align="justify"><strong>Instâncias de aplicações On-demand – </strong>este padrão se aplica durante eventos especiais, quando os aplicativos precisam escalar rapidamente, e depois reduzir o escalonamento. Windows Azure suporta estas necessidades com gerenciadores web e worker roles automaticamente. </div>
</li>
<li>
<div align="justify"><strong>Distribuição Worker Role</strong> – este é usado quando trabalhos longos são feitos em pequenas partes, cada uma delas sendo associadas com um instância de Worker Role.</div>
</li>
</ul>
<p align="justify"><strong>Armazenamento</strong>
<ul>
<li>
<div align="justify"><strong>Blob</strong> – Blobs são usados para armazenar grande quantidade de dados não estruturados. </div>
</li>
<li>
<div align="justify"><strong>Tables</strong> – uma solução não relacional para armazenar uma grande massa de dados. </div>
</li>
<li>
<div align="justify"><strong>DB – </strong>SQL Azure oferece uma banco de dados relacional no cloud. </div>
</li>
<li>
<div align="justify"><strong>Data Protection</strong> – Dados armazenados em um cloud pode ser encriptografados se eles contém informações confidenciais e tem-se que garantir que eles não serão descobertos. Windows Azure fornecerá esses serviços em um futuro próximo. </div>
</li>
<li>
<div align="justify"><strong>Information Service</strong> – Microsoft tem dados de mercado que podem ser comprados ou vendidos por empresas.</div>
</li>
</ul>
<p align="justify"><strong>Comunicação</strong>
<ul>
<li>
<div align="justify"><strong>Service-oriented Integration</strong> – Azure permite aplicações consumirem serviços fornecidos por outras aplicações. A solução integrada da Microsoft é <a href="http://msdn.microsoft.com/en-us/library/dd456779%28v=VS.100%29.aspx">WCF Web Services</a>, worker roles são aptos a expor esses endpoints. </div>
</li>
<li>
<div align="justify"><strong>Mensageria </strong>– Mensageria é fornecido pela Windows Azure Queues para comunicação assíncrona entre web e os worker roles. </div>
</li>
<li>
<div align="justify"><strong>Mensageria <strong>através de </strong></strong><strong>Firewalls</strong> – Aplicações podem comunicar-se com outras através do Service Bus Queues que não exige que nenhuma porta adicional seja aberta.</div>
</li>
</ul>
<p align="justify"><strong>Implantação</strong>
<ul>
<li>
<div align="justify"><strong>Could Deployment</strong> - Aplicações são implantadas no cloud usando serviços distintos e configuração de arquivos, e são empacotadas para as funções específicas. A web e os worker roles e seus tipos são definidos no arquivo de serviço, enquanto o arquivo de configuração de serviço contém os números de cada role. </div>
</li>
<li>
<div align="justify"><strong>Movendo aplicações On-Premise para o Cloud</strong> – enquanto isso não é viável para a maioria dos aplicativos, existem algums que podem ser portados como um simples site web ASP.NET </div>
</li>
<li>
<div align="justify"><strong>Ambientes misturados, On-Premise e o Cloud – </strong>Windows Azure fornece a possibilidade de combinar aplicações on-premises com serviços no cloud usando interfaces REST, acesso seguro ao SQL Azure, Service Bus e Access Control Service. </div>
</li>
<li>
<div align="justify"><strong>Aplicação Dual </strong>– aplicações podem ser projetados para funcionar tanto local quanto nas nuvens, mas o processo de design não é simples. Isto pode ser útil se a organização roda a aplicação em seus próprios servidores, mas usa a nuvem durante os picos como, por exemplo, na época do natal. </div>
</li>
<li>
<div align="justify"><strong>Security Federation</strong> – Windows Azure fornece este tipo de segurança através do Access Control Service. </div>
</li>
<li>
<div align="justify"><strong>SaaS</strong> – Aplicações implantadas em um cloud pode ser fornecidas também como serviços</div>
</li>
</ul>
<p align="justify"><strong>Administração</strong>
<ul>
<li>
<div align="justify"><strong>Design para Operações</strong> – Windows Azure fornece uma API diagnosticar problemas e identificá-los ou monitorá-los. </div>
</li>
<li>
<div align="justify"><strong>Service Instance Management</strong> – instâncias do aplicativo podem ser iniciadas, interrompidas ou suspensas através de uma API ou através do portal Azure.</div>
</li>
</ul>
<p>Você pode baixar o webcast <a href="http://blogs.msdn.com/b/billzack/archive/2010/03/29/windows-azure-design-patterns.aspx">aqui.</a></p>
<p>&nbsp;</p>
<h3><font size="4">Um grande abraço ótimo Estudo!</font></h3>