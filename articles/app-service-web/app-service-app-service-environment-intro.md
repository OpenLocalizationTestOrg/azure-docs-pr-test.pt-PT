---
title: "aaaIntroduction tooApp v1 de ambiente de serviço"
description: "Saiba mais sobre a funcionalidade de Olá v1 de ambiente de serviço de aplicações que fornece unidades de escala segura, associados a VNet, dedicada para executar todas as suas aplicações."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>Introdução tooApp v1 de ambiente de serviço

> [!NOTE]
> Este artigo é sobre Olá v1 de ambiente de serviço de aplicações.  Há uma versão mais recente Olá ambiente de serviço de aplicações que é mais fácil toouse e é executada na infraestrutura mais poderosa. toolearn mais informações sobre a nova versão de Olá começar a utilizar Olá [introdução toohello ambiente de serviço de aplicações](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Descrição geral
Um ambiente de serviço de aplicações é um [Premium] [ PremiumTier] service opção plano do App Service do Azure fornece um ambiente completamente isolado e dedicado para execução segura de aplicações do App Service do Azure numa escala elevada, incluindo [Web Apps][WebApps], [Mobile Apps][MobileApps], e [API Apps][APIApps].  

Ambientes de serviço de aplicações são ideais para cargas de trabalho de aplicações que requerem:

* Muito grande escala
* Isolamento e de acesso à rede segura

Os clientes podem criar vários ambientes do App Service numa única região do Azure, bem como em várias regiões do Azure.  Isto faz com que ambientes do App Service ideal para aumentar horizontalmente camadas de aplicações sem estado para suportar cargas de trabalho RPS elevadas.

Ambientes do App Service são toorunning isolado apenas aplicações de um único cliente e são sempre implementados numa rede virtual.  Os clientes não têm controlo detalhado sobre o tráfego de rede de aplicação de entrada e saída e as aplicações podem estabelecer ligações seguras de alta velocidade através de recursos da empresa tooon local redes virtuais.

Todos os artigos e como-a da sobre ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).

Para uma descrição geral de como ambientes do App Service permitem escala elevada e proteger o acesso de rede, consulte Olá [descrição profunda AzureCon] [ AzureConDeepDive] em ambientes do App Service!

Para uma descrição profunda horizontalmente da receção utilizando o vários ambientes do App Service Consulte o artigo de Olá sobre toosetup um [requisitos de espaço de aplicação geo-distribuição][GeodistributedAppFootprint].

toosee como mostrada na Olá AzureCon detalhada da arquitetura de segurança de Olá foi configurada, consulte o artigo de Olá na implementação de um [em camadas a arquitetura de segurança](app-service-app-service-environment-layered-security.md) com ambientes do App Service.

Aplicações em execução em ambientes do App Service podem ter o respetivo acesso gated pelos dispositivos a montante, tais como firewalls de aplicação web (WAF).  artigo Olá [configurar uma WAF para ambientes do App Service](app-service-app-service-environment-web-application-firewall.md) abrange neste cenário. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Recursos de computação dedicada
Todos os recursos num ambiente de serviço de aplicações estão de computação de Olá dedicado exclusivamente tooa única subscrição e um ambiente de serviço de aplicações pode ser configurado com recursos de computação toofifty (50) para utilização exclusiva por uma única aplicação.

Um ambiente de serviço de aplicações é composto por um agrupamento de recursos de computação de front-end, bem como agrupamentos de recursos de computação do um toothree trabalho. 

conjunto de front-end Olá contém recursos de computação responsável por terminação de SSL como balanceamento de carga bem automático de pedidos de aplicações dentro de um ambiente de serviço de aplicações. 

Cada conjunto de trabalho contém recursos de computação alocados demasiado[planos do App Service][AppServicePlan], que por sua vez, conter uma ou mais aplicações do App Service do Azure.  Uma vez que podem existir dos conjuntos de trabalho diferentes toothree num ambiente de serviço de aplicações, dispõe de recursos de computação diferentes do Olá flexibilidade toochoose para cada conjunto de trabalho.  

Por exemplo, isto permite-lhe toocreate agrupamento de um trabalho com menos eficiente recursos de computação para planos do App Service pretendido para aplicações de desenvolvimento ou teste.  Um conjunto de trabalho segundo (ou mesmo terceiro) utilizar recursos de computação mais poderosos, concebidos para planos de serviço de aplicações a executar aplicações de produção.

Para obter mais detalhes sobre a quantidade de Olá de computação recursos obter toohello disponíveis front-end e os conjuntos de trabalho, consulte [como tooConfigure um ambiente de serviço de aplicações][HowToConfigureanAppServiceEnvironment].  

Para obter detalhes sobre Olá disponível computação tamanhos de recurso suportados num ambiente de serviço de aplicações, consulte Olá [preços do App Service] [ AppServicePricing] página e reveja Olá opções disponíveis para ambientes do App Service no escalão de preço Premium Olá.

## <a name="virtual-network-support"></a>Suporte de rede virtual
Um ambiente de serviço de aplicações podem ser criado na **ou** uma rede virtual do Azure Resource Manager, **ou** uma rede virtual do modelo de implementação clássica ([obter mais informações sobre redes virtuais][MoreInfoOnVirtualNetworks]).  Uma vez que um ambiente de serviço de aplicações sempre existe numa rede virtual e mais precisamente dentro de uma sub-rede de uma rede virtual, pode tirar partido das funcionalidades de segurança de Olá de redes virtuais toocontrol ambas as comunicações de rede de entrada e saída.  

Um ambiente de serviço de aplicações pode ser qualquer um dos Internet com um endereço IP público ou interno com acesso com apenas um endereço de Azure Balanceador de carga interno (ILB).

Pode utilizar [grupos de segurança de rede] [ NetworkSecurityGroups] toorestrict sub-rede toohello comunicações de rede onde reside um ambiente de serviço de aplicação de entrada.  Isto permite que aplicações toorun atrás montante dispositivos e serviços, tais como firewalls de aplicação web e fornecedores de SaaS de rede.

As aplicações necessitam frequentemente também tooaccess recursos empresariais, tais como bases de dados internas e os serviços web.  Uma abordagem comum é toomake estes pontos finais disponíveis toointernal apenas o tráfego de rede que circulam dentro de uma rede virtual do Azure.  Depois de um ambiente de serviço de aplicações associados a um toohello mesma rede virtual que Olá interno dos serviços, aplicações em execução no ambiente de Olá possa aceder aos mesmos, incluindo acessíveis através de pontos finais [Site a Site] [ SiteToSite]e [Azure ExpressRoute] [ ExpressRoute] ligações.

Para obter mais detalhes sobre como funcionam os ambientes do App Service com redes virtuais e redes no local Consulte Olá os seguintes artigos [arquitetura de rede][NetworkArchitectureOverview], [controlar de entrada Tráfego][ControllingInboundTraffic], e [ligar de forma segura tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Introdução
tooget começar a utilizar ambientes do App Service, consulte [como tooCreate um ambiente de serviço de aplicações][HowToCreateAnAppServiceEnvironment]

Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).

Para obter mais informações sobre a plataforma do App Service do Azure de Olá, consulte [App Service do Azure][AzureAppService].

Para obter uma descrição geral de Olá arquitetura de rede do ambiente de serviço de aplicações, consulte Olá [descrição geral da arquitetura de rede] [ NetworkArchitectureOverview] artigo.

Para obter detalhes sobre como utilizar um ambiente de serviço de aplicações com o ExpressRoute, consulte Olá seguinte artigo [Express Route e ambientes do App Service][NetworkConfigDetailsForExpressRoute].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


