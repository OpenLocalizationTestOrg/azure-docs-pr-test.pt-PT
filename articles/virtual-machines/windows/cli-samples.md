---
title: aaaAzure CLI exemplos do Windows | Microsoft Docs
description: Exemplos da CLI do Azure Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="3e99c-103">Virtual machines do Azure CLI amostras para Windows</span><span class="sxs-lookup"><span data-stu-id="3e99c-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="3e99c-104">Olá tabela a seguir inclui ligações toobash scripts compiladas com a CLI do Azure de Olá implementar máquinas virtuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="3e99c-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="3e99c-105">**Criar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="3e99c-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="3e99c-106">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3e99c-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-107">Cria uma máquina virtual do Windows com configuração mínima.</span><span class="sxs-lookup"><span data-stu-id="3e99c-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="3e99c-108">Criar uma máquina virtual totalmente configurada</span><span class="sxs-lookup"><span data-stu-id="3e99c-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-109">Cria um grupo de recursos, a máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="3e99c-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="3e99c-110">Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="3e99c-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-111">Cria várias máquinas virtuais da elevada disponibilidade e a configuração de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="3e99c-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="3e99c-112">Criar uma VM e executar o script de configuração</span><span class="sxs-lookup"><span data-stu-id="3e99c-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-113">Cria uma máquina virtual e utiliza tooinstall de extensão de Script personalizado de Azure Olá IIS.</span><span class="sxs-lookup"><span data-stu-id="3e99c-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="3e99c-114">Criar uma VM e execute a configuração DSC</span><span class="sxs-lookup"><span data-stu-id="3e99c-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-115">Cria uma máquina virtual e utiliza Olá pretendido Estado Configuration (DSC) do Azure extensão tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="3e99c-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="3e99c-116">**Máquinas virtuais da rede**</span><span class="sxs-lookup"><span data-stu-id="3e99c-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="3e99c-117">Proteger o tráfego de rede entre as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="3e99c-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-118">Cria duas máquinas virtuais, relacionados todos os recursos e uma grupos de segurança de rede internos e externos (NSG).</span><span class="sxs-lookup"><span data-stu-id="3e99c-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="3e99c-119">**Proteger máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="3e99c-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="3e99c-120">Encriptar uma VM e discos de dados</span><span class="sxs-lookup"><span data-stu-id="3e99c-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-121">Cria um cofre de chaves do Azure, uma chave de encriptação e um principal de serviço, em seguida, encripta uma VM.</span><span class="sxs-lookup"><span data-stu-id="3e99c-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="3e99c-122">**Monitorizar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="3e99c-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="3e99c-123">Monitorizar uma VM com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3e99c-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3e99c-124">Cria uma máquina virtual, instala o agente do Operations Management Suite Olá e inscreve Olá VM com uma área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="3e99c-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
