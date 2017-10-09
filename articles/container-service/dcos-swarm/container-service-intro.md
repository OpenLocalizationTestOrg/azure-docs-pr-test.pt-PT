---
title: aaaDocker contentor de alojamento na nuvem do Azure | Microsoft Docs
description: "Serviço de contentor do Azure fornece uma forma toosimplify Olá criação, configuração e gestão de um cluster de máquinas virtuais que estão pré-configuradas toorun de aplicações."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contentores, Microserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 46a0071a7497a3ff44d75413b49f1d06f844c446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodocker-container-hosting-solutions-with-azure-container-service"></a>Contentor de tooDocker introdução alojamento soluções com o serviço de contentor do Azure 
Serviço de contentor do Azure torna mais simples para si toocreate, configurar e gerir um cluster de máquinas virtuais que estão pré-configuradas toorun de aplicações. Utiliza uma configuração otimizada de populares ferramentas open-source de agendamento e orquestração. Isto permite-lhe toouse suas competências existentes, ou desenhar após um corpo de grande e crescente de conhecimentos de Comunidade, toodeploy e gerir as aplicações baseadas no contentor no Microsoft Azure.

![Serviço de contentor do Azure fornece um meio toomanage de aplicações em vários anfitriões no Azure.](./media/acs-intro/acs-cluster-new.png)

Olá Docker contentor formato tooensure que os contentores de aplicação são portabilidade total tira partido do serviço de contentor do Azure. Também suporta a sua escolha de Marathon e DC/OS, Docker Swarm ou Kubernetes para que pode dimensionar toothousands estas aplicações de contentores, ou até mesmo dezenas de milhares.

Ao utilizar o serviço de contentor do Azure, pode tirar partido das funcionalidades de nível empresarial do Azure, mantendo ainda portabilidade de aplicação – incluindo portabilidade em camadas de orquestração Olá.

## <a name="using-azure-container-service"></a>Utilizar o Azure Container Service
O nosso objetivo com o serviço de contentor do Azure é tooprovide num ambiente de alojamento do contentor utilizando ferramentas open source e tecnologias que estão atualmente populares entre os nossos clientes. fim de toothis, expomos pontos finais de API standard Olá para o orchestrator escolhido (DC/OS, Docker Swarm ou Kubernetes). Utilizando estes pontos finais, pode tirar partido do software que seja capaz de falar com pontos finais de toothose. Por exemplo, no caso de Olá do ponto final de Docker Swarm do Olá, poderá escolher interface de linha de comandos (CLI) do toouse Olá Docker. Para DC/OS, pode optar por utilizar Olá DCOS CLI. Para Kubernetes, pode optar por `kubectl`.

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a>Criar um cluster de Docker com o Azure Container Service
toobegin utilizando o serviço de contentor do Azure, implementar um cluster do serviço de contentor do Azure através do portal Olá (Olá pesquisa Marketplace para **serviço de contentor Azure**), utilizando um modelo Azure Resource Manager ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/SO](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), ou [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), ou com Olá [Azure CLI 2.0](container-service-create-acs-cluster-cli.md). Olá fornecido modelos de início rápido podem ser modificadas tooinclude adicionais ou avançada configuração do Azure. Para mais informações, consulte [Deploy an Azure Container Service cluster (Implementar um cluster do Azure Container Service)](container-service-deployment.md).

## <a name="deploying-an-application"></a>Implementar uma aplicação
O Azure Container Service permite escolher o Docker Swarm, o DC/OS ou o Kubernetes para orquestração. O modo como implementa a aplicação depende da sua escolha do orquestrador.

### <a name="using-dcos"></a>Utilizar DC/OS
DC/OS é um sistema operativo distribuído com base no kernel do Olá Apache Mesos sistemas distribuídos. O Apache Mesos está alojado no Olá Apache Software Foundation e lista algumas das Olá [nomes maiores no IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) como utilizadores e os contribuintes.

![O Azure Container Service configurado para DC/OS, a mostrar agentes e mestres.](media/acs-intro/dcos.png)

O DC/OS e o Apache Mesos incluem um conjunto impressionante de funcionalidades:

* Escalabilidade comprovada
* Mestre e subordinados replicados com tolerância a falhas, utilizando o Apache ZooKeeper
* Suporte para contentores formatados para Docker
* Isolamento nativo entre tarefas com contentores Linux
* Agendamento de vários recursos (memória, CPU, disco e portas)
* APIs Java, Python e C++ para o desenvolvimento de novas aplicações paralelas
* Uma IU da Web para ver o estado do cluster

Por predefinição, o DC/SO em execução no serviço de contentor do Azure inclui plataforma de orquestração Olá Marathon para cargas de trabalho de agendamento. No entanto, incluído com Olá implementação de DC/SO de ACS é Olá Mesosphere universo de serviços que podem ser adicionados tooyour serviço. Os serviços no Olá universo incluem Spark, Hadoop, Cassandra e muito mais.

![Universo DC/OS no Azure Container Service](media/dcos/universe.png)

#### <a name="using-marathon"></a>Utilizar o Marathon
Marathon é um init em todo o cluster e um sistema de controlo de serviços no cgroups – ou, no caso de Olá do serviço de contentor do Azure, os contentores formatados para Docker. O Marathon fornece uma IU da Web a partir da qual pode implementar as aplicações. Pode aceder-lhe com um URL semelhante a `http://DNS_PREFIX.REGION.cloudapp.azure.com`, em que DNS\_PREFIX e REGION são definidos no momento da implementação. Como é óbvio, também pode fornecer o seu nome DNS. Para obter mais informações sobre a execução de um contentor utilizando a IU da web do Olá Marathon, consulte [gestão de contentores de DC/SO através da IU da web do Olá Marathon](container-service-mesos-marathon-ui.md).

![Lista de Aplicações Marathon](media/dcos/marathon-applications-list.png)

Também pode utilizar Olá REST APIs para comunicar com o Marathon. Existem várias bibliotecas de cliente disponíveis para cada ferramenta. Estes incluem uma variedade de linguagens – e, obviamente, pode utilizar o protocolo HTTP de Olá em qualquer idioma. Além disso, muitas ferramentas DevOps populares fornecem suporte para o Marathon. Isto proporciona flexibilidade máxima para a sua equipa de operações quando estiver a trabalhar com um cluster do Azure Container Service. Para obter mais informações sobre a execução de um contentor utilizando Olá API REST do Marathon, consulte [gestão de contentores de DC/SO através de Olá API REST do Marathon](container-service-mesos-marathon-rest.md).

### <a name="using-docker-swarm"></a>Utilizar o Docker Swarm
O Docker Swarm fornece clustering nativo para o Docker. Uma vez que o Docker Swarm serve Olá API do Docker padrão, qualquer ferramenta que já comunica com um daemon de Docker pode utilizar anfitriões de toomultiple de escala de tootransparently Swarm no serviço de contentor do Azure.

![Serviço de contentor do Azure configurada toouse Swarm.](media/acs-intro/acs-swarm2.png)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Ferramentas suportadas para gerir contentores num Swarm cluster incluem, mas não estarem limitadas aos seguintes Olá:

* Dokku
* CLI do Docker e Docker Compose
* Krane
* Jenkins

### <a name="using-kubernetes"></a>Utilizar Kubernetes
O Kubernetes é uma ferramenta popular de orquestração do contentor de grau de produção de código aberto. O Kubernetes automatiza a implementação, o dimensionamento e a gestão de aplicações no contentor. Porque é uma solução de open source e é controlada pela Comunidade de open source Olá, é executado de forma totalmente integrada no serviço de contentor do Azure e podem ser utilizados toodeploy contentores à escala no serviço de contentor do Azure.

![Serviço de contentor do Azure configurada toouse Kubernetes.](media/acs-intro/kubernetes.png)

Tem um conjunto avançado de funcionalidades, incluindo:
* Dimensionamento horizontal
* Deteção do serviço e balanceamento de carga
* Gestão de segredos e configuração
* Implementações e reversões automáticas com base em API
* Autorrecuperação

## <a name="videos"></a>Vídeos
Introdução ao Azure Container Service (101):  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

Olá aplicações a utilizar a criar serviço de contentor do Azure (compilação 2016)

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a>Passos seguintes

Implementar um cluster do serviço de contentor utilizando Olá [portal](container-service-deployment.md) ou [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).
