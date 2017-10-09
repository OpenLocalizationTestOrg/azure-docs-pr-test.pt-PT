---
title: "aaaDeploying recursos de computação do Windows com modelos do Azure Resource Manager | Microsoft Docs"
description: "Tutorial do DotNet núcleos de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="f8bac-103">Arquitetura de aplicações com modelos Azure Resource Manager para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="f8bac-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="f8bac-104">Ao desenvolver uma implementação do Azure Resource Manager, requisitos de processamento necessário toobe mapeado tooAzure recursos e serviços.</span><span class="sxs-lookup"><span data-stu-id="f8bac-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="f8bac-105">Se uma aplicação consiste de vários pontos finais de http, uma base de dados e um serviço de colocação em cache de dados, hello recursos do Azure que aloja cada um destes componentes tem de toobe rationalized.</span><span class="sxs-lookup"><span data-stu-id="f8bac-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="f8bac-106">Por exemplo, a aplicação de arquivo de música de exemplo de Olá inclui uma aplicação web que está alojada numa máquina virtual e uma base de dados do SQL Server, que está alojado na base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8bac-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="f8bac-107">Este documento fornece detalhes sobre como os recursos de computação do arquivo de música Olá estão configurados no modelo de Gestor de recursos do Azure de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="f8bac-108">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="f8bac-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f8bac-109">Para uma experiência otimizada Olá, pré-implemente uma instância de trabalho, juntamente com o modelo do Azure Resource Manager Olá e Olá solução tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8bac-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="f8bac-110">modelo completo Olá pode ser encontrado aqui – [implementação de arquivo de música em Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="f8bac-110">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="f8bac-111">Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="f8bac-111">Virtual Machine</span></span>
<span data-ttu-id="f8bac-112">Olá aplicação da loja de música inclui uma aplicação web, onde os clientes podem procurar e adquirir música.</span><span class="sxs-lookup"><span data-stu-id="f8bac-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="f8bac-113">Enquanto existirem vários serviços do Azure que podem alojar aplicações web, para este exemplo, uma Máquina Virtual é utilizado.</span><span class="sxs-lookup"><span data-stu-id="f8bac-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="f8bac-114">Utilizar o modelo de arquivo de música de exemplo de Olá, uma máquina virtual é implementada, instalar um servidor web e Web site do arquivo de música Olá instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="f8bac-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="f8bac-115">Para sake Olá deste artigo, apenas a implementação de máquina virtual Olá está detalhada.</span><span class="sxs-lookup"><span data-stu-id="f8bac-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="f8bac-116">configuração de Hello do servidor de web de Olá e aplicação de Olá é detalhada num artigo posterior.</span><span class="sxs-lookup"><span data-stu-id="f8bac-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="f8bac-117">Uma máquina virtual pode ser adicionada modelo tooa utilizando Olá Visual Studio adicionar novo recurso do assistente, ou por inserir o modelo de implementação de Olá JSON válido.</span><span class="sxs-lookup"><span data-stu-id="f8bac-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="f8bac-118">Quando implementar uma máquina virtual, vários recursos relacionados são também necessárias.</span><span class="sxs-lookup"><span data-stu-id="f8bac-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="f8bac-119">Se utilizar o modelo do Visual Studio toocreate Olá, estes recursos são criados por si.</span><span class="sxs-lookup"><span data-stu-id="f8bac-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="f8bac-120">Se manualmente construir o modelo de Olá, estes recursos têm de toobe inserido e configurado.</span><span class="sxs-lookup"><span data-stu-id="f8bac-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="f8bac-121">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [JSON de Máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="f8bac-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
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

<span data-ttu-id="f8bac-122">Depois de implementada, as propriedades da máquina virtual Olá podem ser vistas no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8bac-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Máquina Virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="f8bac-124">Conta de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="f8bac-124">Storage Account</span></span>
<span data-ttu-id="f8bac-125">As contas de armazenamento têm várias capacidades e opções de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8bac-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="f8bac-126">Para o contexto de Olá das máquinas virtuais do Azure, uma conta de armazenamento contém discos rígidos virtuais da máquina virtual de Olá Olá e quaisquer discos de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="f8bac-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="f8bac-127">exemplo de arquivo de música Olá inclui um armazenamento conta toohold Olá disco rígido virtual de cada máquina virtual numa implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="f8bac-128">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="f8bac-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

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

<span data-ttu-id="f8bac-129">Uma conta de armazenamento é associar com uma máquina virtual no interior da declaração de modelo do Resource Manager Olá da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="f8bac-130">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [associação da Máquina Virtual e a conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="f8bac-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

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

<span data-ttu-id="f8bac-131">Após a implementação, conta de armazenamento Olá pode ser visualizada no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8bac-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Conta de Armazenamento](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="f8bac-133">Clicar num contentor de BLOBs de conta de armazenamento Olá, ficheiros de disco rígido virtual Olá para cada máquina virtual implementada com o modelo de Olá podem ser vistos.</span><span class="sxs-lookup"><span data-stu-id="f8bac-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Unidades de disco rígido virtuais](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="f8bac-135">Para obter mais informações sobre o Storage do Azure, consulte [documentação do Storage do Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="f8bac-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="f8bac-136">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="f8bac-136">Virtual Network</span></span>
<span data-ttu-id="f8bac-137">Se precisar de uma máquina virtual à rede interna, tais como a capacidade de Olá toocommunicate com outras máquinas virtuais e os recursos do Azure, uma rede Virtual do Azure, é necessária.</span><span class="sxs-lookup"><span data-stu-id="f8bac-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="f8bac-138">Uma rede virtual não faz máquina virtual de Olá acessível através de Olá internet.</span><span class="sxs-lookup"><span data-stu-id="f8bac-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="f8bac-139">Conectividade pública requer um endereço IP público, que é descrito mais tarde nesta série.</span><span class="sxs-lookup"><span data-stu-id="f8bac-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="f8bac-140">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [sub-redes e de rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="f8bac-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

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

<span data-ttu-id="f8bac-141">De Olá portal do Azure, a rede virtual Olá aspeto Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="f8bac-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="f8bac-142">Tenha em atenção de que todas as máquinas virtuais implementadas com o modelo de Olá são toohello anexado de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f8bac-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Rede Virtual](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="f8bac-144">Interface de rede</span><span class="sxs-lookup"><span data-stu-id="f8bac-144">Network Interface</span></span>
 <span data-ttu-id="f8bac-145">Uma interface de rede liga-se a rede virtual da máquina virtual tooa, mais especificamente tooa sub-rede que tenha sido definido na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="f8bac-146">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [Interface de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="f8bac-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
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
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
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
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="f8bac-147">Cada recurso de máquina virtual inclui um perfil de rede.</span><span class="sxs-lookup"><span data-stu-id="f8bac-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="f8bac-148">interface de rede Olá está associado a máquina virtual de Olá neste perfil.</span><span class="sxs-lookup"><span data-stu-id="f8bac-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="f8bac-149">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [perfil de rede de Máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="f8bac-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="f8bac-150">De Olá portal do Azure, a interface de rede Olá aspeto Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="f8bac-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="f8bac-151">Olá endereço IP e a associação da máquina virtual de Olá podem ser vistos no recurso de interface de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Interface de rede](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="f8bac-153">Para obter mais informações sobre redes virtuais do Azure, consulte [documentação de Virtual Network do Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="f8bac-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="f8bac-154">Base de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f8bac-154">Azure SQL Database</span></span>
<span data-ttu-id="f8bac-155">Além disso tooa virtual máquina que aloja o Web site do arquivo de música Olá, uma base de dados do SQL do Azure é a base de dados do toohost implementado Olá loja de música.</span><span class="sxs-lookup"><span data-stu-id="f8bac-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="f8bac-156">Olá das vantagens da SQL Database do Azure a utilizar aqui é que um segundo conjunto de máquinas virtuais não é necessário, e dimensionamento e disponibilidade está incorporado no serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="f8bac-157">Uma base de dados SQL do Azure pode ser adicionada utilizando Olá Visual Studio adicionar novo recurso do assistente, ou por inserir um JSON válido de um modelo.</span><span class="sxs-lookup"><span data-stu-id="f8bac-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="f8bac-158">Olá recursos do SQL Server inclui um nome de utilizador e palavra-passe que é concedido direitos administrativos na instância do SQL Server de Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="f8bac-159">Além disso, é adicionado um recurso de firewall do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8bac-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="f8bac-160">Por predefinição, as aplicações alojadas no Azure são tooconnect possível com a instância do SQL Olá.</span><span class="sxs-lookup"><span data-stu-id="f8bac-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="f8bac-161">tooallow aplicação externa essa uma SQL Server Management studio tooconnect toohello instância do SQL, firewall Olá tem toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="f8bac-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="f8bac-162">Para sake Olá de demonstração de arquivo de música Olá, a configuração predefinida de Olá é adequada.</span><span class="sxs-lookup"><span data-stu-id="f8bac-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="f8bac-163">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [BD SQL do Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="f8bac-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="f8bac-164">Uma vista do Olá SQL server e base de dados de MusicStore visto na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8bac-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="f8bac-166">Para obter mais informações sobre a implementação da SQL Database do Azure, consulte [documentação da SQL Database do Azure](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="f8bac-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="f8bac-167">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="f8bac-167">Next step</span></span>
<hr>

[<span data-ttu-id="f8bac-168">Passo 2 - acesso e segurança de modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8bac-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

