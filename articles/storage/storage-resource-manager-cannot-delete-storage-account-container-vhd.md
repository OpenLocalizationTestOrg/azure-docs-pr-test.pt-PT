---
title: erros de aaaTroubleshoot ao eliminar as contas do storage do Azure, contentores ou VHDs | Microsoft Docs
description: Resolver erros ao eliminar as contas do storage do Azure, contentores ou VHDs
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="65447-103">Resolver erros ao eliminar as contas do storage do Azure, contentores ou VHDs</span><span class="sxs-lookup"><span data-stu-id="65447-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="65447-104">Poderá receber erros quando tenta toodelete uma conta do storage do Azure, um contentor ou um disco rígido virtual (VHD) em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65447-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="65447-105">Este artigo fornece resolução orientações toohelp resolve Olá problema numa implementação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65447-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="65447-106">Se este artigo não resolver o problema do Azure, visite Olá fóruns do Azure no [MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="65447-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="65447-107">Pode publicar o seu problema nestes fóruns ou too@AzureSupport no Twitter.</span><span class="sxs-lookup"><span data-stu-id="65447-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="65447-108">Além disso, pode ficheiro um pedido de suporte do Azure ao selecionar **obter suporte** no Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="65447-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="65447-109">Sintomas</span><span class="sxs-lookup"><span data-stu-id="65447-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="65447-110">Cenário 1</span><span class="sxs-lookup"><span data-stu-id="65447-110">Scenario 1</span></span>
<span data-ttu-id="65447-111">Quando tenta toodelete um VHD numa conta do storage numa implementação do Resource Manager, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="65447-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="65447-112">**Falha ao blob toodelete 'vhds/BlobName.vhd'. Erro: Não existe atualmente uma concessão no blob Olá e não foi especificado nenhum ID de concessão no pedido de Olá.**</span><span class="sxs-lookup"><span data-stu-id="65447-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="65447-113">Este problema pode ocorrer porque uma máquina virtual (VM) tem uma concessão no Olá VHD que está a tentar toodelete.</span><span class="sxs-lookup"><span data-stu-id="65447-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="65447-114">Cenário 2</span><span class="sxs-lookup"><span data-stu-id="65447-114">Scenario 2</span></span>
<span data-ttu-id="65447-115">Quando tenta toodelete um contentor numa conta do storage numa implementação do Resource Manager, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="65447-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="65447-116">**Falha ao contentor de armazenamento toodelete 'vhds'. Erro: Não existe atualmente uma concessão no contentor de Olá e não foi especificado nenhum ID de concessão no pedido de Olá.**</span><span class="sxs-lookup"><span data-stu-id="65447-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="65447-117">Este problema pode ocorrer porque o contentor de Olá tem uma imagem VHD que estiver bloqueada no estado de concessão de Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="65447-118">Cenário 3</span><span class="sxs-lookup"><span data-stu-id="65447-118">Scenario 3</span></span>
<span data-ttu-id="65447-119">Quando tenta toodelete uma conta de armazenamento numa implementação do Resource Manager, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="65447-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="65447-120">**Falha na conta de armazenamento toodelete 'StorageAccountName'. Erro: não é possível eliminar a conta de armazenamento Olá de devido tooits artefactos estão a ser utilizado.**</span><span class="sxs-lookup"><span data-stu-id="65447-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="65447-121">Este problema pode ocorrer porque a conta de armazenamento Olá contém uma imagem VHD que está no estado de concessão de Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="65447-122">Solução</span><span class="sxs-lookup"><span data-stu-id="65447-122">Solution</span></span> 
<span data-ttu-id="65447-123">tooresolve estes problemas, tem de identificar Olá VHD que está a causar erro Olá e Olá associado à VM.</span><span class="sxs-lookup"><span data-stu-id="65447-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="65447-124">Em seguida, anular a exposição Olá VHD de Olá VM (para os discos de dados) ou eliminar Olá VM que está a utilizar Olá VHD (discos do SO).</span><span class="sxs-lookup"><span data-stu-id="65447-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="65447-125">Isto remove a concessão de Olá Olá VHD e permite que toobe eliminado.</span><span class="sxs-lookup"><span data-stu-id="65447-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="65447-126">toodo, utilize um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="65447-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="65447-127">Método 1 - utilizar o Explorador de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="65447-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="65447-128">Passo 1 identificar Olá VHD que impedem a eliminação da conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="65447-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="65447-129">Ao eliminar a conta de armazenamento Olá, receberá uma caixa de diálogo de mensagem, tais como o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="65447-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![mensagem ao eliminar a conta de armazenamento Olá](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="65447-131">Verifique Olá **disco URL** conta de armazenamento de Olá tooidentify e Olá VHD que impede a eliminar a conta de armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="65447-132">No seguinte exemplo de Olá, cadeia antes de Olá ". w" é o nome de conta do storage Olá, não sendo "SCCM2012-2015-08-28.vhd" nome do VHD Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="65447-133">Olá de eliminação do passo 2 VHD utilizando o Explorador de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="65447-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="65447-134">Transferir e instalar versão mais recente do Olá do [Explorador de armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="65447-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="65447-135">Esta ferramenta é uma aplicação autónoma da Microsoft permite-lhe tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="65447-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="65447-136">Abra o Explorador de armazenamento do Azure, selecione</span><span class="sxs-lookup"><span data-stu-id="65447-136">Open Azure Storage Explorer, select</span></span> ![ícone de conta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="65447-138">na barra de esquerdo Olá, selecione o seu ambiente do Azure e, em seguida, inicie sessão.</span><span class="sxs-lookup"><span data-stu-id="65447-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="65447-139">Selecione todas as subscrições ou subscrição Olá que contém a conta de armazenamento de Olá que pretende toodelete.</span><span class="sxs-lookup"><span data-stu-id="65447-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![Adicionar subscrição](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="65447-141">Aceda a conta de armazenamento de toohello que foi obtidas Olá disco URL anterior, selecione Olá **contentores de BLOBs** > **vhds** e procure Olá VHD que impede a conta de armazenamento de Olá de eliminação.</span><span class="sxs-lookup"><span data-stu-id="65447-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="65447-142">Se for encontrado Olá VHD, verifique Olá **nome da VM** Olá toofind de coluna VM que está a utilizar este VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![Verificação de vm](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="65447-144">Remova concessão Olá Olá VHD utilizando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="65447-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="65447-145">Para obter mais informações, consulte [concessão de Olá remover de Olá VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="65447-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="65447-146">Aceda toohello Explorador de armazenamento do Azure, clique com o botão direito Olá VHD e, em seguida, selecione eliminar.</span><span class="sxs-lookup"><span data-stu-id="65447-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="65447-147">Elimine conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="65447-148">Método 2 - utiliza o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="65447-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="65447-149">Passo 1: Identificar Olá VHD que impedem a eliminação da conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="65447-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="65447-150">Ao eliminar a conta de armazenamento Olá, receberá uma caixa de diálogo de mensagem, tais como o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="65447-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![mensagem ao eliminar a conta de armazenamento Olá](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="65447-152">Verifique Olá **disco URL** conta de armazenamento de Olá tooidentify e Olá VHD que impede a eliminar a conta de armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="65447-153">No seguinte exemplo de Olá, cadeia antes de Olá ". w" é o nome de conta do storage Olá, não sendo "SCCM2012-2015-08-28.vhd" nome do VHD Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="65447-154">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65447-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="65447-155">No menu do Hub de Olá, selecione **todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="65447-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="65447-156">Aceda a conta de armazenamento toohello e, em seguida, selecione **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="65447-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Captura de ecrã do portal de Olá, com a conta de armazenamento de Olá e contentor de "vhds" Olá realçado](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="65447-158">Localize Olá VHD que são obtidos a partir do URL de disco Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="65447-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="65447-159">Em seguida, determinar qual a VM está a utilizar Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="65447-160">Normalmente, pode determinar que VM contém Olá VHD ao verificar o nome do Olá VHD:</span><span class="sxs-lookup"><span data-stu-id="65447-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="65447-161">VM no modelo de programação do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65447-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="65447-162">Discos de SO, geralmente, siga esta Convenção de nomenclatura: VMName-aaaa-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="65447-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="65447-163">Os discos de dados, geralmente, siga esta Convenção de nomenclatura: VMName-aaaa-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="65447-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="65447-164">VM no modelo de programação clássico</span><span class="sxs-lookup"><span data-stu-id="65447-164">VM in Classic development model</span></span>

   * <span data-ttu-id="65447-165">Discos de SO, geralmente, siga esta Convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="65447-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="65447-166">Os discos de dados, geralmente, siga esta Convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="65447-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="65447-167">Passo 2: Remover concessão Olá Olá VHD</span><span class="sxs-lookup"><span data-stu-id="65447-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="65447-168">[Remover a concessão de Olá Olá VHD](#remove-the-lease-from-the-vhd)e, em seguida, elimine a conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="65447-169">O que é uma concessão?</span><span class="sxs-lookup"><span data-stu-id="65447-169">What is a lease?</span></span>
<span data-ttu-id="65447-170">Uma concessão é um bloqueio que pode ser utilizados toocontrol-BLOBs acesso tooa (por exemplo, um VHD).</span><span class="sxs-lookup"><span data-stu-id="65447-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="65447-171">Quando um blob é nos concessionados, apenas os proprietários de Olá de concessão de Olá podem aceder a BLOBs Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="65447-172">Uma concessão é importante para Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="65447-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="65447-173">Impede a danos nos dados se proprietários vários tente toowrite toohello mesma parte do blob de Olá na Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="65447-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="65447-174">Impede que o blob de Olá que está a ser eliminado se algo está ativamente a ser utilizado (por exemplo, uma VM).</span><span class="sxs-lookup"><span data-stu-id="65447-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="65447-175">Impede que conta de armazenamento Olá que está a ser eliminado se algo está ativamente a ser utilizado (por exemplo, uma VM).</span><span class="sxs-lookup"><span data-stu-id="65447-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="65447-176">Remover a concessão de Olá Olá VHD</span><span class="sxs-lookup"><span data-stu-id="65447-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="65447-177">Se Olá VHD é um disco de SO, tem de eliminar concessão do Olá VM tooremove Olá:</span><span class="sxs-lookup"><span data-stu-id="65447-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="65447-178">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65447-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="65447-179">No Olá **Hub** menu, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="65447-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="65447-180">Selecione Olá VM que contém uma concessão no Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="65447-181">Certifique-se de que nada está ativamente a utilizar máquinas virtuais de Olá e que que já não precisa de Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65447-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="65447-182">Na parte superior de Olá de Olá **detalhes VM** painel, selecione **eliminar**e, em seguida, clique em **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="65447-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="65447-183">Olá VM deve ser eliminado, mas pode ser mantida Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="65447-184">No entanto, Olá VHD já não deve ter uma concessão no mesmo.</span><span class="sxs-lookup"><span data-stu-id="65447-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="65447-185">Pode demorar alguns minutos para Olá concessão toobe lançada.</span><span class="sxs-lookup"><span data-stu-id="65447-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="65447-186">tooverify Olá concessão for lançada, visite demasiado**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**.</span><span class="sxs-lookup"><span data-stu-id="65447-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="65447-187">No Olá **Blob propriedades** painel, Olá **estado de concessão** o valor deve ser **Unlocked**.</span><span class="sxs-lookup"><span data-stu-id="65447-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="65447-188">Se Olá VHD for um disco de dados, desanexe Olá VHD de concessão de Olá Olá VM tooremove:</span><span class="sxs-lookup"><span data-stu-id="65447-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="65447-189">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65447-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="65447-190">No Olá **Hub** menu, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="65447-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="65447-191">Selecione Olá VM que contém uma concessão no Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="65447-192">Selecione **discos** no Olá **detalhes VM** painel.</span><span class="sxs-lookup"><span data-stu-id="65447-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="65447-193">Selecione o disco de dados de Olá que contém uma concessão no Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="65447-194">Pode determinar que esteja anexado VHD no disco Olá verificando Olá URL de Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="65447-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="65447-195">Determine com certainty nada ativamente está a utilizar o disco de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="65447-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="65447-196">Clique em **anulação de exposições** no Olá **disco detalhes** painel.</span><span class="sxs-lookup"><span data-stu-id="65447-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="65447-197">disco Olá agora deve ser desligado do Olá VM e Olá VHD já não deve ter uma concessão no mesmo.</span><span class="sxs-lookup"><span data-stu-id="65447-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="65447-198">Pode demorar alguns minutos para Olá concessão toobe lançada.</span><span class="sxs-lookup"><span data-stu-id="65447-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="65447-199">foi lançado tooverify Olá concessão, visite demasiado**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**.</span><span class="sxs-lookup"><span data-stu-id="65447-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="65447-200">No Olá **Blob propriedades** painel, Olá **estado de concessão** o valor deve ser **Unlocked**.</span><span class="sxs-lookup"><span data-stu-id="65447-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65447-201">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="65447-201">Next steps</span></span>
* [<span data-ttu-id="65447-202">Eliminar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="65447-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="65447-203">Como toobreak Olá bloqueado concessão do blob storage no Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="65447-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
