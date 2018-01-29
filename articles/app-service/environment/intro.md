---
title: "Introdução aos ambientes de Serviço de Aplicações do Azure"
description: "Breve descrição geral dos ambientes de Serviço de Aplicações do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 06/13/2017
ms.author: ccompy
ms.custom: mvc
ms.openlocfilehash: 803a1cde5387b549504b42346d1a2e6a5df04746
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="introduction-to-app-service-environments"></a>Introdução aos ambientes de Serviço de Aplicações #
 
## <a name="overview"></a>Descrição geral ##

O Ambiente de Serviço de Aplicações do Azure é uma funcionalidade do Serviço de Aplicações do Azure que fornece um ambiente totalmente isolado e dedicado para executar com segurança as aplicações do Serviço de Aplicações em grande escala. Esta capacidade pode alojar as suas aplicações Web, [aplicações móveis][mobileapps], aplicações API e [funções][Functions].

Os ambientes de Serviço de Aplicações (ASEs) são adequados para cargas de trabalho de aplicações que exigem:

- Dimensionamento muito elevado.
- Isolamento e acesso a uma rede segura.
- Utilização de memória elevada.

Os clientes podem criar vários ASEs numa única região do Azure ou em várias regiões do Azure. Esta flexibilidade torna os ASEs ideais para dimensionar horizontalmente camadas de aplicações sem monitorização de estado para suportar cargas de trabalho RPS elevadas.

Os ASEs são isolados para executarem apenas as aplicações de um único cliente e são sempre implementados numa rede virtual. Os clientes têm um controlo otimizado sobre o tráfego de rede de aplicações de entrada e saída. As aplicações podem estabelecer ligações seguras de alta velocidade em VPNs aos recursos da empresa no local.

* O ASE permite o alojamento de aplicações em grande escala com acesso à rede segura. Para obter mais informações, veja [AzureCon Deep Dive](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) sobre os ASEs.
* É possível utilizar múltiplos ASEs para dimensionar horizontalmente. Para obter mais informações, veja [como configurar requisitos de espaço de uma aplicação geodistribuída](app-service-app-service-environment-geo-distributed-scale.md).
* Os ASEs podem ser utilizados para configurar a arquitetura de segurança, conforme apresentado no AzureCon Deep Dive. Para ver como a arquitetura de segurança apresentada no AzureCon Deep Dive foi configurada, veja o [artigo sobre como implementar uma arquitetura de segurança por camadas](app-service-app-service-environment-layered-security.md) com ambientes de Serviço de Aplicações.
* As aplicações em execução em ASEs podem ter o seu acesso protegido por dispositivos a montante, tais como firewalls de aplicações Web (WAFs). Para obter mais informações, veja [Configurar uma WAF para ambientes de Serviço de Aplicações](app-service-app-service-environment-web-application-firewall.md).

## <a name="dedicated-environment"></a>Ambiente dedicado ##

Um ASE é dedicado exclusivamente a uma subscrição individual e pode alojar 100 instâncias. O intervalo pode abranger de 100 instâncias num único plano do Serviço de Aplicações até 100 planos do Serviço de Aplicações de instância única, e tudo o que está dentro deste intervalo.

Um ASE é composto por front-ends e trabalhos. Os front-ends são responsáveis pela terminação de HTTP/HTTPS e pelo balanceamento de carga automático de pedidos de aplicações num ASE. Os front-ends são adicionados automaticamente à medida que os planos do Serviço de Aplicações no ASE são aumentados horizontalmente.

Os trabalhos são funções que alojam aplicações de cliente. Os trabalhos estão disponíveis em três tamanhos fixos:

* Uma vCPU/3,5 GB de RAM
* Duas vCPU/7 GB de RAM
* Quatro vCPU/14 GB de RAM

Os clientes não precisam de gerir os front-ends e os trabalhos. Toda a infraestrutura é automaticamente adicionada à medida que os clientes aumentam horizontalmente os respetivos planos do Serviço de Aplicações. À medida que os planos do Serviço de Aplicações são criados ou reduzidos verticalmente num ASE, a infraestrutura necessária é adicionada ou removida, conforme adequado.

Existe uma tarifa mensal fixa para um ASE que paga a infraestrutura e não muda com base no tamanho do ASE. Além disso, existe um custo por vCPU do plano do Serviço de Aplicações. Todas as aplicações alojadas num ASE estão na SKU de preços Isolada. Para obter informações sobre os preços de um ASE, veja a página [Preços de Serviço de Aplicações][Pricing] e consulte as opções disponíveis para ASEs.

## <a name="virtual-network-support"></a>Suporte de rede virtual ##

Um ASE só pode ser criado numa rede virtual do Azure Resource Manager. Para saber mais sobre as redes virtuais do Azure, veja as [Perguntas Frequentes sobre as redes virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Um ASE existe sempre numa rede virtual e, mais precisamente, numa sub-rede de uma rede virtual. Pode utilizar as funcionalidades de segurança das redes virtuais para controlar as comunicações de rede de entrada e saída para as suas aplicações.

Um ASE pode ter acesso à Internet com um endereço IP público ou ter acesso interno apenas com um endereço do balanceador de carga interno (ILB) do Azure.

Os [Grupos de Segurança de Rede][NSGs] restringem as comunicações de rede de entrada para a sub-rede onde um ASE se encontra. Pode utilizar NSGs para executar aplicações atrás de dispositivos e serviços a montante, tais como WAFs e fornecedores de SaaS de rede.

As aplicações também precisam de aceder frequentemente a recursos da empresa, tais como bases de dados internas e serviços Web. Se implementar o ASE numa rede virtual que tenha uma ligação VPN à rede no local, as aplicações no ASE podem aceder aos recursos no local. Esta capacidade é verdadeira, independentemente de a VPN ser uma [rede de VPNs](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) ou uma VPN [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/).

Para obter mais informações sobre como os ASEs funcionam com redes virtuais e redes no local, veja [Considerações sobre a rede do Ambiente de Serviço de Aplicações][ASENetwork].

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud/player]

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicações v1 ##

O Ambiente de Serviço de Aplicações tem duas versões: ASEv1 e ASEv2. As informações anteriores tiveram como base a versão ASEv2. Esta secção mostra as diferenças entre as versões ASEv1 e ASEv2. 

No ASEv1, é necessário gerir todos os recursos manualmente. Tal inclui os front-ends, os trabalhos e os endereços IP utilizados para SSL baseado em IP. Para poder aumentar horizontalmente o seu plano do Serviço de Aplicações, primeiro tem de aumentar horizontalmente o conjunto de processos de trabalho onde pretende alojá-lo.

O ASEv1 utiliza um modelo de preços diferente do ASEv2. No ASEv1, paga por cada vCPU alocada. Tal inclui as vCPUs utilizadas para front-ends ou trabalhos que não estejam a alojar quaisquer cargas de trabalho. No ASEv1, o tamanho de dimensionamento máximo predefinido de um ASE é 55 anfitriões no total. Tal inclui os trabalhos e os front-ends. Uma vantagem do ASEv1 é que pode ser implementado numa rede virtual clássica e numa rede virtual do Resource Manager. Para saber mais sobre o ASEv1, veja o artigo [Introdução ao Ambiente de Serviço de Aplicações v1][ASEv1Intro].

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[webapps]: ../app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
