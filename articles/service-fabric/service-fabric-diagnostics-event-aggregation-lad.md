---
title: "aaaAzure agregação de eventos de recursos de infraestrutura de serviço com o Linux do diagnóstico do Azure | Microsoft Docs"
description: "Saiba mais sobre agregar e recolha de eventos utilizando LAD para monitorização e diagnóstico de clusters de Service Fabric do Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Agregação de eventos e a coleção com Linux do diagnóstico do Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Quando estiver a executar um cluster do Service Fabric do Azure, é uma boa ideia toocollect Olá os registos de todos os nós de Olá numa localização central. Ter Olá registos numa localização central ajuda a analisar e resolver problemas no seu cluster, ou problemas em aplicações de Olá e serviços em execução nesse cluster.

Tooupload unidirecional e recolher registos é a extensão de Linux do Azure Diagnostics (LAD) do toouse Olá, que carrega registos tooAzure armazenamento e tem também Olá opção toosend registos tooAzure Application Insights ou Event Hubs. Também pode utilizar eventos processo externo tooread Olá do armazenamento e colocá-los como um produto de plataforma de análise, [análise de registos do OMS](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise do registo.

## <a name="log-and-event-sources"></a>Origens de registo e evento

### <a name="service-fabric-platform-events"></a>Eventos de plataforma do Service Fabric
Service Fabric emite alguns registos de out of box através de [LTTng](http://lttng.org), incluindo eventos operacionais ou eventos de tempo de execução. Estes registos são armazenados na localização de Olá que Olá modelo especifica o Gestor de recursos do cluster. tooget ou definir os detalhes da conta de armazenamento Olá, procure a tag de Olá **AzureTableWinFabETWQueryable** e procure **StoreConnectionString**.

### <a name="application-events"></a>Eventos de aplicações
 Eventos emitidos a partir do código as suas aplicações e dos serviços, conforme especificado por si quando instrumentação o software. Pode utilizar qualquer solução de registo que escreve os ficheiros de registo baseados em texto – por exemplo, LTTng. Para obter mais informações, consulte a documentação de LTTng Olá no rastrear a aplicação.

[Monitorizar e diagnosticar os serviços de uma configuração de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Implementar a extensão de diagnóstico de Olá
Olá primeiro passo para recolher registos é uma extensão de diagnóstico de Olá toodeploy em cada um dos Olá VMs no cluster do Service Fabric Olá. Olá extensão de diagnóstico recolhe registos de cada VM e carrega-os conta de armazenamento toohello que especificar. passos de Olá variam com base no quer utilize Olá portal do Azure ou do Azure Resource Manager.

Definir toodeploy Olá diagnóstico extensão toohello VMs no cluster de Olá como parte da criação do cluster, **diagnóstico** demasiado**no**. Depois de criar o cluster de Olá, não é possível alterar esta definição utilizando Olá portal.

Em seguida, configurar Linux do Azure Diagnostics (LAD) toocollect Olá ficheiros e colocá-los na sua conta de armazenamento. Este processo é explicado como cenário 3 ("carregar os seus próprios ficheiros de registo") no artigo Olá [utilizando LAD toomonitor e diagnosticar VMs com Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Seguinte obtém este processo aceder toohello rastreios. Pode carregar Visualizador tooa de rastreios de Olá à sua escolha.

Também pode implementar a extensão de diagnóstico de Olá utilizando o Gestor de recursos do Azure. Olá processo é semelhante para o Windows e Linux e é documentado para clusters do Windows no [como toocollect regista com o Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

Também pode utilizar o Operations Management Suite, conforme descrito em [análise de registos do Operations Management Suite com o Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Depois de concluir esta configuração, Olá LAD agente monitores Olá ficheiros de registo especificado. Sempre que uma nova linha é anexado toohello ficheiro, cria uma entrada de syslog que é enviado toohello armazenamento que especificou.

## <a name="next-steps"></a>Passos seguintes

toounderstand em mais detalhe que eventos deve examinar durante a resolução de problemas, consulte [LTTng documentação](http://lttng.org/docs) e [utilizando LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
