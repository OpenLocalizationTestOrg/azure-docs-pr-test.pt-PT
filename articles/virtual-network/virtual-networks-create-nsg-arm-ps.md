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
# <a name="create-network-security-groups-using-powershell"></a>Criar grupos de segurança através do PowerShell de rede

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

O Azure tem dois modelos de implementação: a implementação do Azure Resource Manager e a implementação clássica. A Microsoft recomenda a criação de recursos através do modelo de implementação do Resource Manager Olá. mais informações sobre como toolearn Olá diferenças entre os modelos de Olá dois ler Olá [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md) artigo. Este artigo abrange o modelo de implementação do Resource Manager Olá. Também pode [criar NSGs no modelo de implementação clássica Olá](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

exemplo de Olá PowerShell comandos abaixo esperam num ambiente simple já criado com base no cenário de Olá acima. Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá implementando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá Se necessário e siga as instruções de Olá em Olá portal.

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Como toocreate Olá NSG para sub-rede do front-end Olá
toocreate um NSG denominado *NSG-front-end* com base no cenário de Olá, concluir Olá os seguintes passos:

1. Se nunca tiver utilizado o Azure PowerShell, consulte o artigo [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções de Olá todos os toohello de forma Olá terminar toosign no Azure e selecionar a sua subscrição.
2. Crie uma regra de segurança que permite o acesso a partir da Internet de Olá tooport 3389.

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. Crie uma regra de segurança que permite o acesso a partir da Internet de Olá tooport 80.

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. Adicionar regras de Olá criadas acima tooa com o nome do novo NSG **NSG-front-end**.

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. Verifica as regras de Olá criadas no Olá NSG, escrevendo Olá seguinte:

    ```powershell
    $nsg
    ```
   
    Regras de segurança que mostra Olá apenas de saída:
   
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
6. Associar Olá NSG criado acima toohello *front-end* sub-rede.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    Olá apenas do resultado que mostra *front-end* definições da sub-rede, tenha em atenção o valor de Olá para Olá **NetworkSecurityGroup** propriedade:
   
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
   > o resultado de Olá para Olá comando acima mostra conteúdo Olá Olá configuração objeto da rede virtual, que só existe no computador de olá onde estiver a executar o PowerShell. Terá de toorun Olá `Set-AzureRmVirtualNetwork` cmdlet toosave tooAzure estas definições.
   > 
   > 
7. Guarde Olá nova VNet definições tooAzure.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Mostrar apenas parte do Olá NSG de saída:
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Como toocreate Olá NSG para sub-rede de back-end Olá
toocreate um NSG denominado *NSG-back-end* com base no cenário de Olá acima, concluir Olá os seguintes passos:

1. Crie uma regra de segurança que permite o acesso a partir da sub-rede do front-end de Olá tooport 1433 (porta predefinida utilizada pelo SQL Server).

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. Crie uma regra de segurança bloquear toohello de acesso à Internet.

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. Adicionar regras de Olá criadas acima tooa com o nome do novo NSG **NSG-back-end**.

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. Associar Olá NSG criado acima toohello *back-end* sub-rede.

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    Olá apenas do resultado que mostra *back-end* definições da sub-rede, tenha em atenção o valor de Olá para Olá **NetworkSecurityGroup** propriedade:
   
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
5. Guarde Olá nova VNet definições tooAzure.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a>Como tooremove um NSG
toodelete um NSG existente, denominado *NSG-front-end* neste caso, siga o passo de Olá abaixo:

Executar Olá **remover AzureRmNetworkSecurityGroup** mostrado abaixo e ser se tooinclude Olá recursos grupo Olá NSG está em.

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

