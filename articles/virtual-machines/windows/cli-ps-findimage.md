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
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="8ee4d-103">Como de imagens de toofind VM do Windows hello Azure Marketplace com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ee4d-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="8ee4d-104">Este tópico descreve como toouse Azure PowerShell toofind VM imagens no Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="8ee4d-105">Utilize este toospecify informações uma imagem do Marketplace quando criar uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="8ee4d-106">Certifique-se de que é instalado e configurado Olá mais recente [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8ee4d-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="8ee4d-107">Tabela de imagens do Windows utilizadas normalmente</span><span class="sxs-lookup"><span data-stu-id="8ee4d-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="8ee4d-108">Nome do Editor</span><span class="sxs-lookup"><span data-stu-id="8ee4d-108">PublisherName</span></span> | <span data-ttu-id="8ee4d-109">Oferta</span><span class="sxs-lookup"><span data-stu-id="8ee4d-109">Offer</span></span> | <span data-ttu-id="8ee4d-110">Sku</span><span class="sxs-lookup"><span data-stu-id="8ee4d-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8ee4d-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8ee4d-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-112">WindowsServer</span></span> |<span data-ttu-id="8ee4d-113">Centro de dados de 2016</span><span class="sxs-lookup"><span data-stu-id="8ee4d-113">2016-Datacenter</span></span> |
| <span data-ttu-id="8ee4d-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8ee4d-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-115">WindowsServer</span></span> |<span data-ttu-id="8ee4d-116">2016 Centro de dados-Server Core</span><span class="sxs-lookup"><span data-stu-id="8ee4d-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="8ee4d-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8ee4d-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-118">WindowsServer</span></span> |<span data-ttu-id="8ee4d-119">2016 Datacenter com contentores</span><span class="sxs-lookup"><span data-stu-id="8ee4d-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="8ee4d-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8ee4d-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-121">WindowsServer</span></span> |<span data-ttu-id="8ee4d-122">Servidor de Nano de 2016</span><span class="sxs-lookup"><span data-stu-id="8ee4d-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="8ee4d-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8ee4d-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-124">WindowsServer</span></span> |<span data-ttu-id="8ee4d-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="8ee4d-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="8ee4d-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8ee4d-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-127">WindowsServer</span></span> |<span data-ttu-id="8ee4d-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="8ee4d-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="8ee4d-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="8ee4d-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="8ee4d-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="8ee4d-130">DynamicsNAV</span></span> |<span data-ttu-id="8ee4d-131">2017</span><span class="sxs-lookup"><span data-stu-id="8ee4d-131">2017</span></span> |
| <span data-ttu-id="8ee4d-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="8ee4d-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="8ee4d-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="8ee4d-134">2016</span><span class="sxs-lookup"><span data-stu-id="8ee4d-134">2016</span></span> |
| <span data-ttu-id="8ee4d-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="8ee4d-136">SQL2016 WS2016</span><span class="sxs-lookup"><span data-stu-id="8ee4d-136">SQL2016-WS2016</span></span> |<span data-ttu-id="8ee4d-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="8ee4d-137">Enterprise</span></span> |
| <span data-ttu-id="8ee4d-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="8ee4d-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="8ee4d-139">SQL2014SP2 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="8ee4d-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="8ee4d-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="8ee4d-140">Enterprise</span></span> |
| <span data-ttu-id="8ee4d-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="8ee4d-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="8ee4d-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="8ee4d-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="8ee4d-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="8ee4d-143">2012R2</span></span> |
| <span data-ttu-id="8ee4d-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="8ee4d-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="8ee4d-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="8ee4d-145">WindowsServerEssentials</span></span> |<span data-ttu-id="8ee4d-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="8ee4d-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="8ee4d-147">Encontrar imagens específicas</span><span class="sxs-lookup"><span data-stu-id="8ee4d-147">Find specific images</span></span>


<span data-ttu-id="8ee4d-148">Quando criar uma nova máquina virtual com o Azure Resource Manager, em alguns casos tem toospecify uma imagem com combinação de Olá de Olá seguintes propriedades de imagem:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="8ee4d-149">Publicador</span><span class="sxs-lookup"><span data-stu-id="8ee4d-149">Publisher</span></span>
* <span data-ttu-id="8ee4d-150">Oferta</span><span class="sxs-lookup"><span data-stu-id="8ee4d-150">Offer</span></span>
* <span data-ttu-id="8ee4d-151">SKU</span><span class="sxs-lookup"><span data-stu-id="8ee4d-151">SKU</span></span>

<span data-ttu-id="8ee4d-152">Por exemplo, utilize estes valores com Olá [conjunto AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet do PowerShell, ou com um modelo de grupo de recursos no qual tem de especificar o tipo de Olá de toobe VM criada.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="8ee4d-153">Se precisar de toodetermine estes valores, pode executar Olá [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), e [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets imagens de Olá toonavigate.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="8ee4d-154">Determinar estes valores:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-154">You determine these values:</span></span>

1. <span data-ttu-id="8ee4d-155">Lista Olá imagem os Publicadores.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-155">List hello image publishers.</span></span>
2. <span data-ttu-id="8ee4d-156">Para um determinado publicador, liste as respetivas ofertas.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="8ee4d-157">Para uma determinada oferta, liste as respetivas SKUs.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="8ee4d-158">Em primeiro lugar, lista publicadores Olá com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="8ee4d-159">Preencha o nome do publicador escolhido e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="8ee4d-160">Preencha o nome da sua oferta escolhido e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="8ee4d-161">Da saída de Olá de Olá `Get-AzureRMVMImageSku` comando, que tem todas as informações de Olá precisa de imagem de Olá toospecify para uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="8ee4d-162">seguinte Olá mostra um exemplo completo:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="8ee4d-163">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-163">Output:</span></span>

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

<span data-ttu-id="8ee4d-164">Para o publicador de "MicrosoftWindowsServer" Olá:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="8ee4d-165">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="8ee4d-166">Oferta de "Windows" Olá:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="8ee4d-167">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ee4d-167">Output:</span></span>

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

<span data-ttu-id="8ee4d-168">Nesta lista, copie Olá escolhido o nome SKU e tem todas as informações de Olá para Olá `Set-AzureRMVMSourceImage` cmdlet do PowerShell ou de um modelo de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ee4d-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8ee4d-169">Next steps</span></span>
<span data-ttu-id="8ee4d-170">Agora, pode escolher a imagem de Olá precisamente quiser toouse.</span><span class="sxs-lookup"><span data-stu-id="8ee4d-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="8ee4d-171">Consulte de uma máquina virtual utilizando rapidamente Olá as informações da imagem, que apenas encontrado, toocreate [criar máquina virtual do Windows com o PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8ee4d-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
