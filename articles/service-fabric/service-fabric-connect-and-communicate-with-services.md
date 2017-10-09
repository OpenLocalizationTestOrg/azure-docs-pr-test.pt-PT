---
title: "aaaConnect e comunicar com serviços no Azure Service Fabric | Microsoft Docs"
description: "Saiba como ligar tooresolve e comunicar com serviços no Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Ligar e comunicar com serviços no Service Fabric
No Service Fabric, um serviço é executado algures num cluster de Service Fabric, normalmente distribuído por várias VMs. Pode ser afastado do tooanother local, através do proprietário do serviço hello, ou automaticamente Service Fabric. Serviços não estão máquina específica tooa estaticamente associada ou endereço.

Uma aplicação de Service Fabric, geralmente, é composta por vários serviços diferentes, onde cada serviço executa uma tarefa de especializado. Estes serviços podem comunicar com tooform entre si uma função concluída, como as diferentes partes composição de uma aplicação web. Também existem aplicações que ligam tooand comunicam com serviços do cliente. Este documento explica como tooset segurança comunicação com o operador and entre os serviços no Service Fabric.

Este vídeo Microsoft Virtual Academy também descreve comunicação do serviço:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Traga a sua própria protocolo
Recursos de infraestrutura do serviço de ajuda a gerir o ciclo de vida de Olá dos seus serviços, mas não a tomar decisões sobre o que fazem os serviços. Isto inclui a comunicação. Quando o serviço está aberto por Service Fabric, que é tooset de oportunidade do serviço cópia de segurança um ponto final para pedidos recebidos, utilizando qualquer pilha de protocolo ou comunicação que pretende. O serviço irá escutar num normal **IP:port** utilizando qualquer esquema de endereçamento, tais como um URI de endereço. Várias instâncias de serviço ou réplicas podem partilhar um processo de anfitrião, caso em que estes serão tem portas diferentes toouse ou utilizar um mecanismo de partilha de portas, tais como controladores de kernel Olá http.sys do Windows. Em ambos os casos, cada instância de serviço ou a réplica num processo anfitrião tem de ser exclusivamente endereçável.

![pontos finais de serviço][1]

## <a name="service-discovery-and-resolution"></a>Deteção do serviço e resolução
Num sistema distribuído, os serviços podem mover da tooanother de uma máquina ao longo do tempo. Isto pode acontecer por vários motivos, incluindo recursos balanceamento, atualizações, as ativações pós-falha ou Escalamento horizontal. Isto significa que os endereços de ponto final de serviço alterar à medida que o serviço de Olá move toonodes com endereços IP diferentes, poderá abrir portas diferentes, se o serviço de Olá utiliza uma porta dinâmica selecionada.

![Distribuição de serviços][7]

O Service Fabric fornece uma deteção e a resolução do serviço chamado Olá Naming Service. Olá Naming Service mantém uma tabela que mapeia serviço as instâncias nomeadas toohello endereços de ponto final que escutarem. Todas as instâncias de serviço com nome no Service Fabric têm nomes exclusivos representados como os URIs, por exemplo, `"fabric:/MyApplication/MyService"`. nome Olá do serviço de Olá não alteram ao longo da duração Olá do serviço de Olá, é apenas Olá endereços de ponto final que podem ser alteradas quando mover de serviços. Isto é semelhante toowebsites que tenham URLs constantes mas onde pode alterar o endereço IP Olá. E tooDNS semelhante na web Olá, o qual resolve endereços de tooIP de URLs de Web sites, o Service Fabric tem uma entidade de registo que mapeie o endereço de ponto final do serviço de nomes tootheir.

![pontos finais de serviço][2]

Resolver e ligar tooservices envolvem Olá os seguintes passos executados em ciclo:

* **Resolver**: Get ponto final de Olá que tiver publicado um serviço de Olá Naming Service.
* **Ligar**: ligar o serviço de toohello ao longo do que protocolo utiliza esse ponto final.
* **Repita**: uma tentativa de ligação poderá falhar por diversas razões, por exemplo, se o serviço de Olá foi movido, uma vez que o endereço de ponto final de Olá Olá última hora foi resolvido. Nesse caso, Olá precedente resolve e ligue-se passos necessário toobe repetida e este ciclo é repetido até que Olá ligação é bem-sucedida.

## <a name="connecting-tooother-services"></a>Ligar tooother serviços
Serviços ligar tooeach outros no interior de um cluster, geralmente, pode aceder diretamente ao pontos finais de Olá de outros serviços porque nós Olá num cluster Olá mesma rede local. toomake é mais fácil tooconnect entre os serviços, o Service Fabric fornece serviços adicionais que utilizam Olá Naming Service. Um serviço DNS e um serviço de proxy inverso.


### <a name="dns-service"></a>Serviço DNS
Uma vez que vários serviços, especialmente de serviços, podem ter um nome de URL existente, que está a ser capaz de tooresolve estes utilizando Olá padrão protocolo DNS (em vez de protocolo de nomenclatura do serviço de Olá) é muito convenientes, especialmente na aplicação "de comparação de precisão e deslocar" cenários. Isto é exatamente o serviço DNS Olá não. -Permite-lhe toomap DNS nomes tooa nome do serviço e, por conseguinte, resolva endereços de IP do ponto final. 

Como Olá mostrado no diagrama a seguir, Olá serviço DNS, em execução no cluster do Service Fabric Olá, mapeia nomes tooservice os nomes DNS que são, em seguida, resolvidos pelo Olá Naming Service tooreturn Olá endpoint endereços tooconnect para. nome DNS Olá para o serviço de Olá é fornecido na hora de Olá de criação. 

![pontos finais de serviço][9]

Para obter mais detalhes sobre como ver toouse Olá serviço DNS [serviço DNS do Azure Service Fabric](service-fabric-dnsservice.md) artigo.

### <a name="reverse-proxy-service"></a>Serviço de proxy inverso
os endereços de proxy inverso Olá serviços em cluster Olá que expõe os pontos finais HTTP, incluindo HTTPS. proxy inverso Olá simplifica bastante a chamar outros serviços e os respetivos métodos, fazendo com que específico de formato de URI e identificadores Olá resolver, ligar, os passos de repetição necessários para um serviço toocommunicate com a utilização de outro Olá nomenclatura do serviço. Por outras palavras, oculta Olá serviço de nomes do utilizador ao chamar outros serviços ao fazer isto tão simples como chamar um URL.

![pontos finais de serviço][10]

Para obter mais detalhes sobre como toouse Olá inverter o serviço de proxy, consulte [proxy no Azure Service Fabric inverso](service-fabric-reverseproxy.md) artigo.

## <a name="connections-from-external-clients"></a>Ligações de clientes externos
Serviços ligar tooeach outros no interior de um cluster, geralmente, pode aceder diretamente ao pontos finais de Olá de outros serviços porque nós Olá num cluster Olá mesma rede local. Em alguns ambientes, no entanto, um cluster pode estar atrás de um balanceador de carga que encaminha o tráfego de entrada externo através de um conjunto limitado de portas. Nestes casos, os serviços ainda podem comunicar entre si e resolver endereços utilizando Olá Naming Service, mas passos adicionais têm de ser executadas tooallow clientes externos tooconnect tooservices.

## <a name="service-fabric-in-azure"></a>Recursos de infraestrutura de serviço no Azure
Um cluster do Service Fabric no Azure é colocado por trás de um balanceador de carga do Azure. Todos os clusters de toohello tráfego externo tem de passar através do Balanceador de carga Olá. Hello Balanceador de carga será automaticamente reencaminhar tráfego de entrada no tooa determinado porta aleatória *nó* que tenha Olá abrir a mesma porta. Olá Balanceador de carga do Azure apenas conhece portas abertas em Olá *nós*, não conhecimento de abertura de portas por indivíduo *serviços*.

![Topologia de Balanceador de carga e do Service Fabric do Azure][3]

Por exemplo, na ordem tooaccept externo o tráfego na porta **80**, Olá seguir coisas tem de ser configurado:

1. Escreva um serviço de escuta na porta 80. Configurar a porta 80 no ServiceManifest.xml do serviço de Olá e abra um serviço de escuta no serviço de Olá, por exemplo, um servidor web Self-alojada.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Criar um Cluster do Service Fabric no Azure e especifique a porta **80** como uma porta personalizada endpoint Olá tipo de nó que irá alojar o serviço de Olá. Se tiver mais do que um tipo de nó, pode configurar um *restrição de posicionamento* no Olá tooensure de serviço só é executado no tipo de nó Olá que tenha a porta do ponto final personalizado Olá aberta.

    ![Abrir uma porta no tipo de nó][4]
3. Depois de criar o cluster de Olá, configure Olá Balanceador de carga do Azure no tráfego de tooforward de grupo de recursos do cluster Olá na porta 80. Quando criar um cluster através do portal do Azure de Olá, isto é configurado automaticamente para cada porta do ponto final personalizada que foi configurada.

    ![Encaminhar o tráfego no Olá Balanceador de carga do Azure][5]
4. Olá toodetermine uma sonda utiliza o Balanceador de carga do Azure se ou não toosend tráfego tooa determinado nó. Olá sonda periodicamente as verificações de um ponto final num toodetermine cada nó ou não nó Olá está a responder. Se sonda Olá falha tooreceive uma resposta depois de um número de vezes configurado, o Balanceador de carga Olá deixa de nó de toothat tráfego a enviar. Quando criar um cluster através de Olá portal do Azure, uma sonda é configurada automaticamente para cada porta do ponto final personalizada que foi configurada.

    ![Encaminhar o tráfego no Olá Balanceador de carga do Azure][8]

É importante tooremember que Olá Balanceador de carga do Azure e a sonda de Olá apenas conhecer sobre Olá *nós*, não Olá *serviços* em execução em nós de Olá. Olá Balanceador de carga do Azure irá enviar sempre toonodes de tráfego que respondam toohello sonda, pelo que deve ter cuidado tooensure serviços estão disponíveis em nós de Olá que são capazes de toorespond toohello sonda.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services: Opções de API de comunicação incorporada
arquitetura de Reliable Services Olá é fornecido com várias opções de comunicação pré-criadas. Decisão de Olá sobre os quais um funcionarão melhor para si depende da escolha de Olá de Olá Olá programação idioma que os serviços escritos no, framework de comunicação de Olá e modelo de programação.

* **Nenhum protocolo específico:** se não tiver uma escolha específica de estrutura de comunicação, mas quiser tooget algo e funcional, rapidamente, em seguida, Olá opção ideal para si é [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md), que lhe permite tipo seguro de procedimento remoto chama para Reliable Services e Reliable Actors. Este é Olá mais fácil e tooget de forma mais rápida iniciado com comunicação de serviço. Comunicação remota do serviço processa a resolução de endereços de serviço, ligação, tente novamente e processamento de erros. Trata-se disponível para c# e aplicações de Java.
* **HTTP**: para comunicação de linguagem, HTTP fornece uma opção de norma da indústria com servidores HTTP disponíveis em vários idiomas diferentes, todos suportados pelo serviço de recursos de infraestrutura e ferramentas. Os serviços podem utilizar qualquer pilha HTTP disponível, incluindo [API Web do ASP.NET](service-fabric-reliable-services-communication-webapi.md) para aplicações do c#. Os clientes escritos em c# podem tirar partido das Olá `ICommunicationClient` e `ServicePartitionClient` classes, enquanto que para Java, utilize Olá `CommunicationClient` e `FabricServicePartitionClient` classes, [para resolução de serviço, as ligações HTTP e ciclos de repetição](service-fabric-reliable-services-communication.md).
* **WCF**: Se tiver o código existente que utiliza o WCF como o framework de comunicação, em seguida, pode utilizar Olá `WcfCommunicationListener` para o lado do servidor de Olá e `WcfCommunicationClient` e `ServicePartitionClient` classes para o cliente de Olá. No entanto é apenas disponível para aplicações c# em clusters de baseado no Windows. Para obter mais detalhes, consulte este artigo [implementação baseada no WCF da pilha de comunicação de Olá](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Utilizar protocolos personalizados e outras estruturas de comunicação
Os serviços podem utilizar qualquer protocolo ou arquitetura de comunicação, se se trata de um protocolo personalizado de binário através de TCP sockets ou eventos de transmissão em fluxo através de [Event Hubs do Azure](https://azure.microsoft.com/services/event-hubs/) ou [IoT Hub do Azure](https://azure.microsoft.com/services/iot-hub/). O Service Fabric fornece comunicação APIs que pode fixação a pilha de comunicações para, enquanto todas as Olá trabalhar toodiscover e ligar é abstracted do utilizador. Consulte este artigo sobre Olá [modelo de comunicação de serviço fiável](service-fabric-reliable-services-communication.md) para obter mais detalhes.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre conceitos Olá e APIs disponíveis no Olá [modelo de comunicação Reliable Services](service-fabric-reliable-services-communication.md), em seguida, comece a trabalhar rapidamente com [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md) ou vá toolearn aprofundada como toowrite um o serviço de escuta de comunicação com [Web API com OWIN automática alojar](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
