---
title: aaaOverview de Service Fabric e contentores | Microsoft Docs
description: "Uma descrição geral do Service Fabric e Olá a utilização de aplicações de microsserviço toodeploy de contentores. Este artigo fornece uma descrição geral de como contentores podem ser utilizados e Olá capacidades disponíveis no Service Fabric."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Serviço de recursos de infraestrutura e de contentores
> [!NOTE]
> Esta funcionalidade está em pré-visualização do Linux.  Implementar contentores tooa cluster do Service Fabric no Windows 10 não é suportada ainda (brevemente). 
>   

## <a name="introduction"></a>Introdução
Azure Service Fabric é uma [orchestrator](service-fabric-cluster-resource-manager-introduction.md) dos serviços de um cluster de máquinas, com anos de utilização e a otimização de grande escala para serviços Microsoft. Os serviços podem ser desenvolvidos sob vários aspetos, da utilização Olá [modelos de programação do Service Fabric](service-fabric-choose-framework.md) toodeploying [convidado executáveis](service-fabric-deploy-existing-app.md). Por predefinição, o Service Fabric implementa e ativa estes serviços como processos. Processos fornecem ativação mais rápida Olá e mais alta densidade utilização dos recursos de Olá num cluster. Serviço de recursos de infraestrutura também pode implementar serviços nas imagens de contentor. Importante ainda, pode combinar os serviços de processos e serviços nos contentores no Olá mesma aplicação. 

## <a name="containers-and-service-fabric-roadmap"></a>Plano de Service Fabric e contentores
Em versões de lançamento, muitas melhorias estão a ser planeadas de orquestração de contentor com o Service Fabric. As melhorias incluem funcionalidades para melhorada com suporte para as redes virtuais dentro de uma aplicação, funcionalidades de segurança, melhorado de diagnóstico de rede e suporte de ferramentas. Recursos de infraestrutura de serviço permite-lhe aplicações de toocreate misturando contentores compactadas com código existente (por exemplo, aplicações de IIS MVC) com os serviços desenvolvidos utilizando modelos de programação do Service Fabric de Olá.  Pode executar vários essas aplicações num único cluster. 

## <a name="what-are-containers"></a>Quais são contentores?
Contentores são encapsulados, Olá, individualmente implementáveis componentes que são executados como instâncias isoladas no mesmo kernel tootake partido virtualização que fornece um sistema operativo. Assim, cada aplicação e respetivos bibliotecas de tempo de execução, dependências e do sistema executam dentro de um contentor de vista de contentor próprio isolado de toohello acesso completo, privada de construções de sistema operativo. Juntamente com a portabilidade, este nível de isolamento de segurança e de recursos é vantagem principal de Olá para utilizar contentores com o Service Fabric, caso contrário, que executa serviços em processos.

Contentores são uma tecnologia de Virtualização que Virtualiza o sistema operativo subjacente Olá de aplicações. Contentores fornecem um ambiente imutável para aplicações toorun com variando graus de isolamento. Contentores são executados diretamente sobre kernel Olá e tem uma vista do sistema de ficheiros de Olá isolada e outros recursos. As máquinas em comparação com toovirtual contentores têm Olá seguintes vantagens:

* **Pequeno**: contentores utilizarem um único espaço e a camada versões e atualizações tooincrease eficiência de armazenamento.
* **Rápido**: contentores não tem tooboot um sistema operativo completo, para poderem iniciar muito mais rapidamente, normalmente, em segundos.
* **Portabilidade**: uma imagem de aplicação pode ser convertidos serem toorun na nuvem de Olá, no local, dentro de máquinas virtuais, nem diretamente em máquinas físicas.
* **Governação de recursos**: um contentor pode limitar os recursos físicos Olá que se pode consumir no respetivo anfitrião.

## <a name="container-types"></a>Tipos de contentor
Service Fabric suporta contentores no Linux e Windows e também suporta o modo de isolamento de Hyper-V em Olá anterior será ignorada. 

### <a name="docker-containers-on-linux"></a>Contentores de docker no Linux
Docker fornece alto nível toocreate APIs e gerir contentores por cima de contentores de kernel do Linux. Hub de docker é um repositório central toostore e obter as imagens de contentor.
Para um tutorial, consulte [implementar um tooService de contentor do Docker recursos de infraestrutura](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Contentores do Windows Server
Windows Server 2016 fornece dois tipos diferentes de contentores que diferem no nível de Olá de isolamento indicado. Contentores do Windows Server e contentores de Docker são semelhantes porque têm espaço de nomes e o ficheiro de sistema isolamento mas partilha Olá kernel com anfitrião Olá que estão em execução. No Linux, este isolamento tradicionalmente tiver sido fornecido pelo `cgroups` e `namespaces`, e contentores do Windows Server comportam-se da mesma forma.

Os contentores de Hyper-V do Windows fornecem mais segurança e isolamento, porque cada contentor não partilha o kernel do sistema operativo de Olá com outros contentores ou com o anfitrião de Olá. Com este nível de isolamento de segurança mais elevado, contentores de Hyper-V destinam-se cenários hostile, multi-inquilino.
Para um tutorial, consulte [implementar um tooService de contentor do Windows Fabric](service-fabric-get-started-containers.md).

Olá figura seguinte mostra Olá diferentes tipos de Virtualização e isolamento níveis disponíveis no sistema de operativo Olá.
![Plataforma de Service Fabric][Image1]

## <a name="scenarios-for-using-containers"></a>Cenários para utilizar contentores
Seguem-se exemplos típicos onde um contentor é uma boa opção:

* **IIS de comparação de precisão e deslocar**: Se tiver existente [ASP.NET MVC](https://www.asp.net/mvc) aplicações que pretende que o toocontinue toouse, colocá-los num contentor, em vez de migrá-los tooASP.NET Core. Estas aplicações de ASP.NET MVC dependem de serviços de informação Internet (IIS). Pode estas aplicações para imagens de contentor do Olá precreated imagem do IIS do pacote e implementá-los com o Service Fabric. Consulte [imagens do contentor no Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) para obter informações sobre como toocreate imagens IIS.
* **Combinar contentores e micro-serviços de Service Fabric**: utilizar uma imagem de contentor existente para a parte da sua aplicação. Por exemplo, poderá utilizar Olá [contentor NGINX](https://hub.docker.com/_/nginx/) de front-end da Olá web da sua aplicação e a serviços com monitorização de estado para Olá mais intensiva cálculo de back-end.
* **Reduzir o impacto dos serviços de "vizinhos inúteis"**: pode utilizar a capacidade de governação de recursos de Olá de contentores toorestrict Olá recursos que utiliza um serviço num anfitrião. Se os serviços podem consumir muitos recursos e afetar o desempenho de Olá de terceiros (por exemplo, uma operação de execução longa, semelhante de consulta), considere colocar estes serviços ao contentores que tenham a governação de recursos.

## <a name="service-fabric-support-for-containers"></a>Suporte de Service Fabric para contentores
Service Fabric suporta atualmente a implementação de contentores de Docker em contentores de Linux e Windows Server no Windows Server 2016, juntamente com suporte para o modo de isolamento de Hyper-V. 

No Olá Service Fabric [modelo de aplicação](service-fabric-application-model.md), um contentor representa um anfitrião de aplicações no serviço várias réplicas são colocadas. Service Fabric pode executar quaisquer contentores e cenário de Olá toohello semelhante [cenário executável convidado](service-fabric-deploy-existing-app.md), onde o pacote uma aplicação existente no interior de um contentor. Este cenário é Olá comuns caso de utilização para contentores, e os exemplos incluem a executar uma aplicação de escrita em qualquer idioma ou estruturas, mas não utilizar Olá incorporados Service Fabric modelos de programação.

Além disso, pode executar serviços do Service Fabric no interior de contentores bem. Suporte para os serviços do Service Fabric em execução no interior de contentores está limitado atualmente, mas toobe avançada em versões de lançamento.

* **Fiáveis serviços sem monitorização de estado no interior de contentores**: serviços fiável sem monitorização de estado utilizando Olá Reliable Services modelos de programação só são suportados no Linux. Suporte para serviços fiável sem monitorização de Estado nos contentores do Windows é planeado para uma versão futura.
* **Serviços com monitorização de estado no interior de contentores**: utilizam o modelo de programação Reliable Actors ou Reliable Services Olá estes serviços. Suporte para executar os serviços com monitorização de estado no contentores será adicionado num futuro da versão.

Service Fabric tem várias capacidades de contentor que o ajudam a criarem aplicações que são compostas de micro-serviços que são de. Recursos de infraestrutura de serviço oferece Olá seguintes capacidades de serviços:

* Implementação de imagem de contentor e a ativação.
* Governação de recursos.
* Autenticação do repositório.
* Mapeamento de portas de toohost de porta do contentor.
* Deteção de contentor de contentor e comunicação.
* Capacidade tooconfigure e definir variáveis de ambiente.

## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu sobre contentores, que Service Fabric é orchestrator um contentor e de que o Service Fabric tem funcionalidades que suportam contentores. Como passo seguinte, iremos abordará exemplos de cada uma das Olá tooshow de funcionalidades, como toouse-los.

[Implementar um tooService de contentor do Windows Fabric no Windows Server 2016](service-fabric-get-started-containers.md)

[Implementar um tooService de contentor do Docker recursos de infraestrutura no Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
