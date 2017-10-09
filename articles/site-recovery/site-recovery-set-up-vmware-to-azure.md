---
title: "Configurar o ambiente de origem Olá (VMware tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local VMware virtual a replicar máquinas tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="f1b81-103">Configurar o ambiente de origem Olá (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="f1b81-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1b81-104">TooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="f1b81-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="f1b81-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="f1b81-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="f1b81-106">Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local virtual a replicar máquinas em execução no VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f1b81-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1b81-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f1b81-107">Prerequisites</span></span>

<span data-ttu-id="f1b81-108">artigo de Olá pressupõe que já criou:</span><span class="sxs-lookup"><span data-stu-id="f1b81-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="f1b81-109">Um cofre dos serviços de recuperação no Olá [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="f1b81-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="f1b81-110">Uma conta dedicada o VMware vcenter que podem ser utilizadas para [a deteção automática](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f1b81-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="f1b81-111">Uma máquina virtual no servidor de configuração que tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="f1b81-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="f1b81-112">Requisitos mínimos do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="f1b81-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="f1b81-113">software de servidor de configuração de Olá deve ser implementado numa máquina virtual VMware altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="f1b81-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="f1b81-114">Olá, a tabela seguinte lista Olá mínimos de hardware, software e requisitos de rede para um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="f1b81-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="f1b81-115">Servidores proxy baseado em HTTPS não são suportadas pelo servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1b81-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="f1b81-116">Escolha os seus objetivos de proteção</span><span class="sxs-lookup"><span data-stu-id="f1b81-116">Choose your protection goals</span></span>

1. <span data-ttu-id="f1b81-117">Olá portal do Azure, aceda toohello **dos serviços de recuperação** painel do cofre e selecione o cofre.</span><span class="sxs-lookup"><span data-stu-id="f1b81-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="f1b81-118">No menu de recursos de Olá do Cofre de Olá, aceda demasiado**introdução** > **recuperação de Site** > **passo 1: preparar a infraestrutura**  >  **Objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="f1b81-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Selecione os objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="f1b81-120">No **objetivo de proteção**, selecione **tooAzure**e escolha **Sim, com o VMware vSphere hipervisor**.</span><span class="sxs-lookup"><span data-stu-id="f1b81-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="f1b81-121">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1b81-121">Then click **OK**.</span></span>

    ![Selecione os objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="f1b81-123">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="f1b81-123">Set up hello source environment</span></span>
<span data-ttu-id="f1b81-124">Configurar o ambiente de origem Olá envolve dois principais atividades:</span><span class="sxs-lookup"><span data-stu-id="f1b81-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="f1b81-125">Instalar e registar um servidor de configuração com a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="f1b81-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="f1b81-126">Detete máquinas virtuais no local através da ligação de recuperação de Site tooyour local no VMware vCenter ou vSphere EXSi anfitriões.</span><span class="sxs-lookup"><span data-stu-id="f1b81-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="f1b81-127">Passo 1: Instalar e registar um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="f1b81-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="f1b81-128">Clique em **passo 1: preparar infraestrutura** > **origem**.</span><span class="sxs-lookup"><span data-stu-id="f1b81-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="f1b81-129">No **preparar a origem**, se não tiver um servidor de configuração, clique em **+ o servidor de configuração** tooadd um.</span><span class="sxs-lookup"><span data-stu-id="f1b81-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Configurar a origem](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="f1b81-131">No Olá **Adicionar servidor** painel, verifique se **servidor de configuração** aparece no **tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="f1b81-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="f1b81-132">Transfira o ficheiro de instalação do programa de configuração do Site Recovery Unified Olá.</span><span class="sxs-lookup"><span data-stu-id="f1b81-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="f1b81-133">Transferir a chave de registo do cofre Olá.</span><span class="sxs-lookup"><span data-stu-id="f1b81-133">Download hello vault registration key.</span></span> <span data-ttu-id="f1b81-134">Terá de chave de registo Olá quando executar a configuração do Unified.</span><span class="sxs-lookup"><span data-stu-id="f1b81-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="f1b81-135">chave de Olá é válido durante cinco dias depois de gerá-la.</span><span class="sxs-lookup"><span data-stu-id="f1b81-135">hello key is valid for five days after you generate it.</span></span>

    ![Configurar a origem](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="f1b81-137">Na máquina de Olá estiver a utilizar como servidor de configuração de Olá, execute **configuração de unificada do Azure Site Recovery** servidor de configuração do tooinstall Olá, o servidor de processos de Olá e o mestre de Olá servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="f1b81-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="f1b81-138">Configuração de unificada de execução do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f1b81-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="f1b81-139">Registo do servidor de configuração falha se o tempo de Olá no relógio do sistema do computador é diferente da hora local em mais de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="f1b81-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="f1b81-140">Sincronizar o relógio do seu sistema com um [hora Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1b81-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="f1b81-141">servidor de configuração de Olá pode ser instalada através de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="f1b81-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="f1b81-142">Para obter mais informações, consulte [instalar servidor de configuração de Olá utilizando as ferramentas da linha de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="f1b81-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="f1b81-143">Adicionar a conta de VMware Olá para a deteção automática</span><span class="sxs-lookup"><span data-stu-id="f1b81-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="f1b81-144">Passo 2: Adicionar um vCenter</span><span class="sxs-lookup"><span data-stu-id="f1b81-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="f1b81-145">tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente no local, terá de tooconnect o servidor vCenter VMware ou vSphere ESXi anfitriões com a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="f1b81-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="f1b81-146">Selecione **+ vCenter** toostart ligar um servidor VMware vCenter ou um anfitrião do VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="f1b81-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="f1b81-147">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="f1b81-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="f1b81-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f1b81-148">Next steps</span></span>
<span data-ttu-id="f1b81-149">[Configurar o ambiente de destino](./site-recovery-prepare-target-vmware-to-azure.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b81-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
