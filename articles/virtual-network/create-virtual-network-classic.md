---
title: "aaaCreate uma rede virtual do Azure (clássica) com várias sub-redes | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual (clássica) com várias sub-redes no Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="d89d3-103">Criar uma rede virtual (clássica) com várias sub-redes</span><span class="sxs-lookup"><span data-stu-id="d89d3-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d89d3-104">O Azure tem dois [modelos de implementação diferentes](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para criar e trabalhar com recursos: Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="d89d3-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="d89d3-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d89d3-106">A Microsoft recomenda a criação de maioria das redes virtuais novo através do Olá [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) modelo de implementação.</span><span class="sxs-lookup"><span data-stu-id="d89d3-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="d89d3-107">Neste tutorial, saiba como toocreate um básico do Azure (virtual network clássica) que tenha separar sub-redes públicas e privadas.</span><span class="sxs-lookup"><span data-stu-id="d89d3-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="d89d3-108">Pode criar recursos do Azure, como máquinas virtuais e serviços em nuvem numa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d89d3-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="d89d3-109">Recursos criados no redes virtuais (clássicas) podem comunicar entre si e com os recursos na outra rede virtual do redes tooa ligado.</span><span class="sxs-lookup"><span data-stu-id="d89d3-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="d89d3-110">Saiba mais sobre todos os [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md) definições.</span><span class="sxs-lookup"><span data-stu-id="d89d3-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="d89d3-111">Redes virtuais (clássicas) são imediatamente eliminados pelo Azure quando um [a subscrição está desativada](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="d89d3-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="d89d3-112">Redes virtuais (clássica) são eliminados independentemente se recursos existem na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="d89d3-113">Se mais tarde voltar a ativar a subscrição de Olá, os recursos que existiam na rede virtual Olá devem ser recriados.</span><span class="sxs-lookup"><span data-stu-id="d89d3-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="d89d3-114">Pode criar uma rede virtual (clássica) utilizando Olá [portal do Azure](#portal), Olá [interface de linha de comandos do Azure (CLI) 1.0](#azure-cli), ou [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="d89d3-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="d89d3-115">Portal</span><span class="sxs-lookup"><span data-stu-id="d89d3-115">Portal</span></span>

1. <span data-ttu-id="d89d3-116">Num browser da Internet, aceda toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d89d3-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d89d3-117">Inicie sessão com a sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="d89d3-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="d89d3-118">Se não tiver uma conta do Azure, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="d89d3-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="d89d3-119">Clique em **+ novo** no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="d89d3-120">Introduza *rede Virtual* no Olá **Olá pesquisa Marketplace** caixa, Olá parte superior do Olá **novo** painel que aparece.</span><span class="sxs-lookup"><span data-stu-id="d89d3-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="d89d3-121">Clique em **rede Virtual** quando for apresentada nos resultados de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="d89d3-122">Selecione **clássico** no Olá **selecionar um modelo de implementação** caixa Olá **rede Virtual** painel apresentado, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="d89d3-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="d89d3-123">Introduza Olá os seguintes valores no Olá **criar rede virtual (clássica)** painel e clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="d89d3-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="d89d3-124">Definição</span><span class="sxs-lookup"><span data-stu-id="d89d3-124">Setting</span></span>|<span data-ttu-id="d89d3-125">Valor</span><span class="sxs-lookup"><span data-stu-id="d89d3-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="d89d3-126">Nome</span><span class="sxs-lookup"><span data-stu-id="d89d3-126">Name</span></span>|<span data-ttu-id="d89d3-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="d89d3-127">myVnet</span></span>|
    |<span data-ttu-id="d89d3-128">Espaço de endereços</span><span class="sxs-lookup"><span data-stu-id="d89d3-128">Address space</span></span>|<span data-ttu-id="d89d3-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d89d3-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="d89d3-130">Nome da sub-rede</span><span class="sxs-lookup"><span data-stu-id="d89d3-130">Subnet name</span></span>|<span data-ttu-id="d89d3-131">Público</span><span class="sxs-lookup"><span data-stu-id="d89d3-131">Public</span></span>|
    |<span data-ttu-id="d89d3-132">Intervalo de endereços da sub-rede</span><span class="sxs-lookup"><span data-stu-id="d89d3-132">Subnet address range</span></span>|<span data-ttu-id="d89d3-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d89d3-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="d89d3-134">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d89d3-134">Resource group</span></span>|<span data-ttu-id="d89d3-135">Deixe **criar nova** selecionada e, em seguida, introduza **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="d89d3-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="d89d3-136">Subscrição e localização</span><span class="sxs-lookup"><span data-stu-id="d89d3-136">Subscription and location</span></span>|<span data-ttu-id="d89d3-137">Selecione a sua subscrição e localização.</span><span class="sxs-lookup"><span data-stu-id="d89d3-137">Select your subscription and location.</span></span>

    <span data-ttu-id="d89d3-138">Se tiver tooAzure novo, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscrições](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [localizações](https://azure.microsoft.com/regions) (também referida tooas *regiões*).</span><span class="sxs-lookup"><span data-stu-id="d89d3-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="d89d3-139">No portal de Olá, pode criar apenas uma sub-rede quando criar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d89d3-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="d89d3-140">Neste tutorial, crie uma sub-rede do segundo depois de criar rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="d89d3-141">Mais tarde poderá criar recursos acessível através da Internet no Olá **pública** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d89d3-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="d89d3-142">Também poderá criar recursos que não estão acessíveis a partir do Olá Internet no Olá **privada** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d89d3-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="d89d3-143">toocreate Olá segunda sub-rede, introduza **myVnet** no Olá **procurar recursos** caixa na Olá parte superior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="d89d3-144">Clique em **myVnet** quando for apresentada nos resultados de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="d89d3-145">Clique em **sub-redes** (no Olá **definições** secção) no Olá **criar rede virtual (clássica)** painel que aparece.</span><span class="sxs-lookup"><span data-stu-id="d89d3-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="d89d3-146">Clique em **+ adicionar** no Olá **myVnet - sub-redes** painel que aparece.</span><span class="sxs-lookup"><span data-stu-id="d89d3-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="d89d3-147">Introduza **privada** para **nome** no Olá **adicionar sub-rede** painel.</span><span class="sxs-lookup"><span data-stu-id="d89d3-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="d89d3-148">Introduza **10.0.1.0/24** para **intervalo de endereços**.</span><span class="sxs-lookup"><span data-stu-id="d89d3-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="d89d3-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d89d3-149">Click **OK**.</span></span>
8. <span data-ttu-id="d89d3-150">No Olá **myVnet - sub-redes** painel, pode ver Olá **pública** e **privada** sub-redes que criou.</span><span class="sxs-lookup"><span data-stu-id="d89d3-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="d89d3-151">**Opcional**: Quando concluir este tutorial, é aconselhável recursos de Olá toodelete que criou, para que não implicar custos de utilização:</span><span class="sxs-lookup"><span data-stu-id="d89d3-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="d89d3-152">Clique em **descrição geral** no Olá **myVnet** painel.</span><span class="sxs-lookup"><span data-stu-id="d89d3-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="d89d3-153">Clique em Olá **eliminar** ícone na Olá **myVnet** painel.</span><span class="sxs-lookup"><span data-stu-id="d89d3-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="d89d3-154">eliminação de Olá tooconfirm, clique em **Sim** no Olá **Delete de rede virtual** caixa.</span><span class="sxs-lookup"><span data-stu-id="d89d3-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="d89d3-155">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d89d3-155">Azure CLI</span></span>

1. <span data-ttu-id="d89d3-156">Pode [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ou utilize Olá CLI dentro Olá Shell de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d89d3-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="d89d3-157">Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d89d3-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="d89d3-158">Tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta.</span><span class="sxs-lookup"><span data-stu-id="d89d3-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="d89d3-159">tooget ajuda para comandos da CLI, escreva `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="d89d3-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="d89d3-160">Numa sessão CLI, inicie sessão no tooAzure com o comando de Olá que se segue.</span><span class="sxs-lookup"><span data-stu-id="d89d3-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="d89d3-161">Se clicar em **experimente** na caixa de Olá abaixo, uma Shell de nuvem abre.</span><span class="sxs-lookup"><span data-stu-id="d89d3-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="d89d3-162">Pode iniciar sessão tooyour subscrição do Azure, sem introduzir Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d89d3-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="d89d3-163">Olá tooensure CLI está no modo de gestão de serviço, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d89d3-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="d89d3-164">Crie uma rede virtual com uma sub-rede privada:</span><span class="sxs-lookup"><span data-stu-id="d89d3-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="d89d3-165">Crie uma sub-rede pública dentro da rede virtual Olá:</span><span class="sxs-lookup"><span data-stu-id="d89d3-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="d89d3-166">Reveja a rede virtual Olá e sub-redes:</span><span class="sxs-lookup"><span data-stu-id="d89d3-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="d89d3-167">**Opcional**: É aconselhável a recursos de Olá toodelete que criou quando concluir este tutorial, pelo que não implicar custos de utilização:</span><span class="sxs-lookup"><span data-stu-id="d89d3-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="d89d3-168">Apesar de não é possível especificar um toocreate do grupo de recursos uma rede virtual (clássica) utilizando a CLI de Olá, Azure cria a rede virtual Olá num grupo de recursos com o nome *predefinido redes*.</span><span class="sxs-lookup"><span data-stu-id="d89d3-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="d89d3-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d89d3-169">PowerShell</span></span>

1. <span data-ttu-id="d89d3-170">Instale a versão mais recente do Olá do Olá PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) módulo.</span><span class="sxs-lookup"><span data-stu-id="d89d3-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="d89d3-171">Se estiver tooAzure nova do PowerShell, consulte [descrição geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d89d3-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="d89d3-172">Inicie uma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d89d3-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="d89d3-173">No PowerShell, inicie sessão no tooAzure introduzindo Olá `Add-AzureAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="d89d3-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="d89d3-174">Alterar seguinte Olá caminho e nome de ficheiro, conforme adequado, em seguida, Exportar ficheiro de configuração de rede existente:</span><span class="sxs-lookup"><span data-stu-id="d89d3-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="d89d3-175">toocreate uma rede virtual com a sub-redes públicas e privadas, utilize qualquer Olá de tooadd do editor de texto **VirtualNetworkSite** elemento que se segue toohello ficheiro de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="d89d3-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="d89d3-176">Olá revisão completa [esquema do ficheiro de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="d89d3-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="d89d3-177">Importe o ficheiro de configuração de rede Olá:</span><span class="sxs-lookup"><span data-stu-id="d89d3-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="d89d3-178">Importar um ficheiro de configuração foi alterada de rede pode fazer com que as alterações tooexisting redes virtuais (clássica) na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="d89d3-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="d89d3-179">Certifique-se apenas a adicionar rede virtual anterior de Olá e que não alterar ou remover quaisquer redes virtuais existentes da sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="d89d3-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="d89d3-180">Reveja a rede virtual Olá e sub-redes:</span><span class="sxs-lookup"><span data-stu-id="d89d3-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="d89d3-181">**Opcional**: É aconselhável a recursos de Olá toodelete que criou quando concluir este tutorial, pelo que não implicar custos de utilização.</span><span class="sxs-lookup"><span data-stu-id="d89d3-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="d89d3-182">toodelete Olá rede virtual, concluir os passos 4 a 6 novamente, Olá de remover este tempo **VirtualNetworkSite** elemento adicionado no passo 5.</span><span class="sxs-lookup"><span data-stu-id="d89d3-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="d89d3-183">Apesar de não é possível especificar um toocreate do grupo de recursos uma rede virtual (clássica) utilizando o PowerShell, o Azure cria rede virtual Olá num grupo de recursos com o nome *predefinido redes*.</span><span class="sxs-lookup"><span data-stu-id="d89d3-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="d89d3-184">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d89d3-184">Next steps</span></span>

- <span data-ttu-id="d89d3-185">Consulte toolearn sobre todas as definições da sub-rede e a rede virtual [gerir redes virtuais](virtual-network-manage-network.md) e [gerir sub-redes da rede virtual](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="d89d3-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="d89d3-186">Tem várias opções para utilizar redes virtuais e sub-redes um requisitos diferentes do ambiente toomeet de produção.</span><span class="sxs-lookup"><span data-stu-id="d89d3-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="d89d3-187">toofilter entrada e saída tráfego de sub-rede, criar e aplicar [grupos de segurança de rede](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="d89d3-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="d89d3-188">Criar um [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou um [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual e, em seguida, ligue-o tooan de rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d89d3-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="d89d3-189">redes virtuais tooconnect dois na mesma localização do Azure de Olá, crie um [peering de rede virtual](create-peering-different-deployment-models.md) entre redes virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="d89d3-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="d89d3-190">Pode elemento uma rede virtual (Resource Manager) tooa (virtual network clássica), mas não é possível criar um peering entre duas redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="d89d3-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="d89d3-191">Ligar a rede no local do Olá rede virtual tooan utilizando um [Gateway de VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.</span><span class="sxs-lookup"><span data-stu-id="d89d3-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
