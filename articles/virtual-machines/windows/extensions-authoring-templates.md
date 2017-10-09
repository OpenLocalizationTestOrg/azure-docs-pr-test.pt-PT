---
title: "aaaAuthoring modelos com extensões de VM do Windows | Microsoft Docs"
description: "Saiba mais sobre a criação de modelos Azure Resource Manager com as extensões para VMs do Windows"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="f3698-103">Criação de modelos Azure Resource Manager com extensões de VM do Windows</span><span class="sxs-lookup"><span data-stu-id="f3698-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="f3698-104">A partir do Azure PowerShell, execute Olá seguinte cmdlet do PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="f3698-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="f3698-105">Este cmdlet devolve o nome do publicador Olá, nome de extensão e versão da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f3698-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="f3698-106">Estas três propriedades mapeiam demasiado "publisher", "type" e "typeHandlerVersion" respetivamente no Olá acima fragmento de modelo.</span><span class="sxs-lookup"><span data-stu-id="f3698-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="f3698-107">É sempre toouse recomendada Olá mais recente extensão versão tooget Olá atualizada mais funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f3698-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="f3698-108">Identificação Olá esquema para os parâmetros de configuração de extensão Olá</span><span class="sxs-lookup"><span data-stu-id="f3698-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="f3698-109">passo seguinte do Olá com criação de um modelo de extensão é o formato de Olá tooidentify para fornecer parâmetros de configuração.</span><span class="sxs-lookup"><span data-stu-id="f3698-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="f3698-110">Cada extensão suporta o próprio conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f3698-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="f3698-111">toolook em configurações de exemplo para extensões do Windows, consulte [exemplos de extensões do Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3698-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f3698-112">Consulte toohello seguir tooget um modelo totalmente concluído com extensões VM.</span><span class="sxs-lookup"><span data-stu-id="f3698-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="f3698-113">Extensão de Script personalizado na VM do Windows</span><span class="sxs-lookup"><span data-stu-id="f3698-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="f3698-114">Após a criação do modelo de Olá, a poder implementar com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3698-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

