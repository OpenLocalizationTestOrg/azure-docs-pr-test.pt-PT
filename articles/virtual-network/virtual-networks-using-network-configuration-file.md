---
title: "aaaConfigure uma rede Virtual do Azure (clássica) - ficheiro de configuração de rede | Microsoft Docs"
description: "Saiba como toocreate e modificar redes virtuais (clássicas) através da exportação, alterar e importar um ficheiro de configuração de rede."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="12715-103">Configurar uma rede virtual (clássica) utilizando um ficheiro de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="12715-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="12715-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12715-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="12715-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="12715-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="12715-106">A Microsoft recomenda que implementações mais novas utilizem o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="12715-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="12715-107">Pode criar e configurar uma rede virtual (clássica) com um ficheiro de configuração de rede através de Olá interface de linha de comandos do Azure (CLI) 1.0 ou do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12715-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="12715-108">Não é possível criar ou modificar uma rede virtual através do modelo de implementação Azure Resource Manager Olá utilizando um ficheiro de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="12715-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="12715-109">Não é possível utilizar Olá toocreate portal do Azure ou modificar uma rede virtual (clássica) utilizando um ficheiro de configuração de rede, no entanto, pode utilizar Olá toocreate do portal do Azure, uma rede virtual (clássica), sem utilizar um ficheiro de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="12715-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="12715-110">Criar e configurar uma rede virtual (clássica) com um ficheiro de configuração de rede necessitam de exportação, alterar e importar o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="12715-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="12715-111"><a name="export"></a>Exportar um ficheiro de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="12715-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="12715-112">Pode utilizar o PowerShell ou Olá CLI do Azure tooexport um ficheiro de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="12715-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="12715-113">PowerShell exporta um ficheiro XML, enquanto Olá CLI do Azure exporta um ficheiro json.</span><span class="sxs-lookup"><span data-stu-id="12715-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="12715-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12715-114">PowerShell</span></span>
 
1. <span data-ttu-id="12715-115">[Instalar o Azure PowerShell e inicie sessão tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12715-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="12715-116">Altere o diretório de Olá (e certifique-se de que existe) e o nome do ficheiro no Olá os seguintes comandos como pretendido, em seguida, execute Olá comando tooexport Olá rede ficheiro de configuração:</span><span class="sxs-lookup"><span data-stu-id="12715-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="12715-117">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="12715-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="12715-118">[Instalar Olá CLI do Azure 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12715-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="12715-119">Concluir Olá restantes passos de uma linha de comandos da CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="12715-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="12715-120">Inicie sessão no tooAzure introduzindo Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="12715-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="12715-121">Certifique-se de que está no modo asm introduzindo Olá `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="12715-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="12715-122">Altere o diretório de Olá (e certifique-se de que existe) e o nome do ficheiro no Olá os seguintes comandos como pretendido, em seguida, execute Olá comando tooexport Olá rede ficheiro de configuração:</span><span class="sxs-lookup"><span data-stu-id="12715-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="12715-123">Criar ou modificar um ficheiro de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="12715-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="12715-124">Um ficheiro de configuração de rede é um ficheiro XML (ao utilizar o PowerShell) ou um ficheiro json (ao utilizar Olá CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="12715-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="12715-125">Pode editar o ficheiro de Olá em qualquer texto ou editor de XML/json.</span><span class="sxs-lookup"><span data-stu-id="12715-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="12715-126">Olá [definições de esquema do ficheiro de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx) artigo inclui os detalhes de todas as definições.</span><span class="sxs-lookup"><span data-stu-id="12715-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="12715-127">Para obter explicações adicionais das definições de Olá, consulte [ver redes virtuais e definições](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="12715-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="12715-128">alterações de Olá efetuar toohello ficheiro:</span><span class="sxs-lookup"><span data-stu-id="12715-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="12715-129">Deve estar em conformidade com o esquema de Olá de importação de Olá de rede, ou o ficheiro de configuração falhará.</span><span class="sxs-lookup"><span data-stu-id="12715-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="12715-130">Substituir as definições de rede existente para a sua subscrição, por isso, tenha muito cuidado quando efetuar alterações.</span><span class="sxs-lookup"><span data-stu-id="12715-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="12715-131">Por exemplo, referencie Olá exemplo rede ficheiros de configuração que se seguem.</span><span class="sxs-lookup"><span data-stu-id="12715-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="12715-132">Indicar o ficheiro original Olá contidos dois **VirtualNetworkSite** instâncias e foi alterado, conforme ilustrado nos exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="12715-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="12715-133">Quando importar o ficheiro de Olá, Azure elimina a rede virtual do Olá para Olá **VirtualNetworkSite** instância removido no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="12715-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="12715-134">Este cenário simplificado assume que não existem recursos foram na rede virtual Olá, como se existirem, não foi possível eliminar a rede virtual Olá e importar Olá irão falhar.</span><span class="sxs-lookup"><span data-stu-id="12715-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12715-135">Azure considera uma sub-rede que tenha algo implementado tooit como **em utilização**.</span><span class="sxs-lookup"><span data-stu-id="12715-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="12715-136">Quando uma sub-rede em utilização, não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="12715-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="12715-137">Antes de modificar as informações de sub-rede num ficheiro de configuração de rede, mova tudo o que implementou toohello sub-rede tooa outra sub-rede que não está a ser modificado.</span><span class="sxs-lookup"><span data-stu-id="12715-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="12715-138">Consulte [mover um tooa outra sub-rede VM ou instância de função](virtual-networks-move-vm-role-to-subnet.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="12715-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="12715-139">Exemplo XML para utilização com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="12715-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="12715-140">Olá ficheiro de configuração de rede de exemplo seguinte cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereços de *10.0.0.0/16* no Olá *EUA Leste* Azure região.</span><span class="sxs-lookup"><span data-stu-id="12715-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="12715-141">rede virtual Olá contém uma sub-rede designada *mySubnet* com um prefixo de endereço de *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="12715-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="12715-142">Se o ficheiro de configuração de rede de Olá exportou não contém nenhum conteúdo, pode copiar Olá XML no exemplo anterior Olá e cole-o um novo ficheiro.</span><span class="sxs-lookup"><span data-stu-id="12715-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="12715-143">JSON de exemplo para utilização com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="12715-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="12715-144">Olá ficheiro de configuração de rede de exemplo seguinte cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereços de *10.0.0.0/16* no Olá *EUA Leste* Azure região.</span><span class="sxs-lookup"><span data-stu-id="12715-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="12715-145">rede virtual Olá contém uma sub-rede designada *mySubnet* com um prefixo de endereço de *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="12715-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="12715-146">Se o ficheiro de configuração de rede de Olá exportou não contém nenhum conteúdo, pode copiar o json de Olá no exemplo anterior Olá e cole-o um novo ficheiro.</span><span class="sxs-lookup"><span data-stu-id="12715-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="12715-147"><a name="import"></a>Importar um ficheiro de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="12715-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="12715-148">Pode utilizar o PowerShell ou Olá CLI do Azure tooimport um ficheiro de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="12715-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="12715-149">PowerShell importa um ficheiro XML, enquanto Olá CLI do Azure importa um ficheiro json.</span><span class="sxs-lookup"><span data-stu-id="12715-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="12715-150">Se falhar a importação de Olá, confirme que o ficheiro Olá está em conformidade com Olá [esquema de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="12715-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="12715-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12715-151">PowerShell</span></span>
 
1. <span data-ttu-id="12715-152">[Instalar o Azure PowerShell e inicie sessão tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12715-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="12715-153">Alterar o diretório de Olá e nome do ficheiro no Olá os seguintes comandos conforme necessário, em seguida, execute o ficheiro de configuração de rede tooimport Olá Olá comando:</span><span class="sxs-lookup"><span data-stu-id="12715-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="12715-154">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="12715-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="12715-155">[Instalar Olá CLI do Azure 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12715-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="12715-156">Concluir Olá restantes passos de uma linha de comandos da CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="12715-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="12715-157">Inicie sessão no tooAzure introduzindo Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="12715-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="12715-158">Certifique-se de que está no modo asm introduzindo Olá `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="12715-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="12715-159">Alterar o diretório de Olá e nome do ficheiro no Olá os seguintes comandos conforme necessário, em seguida, execute o ficheiro de configuração de rede tooimport Olá Olá comando:</span><span class="sxs-lookup"><span data-stu-id="12715-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
