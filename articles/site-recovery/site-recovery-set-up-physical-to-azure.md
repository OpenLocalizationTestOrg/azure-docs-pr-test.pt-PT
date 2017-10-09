---
title: "Configurar o ambiente de origem Olá (servidores físicos tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local replicar servidores físicos que executem Windows ou Linux no Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="9af03-103">Configurar o ambiente de origem Olá (servidor físico tooAzure)</span><span class="sxs-lookup"><span data-stu-id="9af03-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9af03-104">TooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="9af03-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="9af03-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="9af03-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="9af03-106">Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local replicar servidores físicos que executem Windows ou Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="9af03-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9af03-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9af03-107">Prerequisites</span></span>

<span data-ttu-id="9af03-108">artigo de Olá pressupõe que já tem:</span><span class="sxs-lookup"><span data-stu-id="9af03-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="9af03-109">Um cofre dos serviços de recuperação Olá [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="9af03-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="9af03-110">Um computador físico no servidor de configuração que tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="9af03-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="9af03-111">Requisitos mínimos do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="9af03-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="9af03-112">Olá, a tabela seguinte lista Olá mínimos de hardware, software e requisitos de rede para um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="9af03-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="9af03-113">Servidores proxy baseado em HTTPS não são suportadas pelo servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="9af03-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="9af03-114">Escolha os seus objetivos de proteção</span><span class="sxs-lookup"><span data-stu-id="9af03-114">Choose your protection goals</span></span>

1. <span data-ttu-id="9af03-115">Olá portal do Azure, aceda toohello **dos serviços de recuperação** cofres dos painel e selecione o cofre.</span><span class="sxs-lookup"><span data-stu-id="9af03-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="9af03-116">No Olá **recursos** menu do Cofre de Olá, clique em **introdução** > **recuperação de Site** > **passo 1: preparar Infraestrutura** > **objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="9af03-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Selecione os objetivos](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="9af03-118">No **objetivo de proteção**, selecione **tooAzure** e **não virtualizados/outras**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9af03-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Selecione os objetivos](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="9af03-120">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="9af03-120">Set up hello source environment</span></span>

1. <span data-ttu-id="9af03-121">No **preparar a origem**, se não tiver um servidor de configuração, clique em **+ o servidor de configuração** tooadd um.</span><span class="sxs-lookup"><span data-stu-id="9af03-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Configurar a origem](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="9af03-123">No Olá **Adicionar servidor** painel, verifique se **servidor de configuração** aparece no **tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="9af03-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="9af03-124">Transfira o ficheiro de instalação do programa de configuração do Site Recovery Unified Olá.</span><span class="sxs-lookup"><span data-stu-id="9af03-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="9af03-125">Transferir a chave de registo do cofre Olá.</span><span class="sxs-lookup"><span data-stu-id="9af03-125">Download hello vault registration key.</span></span> <span data-ttu-id="9af03-126">Terá de chave de registo Olá quando executar a configuração do Unified.</span><span class="sxs-lookup"><span data-stu-id="9af03-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="9af03-127">chave de Olá é válido durante cinco dias depois de gerá-la.</span><span class="sxs-lookup"><span data-stu-id="9af03-127">hello key is valid for five days after you generate it.</span></span>

    ![Configurar a origem](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="9af03-129">Na máquina de Olá estiver a utilizar como servidor de configuração de Olá, execute **configuração de unificada do Azure Site Recovery** servidor de configuração do tooinstall Olá, o servidor de processos de Olá e o mestre de Olá servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="9af03-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="9af03-130">Configuração de unificada de execução do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9af03-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="9af03-131">Registo do servidor de configuração falha se o tempo de Olá no relógio do sistema do computador é mais de cinco minutos retire hora local.</span><span class="sxs-lookup"><span data-stu-id="9af03-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="9af03-132">Sincronizar o relógio do seu sistema com um [hora server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="9af03-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="9af03-133">servidor de configuração de Olá pode ser instalada através de uma linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="9af03-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="9af03-134">Para obter mais informações, consulte [instalar servidor de configuração com as ferramentas da linha de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="9af03-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="9af03-135">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="9af03-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="9af03-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9af03-136">Next steps</span></span>

<span data-ttu-id="9af03-137">Passo seguinte envolve [como configurar o ambiente de destino](./site-recovery-prepare-target-physical-to-azure.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="9af03-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
