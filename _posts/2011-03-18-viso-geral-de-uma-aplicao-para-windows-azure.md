---
layout: post
title: Visão geral de uma Aplicação para Windows Azure
date: 2011-03-18
categories:
    - Cloud Computing
    - Microsoft Azure
---

Basicamente, a arquitetura de uma aplicação hospedada no Windows Azure é baseada em elementos escalonáveis, que são construídos sobre código gerenciado, esses elementos são conhecidos como Roles.

Um aplicativo que roda em Windows Azure é um serviço hospedado. Normalmente, um serviço hospedado contém diversos recursos computacionais que, coletivamente, processam as informações e interagem uns com os outros e com mundo externo. Os serviços hospedados no Windows Azure são os papéis(Roles).

Uma aplicação hospedada no Windows Azure implementa uma ou mais Roles, podendo assim executar várias instâncias de uma Role, onde são replicadas em vários computadores. Desta forma, garantindo a total funcionalidade da aplicação em praticamente tempo integral.

Windows Azure atualmente suporta os seguintes tipos de Roles:

### Web Role

IIS7 e ASP.NET em um OS fornecido pelo Windows Azure. O Web Role ASP.NET no Windows Azure é semelhante a um aplicativo da Web ASP.NET. Ele possui arquivos .aspx e o código-fonte, incluindo ferramentas adicionais que permitem que ele seja executado no ambiente Windows Azure. Um Web Role pode receber a maioria dos aplicativos que usam o protocolo HTTP, como o FastCGI ou um serviço WCF usando o esquema basicHttpBinding.

### Worker Role

É um "executável" (como um serviço ou processo), sendo útil para o desenvolvimento generalizado.

### VM Role

O VM Role consiste em um sistema operacional que é construído usando uma VHD. Esta função é um tipo especial para permitir que você defina a configuração e atualizações do sistema operacional da máquina virtual. Utiliza Windows services, scheduled tasks, etc. Você configura e adminstra o sistema operacional. <br />&nbsp;<br />O diagrama a abaixo mostra os componentes de um aplicativo do Windows
Azure:

<p align="center"><a href="http://blob.vitormeriat.com.br/images/2011/03/attachment.jpg"><img alt="attachment" src="http://blob.vitormeriat.com.br/images/2011/03/attachment.jpg"/></a></p>

No diagrama acima podemos notar os papéis(Roles), e suas respectivas ligações. Notem que os papéis são “gerenciados” pelas configurações definidas nos arquivos: <strong>ServiceConfiguration.cscfg</strong> e <strong>ServiceDefinition.csdef.</strong>

## Padrão de aplicação típica para uso dos Papéis(Roles).

Uma aplicação do Windows Azure pode ser implementada com Asp.Net, WCF ou qualquer tecnologia com suporte ao IIS. Você pode por exemplo hospedar uma aplicação PHP, já que o IIS suporta PHP atravéz de <strong>Fast CGI.</strong>

Um dos padrões mais utilizado para aplicativos no Windows Azure é um Web Role para receber as requisições, utilizando de Filas(Queues) do Azure para passar as instâncias de um Worker Role que periodicamente olha para a fila de mensagens a fim de ver se há algum “trabalho” a realizar. O Web Role recupera o resultado do processo. Este padrão pode ser melhor entendido conforme o diagra abaixo:

<p><a href="http://blob.vitormeriat.com.br/images/2011/03/ic417497.png"><img alt="IC417497" src="http://blob.vitormeriat.com.br/images/2011/03/ic417497.png" /></a></p>

#### Um grande abraço e ótimo estudo!
