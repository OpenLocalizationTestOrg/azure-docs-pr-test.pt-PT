---
title: "aaaSet dos pontos finais de uma VM com Linux clássico | Microsoft Docs"
description: "Saiba mais tooset dos pontos finais para uma VM com Linux no Olá comunicação tooallow de portal clássico do Azure com uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="3685a-103">Como tooset dos pontos finais numa máquina virtual clássico Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="3685a-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="3685a-104">Todas as máquinas virtuais do Linux que criar no Azure utilizando o modelo de implementação clássica Olá automaticamente comunicar através de um canal de rede privada com outras máquinas virtuais na Olá que mesma rede virtual ou serviço da nuvem.</span><span class="sxs-lookup"><span data-stu-id="3685a-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="3685a-105">No entanto, os computadores no Olá Internet ou outras redes virtuais necessitam pontos finais toodirect Olá rede entrada tráfego tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3685a-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="3685a-106">Este artigo também está disponível para [máquinas virtuais Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3685a-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3685a-107">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3685a-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3685a-108">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="3685a-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3685a-109">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3685a-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="3685a-110">No Olá **Resource Manager** modelo de implementação, pontos finais são configurados utilizando **grupos de segurança de rede (NSGs)**.</span><span class="sxs-lookup"><span data-stu-id="3685a-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="3685a-111">Para obter mais informações, consulte [abrir portas e os pontos finais](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3685a-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3685a-112">Quando cria uma máquina virtual Linux no Olá portal do Azure, um ponto final de Secure Shell (SSH) é normalmente criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3685a-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="3685a-113">Pode configurar os pontos finais adicionais ao criar a máquina virtual de Olá ou posteriormente, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="3685a-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="3685a-114">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3685a-114">Next steps</span></span>
* <span data-ttu-id="3685a-115">Também pode criar um ponto final da VM utilizando Olá [Interface de linha de comandos do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3685a-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="3685a-116">Executar Olá **criar o ponto final de vm do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="3685a-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="3685a-117">Se tiver criado uma máquina virtual no modelo de implementação do Resource Manager Olá, pode utilizar Olá CLI do Azure no modo Resource Manager demasiado[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol tráfego toohello VM.</span><span class="sxs-lookup"><span data-stu-id="3685a-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
