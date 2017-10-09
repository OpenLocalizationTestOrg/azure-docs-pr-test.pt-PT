---
title: 'Como tooconfigure encaminhamento para um circuito ExpressRoute do Azure: CLI | Microsoft Docs'
description: "Este artigo ajuda-o a criar e aprovisionar Olá privado, público e peering da Microsoft de um circuito ExpressRoute. Este artigo mostra também como estado de Olá toocheck, atualizar ou eliminar peerings no seu circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="47a18-104">Criar e modificar o encaminhamento para um circuito ExpressRoute com a CLI</span><span class="sxs-lookup"><span data-stu-id="47a18-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="47a18-105">Este artigo ajuda-o a criar e gerir a configuração de encaminhamento para um circuito de ExpressRoute no modelo de implementação Resource Manager Olá com a CLI.</span><span class="sxs-lookup"><span data-stu-id="47a18-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="47a18-106">Também pode verificar o estado de Olá, atualizar ou eliminar e retirar o aprovisionamento do peerings para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="47a18-107">Se quiser toouse toowork um método diferente com o seu circuito, selecione um artigo de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="47a18-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47a18-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="47a18-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47a18-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="47a18-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="47a18-111">Vídeo - privada peering</span><span class="sxs-lookup"><span data-stu-id="47a18-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="47a18-112">Vídeo - peering público</span><span class="sxs-lookup"><span data-stu-id="47a18-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="47a18-113">Vídeo - peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="47a18-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="47a18-114">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="47a18-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="47a18-115">Pré-requisitos da configuração</span><span class="sxs-lookup"><span data-stu-id="47a18-115">Configuration prerequisites</span></span>

* <span data-ttu-id="47a18-116">Antes de começar, instale a versão mais recente do Olá dos comandos da CLI Olá (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="47a18-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="47a18-117">Para obter informações sobre a instalação de comandos da CLI Olá, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="47a18-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="47a18-118">Certifique-se de que reviu Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de encaminhamento](expressroute-routing.md), e [fluxo de trabalho](expressroute-workflows.md) páginas antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="47a18-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="47a18-119">Deve ter um circuito ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="47a18-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="47a18-120">Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](howto-circuit-cli.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="47a18-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="47a18-121">Olá circuito ExpressRoute tem de ser num Estado aprovisionado e ativado para que os comandos de Olá toorun capaz de toobe neste artigo.</span><span class="sxs-lookup"><span data-stu-id="47a18-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="47a18-122">Estas instruções aplicam-se apenas toocircuits criados com fornecedores de serviços de oferta de serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="47a18-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="47a18-123">Se estiver a utilizar um fornecedor de serviço que oferece gerido Layer 3 serviços (normalmente, uma VPN de IP, como MPLS), o seu fornecedor de conectividade irá configurar e gerir encaminhamento por si.</span><span class="sxs-lookup"><span data-stu-id="47a18-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="47a18-124">Pode configurar um, dois ou todos os três peerings (Azure privado, Azure público e Microsoft) para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="47a18-125">Pode configurar peerings em qualquer ordem que escolha.</span><span class="sxs-lookup"><span data-stu-id="47a18-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="47a18-126">No entanto, tem de se certificar de que concluir configuração Olá cada peering, um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="47a18-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="47a18-127">Peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-127">Azure private peering</span></span>

<span data-ttu-id="47a18-128">Esta secção ajuda-o a criar, obter, atualizar e eliminar Olá configuração do peering privado do Azure para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="47a18-129">toocreate peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="47a18-130">Instale a versão mais recente do Olá da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="47a18-131">Tem de utilizar Olá a versão mais recente do Olá Interface de linha de comandos do Azure (CLI). * Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="47a18-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="47a18-132">Selecione a subscrição de Olá pretende que o circuito de ExpressRoute toocreate</span><span class="sxs-lookup"><span data-stu-id="47a18-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="47a18-133">Crie um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="47a18-134">Siga Olá instruções toocreate um [circuito ExpressRoute](howto-circuit-cli.md) e solicite ao fornecedor de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="47a18-135">Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="47a18-136">Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="47a18-137">No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, continue a configuração utilizando os passos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="47a18-138">Verifique toomake de circuito de ExpressRoute Olá se de que está aprovisionado e também ativado.</span><span class="sxs-lookup"><span data-stu-id="47a18-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="47a18-139">Utilize o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="47a18-140">resposta Olá é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a18-140">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="47a18-141">Configure o peering privado do Azure para o circuito Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="47a18-142">Certifique-se de que tem Olá seguintes itens antes de continuar com os passos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="47a18-143">Um /30 sub-rede para a ligação primária Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="47a18-144">a sub-rede de Olá não pode ser parte de qualquer espaço de endereços reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="47a18-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="47a18-145">Um /30 sub-rede para a ligação secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="47a18-146">a sub-rede de Olá não pode ser parte de qualquer espaço de endereços reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="47a18-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="47a18-147">Um tooestablish de ID de VLAN válido este peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="47a18-148">Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="47a18-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="47a18-149">Número AS para peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-149">AS number for peering.</span></span> <span data-ttu-id="47a18-150">Pode utilizar números AS de 2 e 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="47a18-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="47a18-151">Pode utilizar um número AS privado para este peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="47a18-152">Assegure que não está a utilizar 65515.</span><span class="sxs-lookup"><span data-stu-id="47a18-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="47a18-153">**Opcional -** um hash MD5 se optar por toouse um.</span><span class="sxs-lookup"><span data-stu-id="47a18-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="47a18-154">Utilize Olá seguir tooconfigure de exemplo para o seu circuito de peering privado do Azure:</span><span class="sxs-lookup"><span data-stu-id="47a18-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="47a18-155">Se optar por toouse um hash MD5, utilize o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="47a18-156">Assegure que especifica o seu número AS como ASN de peering, não cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="47a18-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="47a18-157">tooview detalhes de peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-157">tooview Azure private peering details</span></span>

<span data-ttu-id="47a18-158">Pode obter os detalhes de configuração utilizando o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="47a18-159">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a18-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="47a18-160">tooupdate configuração do peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="47a18-161">Pode atualizar qualquer parte da configuração de Olá utilizando o seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="47a18-162">Neste exemplo, Olá ID de VLAN do circuito Olá está a ser atualizado de 100 too500.</span><span class="sxs-lookup"><span data-stu-id="47a18-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="47a18-163">toodelete peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-163">toodelete Azure private peering</span></span>

<span data-ttu-id="47a18-164">Pode remover a sua configuração de peering executando o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="47a18-165">Tem de se certificar de que todas as redes virtuais são desassociadas do Olá circuito ExpressRoute antes de executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="47a18-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="47a18-166">Peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-166">Azure public peering</span></span>

<span data-ttu-id="47a18-167">Esta secção ajuda-o a criar, obter, atualizar e eliminar Olá configuração do peering público do Azure para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="47a18-168">toocreate peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="47a18-169">Instale a versão mais recente do Olá da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="47a18-170">Tem de utilizar Olá a versão mais recente do Olá Interface de linha de comandos do Azure (CLI). * Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="47a18-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="47a18-171">Selecione a subscrição de Olá para o qual pretende que o circuito de ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="47a18-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="47a18-172">Crie um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="47a18-173">Siga Olá instruções toocreate um [circuito ExpressRoute](howto-circuit-cli.md) e solicite ao fornecedor de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="47a18-174">Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir que o seu fornecedor de conectividade permite peering privado do Azure por si.</span><span class="sxs-lookup"><span data-stu-id="47a18-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="47a18-175">Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="47a18-176">No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, continue a configuração utilizando os passos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="47a18-177">Verifique Olá tooensure de circuito de ExpressRoute está aprovisionado e também ativado.</span><span class="sxs-lookup"><span data-stu-id="47a18-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="47a18-178">Utilize o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="47a18-179">resposta Olá é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a18-179">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="47a18-180">Configure o peering público do Azure para o circuito Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="47a18-181">Certifique-se de que tem Olá seguintes informações antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="47a18-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="47a18-182">Um /30 sub-rede para a ligação primária Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="47a18-183">Esta tem de ser um prefixo IPv4 válido.</span><span class="sxs-lookup"><span data-stu-id="47a18-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="47a18-184">Um /30 sub-rede para a ligação secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="47a18-185">Esta tem de ser um prefixo IPv4 válido.</span><span class="sxs-lookup"><span data-stu-id="47a18-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="47a18-186">Um tooestablish de ID de VLAN válido este peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="47a18-187">Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="47a18-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="47a18-188">Número AS para peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-188">AS number for peering.</span></span> <span data-ttu-id="47a18-189">Pode utilizar números AS de 2 e 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="47a18-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="47a18-190">**Opcional -** um hash MD5 se optar por toouse um.</span><span class="sxs-lookup"><span data-stu-id="47a18-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="47a18-191">Execute Olá seguir tooconfigure de exemplo para o seu circuito de peering público do Azure:</span><span class="sxs-lookup"><span data-stu-id="47a18-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="47a18-192">Se optar por toouse um hash MD5, utilize o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="47a18-193">Assegure que especifica o seu número AS como ASN de peering, não cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="47a18-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="47a18-194">tooview detalhes de peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-194">tooview Azure public peering details</span></span>

<span data-ttu-id="47a18-195">Pode obter os detalhes de configuração com o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="47a18-196">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a18-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="47a18-197">tooupdate configuração do peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="47a18-198">Pode atualizar qualquer parte da configuração de Olá utilizando o seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="47a18-199">Neste exemplo, Olá ID de VLAN do circuito Olá está a ser atualizado de 200 too600.</span><span class="sxs-lookup"><span data-stu-id="47a18-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="47a18-200">toodelete peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-200">toodelete Azure public peering</span></span>

<span data-ttu-id="47a18-201">Pode remover a sua configuração de peering executando o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="47a18-202">Peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="47a18-202">Microsoft peering</span></span>

<span data-ttu-id="47a18-203">Esta secção ajuda-o a criar, obter, atualizar e eliminar Olá configuração peering da Microsoft para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47a18-204">Peering da Microsoft dos circuitos ExpressRoute que foram configuradas tooAugust anterior 1, 2017 terá todos os serviço prefixos anunciados através do peering da Microsoft hello, mesmo se os filtros de rota não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="47a18-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="47a18-205">Peering da Microsoft dos circuitos ExpressRoute que estão configurados em ou após 1 de Agosto de 2017 não terão qualquer prefixos anunciados até que está ligado um filtro de rota toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="47a18-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="47a18-206">Para obter mais informações, consulte [configurar um filtro de rota para peering da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47a18-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="47a18-207">toocreate peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="47a18-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="47a18-208">Instale a versão mais recente do Olá da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="47a18-209">Versão mais recente do Olá de utilização de Olá Interface de linha de comandos do Azure (CLI). * Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="47a18-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="47a18-210">Selecione a subscrição de Olá para o qual pretende que o circuito de ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="47a18-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="47a18-211">Crie um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="47a18-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="47a18-212">Siga Olá instruções toocreate um [circuito ExpressRoute](howto-circuit-cli.md) e solicite ao fornecedor de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="47a18-213">Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="47a18-214">Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="47a18-215">No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, continue a configuração utilizando os passos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="47a18-216">Verifique toomake de circuito de ExpressRoute Olá se de que está aprovisionado e também ativado.</span><span class="sxs-lookup"><span data-stu-id="47a18-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="47a18-217">Utilize o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="47a18-218">resposta Olá é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a18-218">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="47a18-219">Configure o peering da Microsoft para o circuito Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="47a18-220">Certifique-se de que tem Olá seguintes informações antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="47a18-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="47a18-221">Um /30 sub-rede para a ligação primária Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="47a18-222">Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.</span><span class="sxs-lookup"><span data-stu-id="47a18-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="47a18-223">Um /30 sub-rede para a ligação secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="47a18-224">Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.</span><span class="sxs-lookup"><span data-stu-id="47a18-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="47a18-225">Um tooestablish de ID de VLAN válido este peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="47a18-226">Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="47a18-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="47a18-227">Número AS para peering.</span><span class="sxs-lookup"><span data-stu-id="47a18-227">AS number for peering.</span></span> <span data-ttu-id="47a18-228">Pode utilizar números AS de 2 e 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="47a18-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="47a18-229">Prefixos anunciados: tem de fornecer uma lista de todos os prefixos planear tooadvertise através de sessão de BGP Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="47a18-230">São aceites apenas prefixos de endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="47a18-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="47a18-231">Se planear toosend um conjunto de prefixos, pode enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="47a18-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="47a18-232">Estes prefixos têm de ser registado tooyou num RIR / TIR.</span><span class="sxs-lookup"><span data-stu-id="47a18-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="47a18-233">**Opcional -** cliente ASN: Se estiver a anunciar prefixos que não são registado toohello número AS de peering, pode especificar Olá como número toowhich estão registados.</span><span class="sxs-lookup"><span data-stu-id="47a18-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="47a18-234">Nome do registo de encaminhamento: Pode especificar Olá RIR / IRR em relação a que Olá como número e prefixos são registados.</span><span class="sxs-lookup"><span data-stu-id="47a18-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="47a18-235">**Opcional -** um hash MD5 se optar por toouse um.</span><span class="sxs-lookup"><span data-stu-id="47a18-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="47a18-236">Execute o seguinte exemplo tooconfigure peering da Microsoft para o seu circuito de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="47a18-237">Detalhes do tooget Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="47a18-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="47a18-238">Pode obter os detalhes de configuração utilizando o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="47a18-239">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a18-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="47a18-240">configuração do peering da Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="47a18-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="47a18-241">Pode atualizar qualquer parte da configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="47a18-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="47a18-242">Olá anunciados prefixos do circuito Olá estão a ser atualizados de 123.1.0.0/24 too124.1.0.0/24 no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="47a18-243">toodelete peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="47a18-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="47a18-244">Pode remover a sua configuração de peering executando o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="47a18-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="47a18-245">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="47a18-245">Next steps</span></span>

<span data-ttu-id="47a18-246">Passo seguinte, [ligação tooan uma VNet circuito ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="47a18-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="47a18-247">Para obter mais informações sobre o fluxo de trabalho do ExpressRoute, veja [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="47a18-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="47a18-248">Para obter mais informações sobre peering do circuito, veja [Circuitos ExpressRoute e domínios de encaminhamento](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="47a18-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="47a18-249">Para obter mais informações sobre como trabalhar com redes virtuais, veja [Descrição geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47a18-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>