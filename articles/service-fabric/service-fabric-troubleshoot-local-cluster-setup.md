---
title: "aaaTroubleshoot a configuração de cluster do Service Fabric local | Microsoft Docs"
description: "Este artigo aborda um conjunto de sugestões de resolução de problemas de cluster de desenvolvimento local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Resolver problemas relacionados com a configuração de cluster de desenvolvimento local
Caso se depare com um problema ao interagir com o cluster de desenvolvimento local do Azure Service Fabric, reveja Olá sugestões para possíveis soluções a seguir.

## <a name="cluster-setup-failures"></a>Falhas de configuração de cluster
### <a name="cannot-clean-up-service-fabric-logs"></a>Não é possível limpar os registos de Service Fabric
#### <a name="problem"></a>Problema
Ao executar o script de DevClusterSetup Olá, verá um erro semelhante isto:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Solução
Feche Olá atual janela do PowerShell e abrir uma nova janela do PowerShell como administrador. Agora, deve ser toosuccessfully capaz de executar o script de Olá.

## <a name="cluster-connection-failures"></a>Falhas de ligação de cluster
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Cmdlets do PowerShell de Service Fabric não são reconhecidos no Azure PowerShell
#### <a name="problem"></a>Problema
Se tentar toorun qualquer um dos Olá cmdlets do PowerShell de Service Fabric, tais como `Connect-ServiceFabricCluster` numa janela do PowerShell do Azure, não conseguir, indicando que cmdlet Olá não é reconhecido. razão Olá para este é o Azure PowerShell utiliza a versão de 32 bits Olá do Windows PowerShell (mesmo em versões de SO de 64 bits), enquanto Olá cmdlets do Service Fabric só funcionam nos ambientes de 64 bits.

#### <a name="solution"></a>Solução
Sempre executar cmdlets do Service Fabric diretamente a partir do Windows PowerShell.

> [!NOTE]
> versão mais recente do Olá do Azure PowerShell não criar um atalho especial, pelo que este já não deve ocorrer.
> 
> 

### <a name="type-initialization-exception"></a>Exceção de inicialização do tipo
#### <a name="problem"></a>Problema
Quando estiverem a ligar toohello cluster no PowerShell, consulte o erro de Olá TypeInitializationException para System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Solução
A variável de caminho não foi corretamente definida durante a instalação. Terminar a sessão do Windows e inicie sessão novamente. Isto atualiza o seu caminho.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Falha da ligação de cluster com "Objeto está fechado"
#### <a name="problem"></a>Problema
Uma chamada tooConnect-ServiceFabricCluster falha com o erro seguinte:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Solução
Feche Olá atual janela do PowerShell e abrir uma nova janela do PowerShell como administrador. Agora deve ser capaz de ligar toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Excepção de ligação negado de recursos de infraestrutura
#### <a name="problem"></a>Problema
Quando a depuração do Visual Studio, receberá um erro de FabricConnectionDeniedException.

#### <a name="solution"></a>Solução
Este erro ocorre normalmente quando tenta toostart um processo de anfitrião do serviço manualmente, em vez de permitir toostart de tempo de execução do Service Fabric Olá-lo por si.

Certifique-se de que não têm qualquer projetos do serviço definido como projetos de arranque na sua solução. Projetos de aplicação de Service Fabric só devem ser definidos como projetos de arranque.

> [!TIP]
> Se, a seguir o programa de configuração, o cluster local começa toobehave anormalmente, pode repô-lo utilizando a aplicação de tabuleiro do sistema de Gestor do Olá local cluster. Este remove Olá cluster existente e configure um novo. Tenha em atenção que todas as aplicações implementadas e dados associados são removidos.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* [Compreender e resolver problemas de cluster com relatórios de estado de funcionamento do sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualizar o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

