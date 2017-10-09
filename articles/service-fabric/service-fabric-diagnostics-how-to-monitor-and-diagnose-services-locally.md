---
title: "aaaDebug micro-serviços do Azure no Windows | Microsoft Docs"
description: "Saiba como toomonitor e diagnosticar os serviços escritos utilizando o Microsoft Azure Service Fabric numa máquina de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorizar e diagnosticar os serviços de uma configuração de desenvolvimento do computador local
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Monitorização, detetar, diagnosticar e resolver problemas permitem serviços toocontinue mínima interrupção toohello experiência de utilização. Enquanto a monitorização e diagnóstico é crítico num ambiente de produção implementado real, eficiência de Olá dependerá adotar um modelo semelhante durante o desenvolvimento de tooensure serviços funcionam quando move tooa a configuração do mundo real. Service Fabric torna mais fácil para tooimplement de diagnóstico de programadores de serviço que funciona na perfeição entre setups única máquina de desenvolvimento local e setups de cluster de produção do mundo real.

## <a name="event-tracing-for-windows"></a>Rastreio de eventos para o Windows
[O rastreio de eventos do Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) é Olá recomendado a tecnologia de mensagens de rastreio no Service Fabric. Alguns benefícios da utilização ETW são:

* **ETW é rápida.** Foi criada como uma tecnologia de rastreio que tem um impacto mínimo no código os tempos de execução.
* **O rastreio ETW funciona na perfeição entre ambientes de desenvolvimento local e também setups de cluster do mundo real.** Isto significa que não tem toorewrite o rastreio code quando estiver pronto toodeploy cluster código tooa real.
* **Código de sistema do Service Fabric utiliza também ETW para o rastreio interno.** Isto permite-lhe tooview interleaved seus rastreios de aplicação com os rastreios de sistema do Service Fabric. Também ajuda a toomore compreender facilmente interrelationships entre o seu código da aplicação e eventos e sequências de Olá no sistema subjacente Olá.
* **Não há suporte incorporado nas ferramentas do Visual Studio do serviço Fabric tooview Eventos ETW.** Eventos ETW aparecem na Olá vista de eventos de diagnóstico do Visual Studio depois do Visual Studio está corretamente configurada com o Service Fabric. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Ver eventos de sistema do Service Fabric no Visual Studio
Service Fabric emite Eventos ETW, os programadores de aplicações toohelp compreender o que acontece no plataforma Olá. Se ainda não o fez, avançar e seguir os passos Olá [criar a sua primeira aplicação no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Estas informações ajudará depara-se uma aplicação em execução com Olá Visualizador de eventos de diagnóstico que mostra Olá mensagens de rastreio.

1. Se a janela de eventos não apresentam automaticamente, de diagnóstico de Olá aceda toohello **vista** separador no Visual Studio, escolha **outras janelas** e, em seguida, **Visualizador de eventos de diagnóstico**.
2. Cada evento tem informações de metadados padrão que indica o evento de Olá de nó, aplicações e serviço Olá for proveniente de. Também pode filtrar a lista de Olá de eventos utilizando Olá **filtrar eventos** caixa na Olá parte superior da janela de eventos de Olá. Por exemplo, pode filtrar por **nome de nó** ou **nome do serviço.** E quando está a observar os detalhes do evento, pode também colocar em pausa utilizando Olá **colocar em pausa** botão em Olá parte superior da janela de eventos de Olá e retomar mais tarde sem qualquer perda de eventos.
   
   ![Visualizador de eventos de diagnóstico do Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Adicionar o seu próprio código de aplicação de toohello rastreios personalizado
modelos de projeto do Visual Studio do serviço Fabric Olá contém o código de exemplo. código de Olá mostra como o código de aplicação personalizada tooadd ETW rastreios que mostram cópias de segurança no Visualizador de Visual Studio ETW Olá juntamente com os rastreios de sistema do Service Fabric. Olá partido deste método é que os metadados é adicionado automaticamente tootraces e Olá Visual Visualizador de eventos de diagnóstico de outros Studio já se encontra configurado toodisplay-los.

Para projetos criados a partir de Olá **modelos de serviço** (sem monitorização de estado ou com monitorização de estado) apenas procure Olá `RunAsync` implementação:

1. Olá chamada demasiado`ServiceEventSource.Current.ServiceMessage` no Olá `RunAsync` método mostra um exemplo de um rastreio ETW personalizada do código da aplicação Olá.
2. No Olá **ServiceEventSource.cs** ficheiro, encontrará uma sobrecarga para Olá `ServiceEventSource.ServiceMessage` método que deve ser utilizado para eventos de alta frequência devido a razões tooperformance.

Para projetos criados a partir de Olá **modelos de ator** (sem monitorização de estado ou com monitorização de estado):

1. Abra Olá **"ProjectName" CS** ficheiro onde *ProjectName* é o nome de Olá que escolheu para o seu projeto de Visual Studio.  
2. Localizar o código de Olá `ActorEventSource.Current.ActorMessage(this, "Doing Work");` no Olá *DoWorkAsync* método.  Este é um exemplo de um rastreio ETW personalizada escrito a partir do código da aplicação.  
3. No ficheiro **ActorEventSource.cs**, encontrará uma sobrecarga para Olá `ActorEventSource.ActorMessage` método que deve ser utilizado para eventos de alta frequência devido a razões tooperformance.

Depois de adicionar ETW personalizado tooyour código do serviço de rastreio, pode criar, implementar e executar a aplicação Olá toosee novamente o evento (s) na Olá Visualizador de eventos de diagnóstico. Se a depuração aplicação Olá com **F5**, Olá Visualizador de eventos de diagnóstico será aberta automaticamente.

## <a name="next-steps"></a>Passos seguintes
Olá mesmo código de rastreio que adicionou a aplicação de tooyour acima para obter um diagnóstico local irá funcionar com ferramentas que pode utilizar tooview estes eventos quando executar a aplicação num cluster do Azure. Consulte estes artigos que abordam Olá opções diferentes para as ferramentas de Olá e descrevem como pode configurá-los.

* [Modo de registo de toocollect com diagnósticos do Azure](service-fabric-diagnostics-how-to-setup-wad.md)
* [Agregação de eventos e coleção utilizando EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

