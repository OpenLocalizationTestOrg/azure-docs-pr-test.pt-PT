---
title: "máquinas virtuais de aaaManage utilizando Olá Explorador do Azure para o Eclipse | Microsoft Docs"
description: "Saiba como toomanage as máquinas virtuais do Azure utilizando Olá Explorador do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="5651d-103">Gerir máquinas virtuais utilizando Olá Explorador do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="5651d-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="5651d-104">Olá Explorador do Azure, o que faz parte do Olá Toolkit do Azure para o Eclipse, fornece aos programadores de Java com uma solução fácil de utilizar para gerir máquinas virtuais da conta do Azure a partir da ambiente de desenvolvimento integrado do Olá Eclipse (IDE).</span><span class="sxs-lookup"><span data-stu-id="5651d-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="5651d-105">Criar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="5651d-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="5651d-106">toocreate uma máquina virtual utilizando o Explorador do Azure, de Olá Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="5651d-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="5651d-107">Inicie sessão tooyour conta do Azure utilizando Olá [instruções de início de sessão para Olá Toolkit do Azure para o Eclipse].</span><span class="sxs-lookup"><span data-stu-id="5651d-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="5651d-108">No Olá **Explorador do Azure** ver, expanda Olá **Azure** nó, clique com botão direito **máquinas virtuais**e, em seguida, clique em **criar VM**.</span><span class="sxs-lookup"><span data-stu-id="5651d-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="5651d-109">![Olá comando Criar VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="5651d-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="5651d-110">Olá **Criar Nova Máquina Virtual** é aberto o assistente.</span><span class="sxs-lookup"><span data-stu-id="5651d-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="5651d-111">No Olá **escolha uma subscrição** janela, selecione a sua subscrição e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5651d-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Olá, escolha uma janela de subscrição][CR02]

4. <span data-ttu-id="5651d-113">No Olá **selecionar uma imagem de Máquina Virtual** janela, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5651d-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="5651d-114">**Localização**: Especifica onde será criada a máquina virtual (por exemplo, *EUA oeste*).</span><span class="sxs-lookup"><span data-stu-id="5651d-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="5651d-115">**Publicador**: Especifica o publicador de Olá que criou a imagem de Olá utilizará toocreate a máquina virtual (por exemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="5651d-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="5651d-116">**Oferecer**: Especifica a máquina virtual de Olá oferta toouse do publicador selecionado Olá (por exemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="5651d-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="5651d-117">**SKU**: Especifica Olá stockkeeping unidade (SKU) toouse da oferta selecionado Olá (por exemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="5651d-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="5651d-118">**Versão #**: Especifica a versão de Olá selecionado SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="5651d-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Olá, selecione um período de imagem de Máquina Virtual][CR03]

5. <span data-ttu-id="5651d-120">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5651d-120">Click **Next**.</span></span>

6. <span data-ttu-id="5651d-121">No Olá **definições básicas de Máquina Virtual** janela, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5651d-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="5651d-122">**Nome da máquina virtual**: Especifica o nome de Olá para a nova máquina virtual, que tem de começar com uma letra e conter apenas letras, números e hífenes.</span><span class="sxs-lookup"><span data-stu-id="5651d-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="5651d-123">**Tamanho**: Especifica o número de Olá de núcleos e tooallocate de memória para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5651d-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="5651d-124">**Nome de utilizador**: Especifica Olá toocreate de conta de administrador para gerir a sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5651d-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="5651d-125">**Palavra-passe** e **confirmar**: Especifica Olá palavra-passe da sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="5651d-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![janela de definições da Máquina Virtual básico Olá][CR04]

7. <span data-ttu-id="5651d-127">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5651d-127">Click **Next**.</span></span>

8. <span data-ttu-id="5651d-128">No Olá **criar nova conta do Storage** janela, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5651d-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="5651d-129">**Grupo de recursos**: Especifica o grupo de recursos de Olá para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5651d-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="5651d-130">Selecione uma das seguintes opções de Olá:</span><span class="sxs-lookup"><span data-stu-id="5651d-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="5651d-131">**Criar um novo**: Especifica que pretende toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5651d-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="5651d-132">**Utilizar existentes**: Especifica que pretende tooselect um grupo de recursos que já está associado a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5651d-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![caixa de diálogo Criar nova conta do Storage Olá][CR05]

   * <span data-ttu-id="5651d-134">**Conta de armazenamento**: Especifica Olá toouse de conta de armazenamento para armazenar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5651d-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="5651d-135">Pode utilizar uma conta de armazenamento existente ou crie uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="5651d-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="5651d-136">**Rede virtual** e **sub-rede**: Especifica a rede virtual Olá e a sub-rede que a máquina virtual ligará.</span><span class="sxs-lookup"><span data-stu-id="5651d-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="5651d-137">Pode utilizar uma rede existente e sub-rede ou pode criar uma nova rede e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5651d-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="5651d-138">Se selecionar **criar nova**, Olá seguintes da caixa de diálogo é apresentada:</span><span class="sxs-lookup"><span data-stu-id="5651d-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![caixa de diálogo Criar nova rede Virtual Olá][CR06]

9. <span data-ttu-id="5651d-140">No Olá **recursos associados** janela, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5651d-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="5651d-141">**Endereço IP público**: Especifica um endereço IP de acesso externo para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5651d-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="5651d-142">Pode escolher toocreate um novo endereço IP ou, se a máquina virtual não tiver um endereço IP público, pode selecionar **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="5651d-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="5651d-143">**Grupo de segurança de rede**: Especifica uma firewall de rede opcional para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5651d-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="5651d-144">Pode selecionar uma firewall existente ou, se a máquina virtual não utilizará uma firewall de rede, pode selecionar **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="5651d-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="5651d-145">**Conjunto de disponibilidade**: Especifica um opcional conjunto de disponibilidade que a máquina virtual podem pertencer a.</span><span class="sxs-lookup"><span data-stu-id="5651d-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="5651d-146">Pode selecionar um conjunto de disponibilidade existente ou criar um novo conjunto de disponibilidade ou, se a máquina virtual não irão pertencer tooan conjunto de disponibilidade, pode selecionar **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="5651d-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![janela de recursos associados Olá][CR07]

9. <span data-ttu-id="5651d-148">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="5651d-148">Click **Finish**.</span></span>  
  <span data-ttu-id="5651d-149">A nova máquina virtual é apresentada na janela de ferramenta Olá Explorador do Azure.</span><span class="sxs-lookup"><span data-stu-id="5651d-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nova Máquina Virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="5651d-151">Reiniciar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="5651d-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="5651d-152">toorestart uma máquina virtual utilizando Olá Explorador do Azure no Eclipse, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="5651d-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="5651d-153">No Olá **Explorador do Azure** ver, faça duplo clique Olá máquina e, em seguida, selecione **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="5651d-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Olá comandos de reinício de máquinas virtuais][RE01]

2. <span data-ttu-id="5651d-155">Na janela de confirmação de Olá, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5651d-155">In hello confirmation window, click **Yes**.</span></span>

   ![janela de confirmação de reinício de Olá][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="5651d-157">Encerrar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="5651d-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="5651d-158">tooshut para baixo de uma máquina virtual em execução utilizando Olá Explorador do Azure no Eclipse, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="5651d-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="5651d-159">No Olá **Explorador do Azure** ver, faça duplo clique Olá máquina e, em seguida, selecione **encerramento**.</span><span class="sxs-lookup"><span data-stu-id="5651d-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Olá comandos de encerramento da máquina virtual][SH01]

2. <span data-ttu-id="5651d-161">Na janela de confirmação de Olá, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5651d-161">In hello confirmation window, click **Yes**.</span></span>

   ![janela de confirmação de encerramento da máquina virtual de Olá][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="5651d-163">Eliminar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="5651d-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="5651d-164">toodelete uma máquina virtual utilizando Olá Explorador do Azure no Eclipse, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="5651d-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="5651d-165">No Olá **Explorador do Azure** ver, faça duplo clique Olá máquina e, em seguida, selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="5651d-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![Olá comando de eliminação da máquina virtual][DE01]

2. <span data-ttu-id="5651d-167">Na janela de confirmação de Olá, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5651d-167">In hello confirmation window, click **Yes**.</span></span>

   ![janela de confirmação de eliminação da máquina virtual de Olá][DE02]

## <a name="next-steps"></a><span data-ttu-id="5651d-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5651d-169">Next steps</span></span>
<span data-ttu-id="5651d-170">Para obter mais informações sobre os tamanhos de máquina virtual do Azure e preços, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="5651d-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="5651d-171">Tamanhos de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5651d-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="5651d-172">[Tamanhos de máquinas virtuais do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="5651d-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="5651d-173">[Tamanhos de máquinas virtuais do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="5651d-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="5651d-174">Preços de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5651d-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="5651d-175">[Preços de máquina virtual do Windows]</span><span class="sxs-lookup"><span data-stu-id="5651d-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="5651d-176">[Preços de máquina virtual do Linux]</span><span class="sxs-lookup"><span data-stu-id="5651d-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="5651d-177">Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="5651d-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="5651d-178">[Toolkit do Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5651d-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5651d-179">[Novidades no Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5651d-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5651d-180">[Instalar Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5651d-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5651d-181">[instruções de início de sessão para Olá Toolkit do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5651d-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5651d-182">[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5651d-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="5651d-183">[Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5651d-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5651d-184">[Novidades no Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5651d-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5651d-185">[Instalar Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5651d-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5651d-186">[Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5651d-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5651d-187">[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5651d-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="5651d-188">Para obter mais informações sobre como utilizar o Azure com Java, consulte [Centro de programadores Java do Azure] e [ferramentas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5651d-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Toolkit do Azure do Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalar Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instruções de início de sessão para Olá Toolkit do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamanhos de máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos de máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquina virtual do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquina virtual do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
