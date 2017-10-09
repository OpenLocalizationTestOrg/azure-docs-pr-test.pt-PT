---
title: "aaaCreate de rede de grupos de segurança - modelo do Azure Resource Manager | Microsoft Docs"
description: "Saiba como toocreate e implementar grupos de segurança de rede através de um modelo Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="d48a5-103">Criar rede grupos de segurança através de um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d48a5-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d48a5-104">Este artigo abrange o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="d48a5-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d48a5-105">Também pode [criar NSGs no modelo de implementação clássica Olá](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d48a5-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="d48a5-106">Recursos NSG num ficheiro de modelo</span><span class="sxs-lookup"><span data-stu-id="d48a5-106">NSG resources in a template file</span></span>
<span data-ttu-id="d48a5-107">Pode ver e transferir Olá [modelo de exemplo](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="d48a5-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="d48a5-108">Olá secção seguinte mostra a definição de Olá de Olá NSG front-end, com base no cenário de Olá.</span><span class="sxs-lookup"><span data-stu-id="d48a5-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="d48a5-109">tooassociate Olá NSG toohello front-end sub-rede, tem de definição de sub-rede Olá toochange no modelo de Olá e utilizar id de referência de Olá para Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="d48a5-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="d48a5-110">Tenha em atenção Olá mesmo a ser efetuada para Olá back-end NSG e Olá back-end sub-rede do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d48a5-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="d48a5-111">Implementar a modelo ARM Olá utilizando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="d48a5-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="d48a5-112">Olá modelo de exemplo disponível no repositório público Olá utiliza um ficheiro de parâmetros que contém as cenário de Olá valores utilizados de predefinição do Olá toogenerate descrito acima.</span><span class="sxs-lookup"><span data-stu-id="d48a5-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="d48a5-113">toodeploy utilizando este modelo Clique toodeploy, siga [esta ligação](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá se necessário e siga as instruções de Olá no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="d48a5-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="d48a5-114">Implementar a modelo ARM Olá utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d48a5-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="d48a5-115">modelo ARM toodeploy Olá transferidas utilizando o PowerShell, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="d48a5-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="d48a5-116">Se nunca tiver utilizado o Azure PowerShell, siga as instruções de Olá Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall e configurá-la.</span><span class="sxs-lookup"><span data-stu-id="d48a5-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="d48a5-117">Executar Olá  **`New-AzureRmResourceGroup`**  toocreate cmdlet um grupo de recursos utilizando Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="d48a5-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="d48a5-118">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d48a5-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="d48a5-119">Implementar o modelo ARM Olá utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d48a5-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="d48a5-120">modelo ARM Olá toodeploy utilizando Olá CLI do Azure, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="d48a5-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="d48a5-121">Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="d48a5-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d48a5-122">Executar Olá  **`azure config mode`**  comando tooswitch tooResource modo Manager, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d48a5-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d48a5-123">Olá segue-se o resultado de Olá esperado para Olá comando:</span><span class="sxs-lookup"><span data-stu-id="d48a5-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="d48a5-124">Executar Olá  **`azure group deployment create`**  cmdlet toodeploy Olá nova VNet através da utilização de parâmetros de modelo de Olá e ficheiros que transferiu e alterou acima.</span><span class="sxs-lookup"><span data-stu-id="d48a5-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="d48a5-125">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="d48a5-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="d48a5-126">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d48a5-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="d48a5-127">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="d48a5-127">**-n (or --name)**.</span></span> <span data-ttu-id="d48a5-128">Nome do toobe de grupo de recursos de Olá criado.</span><span class="sxs-lookup"><span data-stu-id="d48a5-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="d48a5-129">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="d48a5-129">**-l (or --location)**.</span></span> <span data-ttu-id="d48a5-130">Região do Azure onde será criado o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d48a5-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="d48a5-131">**-f (ou --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="d48a5-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="d48a5-132">Ficheiro do modelo ARM tooyour de caminho.</span><span class="sxs-lookup"><span data-stu-id="d48a5-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="d48a5-133">**-e (ou --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="d48a5-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="d48a5-134">Ficheiro de parâmetros do caminho tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="d48a5-134">Path tooyour ARM parameters file.</span></span>

