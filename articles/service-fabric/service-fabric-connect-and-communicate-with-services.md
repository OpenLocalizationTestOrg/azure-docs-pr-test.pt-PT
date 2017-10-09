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
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="6af97-103">Ligar e comunicar com serviços no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6af97-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="6af97-104">No Service Fabric, um serviço é executado algures num cluster de Service Fabric, normalmente distribuído por várias VMs.</span><span class="sxs-lookup"><span data-stu-id="6af97-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="6af97-105">Pode ser afastado do tooanother local, através do proprietário do serviço hello, ou automaticamente Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6af97-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="6af97-106">Serviços não estão máquina específica tooa estaticamente associada ou endereço.</span><span class="sxs-lookup"><span data-stu-id="6af97-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="6af97-107">Uma aplicação de Service Fabric, geralmente, é composta por vários serviços diferentes, onde cada serviço executa uma tarefa de especializado.</span><span class="sxs-lookup"><span data-stu-id="6af97-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="6af97-108">Estes serviços podem comunicar com tooform entre si uma função concluída, como as diferentes partes composição de uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="6af97-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="6af97-109">Também existem aplicações que ligam tooand comunicam com serviços do cliente.</span><span class="sxs-lookup"><span data-stu-id="6af97-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="6af97-110">Este documento explica como tooset segurança comunicação com o operador and entre os serviços no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6af97-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="6af97-111">Este vídeo Microsoft Virtual Academy também descreve comunicação do serviço:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="6af97-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="6af97-112">Traga a sua própria protocolo</span><span class="sxs-lookup"><span data-stu-id="6af97-112">Bring your own protocol</span></span>
<span data-ttu-id="6af97-113">Recursos de infraestrutura do serviço de ajuda a gerir o ciclo de vida de Olá dos seus serviços, mas não a tomar decisões sobre o que fazem os serviços.</span><span class="sxs-lookup"><span data-stu-id="6af97-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="6af97-114">Isto inclui a comunicação.</span><span class="sxs-lookup"><span data-stu-id="6af97-114">This includes communication.</span></span> <span data-ttu-id="6af97-115">Quando o serviço está aberto por Service Fabric, que é tooset de oportunidade do serviço cópia de segurança um ponto final para pedidos recebidos, utilizando qualquer pilha de protocolo ou comunicação que pretende.</span><span class="sxs-lookup"><span data-stu-id="6af97-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="6af97-116">O serviço irá escutar num normal **IP:port** utilizando qualquer esquema de endereçamento, tais como um URI de endereço.</span><span class="sxs-lookup"><span data-stu-id="6af97-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="6af97-117">Várias instâncias de serviço ou réplicas podem partilhar um processo de anfitrião, caso em que estes serão tem portas diferentes toouse ou utilizar um mecanismo de partilha de portas, tais como controladores de kernel Olá http.sys do Windows.</span><span class="sxs-lookup"><span data-stu-id="6af97-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="6af97-118">Em ambos os casos, cada instância de serviço ou a réplica num processo anfitrião tem de ser exclusivamente endereçável.</span><span class="sxs-lookup"><span data-stu-id="6af97-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![pontos finais de serviço][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="6af97-120">Deteção do serviço e resolução</span><span class="sxs-lookup"><span data-stu-id="6af97-120">Service discovery and resolution</span></span>
<span data-ttu-id="6af97-121">Num sistema distribuído, os serviços podem mover da tooanother de uma máquina ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="6af97-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="6af97-122">Isto pode acontecer por vários motivos, incluindo recursos balanceamento, atualizações, as ativações pós-falha ou Escalamento horizontal. Isto significa que os endereços de ponto final de serviço alterar à medida que o serviço de Olá move toonodes com endereços IP diferentes, poderá abrir portas diferentes, se o serviço de Olá utiliza uma porta dinâmica selecionada.</span><span class="sxs-lookup"><span data-stu-id="6af97-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Distribuição de serviços][7]

<span data-ttu-id="6af97-124">O Service Fabric fornece uma deteção e a resolução do serviço chamado Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="6af97-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="6af97-125">Olá Naming Service mantém uma tabela que mapeia serviço as instâncias nomeadas toohello endereços de ponto final que escutarem.</span><span class="sxs-lookup"><span data-stu-id="6af97-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="6af97-126">Todas as instâncias de serviço com nome no Service Fabric têm nomes exclusivos representados como os URIs, por exemplo, `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="6af97-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="6af97-127">nome Olá do serviço de Olá não alteram ao longo da duração Olá do serviço de Olá, é apenas Olá endereços de ponto final que podem ser alteradas quando mover de serviços.</span><span class="sxs-lookup"><span data-stu-id="6af97-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="6af97-128">Isto é semelhante toowebsites que tenham URLs constantes mas onde pode alterar o endereço IP Olá.</span><span class="sxs-lookup"><span data-stu-id="6af97-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="6af97-129">E tooDNS semelhante na web Olá, o qual resolve endereços de tooIP de URLs de Web sites, o Service Fabric tem uma entidade de registo que mapeie o endereço de ponto final do serviço de nomes tootheir.</span><span class="sxs-lookup"><span data-stu-id="6af97-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![pontos finais de serviço][2]

<span data-ttu-id="6af97-131">Resolver e ligar tooservices envolvem Olá os seguintes passos executados em ciclo:</span><span class="sxs-lookup"><span data-stu-id="6af97-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="6af97-132">**Resolver**: Get ponto final de Olá que tiver publicado um serviço de Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="6af97-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="6af97-133">**Ligar**: ligar o serviço de toohello ao longo do que protocolo utiliza esse ponto final.</span><span class="sxs-lookup"><span data-stu-id="6af97-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="6af97-134">**Repita**: uma tentativa de ligação poderá falhar por diversas razões, por exemplo, se o serviço de Olá foi movido, uma vez que o endereço de ponto final de Olá Olá última hora foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="6af97-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="6af97-135">Nesse caso, Olá precedente resolve e ligue-se passos necessário toobe repetida e este ciclo é repetido até que Olá ligação é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6af97-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="6af97-136">Ligar tooother serviços</span><span class="sxs-lookup"><span data-stu-id="6af97-136">Connecting tooother services</span></span>
<span data-ttu-id="6af97-137">Serviços ligar tooeach outros no interior de um cluster, geralmente, pode aceder diretamente ao pontos finais de Olá de outros serviços porque nós Olá num cluster Olá mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="6af97-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="6af97-138">toomake é mais fácil tooconnect entre os serviços, o Service Fabric fornece serviços adicionais que utilizam Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="6af97-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="6af97-139">Um serviço DNS e um serviço de proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="6af97-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="6af97-140">Serviço DNS</span><span class="sxs-lookup"><span data-stu-id="6af97-140">DNS service</span></span>
<span data-ttu-id="6af97-141">Uma vez que vários serviços, especialmente de serviços, podem ter um nome de URL existente, que está a ser capaz de tooresolve estes utilizando Olá padrão protocolo DNS (em vez de protocolo de nomenclatura do serviço de Olá) é muito convenientes, especialmente na aplicação "de comparação de precisão e deslocar" cenários.</span><span class="sxs-lookup"><span data-stu-id="6af97-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="6af97-142">Isto é exatamente o serviço DNS Olá não.</span><span class="sxs-lookup"><span data-stu-id="6af97-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="6af97-143">-Permite-lhe toomap DNS nomes tooa nome do serviço e, por conseguinte, resolva endereços de IP do ponto final.</span><span class="sxs-lookup"><span data-stu-id="6af97-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="6af97-144">Como Olá mostrado no diagrama a seguir, Olá serviço DNS, em execução no cluster do Service Fabric Olá, mapeia nomes tooservice os nomes DNS que são, em seguida, resolvidos pelo Olá Naming Service tooreturn Olá endpoint endereços tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="6af97-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="6af97-145">nome DNS Olá para o serviço de Olá é fornecido na hora de Olá de criação.</span><span class="sxs-lookup"><span data-stu-id="6af97-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![pontos finais de serviço][9]

<span data-ttu-id="6af97-147">Para obter mais detalhes sobre como ver toouse Olá serviço DNS [serviço DNS do Azure Service Fabric](service-fabric-dnsservice.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6af97-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="6af97-148">Serviço de proxy inverso</span><span class="sxs-lookup"><span data-stu-id="6af97-148">Reverse proxy service</span></span>
<span data-ttu-id="6af97-149">os endereços de proxy inverso Olá serviços em cluster Olá que expõe os pontos finais HTTP, incluindo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6af97-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="6af97-150">proxy inverso Olá simplifica bastante a chamar outros serviços e os respetivos métodos, fazendo com que específico de formato de URI e identificadores Olá resolver, ligar, os passos de repetição necessários para um serviço toocommunicate com a utilização de outro Olá nomenclatura do serviço.</span><span class="sxs-lookup"><span data-stu-id="6af97-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="6af97-151">Por outras palavras, oculta Olá serviço de nomes do utilizador ao chamar outros serviços ao fazer isto tão simples como chamar um URL.</span><span class="sxs-lookup"><span data-stu-id="6af97-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![pontos finais de serviço][10]

<span data-ttu-id="6af97-153">Para obter mais detalhes sobre como toouse Olá inverter o serviço de proxy, consulte [proxy no Azure Service Fabric inverso](service-fabric-reverseproxy.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6af97-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="6af97-154">Ligações de clientes externos</span><span class="sxs-lookup"><span data-stu-id="6af97-154">Connections from external clients</span></span>
<span data-ttu-id="6af97-155">Serviços ligar tooeach outros no interior de um cluster, geralmente, pode aceder diretamente ao pontos finais de Olá de outros serviços porque nós Olá num cluster Olá mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="6af97-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="6af97-156">Em alguns ambientes, no entanto, um cluster pode estar atrás de um balanceador de carga que encaminha o tráfego de entrada externo através de um conjunto limitado de portas.</span><span class="sxs-lookup"><span data-stu-id="6af97-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="6af97-157">Nestes casos, os serviços ainda podem comunicar entre si e resolver endereços utilizando Olá Naming Service, mas passos adicionais têm de ser executadas tooallow clientes externos tooconnect tooservices.</span><span class="sxs-lookup"><span data-stu-id="6af97-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="6af97-158">Recursos de infraestrutura de serviço no Azure</span><span class="sxs-lookup"><span data-stu-id="6af97-158">Service Fabric in Azure</span></span>
<span data-ttu-id="6af97-159">Um cluster do Service Fabric no Azure é colocado por trás de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="6af97-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="6af97-160">Todos os clusters de toohello tráfego externo tem de passar através do Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="6af97-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="6af97-161">Hello Balanceador de carga será automaticamente reencaminhar tráfego de entrada no tooa determinado porta aleatória *nó* que tenha Olá abrir a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="6af97-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="6af97-162">Olá Balanceador de carga do Azure apenas conhece portas abertas em Olá *nós*, não conhecimento de abertura de portas por indivíduo *serviços*.</span><span class="sxs-lookup"><span data-stu-id="6af97-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Topologia de Balanceador de carga e do Service Fabric do Azure][3]

<span data-ttu-id="6af97-164">Por exemplo, na ordem tooaccept externo o tráfego na porta **80**, Olá seguir coisas tem de ser configurado:</span><span class="sxs-lookup"><span data-stu-id="6af97-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="6af97-165">Escreva um serviço de escuta na porta 80.</span><span class="sxs-lookup"><span data-stu-id="6af97-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="6af97-166">Configurar a porta 80 no ServiceManifest.xml do serviço de Olá e abra um serviço de escuta no serviço de Olá, por exemplo, um servidor web Self-alojada.</span><span class="sxs-lookup"><span data-stu-id="6af97-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="6af97-167">Criar um Cluster do Service Fabric no Azure e especifique a porta **80** como uma porta personalizada endpoint Olá tipo de nó que irá alojar o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="6af97-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="6af97-168">Se tiver mais do que um tipo de nó, pode configurar um *restrição de posicionamento* no Olá tooensure de serviço só é executado no tipo de nó Olá que tenha a porta do ponto final personalizado Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="6af97-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Abrir uma porta no tipo de nó][4]
3. <span data-ttu-id="6af97-170">Depois de criar o cluster de Olá, configure Olá Balanceador de carga do Azure no tráfego de tooforward de grupo de recursos do cluster Olá na porta 80.</span><span class="sxs-lookup"><span data-stu-id="6af97-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="6af97-171">Quando criar um cluster através do portal do Azure de Olá, isto é configurado automaticamente para cada porta do ponto final personalizada que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="6af97-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Encaminhar o tráfego no Olá Balanceador de carga do Azure][5]
4. <span data-ttu-id="6af97-173">Olá toodetermine uma sonda utiliza o Balanceador de carga do Azure se ou não toosend tráfego tooa determinado nó.</span><span class="sxs-lookup"><span data-stu-id="6af97-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="6af97-174">Olá sonda periodicamente as verificações de um ponto final num toodetermine cada nó ou não nó Olá está a responder.</span><span class="sxs-lookup"><span data-stu-id="6af97-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="6af97-175">Se sonda Olá falha tooreceive uma resposta depois de um número de vezes configurado, o Balanceador de carga Olá deixa de nó de toothat tráfego a enviar.</span><span class="sxs-lookup"><span data-stu-id="6af97-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="6af97-176">Quando criar um cluster através de Olá portal do Azure, uma sonda é configurada automaticamente para cada porta do ponto final personalizada que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="6af97-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Encaminhar o tráfego no Olá Balanceador de carga do Azure][8]

<span data-ttu-id="6af97-178">É importante tooremember que Olá Balanceador de carga do Azure e a sonda de Olá apenas conhecer sobre Olá *nós*, não Olá *serviços* em execução em nós de Olá.</span><span class="sxs-lookup"><span data-stu-id="6af97-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="6af97-179">Olá Balanceador de carga do Azure irá enviar sempre toonodes de tráfego que respondam toohello sonda, pelo que deve ter cuidado tooensure serviços estão disponíveis em nós de Olá que são capazes de toorespond toohello sonda.</span><span class="sxs-lookup"><span data-stu-id="6af97-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="6af97-180">Reliable Services: Opções de API de comunicação incorporada</span><span class="sxs-lookup"><span data-stu-id="6af97-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="6af97-181">arquitetura de Reliable Services Olá é fornecido com várias opções de comunicação pré-criadas.</span><span class="sxs-lookup"><span data-stu-id="6af97-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="6af97-182">Decisão de Olá sobre os quais um funcionarão melhor para si depende da escolha de Olá de Olá Olá programação idioma que os serviços escritos no, framework de comunicação de Olá e modelo de programação.</span><span class="sxs-lookup"><span data-stu-id="6af97-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="6af97-183">**Nenhum protocolo específico:** se não tiver uma escolha específica de estrutura de comunicação, mas quiser tooget algo e funcional, rapidamente, em seguida, Olá opção ideal para si é [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md), que lhe permite tipo seguro de procedimento remoto chama para Reliable Services e Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="6af97-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="6af97-184">Este é Olá mais fácil e tooget de forma mais rápida iniciado com comunicação de serviço.</span><span class="sxs-lookup"><span data-stu-id="6af97-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="6af97-185">Comunicação remota do serviço processa a resolução de endereços de serviço, ligação, tente novamente e processamento de erros.</span><span class="sxs-lookup"><span data-stu-id="6af97-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="6af97-186">Trata-se disponível para c# e aplicações de Java.</span><span class="sxs-lookup"><span data-stu-id="6af97-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="6af97-187">**HTTP**: para comunicação de linguagem, HTTP fornece uma opção de norma da indústria com servidores HTTP disponíveis em vários idiomas diferentes, todos suportados pelo serviço de recursos de infraestrutura e ferramentas.</span><span class="sxs-lookup"><span data-stu-id="6af97-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="6af97-188">Os serviços podem utilizar qualquer pilha HTTP disponível, incluindo [API Web do ASP.NET](service-fabric-reliable-services-communication-webapi.md) para aplicações do c#.</span><span class="sxs-lookup"><span data-stu-id="6af97-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="6af97-189">Os clientes escritos em c# podem tirar partido das Olá `ICommunicationClient` e `ServicePartitionClient` classes, enquanto que para Java, utilize Olá `CommunicationClient` e `FabricServicePartitionClient` classes, [para resolução de serviço, as ligações HTTP e ciclos de repetição](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="6af97-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="6af97-190">**WCF**: Se tiver o código existente que utiliza o WCF como o framework de comunicação, em seguida, pode utilizar Olá `WcfCommunicationListener` para o lado do servidor de Olá e `WcfCommunicationClient` e `ServicePartitionClient` classes para o cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="6af97-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="6af97-191">No entanto é apenas disponível para aplicações c# em clusters de baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="6af97-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="6af97-192">Para obter mais detalhes, consulte este artigo [implementação baseada no WCF da pilha de comunicação de Olá](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="6af97-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="6af97-193">Utilizar protocolos personalizados e outras estruturas de comunicação</span><span class="sxs-lookup"><span data-stu-id="6af97-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="6af97-194">Os serviços podem utilizar qualquer protocolo ou arquitetura de comunicação, se se trata de um protocolo personalizado de binário através de TCP sockets ou eventos de transmissão em fluxo através de [Event Hubs do Azure](https://azure.microsoft.com/services/event-hubs/) ou [IoT Hub do Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="6af97-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="6af97-195">O Service Fabric fornece comunicação APIs que pode fixação a pilha de comunicações para, enquanto todas as Olá trabalhar toodiscover e ligar é abstracted do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6af97-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="6af97-196">Consulte este artigo sobre Olá [modelo de comunicação de serviço fiável](service-fabric-reliable-services-communication.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6af97-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6af97-197">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6af97-197">Next steps</span></span>
<span data-ttu-id="6af97-198">Saiba mais sobre conceitos Olá e APIs disponíveis no Olá [modelo de comunicação Reliable Services](service-fabric-reliable-services-communication.md), em seguida, comece a trabalhar rapidamente com [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md) ou vá toolearn aprofundada como toowrite um o serviço de escuta de comunicação com [Web API com OWIN automática alojar](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="6af97-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
