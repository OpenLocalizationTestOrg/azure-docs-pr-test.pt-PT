---
title: "aaaTroubleshoot implementar problemas da máquina virtual com Linux no Azure | Microsoft Docs"
description: "Resolva problemas da máquina virtual Linux implementação no modelo de implementação Azurethe Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="657e5-103">Resolver problemas de máquina virtual Linux implementar no Azure</span><span class="sxs-lookup"><span data-stu-id="657e5-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="657e5-104">problemas de implementação de máquina virtual (VM) tootroubleshoot no Azure, reveja Olá [principais problemas](#top-issues) para falhas e resoluções comuns.</span><span class="sxs-lookup"><span data-stu-id="657e5-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="657e5-105">Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="657e5-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="657e5-106">Em alternativa, pode ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="657e5-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="657e5-107">Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporta**.</span><span class="sxs-lookup"><span data-stu-id="657e5-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="657e5-108">Problemas principais</span><span class="sxs-lookup"><span data-stu-id="657e5-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="657e5-109">Não é possível suportar cluster Olá Olá solicitado o tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="657e5-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="657e5-110">Repita o pedido de Olá utilizando um tamanho mais pequeno da VM.</span><span class="sxs-lookup"><span data-stu-id="657e5-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="657e5-111">Se hello o tamanho do Olá pedido que não é possível alterar a VM:</span><span class="sxs-lookup"><span data-stu-id="657e5-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="657e5-112">Pare todas as VMs de Olá no conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="657e5-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="657e5-113">Clique em **grupos de recursos** > o grupo de recursos > **recursos** > o conjunto de disponibilidade > **máquinas virtuais** > sua máquina virtual >  **Parar**.</span><span class="sxs-lookup"><span data-stu-id="657e5-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="657e5-114">Após todos os Olá parar de VMs, criar Olá VM tamanho Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="657e5-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="657e5-115">Iniciar Olá nova VM primeiro e, em seguida, selecione cada Olá parado VMs e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="657e5-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="657e5-116">Olá cluster não tem recursos gratuitos</span><span class="sxs-lookup"><span data-stu-id="657e5-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="657e5-117">Repita o pedido de Olá mais tarde.</span><span class="sxs-lookup"><span data-stu-id="657e5-117">Retry hello request later.</span></span>
- <span data-ttu-id="657e5-118">Se hello nova VM pode ser faz parte de uma disponibilidade diferente conjunto</span><span class="sxs-lookup"><span data-stu-id="657e5-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="657e5-119">Criar uma VM de um conjunto de disponibilidade diferente (no Olá mesma região).</span><span class="sxs-lookup"><span data-stu-id="657e5-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="657e5-120">Adicionar Olá nova VM toohello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="657e5-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="657e5-121">Como ativar o meu crédito mensal para Visual studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="657e5-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="657e5-122">tooactivate sua mensal de crédito, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="657e5-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="657e5-123">Por que motivo devo instalar não Olá GPU controlador para uma VM de NV Ubuntu?</span><span class="sxs-lookup"><span data-stu-id="657e5-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="657e5-124">Atualmente, o suporte de Linux GPU só está disponível em VMs do Azure NC Ubuntu Server 16.04 LTS a executar.</span><span class="sxs-lookup"><span data-stu-id="657e5-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="657e5-125">Para obter mais informações, consulte [configurar controladores GPU para VMs de série N executar Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="657e5-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="657e5-126">A minha controladores estão em falta para a minha VM do Linux série N</span><span class="sxs-lookup"><span data-stu-id="657e5-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="657e5-127">Controladores para as VMs baseadas em Linux estão localizadas [aqui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="657e5-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="657e5-128">Não é possível localizar a uma instância GPU na minha VM série N</span><span class="sxs-lookup"><span data-stu-id="657e5-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="657e5-129">tootake partido das capacidades GPU Olá das VMs do Azure de N série com o Windows Server 2016 ou o Windows Server 2012 R2, tem de instalar os controladores da placa NVIDIA em cada VM após a implementação.</span><span class="sxs-lookup"><span data-stu-id="657e5-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="657e5-130">As informações de configuração de controladores estão disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md) e [VMs com Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="657e5-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="657e5-131">Série N VMs está disponível na minha região?</span><span class="sxs-lookup"><span data-stu-id="657e5-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="657e5-132">Pode verificar a disponibilidade de Olá de Olá [produtos disponíveis por tabela de região](https://azure.microsoft.com/regions/services)e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="657e5-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="657e5-133">Não sou consegue toosee família de tamanho da VM que pretendo quando redimensionar a minha VM.</span><span class="sxs-lookup"><span data-stu-id="657e5-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="657e5-134">Quando uma VM está em execução, é implementado tooa servidor físico.</span><span class="sxs-lookup"><span data-stu-id="657e5-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="657e5-135">servidores físicos do Olá em regiões do Azure estão agrupados em clusters de hardware físico comum.</span><span class="sxs-lookup"><span data-stu-id="657e5-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="657e5-136">Redimensionar uma VM que necessita de clusters de hardware do Olá VM toobe movido toodifferent é diferente consoante o modelo de implementação foi utilizado toodeploy Olá VM.</span><span class="sxs-lookup"><span data-stu-id="657e5-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="657e5-137">VMs implementadas no modelo de implementação clássica, implementação de serviço de nuvem Olá tem de ser removidas e a implementar toochange Olá VMs tooa tamanho outra família de tamanho.</span><span class="sxs-lookup"><span data-stu-id="657e5-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="657e5-138">VMs implementadas no modelo de implementação do Resource Manager, tem de parar todas as VMs no conjunto antes de alterar o tamanho de Olá qualquer VM no conjunto de disponibilidade de Olá de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="657e5-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="657e5-139">Olá listado tamanho da VM não é suportado durante a implementação num conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="657e5-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="657e5-140">Escolha um tamanho que é suportado no cluster de conjunto de disponibilidade a Olá.</span><span class="sxs-lookup"><span data-stu-id="657e5-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="657e5-141">Recomenda-se ao criar que um conjunto de disponibilidade toochoose Olá maior tamanho da VM pensa que precisa e tem que ser a primeira toohello de implementação que do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="657e5-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="657e5-142">Quais as distribuições de Linux/as versões são suportadas no Azure?</span><span class="sxs-lookup"><span data-stu-id="657e5-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="657e5-143">Pode encontrar a lista de Olá em Linux no [Azure-Endorsed distribuições](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="657e5-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="657e5-144">Pode adicionar um conjunto de disponibilidade de tooan VMS clássicas existente?</span><span class="sxs-lookup"><span data-stu-id="657e5-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="657e5-145">Sim.</span><span class="sxs-lookup"><span data-stu-id="657e5-145">Yes.</span></span> <span data-ttu-id="657e5-146">Pode adicionar um existente clássico VM tooa novo ou existente do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="657e5-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="657e5-147">Para obter mais informações consulte [adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="657e5-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="657e5-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="657e5-148">Next steps</span></span>
<span data-ttu-id="657e5-149">Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="657e5-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="657e5-150">Em alternativa, pode ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="657e5-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="657e5-151">Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporta**.</span><span class="sxs-lookup"><span data-stu-id="657e5-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
