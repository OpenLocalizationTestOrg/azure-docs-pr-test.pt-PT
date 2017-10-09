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
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a>Criar rede grupos de segurança através de um modelo Azure Resource Manager

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo abrange o modelo de implementação do Resource Manager Olá. Também pode [criar NSGs no modelo de implementação clássica Olá](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a>Recursos NSG num ficheiro de modelo
Pode ver e transferir Olá [modelo de exemplo](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).

Olá secção seguinte mostra a definição de Olá de Olá NSG front-end, com base no cenário de Olá.

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
tooassociate Olá NSG toohello front-end sub-rede, tem de definição de sub-rede Olá toochange no modelo de Olá e utilizar id de referência de Olá para Olá NSG.

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

Tenha em atenção Olá mesmo a ser efetuada para Olá back-end NSG e Olá back-end sub-rede do modelo de Olá.

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Implementar a modelo ARM Olá utilizando clique toodeploy
Olá modelo de exemplo disponível no repositório público Olá utiliza um ficheiro de parâmetros que contém as cenário de Olá valores utilizados de predefinição do Olá toogenerate descrito acima. toodeploy utilizando este modelo Clique toodeploy, siga [esta ligação](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá se necessário e siga as instruções de Olá no portal de Olá.

## <a name="deploy-hello-arm-template-by-using-powershell"></a>Implementar a modelo ARM Olá utilizando o PowerShell
modelo ARM toodeploy Olá transferidas utilizando o PowerShell, siga os passos de Olá abaixo.

1. Se nunca tiver utilizado o Azure PowerShell, siga as instruções de Olá Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall e configurá-la.
2. Executar Olá  **`New-AzureRmResourceGroup`**  toocreate cmdlet um grupo de recursos utilizando Olá modelo.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Resultado esperado:

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

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a>Implementar o modelo ARM Olá utilizando Olá CLI do Azure
modelo ARM Olá toodeploy utilizando Olá CLI do Azure, siga os passos de Olá abaixo.

1. Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.
2. Executar Olá  **`azure config mode`**  comando tooswitch tooResource modo Manager, como mostrado abaixo.

    ```azurecli
    azure config mode arm
    ```

    Olá segue-se o resultado de Olá esperado para Olá comando:

        info:    New mode is arm

3. Executar Olá  **`azure group deployment create`**  cmdlet toodeploy Olá nova VNet através da utilização de parâmetros de modelo de Olá e ficheiros que transferiu e alterou acima. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Resultado esperado:
   
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
   
   * **-n (ou --name)**. Nome do toobe de grupo de recursos de Olá criado.
   * **-l (ou --location)**. Região do Azure onde será criado o grupo de recursos de Olá.
   * **-f (ou --template-file)**. Ficheiro do modelo ARM tooyour de caminho.
   * **-e (ou --parameters-file)**. Ficheiro de parâmetros do caminho tooyour ARM.

