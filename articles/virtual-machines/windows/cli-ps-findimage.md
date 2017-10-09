---
title: imagens de aaaSelect VM do Windows no Azure | Microsoft Docs
description: "Saiba como toouse Azure PowerSHell toodetermine Olá publicador, oferta, SKU e versão para imagens de VM do Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Como de imagens de toofind VM do Windows hello Azure Marketplace com o Azure PowerShell

Este tópico descreve como toouse Azure PowerShell toofind VM imagens no Olá Azure Marketplace. Utilize este toospecify informações uma imagem do Marketplace quando criar uma VM do Windows.

Certifique-se de que é instalado e configurado Olá mais recente [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tabela de imagens do Windows utilizadas normalmente
| Nome do Editor | Oferta | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |Centro de dados de 2016 |
| MicrosoftWindowsServer |WindowsServer |2016 Centro de dados-Server Core |
| MicrosoftWindowsServer |WindowsServer |2016 Datacenter com contentores |
| MicrosoftWindowsServer |WindowsServer |Servidor de Nano de 2016 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016 WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2 WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Encontrar imagens específicas


Quando criar uma nova máquina virtual com o Azure Resource Manager, em alguns casos tem toospecify uma imagem com combinação de Olá de Olá seguintes propriedades de imagem:

* Publicador
* Oferta
* SKU

Por exemplo, utilize estes valores com Olá [conjunto AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet do PowerShell, ou com um modelo de grupo de recursos no qual tem de especificar o tipo de Olá de toobe VM criada.

Se precisar de toodetermine estes valores, pode executar Olá [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), e [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets imagens de Olá toonavigate. Determinar estes valores:

1. Lista Olá imagem os Publicadores.
2. Para um determinado publicador, liste as respetivas ofertas.
3. Para uma determinada oferta, liste as respetivas SKUs.

Em primeiro lugar, lista publicadores Olá com Olá os seguintes comandos:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Preencha o nome do publicador escolhido e execute Olá os seguintes comandos:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Preencha o nome da sua oferta escolhido e execute Olá os seguintes comandos:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Da saída de Olá de Olá `Get-AzureRMVMImageSku` comando, que tem todas as informações de Olá precisa de imagem de Olá toospecify para uma nova máquina virtual.

seguinte Olá mostra um exemplo completo:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Saída:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Para o publicador de "MicrosoftWindowsServer" Olá:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Saída:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Oferta de "Windows" Olá:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Saída:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

Nesta lista, copie Olá escolhido o nome SKU e tem todas as informações de Olá para Olá `Set-AzureRMVMSourceImage` cmdlet do PowerShell ou de um modelo de grupo de recursos.

## <a name="next-steps"></a>Passos seguintes
Agora, pode escolher a imagem de Olá precisamente quiser toouse. Consulte de uma máquina virtual utilizando rapidamente Olá as informações da imagem, que apenas encontrado, toocreate [criar máquina virtual do Windows com o PowerShell](quick-create-powershell.md).
