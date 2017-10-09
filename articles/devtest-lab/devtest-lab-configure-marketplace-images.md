---
title: "definições de imagens do Azure Marketplace aaaConfigure no Azure DevTest Labs | Microsoft Docs"
description: Configurar as imagens do Azure Marketplace podem ser utilizadas ao criar uma VM no Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="f06ec-103">Configurar definições de imagem do Azure Marketplace no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f06ec-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="f06ec-104">DevTest Labs suporta criar VMs baseadas nas imagens do Azure Marketplace, dependendo de como tiver configurado o Azure Marketplace imagens toobe utilizado no laboratório.</span><span class="sxs-lookup"><span data-stu-id="f06ec-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="f06ec-105">Este artigo mostra como toospecify que, se existirem, as imagens do Azure Marketplace podem ser utilizado ao criar as VMs num laboratório.</span><span class="sxs-lookup"><span data-stu-id="f06ec-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="f06ec-106">Isto garante que a sua equipa tiver apenas imagens do Marketplace toohello acesso que precisam.</span><span class="sxs-lookup"><span data-stu-id="f06ec-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="f06ec-107">Selecione as imagens do Azure Marketplace são permitidas quando criar uma VM</span><span class="sxs-lookup"><span data-stu-id="f06ec-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="f06ec-108">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f06ec-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f06ec-109">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="f06ec-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f06ec-110">Na lista de Olá de laboratórios, selecione laboratório pretendido Olá.</span><span class="sxs-lookup"><span data-stu-id="f06ec-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="f06ec-111">No painel do laboratório de Olá, selecione **políticas de configuração e**.</span><span class="sxs-lookup"><span data-stu-id="f06ec-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="f06ec-112">Do laboratório **políticas de configuração e** painel em **Bases de máquinas virtuais**, selecione **imagens do Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="f06ec-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="f06ec-113">Especifique se pretende que todos os Olá qualificado Azure Marketplace imagens toobe disponível para utilização como base de uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="f06ec-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="f06ec-114">Se selecionar **Sim**, em seguida, todos os Olá Azure Marketplace que cumpram Olá, todos os seguintes critérios são permitidas imagens na laboratório Olá:</span><span class="sxs-lookup"><span data-stu-id="f06ec-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="f06ec-115">imagem de Olá cria uma única VM, **e**</span><span class="sxs-lookup"><span data-stu-id="f06ec-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="f06ec-116">imagem de Olá utiliza VMs do Azure Resource Manager tooprovision, **e**</span><span class="sxs-lookup"><span data-stu-id="f06ec-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="f06ec-117">imagem de Olá não necessita de comprar um plano de licenciamento extra</span><span class="sxs-lookup"><span data-stu-id="f06ec-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="f06ec-118">Se quiser não toobe imagens permitido, ou se quiser toospecify que imagens podem ser utilizados, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="f06ec-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Opção tooallow todos os toobe de imagens do Marketplace utilizado como base imagens para VMs](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="f06ec-120">Se selecionar **não** toohello anterior passo, hello **permitidos imagens/selecionar todos os** caixa de verificação está ativada.</span><span class="sxs-lookup"><span data-stu-id="f06ec-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="f06ec-121">Pode utilizar esta opção juntamente com Olá pesquisa caixa tooquickly selecione ou desmarque todas as Olá itens apresentados na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="f06ec-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="f06ec-122">Selecione as imagens do Azure Marketplace Olá pretende tooallow para a criação de VM individualmente marcando a caixa de verificação correspondente de cada imagem.</span><span class="sxs-lookup"><span data-stu-id="f06ec-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="f06ec-123">Selecione nada Olá lista se não quiser tooallow qualquer toobe de imagens do Azure Marketplace utilizado no laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="f06ec-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Pode especificar as imagens do Azure Marketplace podem ser utilizadas como base imagens para VMs](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="f06ec-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f06ec-125">Next steps</span></span>
<span data-ttu-id="f06ec-126">Assim que tiver configurado como imagens do Azure Marketplace são permitidas quando criar uma VM, o passo seguinte Olá é demasiado[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="f06ec-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

