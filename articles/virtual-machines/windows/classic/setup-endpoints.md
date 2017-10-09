---
title: "aaaSet dos pontos finais numa VM Windows clássico | Microsoft Docs"
description: "Saiba tooset dos pontos finais para uma VM do Windows no Olá comunicação tooallow de portal clássico do Azure com uma máquina virtual do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="050a8-103">Como tooset dos pontos finais na máquina virtual clássico do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="050a8-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="050a8-104">Olá Windows todas as máquinas virtuais que criar no Azure utilizando o modelo de implementação clássica Olá automaticamente pode comunicar através de um canal de rede privada com outras máquinas virtuais no mesmo serviço em nuvem ou de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="050a8-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="050a8-105">No entanto, os computadores no Olá Internet ou outras redes virtuais necessitam pontos finais toodirect Olá rede entrada tráfego tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="050a8-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="050a8-106">Este artigo também está disponível para [máquinas virtuais do Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="050a8-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="050a8-107">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="050a8-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="050a8-108">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="050a8-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="050a8-109">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="050a8-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="050a8-110">No Olá **Resource Manager** modelo de implementação, pontos finais são configurados utilizando **grupos de segurança de rede (NSGs)**.</span><span class="sxs-lookup"><span data-stu-id="050a8-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="050a8-111">Para obter mais informações, consulte [permitir acesso externo tooyour VM utilizando Olá portal do Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="050a8-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="050a8-112">Quando cria uma máquina virtual do Windows no portal do Azure de Olá, pontos finais comuns, como os referentes ao ambiente de trabalho remoto e a comunicação remota do Windows PowerShell são normalmente criados por si automaticamente.</span><span class="sxs-lookup"><span data-stu-id="050a8-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="050a8-113">Pode configurar os pontos finais adicionais ao criar a máquina virtual de Olá ou posteriormente, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="050a8-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="050a8-114">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="050a8-114">Next steps</span></span>
* <span data-ttu-id="050a8-115">toouse um tooset de cmdlet do PowerShell do Azure se um ponto final de VM, consulte [adicionar AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="050a8-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="050a8-116">toouse um toomanage de cmdlet do PowerShell do Azure uma ACL num ponto final, consulte [gerir acesso listas de controlo (ACLs) para pontos finais utilizando o PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="050a8-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="050a8-117">Se tiver criado uma máquina virtual no modelo de implementação do Resource Manager Olá, pode utilizar o Azure PowerShell demasiado[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol tráfego toohello VM.</span><span class="sxs-lookup"><span data-stu-id="050a8-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
