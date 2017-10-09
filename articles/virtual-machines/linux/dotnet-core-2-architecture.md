---
title: "aaaDeploying recursos de computação do Linux com modelos do Azure Resource Manager | Microsoft Docs"
description: "Tutorial do DotNet núcleos de Máquina Virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a>Arquitetura de aplicações com modelos Azure Resource Manager para VMs com Linux

Ao desenvolver uma implementação do Azure Resource Manager, requisitos de processamento necessário toobe mapeado tooAzure recursos e serviços. Se uma aplicação consiste de vários pontos finais de http, uma base de dados e um serviço de colocação em cache de dados, hello recursos do Azure que aloja cada um destes componentes tem de toobe rationalized. Por exemplo, a aplicação de arquivo de música de exemplo de Olá inclui uma aplicação web que está alojada numa máquina virtual e uma base de dados do SQL Server, que está alojado na base de dados SQL do Azure. 

Este documento fornece detalhes sobre como os recursos de computação do arquivo de música Olá estão configurados no modelo de Gestor de recursos do Azure de exemplo de Olá. Todas as dependências e configurações exclusivas são realçadas. Para uma experiência otimizada Olá, pré-implemente uma instância de trabalho, juntamente com o modelo do Azure Resource Manager Olá e Olá solução tooyour subscrição do Azure. modelo completo Olá pode ser encontrado aqui – [a implementação da loja de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="virtual-machine"></a>Máquina Virtual
Olá aplicação da loja de música inclui uma aplicação web, onde os clientes podem procurar e adquirir música. Enquanto existirem vários serviços do Azure que podem alojar aplicações web, para este exemplo, uma Máquina Virtual é utilizado. Utilizar o modelo de arquivo de música de exemplo de Olá, uma máquina virtual é implementada, instalar um servidor web e Web site do arquivo de música Olá instalado e configurado. Para sake Olá deste artigo, apenas a implementação de máquina virtual Olá está detalhada. configuração de Hello do servidor de web de Olá e aplicação de Olá é detalhada num artigo posterior.

Uma máquina virtual pode ser adicionada modelo tooa utilizando Olá Visual Studio adicionar novo recurso do assistente, ou por inserir o modelo de implementação de Olá JSON válido. Quando implementar uma máquina virtual, vários recursos relacionados são também necessárias. Se utilizar o modelo do Visual Studio toocreate Olá, estes recursos são criados por si. Se manualmente construir o modelo de Olá, estes recursos têm de toobe inserido e configurado.

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [JSON de Máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

Depois de implementada, as propriedades da máquina virtual Olá podem ser vistas no Olá portal do Azure.

![Máquina Virtual](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a>Conta de Armazenamento
As contas de armazenamento têm várias capacidades e opções de armazenamento. Para o contexto de Olá das máquinas virtuais do Azure, uma conta de armazenamento contém discos rígidos virtuais da máquina virtual de Olá Olá e quaisquer discos de dados adicionais. exemplo de arquivo de música Olá inclui um armazenamento conta toohold Olá disco rígido virtual de cada máquina virtual numa implementação de Olá. 

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Uma conta de armazenamento é associar com uma máquina virtual no interior da declaração de modelo do Resource Manager Olá da máquina virtual de Olá. 

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [associação da Máquina Virtual e a conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Após a implementação, conta de armazenamento Olá pode ser visualizada no Olá portal do Azure.

![Conta de Armazenamento](./media/dotnet-core-2-architecture/storacct.png)

Clicar num contentor de BLOBs de conta de armazenamento Olá, ficheiros de disco rígido virtual Olá para cada máquina virtual implementada com o modelo de Olá podem ser vistos.

![Unidades de disco rígido virtuais](./media/dotnet-core-2-architecture/vhd.png)

Para obter mais informações sobre o Storage do Azure, consulte [documentação do Storage do Azure](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Rede Virtual
Se precisar de uma máquina virtual à rede interna, tais como a capacidade de Olá toocommunicate com outras máquinas virtuais e os recursos do Azure, uma rede Virtual do Azure, é necessária.  Uma rede virtual não faz máquina virtual de Olá acessível através de Olá internet. Conectividade pública requer um endereço IP público, que é descrito mais tarde nesta série.

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [sub-redes e de rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

De Olá portal do Azure, a rede virtual Olá aspeto Olá seguinte imagem. Tenha em atenção de que todas as máquinas virtuais implementadas com o modelo de Olá são toohello anexado de rede virtual.

![Rede Virtual](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a>Interface de rede
 Uma interface de rede liga-se a rede virtual da máquina virtual tooa, mais especificamente tooa sub-rede que tenha sido definido na rede virtual Olá. 

 Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [Interface de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Cada recurso de máquina virtual inclui um perfil de rede. interface de rede Olá está associado a máquina virtual de Olá neste perfil.  

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [perfil de rede de Máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

De Olá portal do Azure, a interface de rede Olá aspeto Olá seguinte imagem. Olá endereço IP e a associação da máquina virtual de Olá podem ser vistos no recurso de interface de rede Olá.

![Interface de rede](./media/dotnet-core-2-architecture/nic.png)

Para obter mais informações sobre redes virtuais do Azure, consulte [documentação de Virtual Network do Azure](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Base de Dados SQL do Azure
Além disso tooa virtual máquina que aloja o Web site do arquivo de música Olá, uma base de dados do SQL do Azure é a base de dados do toohost implementado Olá loja de música. Olá das vantagens da SQL Database do Azure a utilizar aqui é que um segundo conjunto de máquinas virtuais não é necessário, e dimensionamento e disponibilidade está incorporado no serviço de Olá.

Uma base de dados SQL do Azure pode ser adicionada utilizando Olá Visual Studio adicionar novo recurso do assistente, ou por inserir um JSON válido de um modelo. Olá recursos do SQL Server inclui um nome de utilizador e palavra-passe que é concedido direitos administrativos na instância do SQL Server de Olá. Além disso, é adicionado um recurso de firewall do SQL Server. Por predefinição, as aplicações alojadas no Azure são tooconnect possível com a instância do SQL Olá. tooallow aplicação externa essa uma SQL Server Management studio tooconnect toohello instância do SQL, firewall Olá tem toobe configurado. Para sake Olá de demonstração de arquivo de música Olá, a configuração predefinida de Olá é adequada. 

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [BD SQL do Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Uma vista do Olá SQL server e base de dados de MusicStore visto na Olá portal do Azure.

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

Para obter mais informações sobre a implementação da SQL Database do Azure, consulte [documentação da SQL Database do Azure](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Passo seguinte
<hr>

[Passo 2 - acesso e segurança de modelos Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

