---
title: aaaTroubleshooting com o rastreio de eventos | Microsoft Docs
description: "problemas mais comuns de Olá encontrados durante a implementação de serviços no Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Resolver problemas comuns quando implementar serviços no Azure Service Fabric
Quando estiver a executar serviços no seu computador de programador, é fácil toouse [ferramentas de depuração do Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Para clusters remotos, [relatórios de estado de funcionamento](service-fabric-view-entities-aggregated-health.md) são sempre toostart um bom local. Olá mais fácil tooaccess formas estes relatórios são através do PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md). Este artigo assume que está a depurar um cluster remoto e que têm um conhecimento básico de como toouse qualquer uma destas ferramentas.

## <a name="application-crash"></a>Falhas de aplicação
Olá "partição está abaixo contagem de instâncias ou de réplica de destino" relatório é um bom indicador de que o serviço esteja a falhar. toofind enviados em que esteja a falhar o serviço demora investigação mais um pequeno. Quando o serviço está em execução em escala, sua melhor amigo será um conjunto de rastreios de well thought Escalamento.  Sugerimos que tente [diagnósticos do Azure](service-fabric-diagnostics-how-to-setup-wad.md) para recolher os rastreios e através de uma solução, como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para ver e procurar rastreios Olá.

![O estado de funcionamento do SFX partição](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Durante a inicialização do serviço ou ator
Quaisquer exceções antes de inicializar o tipo de serviço Olá fará Olá toocrash de processo. Para estes tipos de falhas, o registo de eventos de aplicações de Olá irá mostrar erro Olá do seu serviço.
Estes são Olá mais comuns exceções toosee antes de inicializar o serviço de Olá.

***System.IO.FileNotFoundException***

Este erro é frequentemente devido a dependências de assemblagem toomissing. Verificar a propriedade de CopyLocal de Olá no Visual Studio ou da cache de assemblagem global Olá para o nó de Olá.

***System.Runtime.InteropServices.COMException*** *em System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Isto indica que esse nome de tipo de serviço registado Olá não corresponde ao manifesto do serviço de Olá.

[Diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) pode ser configurado tooupload registo de eventos de aplicações Olá para todos os seus nós automaticamente.

### <a name="runasync-or-onactivateasync"></a>RunAsync() ou OnActivateAsync()
Se a falhas de Olá acontece durante a inicialização de Olá ou em execução do seu tipo de serviço registado ou ator, Olá excepção será detectada pelo Azure Service Fabric. Pode ver estes de fornecedores de EventSource Olá detalhados Olá "Passos" secção.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre os diagnósticos existentes fornecidos pelo serviço de recursos de infraestrutura:

* [Diagnóstico do Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Diagnóstico de serviços fiável](service-fabric-reliable-services-diagnostics.md)

