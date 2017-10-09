---
title: aaaCreate uma regra de Balanceador de carga do Azure para um cluster
description: Configure portas de tooopen um balanceador de carga do Azure para o cluster do Service Fabric do Azure.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Abra portas para um cluster do Service Fabric

Balanceador de carga Olá implementado com o cluster do Azure Service Fabric direciona o tráfego tooyour aplicação em execução num nó. Se alterar o toouse aplicação uma porta diferente, tem de expor essa porta (ou uma porta diferente de rotas) no Olá Balanceador de carga do Azure.

Quando tiver implementado o tooAzure de cluster de recursos de infraestrutura de serviço, um balanceador de carga foi criado automaticamente para si. Se não tiver um balanceador de carga, consulte [configurar um balanceador de carga para a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Configurar recursos de infraestrutura de serviço

A aplicação de Service Fabric **ServiceManifest.xml** ficheiro de configuração define os pontos finais de Olá toouse espera que a aplicação. Depois do ficheiro de configuração de Olá tiver sido atualizado toodefine um ponto final, o Balanceador de carga Olá tem de ser atualizado tooexpose esse (ou uma diferentes) porta. Para obter mais informações sobre como toocreate Olá ponto final de recursos de infraestrutura de serviço, consulte [configurar um ponto final](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Criar uma regra de Balanceador de carga

Uma regra de Balanceador de carga abre uma porta de acesso à internet e reencaminha a porta de tráfego toohello interno do nó utilizada pela sua aplicação. Se não tiver um balanceador de carga, consulte [configurar um balanceador de carga para a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

regra de toocreate um balanceador de carga, terá de Olá toocollect seguintes informações:

- Nome do Balanceador de carga.
- Grupo de recursos Olá carregar balanceador e cluster do service fabric.
- Porta externa.
- Porta interna.

## <a name="azure-cli"></a>CLI do Azure
>[!NOTE]
>Se precisar de nome de Olá toodetermine Olá de Balanceador de carga, utilize uma lista de todos os balanceadores de carga e grupos de recursos de Olá associado get de tooquickly este comando.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Demora apenas um único comando toocreate uma regra de Balanceador de carga com Olá **CLI do Azure**. Basta tooknow tanto nome Olá de Olá carga balanceador e recursos grupo toocreate uma nova regra.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Olá comando da CLI do Azure tem alguns parâmetros que são descritos nas Olá a tabela seguinte:

| Parâmetro | Descrição |
| --------- | ----------- |
| `--backend-port`  | aplicação de recursos de infraestrutura de serviço do Olá porta Olá está a escutar. |
| `--frontend-port` | Olá de porta de Olá carregar balanceador expõe para ligações externas. |
| `-lb-name` | nome Olá Olá toochange de Balanceador de carga. |
| `-g`       | grupo de recursos de Olá que tenha o Balanceador de carga Olá e cluster do service fabric. |
| `-n`       | Olá escolhido o nome da regra de Olá. |


>[!NOTE]
>Para mais informações sobre como toocreate um balanceador de carga com Olá CLI do Azure, consulte o artigo [criar um balanceador de carga com Olá CLI do Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Se precisar de nome de Olá toodetermine Olá de Balanceador de carga, utilize get de tooquickly este comando uma lista de todos os balanceadores de carga e grupos de recursos associados.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell é um pouco mais complicada que Olá CLI do Azure. Concecionais, fazê-lo Olá toocreate passos a seguir uma regra.

1. Obter o Balanceador de carga Olá a partir do Azure.
2. Crie uma regra.
3. Adicione regra de Olá toohello Balanceador de carga.
4. Atualize o Balanceador de carga Olá.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Sobre Olá `New-AzureRmLoadBalancerRuleConfig` comando, hello `-FrontendPort` Balanceador de carga do representa Olá porta Olá expõe para ligações externas e Olá `-BackendPort` representa Olá porta Olá recursos de infraestrutura do app service está a escutar.

>[!NOTE]
>Para mais informações sobre como toocreate um balanceador de carga com o PowerShell, consulte o artigo [criar um balanceador de carga com o PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

