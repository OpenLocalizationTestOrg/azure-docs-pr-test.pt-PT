---
title: "utilização de aaaAdvanced dos Reliable Services | Microsoft Docs"
description: "Saiba mais sobre a utilização avançada de Service Fabric Reliable Services flexibilidade adicional nos seus serviços."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>Utilização de Olá Reliable Services modelo de programação de avançadas
Azure Service Fabric simplifica escrever e gerir serviços sem monitorização de estado e com monitorização de estado fiáveis. Este guia aborda as utilizações avançadas de toogain Reliable Services mais controlo e flexibilidade sobre os serviços. Tooreading antes de este guia, familiarize-se com [o modelo de programação do Olá Reliable Services](service-fabric-reliable-services-introduction.md).

Serviços com monitorização de estado e sem monitorização de estado tem dois pontos de entrada principal para o código de utilizador:

* `RunAsync(C#) / runAsync(Java)`é um ponto de entrada para fins gerais para o seu código de serviço.
* `CreateServiceReplicaListeners(C#)`e `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` é para abrir os serviços de escuta de comunicação para pedidos de cliente.

Para a maioria dos serviços, estes pontos de duas entrada são suficientes. Em casos raros quando mais controlo sobre o ciclo de vida de um serviço é necessário, os eventos de ciclo de vida adicionais estão disponíveis.

## <a name="stateless-service-instance-lifecycle"></a>Ciclo de vida de instância de serviço sem monitorização de estado
Ciclo de vida de um serviço sem monitorização de estado é muito simple. Um serviço sem estado só pode ser aberto, fechado ou abortado. `RunAsync`num serviço sem monitorização de estado é executado quando uma instância de serviço é aberta e cancelada quando uma instância de serviço está fechada ou abortada.

Embora `RunAsync` deve ser suficiente na quase todos os casos, Olá aberto, feche e eventos de abortar num serviço sem monitorização de estado também estão disponíveis:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync é chamado quando a instância de serviço sem monitorização de estado de Olá é sobre toobe utilizado. Tarefas de inicialização do serviço expandida podem ser iniciadas neste momento.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync é chamado quando a instância de serviço sem monitorização de estado de Olá vai toobe corretamente encerrado para baixo. Isto pode ocorrer quando o código do serviço de Olá está a ser atualizado, instância de serviço Olá está a ser movida devido tooload balanceamento ou foi detetado um erro transitório. OnCloseAsync podem utilizado toosafely feche quaisquer recursos, pare qualquer processamento em segundo plano, concluir guardar Estado externo ou fechar-se para baixo de ligações existentes.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort é chamado quando a instância de serviço sem monitorização de estado de Olá está a ser forçadamente encerrada. Esta opção geralmente é chamada quando é detetada uma falha permanente num nó de hello, ou quando o Service Fabric fiável não pode gerir o ciclo de vida de instância de serviço a Olá devido a falhas de toointernal.

## <a name="stateful-service-replica-lifecycle"></a>Ciclo de vida de réplica de serviço com estado

> [!NOTE]
> Serviços fiáveis com monitorização de estado não são suportados ainda em Java.
>
>

Ciclo de vida de uma réplica de serviço com estado é muito mais complexo do que uma instância de serviço sem estado. Além disso tooopen, fechar e abortar eventos, uma réplica de serviço com estado sofre alterações de função durante a respetiva duração. Quando uma réplica de serviço com estado é alterado função, Olá `OnChangeRoleAsync` evento é acionado:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync é chamado quando a réplica de serviço com estado Olá está a alterar função, por exemplo, tooprimary ou secundário. Réplicas primárias recebem o estado de escrita (são permitidos toocreate e escrever tooReliable coleções). As réplicas secundárias são indicadas o estado de leitura (pode apenas ler a partir do coleções fiável existente). A maioria das trabalho num serviço de monitorização de estado é efetuado na réplica primária Olá. As réplicas secundárias podem efetuar a validação de só de leitura, a geração de relatórios, extração de dados ou outras tarefas só de leitura.

Num serviço com monitorização de estado, apenas Olá réplica primária tem acesso de escrita toostate e por isso, normalmente, quando o serviço de Olá está a efetuar o trabalho real. Olá `RunAsync` método num serviço de monitorização de estado é executado apenas quando a réplica de serviço com estado Olá é primária. Olá `RunAsync` método é cancelado quando as alterações da função de uma réplica primária na direção oposta ao site primário, bem como durante Olá fecham e eventos de abortar.

Utilizar Olá `OnChangeRoleAsync` eventos permite-lhe tooperform trabalho dependendo da função de réplica, bem como em alteração toorole de resposta.

Um serviço com estado fornece também eventos de ciclo de vida de Olá quatro mesmo como um serviço sem monitorização de estado, com Olá a mesma semântica e casos de utilização:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Passos seguintes
Para mais avançada Tópicos relacionados tooService recursos de infraestrutura, consulte Olá seguintes artigos:

* [Configurar Reliable Services com monitorização de estado](service-fabric-reliable-services-configuration.md)
* [Introdução de estado de funcionamento do Service Fabric](service-fabric-health-introduction.md)
* [Utilizar relatórios de estado de funcionamento do sistema para resolução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Configurar os serviços com Olá Gestor de recursos de Cluster do Service Fabric](service-fabric-cluster-resource-manager-configure-services.md)
