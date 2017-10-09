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
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="75969-103">Abra portas para um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="75969-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="75969-104">Balanceador de carga Olá implementado com o cluster do Azure Service Fabric direciona o tráfego tooyour aplicação em execução num nó.</span><span class="sxs-lookup"><span data-stu-id="75969-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="75969-105">Se alterar o toouse aplicação uma porta diferente, tem de expor essa porta (ou uma porta diferente de rotas) no Olá Balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="75969-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="75969-106">Quando tiver implementado o tooAzure de cluster de recursos de infraestrutura de serviço, um balanceador de carga foi criado automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="75969-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="75969-107">Se não tiver um balanceador de carga, consulte [configurar um balanceador de carga para a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="75969-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="75969-108">Configurar recursos de infraestrutura de serviço</span><span class="sxs-lookup"><span data-stu-id="75969-108">Configure service fabric</span></span>

<span data-ttu-id="75969-109">A aplicação de Service Fabric **ServiceManifest.xml** ficheiro de configuração define os pontos finais de Olá toouse espera que a aplicação.</span><span class="sxs-lookup"><span data-stu-id="75969-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="75969-110">Depois do ficheiro de configuração de Olá tiver sido atualizado toodefine um ponto final, o Balanceador de carga Olá tem de ser atualizado tooexpose esse (ou uma diferentes) porta.</span><span class="sxs-lookup"><span data-stu-id="75969-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="75969-111">Para obter mais informações sobre como toocreate Olá ponto final de recursos de infraestrutura de serviço, consulte [configurar um ponto final](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="75969-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="75969-112">Criar uma regra de Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="75969-112">Create a load balancer rule</span></span>

<span data-ttu-id="75969-113">Uma regra de Balanceador de carga abre uma porta de acesso à internet e reencaminha a porta de tráfego toohello interno do nó utilizada pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="75969-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="75969-114">Se não tiver um balanceador de carga, consulte [configurar um balanceador de carga para a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="75969-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="75969-115">regra de toocreate um balanceador de carga, terá de Olá toocollect seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="75969-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="75969-116">Nome do Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="75969-116">Load balancer name.</span></span>
- <span data-ttu-id="75969-117">Grupo de recursos Olá carregar balanceador e cluster do service fabric.</span><span class="sxs-lookup"><span data-stu-id="75969-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="75969-118">Porta externa.</span><span class="sxs-lookup"><span data-stu-id="75969-118">External port.</span></span>
- <span data-ttu-id="75969-119">Porta interna.</span><span class="sxs-lookup"><span data-stu-id="75969-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="75969-120">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="75969-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="75969-121">Se precisar de nome de Olá toodetermine Olá de Balanceador de carga, utilize uma lista de todos os balanceadores de carga e grupos de recursos de Olá associado get de tooquickly este comando.</span><span class="sxs-lookup"><span data-stu-id="75969-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="75969-122">Demora apenas um único comando toocreate uma regra de Balanceador de carga com Olá **CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="75969-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="75969-123">Basta tooknow tanto nome Olá de Olá carga balanceador e recursos grupo toocreate uma nova regra.</span><span class="sxs-lookup"><span data-stu-id="75969-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="75969-124">Olá comando da CLI do Azure tem alguns parâmetros que são descritos nas Olá a tabela seguinte:</span><span class="sxs-lookup"><span data-stu-id="75969-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="75969-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="75969-125">Parameter</span></span> | <span data-ttu-id="75969-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="75969-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="75969-127">aplicação de recursos de infraestrutura de serviço do Olá porta Olá está a escutar.</span><span class="sxs-lookup"><span data-stu-id="75969-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="75969-128">Olá de porta de Olá carregar balanceador expõe para ligações externas.</span><span class="sxs-lookup"><span data-stu-id="75969-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="75969-129">nome Olá Olá toochange de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="75969-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="75969-130">grupo de recursos de Olá que tenha o Balanceador de carga Olá e cluster do service fabric.</span><span class="sxs-lookup"><span data-stu-id="75969-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="75969-131">Olá escolhido o nome da regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="75969-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="75969-132">Para mais informações sobre como toocreate um balanceador de carga com Olá CLI do Azure, consulte o artigo [criar um balanceador de carga com Olá CLI do Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="75969-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="75969-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="75969-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="75969-134">Se precisar de nome de Olá toodetermine Olá de Balanceador de carga, utilize get de tooquickly este comando uma lista de todos os balanceadores de carga e grupos de recursos associados.</span><span class="sxs-lookup"><span data-stu-id="75969-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="75969-135">PowerShell é um pouco mais complicada que Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="75969-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="75969-136">Concecionais, fazê-lo Olá toocreate passos a seguir uma regra.</span><span class="sxs-lookup"><span data-stu-id="75969-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="75969-137">Obter o Balanceador de carga Olá a partir do Azure.</span><span class="sxs-lookup"><span data-stu-id="75969-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="75969-138">Crie uma regra.</span><span class="sxs-lookup"><span data-stu-id="75969-138">Create a rule.</span></span>
3. <span data-ttu-id="75969-139">Adicione regra de Olá toohello Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="75969-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="75969-140">Atualize o Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="75969-140">Update hello load balancer.</span></span>

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

<span data-ttu-id="75969-141">Sobre Olá `New-AzureRmLoadBalancerRuleConfig` comando, hello `-FrontendPort` Balanceador de carga do representa Olá porta Olá expõe para ligações externas e Olá `-BackendPort` representa Olá porta Olá recursos de infraestrutura do app service está a escutar.</span><span class="sxs-lookup"><span data-stu-id="75969-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="75969-142">Para mais informações sobre como toocreate um balanceador de carga com o PowerShell, consulte o artigo [criar um balanceador de carga com o PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="75969-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

