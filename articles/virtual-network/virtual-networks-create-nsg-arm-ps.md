---
title: "aaaCreate de rede de grupos de segurança - Azure PowerShell | Microsoft Docs"
description: "Saiba como toocreate e implementar grupos de segurança de rede com o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="e813d-103">Criar grupos de segurança através do PowerShell de rede</span><span class="sxs-lookup"><span data-stu-id="e813d-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="e813d-104">O Azure tem dois modelos de implementação: a implementação do Azure Resource Manager e a implementação clássica.</span><span class="sxs-lookup"><span data-stu-id="e813d-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e813d-105">A Microsoft recomenda a criação de recursos através do modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="e813d-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="e813d-106">mais informações sobre como toolearn Olá diferenças entre os modelos de Olá dois ler Olá [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="e813d-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="e813d-107">Este artigo abrange o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="e813d-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="e813d-108">Também pode [criar NSGs no modelo de implementação clássica Olá](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e813d-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="e813d-109">exemplo de Olá PowerShell comandos abaixo esperam num ambiente simple já criado com base no cenário de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="e813d-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="e813d-110">Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá implementando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá Se necessário e siga as instruções de Olá em Olá portal.</span><span class="sxs-lookup"><span data-stu-id="e813d-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="e813d-111">Como toocreate Olá NSG para sub-rede do front-end Olá</span><span class="sxs-lookup"><span data-stu-id="e813d-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="e813d-112">toocreate um NSG denominado *NSG-front-end* com base no cenário de Olá, concluir Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="e813d-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="e813d-113">Se nunca tiver utilizado o Azure PowerShell, consulte o artigo [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções de Olá todos os toohello de forma Olá terminar toosign no Azure e selecionar a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="e813d-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="e813d-114">Crie uma regra de segurança que permite o acesso a partir da Internet de Olá tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="e813d-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="e813d-115">Crie uma regra de segurança que permite o acesso a partir da Internet de Olá tooport 80.</span><span class="sxs-lookup"><span data-stu-id="e813d-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="e813d-116">Adicionar regras de Olá criadas acima tooa com o nome do novo NSG **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e813d-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="e813d-117">Verifica as regras de Olá criadas no Olá NSG, escrevendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="e813d-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="e813d-118">Regras de segurança que mostra Olá apenas de saída:</span><span class="sxs-lookup"><span data-stu-id="e813d-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="e813d-119">Associar Olá NSG criado acima toohello *front-end* sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e813d-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="e813d-120">Olá apenas do resultado que mostra *front-end* definições da sub-rede, tenha em atenção o valor de Olá para Olá **NetworkSecurityGroup** propriedade:</span><span class="sxs-lookup"><span data-stu-id="e813d-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="e813d-121">o resultado de Olá para Olá comando acima mostra conteúdo Olá Olá configuração objeto da rede virtual, que só existe no computador de olá onde estiver a executar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e813d-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="e813d-122">Terá de toorun Olá `Set-AzureRmVirtualNetwork` cmdlet toosave tooAzure estas definições.</span><span class="sxs-lookup"><span data-stu-id="e813d-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="e813d-123">Guarde Olá nova VNet definições tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e813d-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="e813d-124">Mostrar apenas parte do Olá NSG de saída:</span><span class="sxs-lookup"><span data-stu-id="e813d-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="e813d-125">Como toocreate Olá NSG para sub-rede de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="e813d-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="e813d-126">toocreate um NSG denominado *NSG-back-end* com base no cenário de Olá acima, concluir Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="e813d-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="e813d-127">Crie uma regra de segurança que permite o acesso a partir da sub-rede do front-end de Olá tooport 1433 (porta predefinida utilizada pelo SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e813d-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="e813d-128">Crie uma regra de segurança bloquear toohello de acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="e813d-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="e813d-129">Adicionar regras de Olá criadas acima tooa com o nome do novo NSG **NSG-back-end**.</span><span class="sxs-lookup"><span data-stu-id="e813d-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="e813d-130">Associar Olá NSG criado acima toohello *back-end* sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e813d-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="e813d-131">Olá apenas do resultado que mostra *back-end* definições da sub-rede, tenha em atenção o valor de Olá para Olá **NetworkSecurityGroup** propriedade:</span><span class="sxs-lookup"><span data-stu-id="e813d-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="e813d-132">Guarde Olá nova VNet definições tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e813d-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="e813d-133">Como tooremove um NSG</span><span class="sxs-lookup"><span data-stu-id="e813d-133">How tooremove an NSG</span></span>
<span data-ttu-id="e813d-134">toodelete um NSG existente, denominado *NSG-front-end* neste caso, siga o passo de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="e813d-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="e813d-135">Executar Olá **remover AzureRmNetworkSecurityGroup** mostrado abaixo e ser se tooinclude Olá recursos grupo Olá NSG está em.</span><span class="sxs-lookup"><span data-stu-id="e813d-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

