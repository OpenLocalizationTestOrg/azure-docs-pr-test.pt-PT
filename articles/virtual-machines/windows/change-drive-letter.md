---
title: "Certifique-Olá unidade d: de uma VM de um disco de dados | Microsoft Docs"
description: "Descreve como unidade de toochange letras de uma VM do Windows para que possa utilizar unidade de d: Olá como uma unidade de dados."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="5c155-103">Utilizar a unidade de d: Olá como uma unidade de dados numa VM do Windows</span><span class="sxs-lookup"><span data-stu-id="5c155-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="5c155-104">Se a sua aplicação tiver toouse Olá dados de toostore de unidade D, siga estas instruções toouse uma letra de unidade diferente para o disco temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="5c155-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="5c155-105">Nunca utilize Olá disco temporário toostore dados que precisa de tookeep.</span><span class="sxs-lookup"><span data-stu-id="5c155-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="5c155-106">Se redimensionar ou **paragem (Deallocate)** uma máquina virtual, isto pode acionar colocação Olá tooa de máquina virtual hipervisor novo.</span><span class="sxs-lookup"><span data-stu-id="5c155-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="5c155-107">Um evento de manutenção planeada ou também pode acionar Esta colocação.</span><span class="sxs-lookup"><span data-stu-id="5c155-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="5c155-108">Neste cenário, o disco temporário Olá será toohello reatribuídas primeira letra de unidade disponível.</span><span class="sxs-lookup"><span data-stu-id="5c155-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="5c155-109">Se tiver uma aplicação que necessite especificamente de unidade de d: Olá, terá de toofollow estes passos tootemporarily mover Olá pagefile.sys, anexar um disco de dados nova e atribua-letra Olá D e, em seguida, mover Olá pagefile.sys fazer uma cópia de unidade temporária toohello.</span><span class="sxs-lookup"><span data-stu-id="5c155-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="5c155-110">Depois de concluído, Azure não entrarão novamente Olá d: se Olá VM move hipervisor diferentes tooa.</span><span class="sxs-lookup"><span data-stu-id="5c155-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="5c155-111">Para obter mais informações sobre como o Azure utiliza disco temporário Olá, consulte [compreender unidade temporária de Olá em do Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="5c155-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="5c155-112">Anexar o disco de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="5c155-112">Attach hello data disk</span></span>
<span data-ttu-id="5c155-113">Em primeiro lugar, irá precisar de máquina virtual de toohello disco tooattach Olá dados.</span><span class="sxs-lookup"><span data-stu-id="5c155-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="5c155-114">toodo este através do portal Olá, consulte [como tooattach um dados geridos em disco no portal do Azure de Olá](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c155-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="5c155-115">Mover temporariamente pagefile.sys tooC unidade</span><span class="sxs-lookup"><span data-stu-id="5c155-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="5c155-116">Ligar a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="5c155-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="5c155-117">Contexto Olá **iniciar** menu e selecione **sistema**.</span><span class="sxs-lookup"><span data-stu-id="5c155-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="5c155-118">No menu da esquerda Olá, selecione **definições de sistema avançadas**.</span><span class="sxs-lookup"><span data-stu-id="5c155-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="5c155-119">No Olá **desempenho** secção, selecione **definições**.</span><span class="sxs-lookup"><span data-stu-id="5c155-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="5c155-120">Selecione Olá **avançadas** separador.</span><span class="sxs-lookup"><span data-stu-id="5c155-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="5c155-121">No Olá **Memória Virtual** secção, selecione **alteração**.</span><span class="sxs-lookup"><span data-stu-id="5c155-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="5c155-122">Selecione Olá **C** unidade e, em seguida, clique em **sistema gerido tamanho** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="5c155-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="5c155-123">Selecione Olá **D** unidade e, em seguida, clique em **nenhum ficheiro de paginação** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="5c155-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="5c155-124">Clique em aplicar.</span><span class="sxs-lookup"><span data-stu-id="5c155-124">Click Apply.</span></span> <span data-ttu-id="5c155-125">Irá receber um aviso que nesse computador Olá tem toobe reiniciado para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="5c155-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="5c155-126">Reinicie a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c155-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="5c155-127">Alterar as letras de unidade de Olá</span><span class="sxs-lookup"><span data-stu-id="5c155-127">Change hello drive letters</span></span>
1. <span data-ttu-id="5c155-128">Uma vez Olá VM reinícios, iniciar sessão novamente toohello VM.</span><span class="sxs-lookup"><span data-stu-id="5c155-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="5c155-129">Clique em Olá **iniciar** menu e tipo **diskmgmt.msc** e prima Enter.</span><span class="sxs-lookup"><span data-stu-id="5c155-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="5c155-130">Gestão de discos será iniciado.</span><span class="sxs-lookup"><span data-stu-id="5c155-130">Disk Management will start.</span></span>
3. <span data-ttu-id="5c155-131">Clique com o botão direito no **D**, Olá unidade de armazenamento temporário e selecione **letra de unidade de alteração e caminhos**.</span><span class="sxs-lookup"><span data-stu-id="5c155-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="5c155-132">Em letra de unidade, selecione uma nova unidade, tais como **T** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c155-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="5c155-133">Faça duplo clique no disco de dados de Olá e selecione **letra de unidade de alteração e caminhos**.</span><span class="sxs-lookup"><span data-stu-id="5c155-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="5c155-134">Em letra de unidade, selecione a unidade **D** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c155-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="5c155-135">Mover a unidade de armazenamento temporário de back-toohello pagefile.sys</span><span class="sxs-lookup"><span data-stu-id="5c155-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="5c155-136">Contexto Olá **iniciar** menu e selecione **sistema**</span><span class="sxs-lookup"><span data-stu-id="5c155-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="5c155-137">No menu da esquerda Olá, selecione **definições de sistema avançadas**.</span><span class="sxs-lookup"><span data-stu-id="5c155-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="5c155-138">No Olá **desempenho** secção, selecione **definições**.</span><span class="sxs-lookup"><span data-stu-id="5c155-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="5c155-139">Selecione Olá **avançadas** separador.</span><span class="sxs-lookup"><span data-stu-id="5c155-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="5c155-140">No Olá **Memória Virtual** secção, selecione **alteração**.</span><span class="sxs-lookup"><span data-stu-id="5c155-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="5c155-141">Selecione a unidade de Olá SO **C** e clique em **nenhum ficheiro de paginação** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="5c155-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="5c155-142">Selecione a unidade de armazenamento temporário de Olá **T** e, em seguida, clique em **sistema gerido tamanho** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="5c155-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="5c155-143">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5c155-143">Click **Apply**.</span></span> <span data-ttu-id="5c155-144">Irá receber um aviso que nesse computador Olá tem toobe reiniciado para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="5c155-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="5c155-145">Reinicie a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c155-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c155-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5c155-146">Next steps</span></span>
* <span data-ttu-id="5c155-147">Pode aumentar a máquina virtual do Olá armazenamento disponível tooyour por [anexar um disco de dados adicionais](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c155-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

