---
title: "Ambiente de serviço de aplicações de aaaAzure Leia-me"
description: "Apresenta uma lista de documentação de Olá que descreve o ambiente de serviço de aplicações do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a>Documentação de ambiente de serviço de aplicações
 Ambiente de serviço de aplicações do Azure é uma funcionalidade do App Service do Azure que fornece um ambiente completamente isolado e dedicado para execução segura de aplicações do App Service numa escala elevada. Esta capacidade pode alojar o [aplicações web][webapps], [aplicações móveis][mobileapps], [das API apps] [ APIApps], e [funções][Functions].

Ambientes do App Service (ASEs) são ideais para cargas de trabalho da aplicação que necessitam:

* Muito grande escala.
* Isolamento e um acesso de rede.

Os clientes podem criar vários ASEs numa única região do Azure e em várias regiões do Azure. Este versatility torna ASEs ideal para aumentar horizontalmente camadas da aplicação sem monitorização de estado para suportar cargas de trabalho RPS elevadas.

ASEs são isolada toorunning apenas aplicações de um único cliente e sempre são implementadas numa rede virtual do Azure. Os clientes têm um controlo detalhado sobre o tráfego de rede de aplicação de entrada e saída utilizando [grupos de segurança de rede][NSGs]. Aplicações também podem estabelecer ligações de alta velocidade seguras através de recursos da empresa tooon local redes virtuais.

As aplicações necessitam frequentemente tooaccess recursos empresariais, tais como bases de dados internas e os serviços web. As aplicações que são executados no ASEs podem aceder a recursos através de [site para site] [ SiteToSite] VPN e [Azure ExpressRoute] [ ExpressRoute] ligações.

* [O que é um ambiente de serviço de aplicações?][Intro]
* [Criar um ambiente de serviço de aplicações][MakeExternalASE]
* [Criar um ambiente de serviço de aplicações do Balanceador de carga interno][MakeILBASE]
* [Utilizar um ambiente de serviço de aplicações][UsingASE]
* [Considerações de redes e Olá ambiente de serviço de aplicações][ASENetwork]
* [Criar um ambiente de serviço de aplicações a partir de um modelo][MakeASEfromTemplate]


## <a name="videos"></a>Vídeos
Mestre moderna PaaS para Olá Enterprise App Service do Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Implementar Aplicações altamente dimensionáveis e seguras
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Executar Aplicações Móveis e Web Enterprise no Serviço de Aplicações do Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicações v1 ##
Existem duas versões do ambiente de serviço de aplicações: ASEv1 e ASEv2. Para obter informações sobre ASEv1, consulte [documentação do ambiente de serviço de aplicações v1][ASEv1README].


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
