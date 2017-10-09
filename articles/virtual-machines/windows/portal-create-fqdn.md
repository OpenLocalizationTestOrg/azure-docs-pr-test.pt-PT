---
title: aaaCreate FQDN para uma VM com o Windows hello portal do Azure | Microsoft Docs
description: "Saiba como toocreate um nome de domínio completamente qualificado, ou FQDN, para um Gestor de recursos com base em máquina virtual no Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="052ab-103">Criar um nome de domínio completamente qualificado no Olá portal do Azure para uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="052ab-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="052ab-104">Quando cria uma máquina virtual (VM) no Olá [portal do Azure](https://portal.azure.com), um recurso IP público para a máquina virtual de Olá é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="052ab-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="052ab-105">Utilize este Olá de acesso de tooremotely de endereço IP VM.</span><span class="sxs-lookup"><span data-stu-id="052ab-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="052ab-106">Embora o portal de Olá não cria um [nome de domínio completamente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou FQDN, pode criar um depois hello é criada a VM.</span><span class="sxs-lookup"><span data-stu-id="052ab-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="052ab-107">Este artigo demonstra Olá passos toocreate um nome DNS ou o FQDN.</span><span class="sxs-lookup"><span data-stu-id="052ab-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="052ab-108">Criar um FQDN</span><span class="sxs-lookup"><span data-stu-id="052ab-108">Create a FQDN</span></span>
<span data-ttu-id="052ab-109">Este artigo pressupõe que já criou uma VM.</span><span class="sxs-lookup"><span data-stu-id="052ab-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="052ab-110">Se necessário, pode [criar uma VM no portal de Olá](quick-create-portal.md) ou [com o Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="052ab-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="052ab-111">Assim que a VM está a funcionar, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="052ab-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="052ab-112">Pode agora ligar remotamente toohello VM com este nome DNS, tal como para o protocolo de ambiente de trabalho remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="052ab-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="052ab-113">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="052ab-113">Next steps</span></span>
<span data-ttu-id="052ab-114">Agora que a VM tem um nome IP e DNS público, pode implementar comuns das estruturas de aplicações ou serviços como o IIS, SQL Server ou SharePoint.</span><span class="sxs-lookup"><span data-stu-id="052ab-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="052ab-115">Também pode ler mais sobre [com o Resource Manager](../../azure-resource-manager/resource-group-overview.md) para sugestões sobre como criar as suas implementações do Azure.</span><span class="sxs-lookup"><span data-stu-id="052ab-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

