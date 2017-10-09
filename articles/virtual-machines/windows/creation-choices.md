---
title: aaaDifferent formas toocreate uma VM do Windows no Azure | Microsoft Docs
description: "Apresenta uma lista de formas diferentes de Olá toocreate uma máquina virtual do Windows com o Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="9e145-103">Diferentes formas toocreate máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="9e145-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="9e145-104">O Azure oferece diferentes formas toocreate uma máquina virtual porque as máquinas virtuais são adequadas para diferentes utilizadores e efeitos.</span><span class="sxs-lookup"><span data-stu-id="9e145-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="9e145-105">Isto significa que terá de toomake algumas opções sobre a máquina virtual de Olá e como toocreate-lo.</span><span class="sxs-lookup"><span data-stu-id="9e145-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="9e145-106">Este artigo dá-lhe um resumo destas opções e liga tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="9e145-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="9e145-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9e145-107">Azure portal</span></span>
<span data-ttu-id="9e145-108">A utilização de Olá portal do Azure é um tootry de forma simples de saída de uma máquina virtual, especialmente se é inexperiente com o Azure.</span><span class="sxs-lookup"><span data-stu-id="9e145-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="9e145-109">Criar uma máquina virtual com o Windows através do portal Olá</span><span class="sxs-lookup"><span data-stu-id="9e145-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="9e145-110">Modelo</span><span class="sxs-lookup"><span data-stu-id="9e145-110">Template</span></span>
<span data-ttu-id="9e145-111">Máquinas virtuais requerem uma combinação de recursos (por exemplo, uma disponibilidade conjuntos e as contas de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="9e145-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="9e145-112">Em vez de implementar e gerir separadamente cada recurso, pode criar um modelo Azure Resource Manager que implementa e aprovisiona todos os recursos de Olá numa operação única e coordenada.</span><span class="sxs-lookup"><span data-stu-id="9e145-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="9e145-113">Criar uma máquina virtual do Windows com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e145-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="9e145-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e145-114">Azure PowerShell</span></span>
<span data-ttu-id="9e145-115">Se preferir trabalhar numa shell de comandos, pode utilizar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e145-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="9e145-116">Criar uma VM do Windows com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e145-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="9e145-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e145-117">Visual Studio</span></span>
<span data-ttu-id="9e145-118">Utilizar o Visual Studio toobuild, gerir, implementar VMs com ferramentas do Azure Olá para Visual Studio e Olá Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="9e145-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="9e145-119">Ferramentas do Azure para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e145-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

