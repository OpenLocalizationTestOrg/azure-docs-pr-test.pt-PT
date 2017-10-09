---
title: aaaOverview do Service Fabric no Azure | Microsoft Docs
description: "Uma descrição geral do Service Fabric, onde as aplicações são compostas por muitas micro-serviços tooprovide dimensionamento e resiliência. Service Fabric é uma plataforma de sistemas distribuídos utilizado toobuild dimensionável, fiável e facilmente as aplicações para a nuvem de Olá de gerido."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Descrição geral dos recursos de infraestrutura de serviço do Azure
Azure Service Fabric é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implementar e gerir micro-serviços escaláveis e fiáveis e contentores. Service Fabric também aborda os desafios significativos de Olá no desenvolvimento e gestão de aplicações nativas de nuvem. Permite, assim, que os programadores e administradores evitem problemas complexos de infraestrutura e se concentrem na implementação de cargas de trabalho exigentes e fundamentais que sejam dimensionáveis, fiáveis e geríveis. Service Fabric representa a plataforma de próxima geração de Olá para criar e gerir estes empresarial, a camada-1, a aplicações de escala da nuvem em execução nos contentores.

Este breve vídeo apresenta Service Fabric e micro-serviços:<center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Aplicações composto micro-serviços 
Recursos de infraestrutura de serviço permite-lhe toobuild e gerir aplicações escaláveis e fiáveis compostas micro-serviços que funcionam com alta densidade num agrupamento partilhado de máquinas, que é referido tooas um cluster. Fornece um toobuild sofisticadas, simples runtime distribuído, micro-serviços dimensionáveis, sem monitorização de estado e com monitorização de estado em execução nos contentores. Também fornece tooprovision de capacidades de Gestão abrangente de aplicações, implementar, monitorizar, atualização/patch e eliminar aplicações implementadas, incluindo de serviços.

Muitos serviços Microsoft hoje em dia, incluindo a SQL Database do Azure está na base do Service Fabric, base de dados do Azure Cosmos, Cortana, Microsoft Power BI, Microsoft Intune, Event Hubs do Azure, IoT Hub do Azure, Dynamics 365, Skype para empresas e muitas principais serviços do Azure.

Service Fabric é toocreate personalizáveis nativo os serviços em nuvem podem começar por algo pequeno, conforme necessário e aumentar a escala de toomassive com centenas ou milhares de máquinas.

Serviços de escala de Internet de hoje são criados de micro-serviços. Micro-serviços exemplos de gateways de protocolo, perfis de utilizador, compras carts, inventário de processamento, filas e coloca em cache. Service Fabric é uma plataforma de micro-serviços que proporcione cada microsserviço (ou contentor) um nome exclusivo que pode ser sem monitorização de estado ou com monitorização de estado.

O Service Fabric fornece abrangente runtime e do ciclo de vida de gestão capacidades tooapplications que são compostas por estas micro-serviços. Micro-serviços dentro de contentores que são implementadas e ativadas em cluster do Service Fabric Olá nele alojado. Uma mudança de máquinas virtuais toocontainers torna possível um aumento de ordem de magnitude no densidade. Da mesma forma, outro ordem de grandeza no densidade torna-se possíveis quando move de contentores toomicroservices estes contentores. Por exemplo, um único cluster para a SQL Database do Azure é composto por centenas de máquinas com dezenas de milhares de contentores que alojam um total de centenas de milhares de bases de dados. Cada base de dados é um microsserviço com monitorização de estado de Service Fabric. 

Para mais informações sobre a abordagem de micro-serviços Olá, leia o artigo [razão pela qual um aplicações de toobuilding abordagem micro-serviços?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Orquestração e implementação do contentor
Service Fabric é da Microsoft [orchestrator contentor](service-fabric-cluster-resource-manager-introduction.md) implementação micro-serviços através de um cluster de máquinas. Podem ser desenvolvidos micro-serviços de várias maneiras de utilizar Olá [modelos de programação do Service Fabric](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [qualquer código à sua escolha](service-fabric-deploy-existing-app.md). Importante ainda, pode combinar ambos os serviços de processos e serviços nos contentores no Olá mesma aplicação. Se pretender apenas demasiado[implementar e gerir contentores](service-fabric-containers-overview.md), Service Fabric é uma opção perfeita como orchestrator um contentor.

## <a name="any-os-any-cloud"></a>Qualquer SO, qualquer na nuvem
Recursos de infraestrutura de serviço é executado everywhere. Pode criar clusters de Service Fabric em muitos ambientes, incluindo o Azure ou no local, no Windows Server ou no Linux. Pode ainda criar clusters em outras nuvens públicas. Além disso, o ambiente de desenvolvimento de Olá no Olá SDK é **idênticos** toohello ambiente de produção, com nenhuma emuladores envolvidos. Por outras palavras, o que é executado no seu cluster de desenvolvimento local implementa clusters toohello nos outros ambientes.

![Plataforma de Service Fabric][Image1]

Para obter mais informações sobre a criação de clusters no local, leia [criar um cluster no Windows Server ou Linux](service-fabric-deploy-anywhere.md) ou para o Azure, criar um cluster [através do portal do Azure de Olá](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Micro-serviços sem monitorização de estado e com monitorização de estado para o Service Fabric
Recursos de infraestrutura de serviço permite-lhe toobuild aplicações que são compostos micro-serviços ou contentores. Sem monitorização de estado micro-serviços (como gateways de protocolo e web proxies) não manter um Estado mutável fora de um pedido e a resposta do serviço de Olá. As funções de trabalho de serviços em nuvem do Azure são um exemplo de um serviço sem estado. Com monitorização de estado micro-serviços (por exemplo, contas de utilizador, as bases de dados, dispositivos, carts compras e filas) mantêm um Estado mutável, autoritativo, para além do pedido de Olá e respetiva resposta. Aplicações de dimensionamento de Internet de hoje consistem de uma combinação de micro-serviços sem monitorização de estado e com monitorização de estado. 

Uma chave differentation com o Service Fabric é o foco forte na criação de serviços com monitorização de estado, com Olá [modelos de programação incorporados ](service-fabric-choose-framework.md) ou de serviços com monitorização de estado. Olá [cenários de aplicação](service-fabric-application-scenarios.md) descrevem os cenários de olá onde são utilizados serviços com monitorização de estado.


## <a name="application-lifecycle-management"></a>Gestão de ciclo de vida de aplicações
Service Fabric fornece suporte para ciclo de vida de aplicação completa de Olá e CI/CD das aplicações em nuvem, incluindo contentores. Este ciclo de vida inclui desenvolvimento através da implementação, gestão diária e desativação de tooeventual de manutenção.

Capacidades de gestão de ciclo de vida de aplicação de Service Fabric ativar administradores da aplicação e IT operadores toouse fluxos de trabalho simples e baixa touch tooprovision, implementar, patches e monitorizar aplicações. Estes fluxos de trabalho incorporados reduzem significativamente a carga de Olá sobre aplicações de tookeep de operadores de TI continuamente disponíveis.

A maioria das aplicações é constituída por uma combinação de micro-serviços sem monitorização de estado e com monitorização de estado, contentores e outros executáveis que são implementadas em conjunto. Por ter tipos seguros em aplicações de Olá, Service Fabric permite a implementação de Olá de várias instâncias da aplicação. Cada instância é gerida e atualizar independentemente. Importante ainda, o Service Fabric pode implementar contentores ou qualquer executáveis e torná-los fiável. Por exemplo, Service Fabric pode implementar .NET, núcleo de ASP.NET, node.js, Windows contentores, Linux contentores, Java máquinas virtuais, scripts, Angular ou literalmente tudo o que constitui a sua aplicação.

Service Fabric está integrado com ferramentas de CI/CD como [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html), e [Octopus implementar](https://octopus.com/) e pode ser utilizado com qualquer outra ferramenta CI/CD popular.

Para obter mais informações sobre a gestão de ciclo de vida de aplicação, leia o artigo [ciclo de vida de aplicação](service-fabric-application-lifecycle.md). Para obter mais informações sobre como toodeploy qualquer código, consulte [implementar um executável de convidado](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Principais capacidades
Ao utilizar o Service Fabric, pode:

* Implemente tooAzure ou tooon local centros de dados que executam o Windows ou Linux com zero alterações de código. Escrever uma vez e, em seguida, implementar em qualquer lugar tooany cluster do Service Fabric.
* Desenvolva aplicações dimensionáveis que são compostas de micro-serviços utilizando modelos de programação do Service Fabric de Olá, contentores ou qualquer código.
* Desenvolva altamente fiáveis micro-serviços sem monitorização de estado e com monitorização de estado. Simplifica a estrutura de Olá da sua aplicação utilizando micro-serviços com monitorização de estado. 
* Utilize Olá novel Reliable Actors programação modelo toocreate objetos da nuvem com o código de self contido e estado.
* Implementar e orquestrar contentores que incluem a contentores do Windows e Linux contentores. Recursos de infraestrutura de serviço é um orchestrator de contentor, a monitorização de estado, de dados.
* Implemente aplicações em segundos, em alta densidade com centenas ou milhares de aplicações ou de contentores por máquina.
* Implemente versões diferentes do Olá mesma aplicação de lado pelo lado e atualizar cada aplicação de forma independente.
* Gerir Olá ciclo de vida das suas aplicações sem qualquer período de inatividade, incluindo atualizações interrompendo e nonbreaking.
* Aumentar ou reduzir horizontalmente num número de Olá de nós num cluster. À medida que nós, as aplicações de dimensionar.
* Monitorizar e diagnosticar o estado de funcionamento de Olá das suas aplicações e definir políticas para a execução automáticas reparações.
* Veja o Balanceador de recursos de Olá orquestrar redistribuição Olá das aplicações em cluster Olá. Service Fabric recupera contra falhas e otimiza a distribuição de Olá de carga com base nos recursos disponíveis.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passos seguintes
* Para mais informações:
  * [Por que motivo um micro-serviços abordar toobuilding aplicações?](service-fabric-overview-microservices.md)
  * [Descrição geral de terminologia](service-fabric-technical-overview.md)
* Configurar o Service Fabric [ambiente de desenvolvimento](service-fabric-get-started.md)  
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
