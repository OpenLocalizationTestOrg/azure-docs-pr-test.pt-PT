---
title: "aaaReport e verificação de estado de funcionamento com o Azure Service Fabric | Microsoft Docs"
description: "Saiba como os relatórios de estado de toosend do código do serviço e como o estado de funcionamento do toocheck Olá do seu serviço utilizando o estado de funcionamento de Olá ferramentas de monitorização que Azure Service Fabric fornece."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Comunicar e verificar o estado de funcionamento dos serviços
Quando os serviços de encontrarem problemas, os incidentes de correção capacidade toorespond tooand e falhas depende os problemas de Olá toodetect capacidade rapidamente. Se comunicar problemas e falhas de Gestor de estado de funcionamento do Azure Service Fabric toohello do código do serviço, pode utilizar o estado de funcionamento padrão ferramentas que o Service Fabric fornece o estado de funcionamento de Olá toocheck de monitorização.

Existem três formas que pode comunicar o estado de funcionamento do serviço de Olá:

* Utilize [partição](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objetos.  
  Pode utilizar Olá `Partition` e `CodePackageActivationContext` objetos de estado de funcionamento do tooreport Olá dos elementos que fazem parte do contexto atual Olá. Por exemplo, o código que é executado como parte de uma réplica pode comunicar o estado de funcionamento apenas essa réplica, Olá partição que pertence e aplicação Olá que faz parte do.
* Utilize `FabricClient`.   
  Pode utilizar `FabricClient` tooreport estado de funcionamento a partir do código do serviço de Olá cluster Olá não esteja [segura](service-fabric-cluster-security.md) ou se o serviço de Olá está em execução com privilégios de administrador. A maioria dos cenários no mundo real não utilizar clusters protegidas, ou forneça privilégios de administrador. Com `FabricClient`, pode comunicar o estado de funcionamento em qualquer entidade que faz parte do cluster de Olá. Idealmente, no entanto, código do serviço deve apenas enviar relatórios que estão relacionados tooits própria estado de funcionamento.
* Utilize Olá REST APIs no cluster Olá, aplicação, aplicação implementada, serviço, o pacote de serviço, partição, réplica ou níveis de nó. Isto pode ser utilizado tooreport o estado de funcionamento da num contentor.

Este artigo explica como um exemplo que comunica o estado de funcionamento a partir do código do serviço de Olá. exemplo de Olá também mostra como as ferramentas de Olá fornecidas pelo serviço de recursos de infraestrutura podem ser utilizados toocheck Olá o estado de funcionamento. Este artigo é um Estado de funcionamento introdução rápida toohello capacidades dos recursos de infraestrutura do serviço de monitorização de toobe pretendido. Para obter informações mais detalhadas, pode ler série Olá dos artigos aprofundados sobre o estado de funcionamento que começam com ligação Olá no fim de Olá deste artigo.

## <a name="prerequisites"></a>Pré-requisitos
Tem de ter o seguinte Olá instalado:

* Visual Studio 2015 ou Visual Studio 2017
* SDK do Service Fabric

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate um cluster de desenvolvimento seguro local
* Abra o PowerShell com privilégios de administrador e execute Olá os seguintes comandos:

![Os comandos que mostram como toocreate um cluster de desenvolvimento seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy uma aplicação e verificar o estado de funcionamento
1. Abra o Visual Studio como administrador.
2. Criar um projeto utilizando Olá **serviço de monitorização de estado** modelo.
   
    ![Criar uma aplicação de Service Fabric com o serviço de monitorização de estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Prima **F5** aplicação de Olá toorun no modo de depuração. aplicação Olá é cluster local toohello implementado.
4. Após a aplicação Olá está em execução, clique no ícone do Gestor de clusters locais Olá na área de notificação de Olá e selecione **gerir Cluster Local** de tooopen de menu de atalho Olá Service Fabric Explorer.
   
    ![Abra o Explorador de recursos de infraestrutura de serviço da área de notificação](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. Estado de funcionamento da aplicação Olá deverá ser apresentado como esta imagem. Neste momento, aplicação Olá deve estar em bom estado sem erros.
   
    ![Aplicação bom estado de funcionamento no Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Também pode verificar o estado de funcionamento de Olá utilizando o PowerShell. Pode utilizar ```Get-ServiceFabricApplicationHealth``` toocheck pode utilizar o estado de funcionamento de uma aplicação e ```Get-ServiceFabricServiceHealth``` toocheck estado de funcionamento de um serviço. Olá, relatório de estado de funcionamento para Olá mesma aplicação no PowerShell está nesta imagem.
   
    ![Aplicação bom estado de funcionamento no PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>código do serviço tooyour tooadd estado de funcionamento personalizado eventos
Olá modelos de projeto de Service Fabric no Visual Studio contêm código de exemplo. Olá passos seguintes mostram como pode comunicar eventos de estado de funcionamento personalizado a partir do seu código de serviço. Esses relatórios apareçam automaticamente nas ferramentas padrão de Olá para que o Service Fabric fornece, como o Service Fabric Explorer, vista de estado de funcionamento de portal do Azure e do PowerShell de monitorização de estado de funcionamento.

1. Reabra a aplicação Olá que criou anteriormente no Visual Studio ou criar uma nova aplicação utilizando Olá **serviço de monitorização de estado** modelo do Visual Studio.
2. Abrir o ficheiro de Stateful1.cs Olá e determinar Olá `myDictionary.TryGetValueAsync` chamada em Olá `RunAsync` método. Pode ver que este método devolve um `result` que detém Olá valor atual do contador de Olá porque Olá lógica chave esta aplicação é tookeep uma execução de contagem. Se isto foram real da aplicação e se a falta de Olá de resultado representado uma falha, seria aconselhável tooflag esse evento.
3. tooreport um evento de estado de funcionamento quando a falta de Olá de resultado representa uma falha, adicione Olá os seguintes passos.
   
    a. Adicionar Olá `System.Fabric.Health` espaço de nomes toohello Stateful1.cs ficheiro.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Adicionar Olá seguinte código após Olá `myDictionary.TryGetValueAsync` chamar
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Elaboramos relatórios de estado de funcionamento de réplica porque está a ser reportado num serviço de monitorização de estado. Olá `HealthInformation` parâmetro armazena informações sobre o problema de estado de funcionamento de Olá que está a ser reportado.
   
    Se criou um serviço sem monitorização de estado, utilize Olá seguinte código
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Se o serviço está em execução com privilégios de administrador ou se hello o cluster não está [segura](service-fabric-cluster-security.md), também pode utilizar `FabricClient` tooreport de estado de funcionamento conforme mostrado no Olá os seguintes passos.  
   
    a. Criar Olá `FabricClient` instância após Olá `var myDictionary` declaração.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Adicionar Olá seguinte código após Olá `myDictionary.TryGetValueAsync` chamada.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Vamos simular desta falha e veja-apareçam nas ferramentas de monitorização de estado de funcionamento de Olá. Falha de Olá toosimulate, comente a primeira linha de Olá no estado de funcionamento de Olá reporting código que adicionou anteriormente. Depois de comente a primeira linha de Olá, código de Olá terá um aspeto semelhante Olá seguinte exemplo.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Este código desencadeado relatório de estado de funcionamento de Olá sempre `RunAsync` executa. Depois de efetuar Olá alterar, prima **F5** aplicação de Olá toorun.
6. Após a aplicação Olá está em execução, abra o estado de funcionamento do Service Fabric Explorer toocheck Olá da aplicação Olá. Neste momento, Service Fabric Explorer mostra que a aplicação Olá está danificada. Trata-se devido ao erro Olá que foi reportado a partir do código Olá que adicionamos anteriormente.
   
    ![Aplicação mau estado de funcionamento no Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Se selecionar a réplica primária Olá na vista de árvore Olá do Service Fabric Explorer, verá que **estado de funcionamento** indica um erro, demasiado. Service Fabric Explorer apresenta também o relatório de estado de funcionamento de Olá detalhes que foram adicionados toohello `HealthInformation` parâmetro Olá code. Pode ver Olá mesmo relatórios de estado de funcionamento no PowerShell e Olá portal do Azure.
   
    ![Estado de funcionamento de réplica no Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Este relatório permanece no Gestor de estado de funcionamento de Olá até é substituído por outro relatório ou até que esta réplica foi eliminada. Porque não foi possível definir não `TimeToLive` para este relatório de estado de funcionamento no Olá `HealthInformation` objeto relatório Olá nunca expira.

Recomendamos que o estado de funcionamento deve ser comunicado no nível mais granular Olá, que neste caso é réplica Olá. Também pode comunicar o estado de funcionamento no `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

Estado de funcionamento tooreport em `Application`, `DeployedApplication`, e `DeployedServicePackage`, utilize `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Passos seguintes
* [Descrição profunda sobre o estado de funcionamento do Service Fabric](service-fabric-health-introduction.md)
* [API REST para os relatórios do Estado de funcionamento do serviço](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [API REST para os relatórios do Estado de funcionamento da aplicação](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

