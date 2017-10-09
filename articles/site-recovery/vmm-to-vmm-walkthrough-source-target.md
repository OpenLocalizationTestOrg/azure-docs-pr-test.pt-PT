---
title: "aaaSet segurança Olá origem e de destino para o site secundário do tooa de replicação de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset origem Olá de segurança e de destino quando replicar VMs Hyper-V toosecondary VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="f9a54-103">Passo 6: Configurar a origem de replicação de Olá e de destino</span><span class="sxs-lookup"><span data-stu-id="f9a54-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="f9a54-104">Depois de criar dos serviços de recuperação cofre para Hyper-V replicação tooa site VMM secundário com [do Azure Site Recovery](site-recovery-overview.md), utilize este artigo tooset segurança origem Olá e localizações de replicação de destino.</span><span class="sxs-lookup"><span data-stu-id="f9a54-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="f9a54-105">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f9a54-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="f9a54-106">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="f9a54-106">Set up hello source environment</span></span>

<span data-ttu-id="f9a54-107">Instalar Olá fornecedor do Azure Site Recovery nos servidores do VMM, detetar e registar os servidores no Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="f9a54-108">Clique em **passo 1: preparar infraestrutura** > **origem**.</span><span class="sxs-lookup"><span data-stu-id="f9a54-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Configurar a origem](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="f9a54-110">No **preparar a origem**, clique em **+ VMM** tooadd um servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="f9a54-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Configurar a origem](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="f9a54-112">No **Adicionar servidor**, verifique se **servidor VMM do System Center** aparece no **tipo de servidor** e esse servidor do VMM Olá cumpre Olá [pré-requisitos](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="f9a54-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="f9a54-113">Transfira o ficheiro de instalação do fornecedor do Azure Site Recovery Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="f9a54-114">Transfira a chave de registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-114">Download hello registration key.</span></span> <span data-ttu-id="f9a54-115">Precisará disto quando executar a configuração.</span><span class="sxs-lookup"><span data-stu-id="f9a54-115">You need this when you run setup.</span></span> <span data-ttu-id="f9a54-116">chave de Olá é válido durante cinco dias depois de gerá-la.</span><span class="sxs-lookup"><span data-stu-id="f9a54-116">hello key is valid for five days after you generate it.</span></span>

    ![Configurar a origem](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="f9a54-118">Instale Olá fornecedor do Azure Site Recovery no servidor do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="f9a54-119">Não precisa de tooexplicitly instala nada nos servidores de anfitrião do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f9a54-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="f9a54-120">Instalar Olá Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="f9a54-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="f9a54-121">Execute o ficheiro de configuração do fornecedor de Olá em cada servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="f9a54-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="f9a54-122">Se o VMM for implementado num cluster, efetue Olá seguir Olá pela primeira vez que instala:</span><span class="sxs-lookup"><span data-stu-id="f9a54-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="f9a54-123">Instale o fornecedor de Olá num nó ativo e concluir o servidor do Olá instalação tooregister Olá VMM no Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="f9a54-124">Em seguida, instale o Olá fornecedor no Olá outros nós.</span><span class="sxs-lookup"><span data-stu-id="f9a54-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="f9a54-125">Os nós do cluster devem executar todos os Olá mesma versão do fornecedor de Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="f9a54-126">A configuração executa algumas verificações de pré-requisitos e os pedidos de serviço do VMM permissão toostop Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="f9a54-127">Olá serviço VMM será reiniciado automaticamente após a conclusão do programa de configuração.</span><span class="sxs-lookup"><span data-stu-id="f9a54-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="f9a54-128">Se instalar num VMM cluster, está a função de Cluster de Olá toostop pedido.</span><span class="sxs-lookup"><span data-stu-id="f9a54-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="f9a54-129">No **Microsoft Update**, pode optar toospecify que as atualizações do fornecedor são instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f9a54-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="f9a54-130">No **instalação**, aceite ou modifique a localização de instalação predefinida de Olá e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f9a54-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Localização de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="f9a54-132">Depois de concluída a instalação, clique em **registar** tooregister servidor Olá cofre Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Localização de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="f9a54-134">No **nome do cofre**, verifique o nome de Olá do Cofre de Olá no qual Olá servidor será registado.</span><span class="sxs-lookup"><span data-stu-id="f9a54-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="f9a54-135">Clique em *Seguinte*.</span><span class="sxs-lookup"><span data-stu-id="f9a54-135">Click *Next*.</span></span>

    ![Registo do servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="f9a54-137">No **ligação à Internet**, especifique como o fornecedor de Olá em execução no servidor do VMM Olá se liga a tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f9a54-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Definições da Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="f9a54-139">Pode especificar esse fornecedor Olá deve ligar diretamente toohello internet, ou através de um proxy.</span><span class="sxs-lookup"><span data-stu-id="f9a54-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="f9a54-140">Especifique as definições de proxy, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f9a54-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="f9a54-141">Se utilizar um proxy, uma conta RunAs do VMM (DRAProxyAccount) é automaticamente criada utilizando Olá especificada credenciais de proxy.</span><span class="sxs-lookup"><span data-stu-id="f9a54-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="f9a54-142">Configure o servidor de proxy de Olá, para que esta conta pode autenticar com êxito.</span><span class="sxs-lookup"><span data-stu-id="f9a54-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="f9a54-143">Olá definições de conta RunAs podem ser modificadas na consola do VMM Olá > **definições** > **segurança** > **contas Run as**.</span><span class="sxs-lookup"><span data-stu-id="f9a54-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="f9a54-144">Reinicie Olá VMM serviço tooupdate é alterada.</span><span class="sxs-lookup"><span data-stu-id="f9a54-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="f9a54-145">No **chave de registo**, selecione chave Olá que transferido a partir do Azure Site Recovery e copiou toohello o servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="f9a54-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="f9a54-146">definição de encriptação de Olá só é utilizada quando replicar VMs Hyper-V no tooAzure de nuvens do VMM.</span><span class="sxs-lookup"><span data-stu-id="f9a54-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="f9a54-147">Se estiver a replicar tooa site secundário não é utilizado.</span><span class="sxs-lookup"><span data-stu-id="f9a54-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="f9a54-148">No **nome do servidor**, especifique o servidor de nome amigável tooidentify Olá VMM no Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="f9a54-149">Numa configuração de cluster especifique o nome de função de cluster do Olá VMM.</span><span class="sxs-lookup"><span data-stu-id="f9a54-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="f9a54-150">No **sincronizar metadados da nuvem**, selecione se pretende toosynchronize metadados para todas as nuvens no servidor do VMM Olá Vault Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="f9a54-151">Esta ação só deverá toohappen uma vez em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="f9a54-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="f9a54-152">Se não quiser toosynchronize todas as nuvens, pode deixar esta definição desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem de Olá na consola do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="f9a54-153">Clique em **seguinte** processo de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f9a54-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="f9a54-154">Após o registo, os metadados hello do servidor do VMM são obtidos pelo Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f9a54-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="f9a54-155">servidor de Olá é apresentado no Olá **servidores VMM** separador Olá **servidores** página no Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="f9a54-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Servidor](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="f9a54-157">Depois do servidor de Olá está disponível na consola da recuperação de sites de Olá, no **origem** > **preparar a origem** selecionar servidor do VMM Olá e nuvem de Olá selecione em que Olá Hyper-V anfitrião se encontra.</span><span class="sxs-lookup"><span data-stu-id="f9a54-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="f9a54-158">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9a54-158">Then click **OK**.</span></span>

<span data-ttu-id="f9a54-159">Também pode instalar o fornecedor de Olá Olá linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="f9a54-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="f9a54-160">Configurar o ambiente de destino Olá</span><span class="sxs-lookup"><span data-stu-id="f9a54-160">Set up hello target environment</span></span>

<span data-ttu-id="f9a54-161">Selecione o servidor do VMM de destino de Olá e na nuvem:</span><span class="sxs-lookup"><span data-stu-id="f9a54-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="f9a54-162">Clique em **preparar a infraestrutura** > **destino**e o servidor VMM de destino selecione Olá pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="f9a54-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="f9a54-163">Serão apresentadas nuvens no servidor de Olá que são sincronizadas com a recuperação de sites.</span><span class="sxs-lookup"><span data-stu-id="f9a54-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="f9a54-164">Selecione a nuvem de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="f9a54-164">Select hello target cloud.</span></span>

   ![destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="f9a54-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f9a54-166">Next steps</span></span>

<span data-ttu-id="f9a54-167">Aceda demasiado[passo 7: configurar o mapeamento da rede](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="f9a54-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
