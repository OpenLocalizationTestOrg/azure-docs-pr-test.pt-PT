---
title: "aaaAdd ou remover cluster do Service Fabric nós tooa autónomo | Microsoft Docs"
description: "Saiba como tooadd ou remover nós tooan Azure Service Fabric cluster numa máquina física ou virtual com o Windows Server, que pode ser no local ou em nenhuma nuvem."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Adicionar ou remover nós tooa autónomo cluster do Service Fabric em execução no Windows Server
Depois de ter [criado o seu cluster do Service Fabric autónomo nas máquinas do Windows Server](service-fabric-cluster-creation-for-windows-server.md), podem alterar as necessidades de negócio e pode precisar de tooadd ou remover nós tooyour cluster. Este artigo fornece os passos detalhados tooachieve isto. Tenha em atenção que adicionar/remover a funcionalidade de nó não é suportada em clusters de desenvolvimento local.

## <a name="add-nodes-tooyour-cluster"></a>Adicionar nós tooyour cluster
1. Preparar Olá VM/máquina que pretende tooadd tooyour cluster seguindo os passos de Olá mencionados Olá [Olá preparar máquinas pré-requisitos de Olá toomeet para implementação de cluster](service-fabric-cluster-creation-for-windows-server.md) secção
2. Identificar o domínio de falhas e são curso tooadd desta VM máquina para o domínio de atualização
3. Ambiente de trabalho remoto (RDP) para Olá VM/máquina que pretende que o cluster de toohello tooadd
4. Copiar ou [transferir o pacote de autónomo do Olá para recursos de infraestrutura de serviço para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/máquina e deszipe o pacote de Olá
5. Executar o Powershell com privilégios elevados e navegue até toohello localização do pacote deszipada Olá
6. Executar Olá *AddNode.ps1* script com parâmetros de Olá descrever Olá novo nó tooadd. exemplo de Olá abaixo adiciona um novo nó chamado VM5, com o tipo NodeType0 e endereços IP 182.17.34.52, UD1 e DF: / dc1/r0. Olá *ExistingClusterConnectionEndPoint* já se encontra um ponto final de ligação para um nó de cluster existente Olá, que pode ser o endereço IP Olá *qualquer* nó no cluster de Olá.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Assim que o script de Olá termina em execução, pode verificar se o novo nó de Olá foi adicionado ao executar Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.

7. consistência tooensure em diferentes nós num cluster de Olá, tem de iniciar uma atualização da configuração. Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Olá o ficheiro de configuração mais recente e adicione Olá recém-adicionada nó demasiado secção "Nós". Recomenda-se também tooalways ter Olá mais recente configuração de cluster disponível no caso de Olá terá tooredploy num cluster com Olá mesma configuração.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) atualização de Olá toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer. Em alternativa, pode executar [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Adicionar nós tooclusters configurado com a segurança do Windows utilizam a gMSA
Para clusters configurados com o grupo gerido serviço Account(gMSA) (https://technet.microsoft.com/library/hh831782.aspx), um novo nó pode ser adicionado através de uma atualização da configuração:
1. Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) em qualquer um de nós existentes Olá tooget Olá o ficheiro de configuração mais recente e adicione os detalhes sobre o novo nó de Olá pretende tooadd na secção de nós"Olá". Certifique-se de que o novo nó de Olá faz parte de Olá mesmo a conta gerida de grupo. Esta conta deve ser um administrador em todas as máquinas.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) atualização de Olá toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer. Em alternativa, pode executar [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>Adicionar nó tipos tooyour cluster
Na ordem tooadd um novo tipo de nó, modifique a sua configuração tooinclude Olá novo tipo de nó na secção "NodeTypes" em "Propriedades" e começar a uma configuração de fazer a actualização utilizando [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Uma vez concluída a atualização de Olá, pode adicionar o novo cluster de tooyour de nós com este tipo de nó.

## <a name="remove-nodes-from-your-cluster"></a>Remover nós do cluster
Um nó pode ser removido de um cluster com uma atualização da configuração, no Olá seguinte forma:

1. Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) ficheiro de configuração mais recente do tooget Olá e *remover* nó Olá da secção "Nós".
Adicionar Olá "NodesToBeRemoved" parâmetro demasiado "Configurar" secção no interior da secção "FabricSettings". Olá "valor" deve ser uma lista separada por vírgulas de nomes de nó de nós que necessitam de toobe removido.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) atualização de Olá toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer. Em alternativa, pode executar [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> Remoção de nós, pode iniciar várias atualizações. Alguns nós são marcados com `IsSeedNode=”true”` Etiquetar e podem ser identificados através de consultas cluster Olá manifesto utilizando `Get-ServiceFabricClusterManifest`. Remoção de nós pode demorar mais do que outras pessoas, uma vez que nós de seed Olá terão toobe moveu em torno em tais cenários. cluster de Olá tem de manter um mínimo de 3 nós de tipo de nó principal.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Remover tipos de nó do cluster
Antes de remover um tipo de nó, verifique duplo se existem quaisquer nós que referencia o tipo de nó Olá. Remova estes nós antes de remover o tipo de nó Olá correspondente. Depois de todos os nós correspondentes são removidos, pode remover a configuração de cluster Olá Olá NodeType e começar a uma configuração de fazer a actualização utilizando [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Substitua primários nós do cluster
substituição de Olá de nós principais deve ser executado um nó após a outra, em vez de remover e, em seguida, adicionar em lotes.


## <a name="next-steps"></a>Passos seguintes
* [Definições de configuração do cluster do Windows autónomo](service-fabric-cluster-manifest.md)
* [Proteger um cluster autónomo no Windows utilizando X509 certificados](service-fabric-windows-cluster-x509-security.md)
* [Criar um cluster do Service Fabric autónomo com as VMs do Azure com o Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)

