---
title: "aaaCreate uma VM do Linux clássica utilizando Olá CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual do Linux com a utilização de Olá CLI do Azure 1.0 Olá modelo de implementação clássica"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="bcbf1-103">Como tooCreate uma VM com Linux clássico com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bcbf1-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="bcbf1-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bcbf1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bcbf1-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="bcbf1-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bcbf1-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="bcbf1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bcbf1-107">Para a versão do Gestor de recursos de Olá, consulte [aqui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bcbf1-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bcbf1-108">Este tópico descreve como toocreate Linux máquinas virtuais (VMS) com a utilização de Olá CLI do Azure 1.0 Olá modelo de implementação clássica.</span><span class="sxs-lookup"><span data-stu-id="bcbf1-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="bcbf1-109">Utilizamos uma imagem de Linux do Olá disponível **imagens** no Azure.</span><span class="sxs-lookup"><span data-stu-id="bcbf1-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="bcbf1-110">comandos de Olá CLI do Azure 1.0 dar Olá seguintes opções de configuração, entre outras pessoas:</span><span class="sxs-lookup"><span data-stu-id="bcbf1-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="bcbf1-111">A ligação de rede virtual do Olá VM tooa</span><span class="sxs-lookup"><span data-stu-id="bcbf1-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="bcbf1-112">Adicionar serviço de nuvem Olá VM tooan existente</span><span class="sxs-lookup"><span data-stu-id="bcbf1-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="bcbf1-113">Adicionar conta de armazenamento Olá VM tooan existente</span><span class="sxs-lookup"><span data-stu-id="bcbf1-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="bcbf1-114">Adicionar o conjunto de disponibilidade do Olá VM tooan ou localização</span><span class="sxs-lookup"><span data-stu-id="bcbf1-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcbf1-115">Se pretender que a sua toouse VM numa rede virtual para que possa ligar tooit diretamente pelo nome de anfitrião ou configurar ligações entre locais, certifique-se de que especificar uma rede virtual Olá quando criar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="bcbf1-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="bcbf1-116">Uma VM pode ser configurado toojoin uma rede virtual, apenas quando são criados Olá VM.</span><span class="sxs-lookup"><span data-stu-id="bcbf1-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="bcbf1-117">Para obter detalhes sobre redes virtuais, consulte [descrição geral de rede Virtual do Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="bcbf1-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="bcbf1-118">Como toocreate uma VM com Linux utilizando Olá modelo de implementação clássica</span><span class="sxs-lookup"><span data-stu-id="bcbf1-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

