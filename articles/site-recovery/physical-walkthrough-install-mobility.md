---
title: "Olá aaaInstall serviço de mobilidade de replicação do servidor físico tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooinstall Olá agente do serviço de mobilidade em servidores físicos a replicar tooAzure com o serviço do Azure Site Recovery Olá."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="c28d4-103">Passo 9: Instalar o serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="c28d4-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="c28d4-104">Este artigo descreve como componente de serviço de mobilidade do tooinstall Olá quando replicar no local tooAzure de servidores físicos Windows/Linux, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c28d4-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="c28d4-105">Olá serviço de mobilidade obtém dados, escreve numa máquina e reencaminha-os toohello servidor de processos.</span><span class="sxs-lookup"><span data-stu-id="c28d4-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="c28d4-106">Deve ser instalado em cada servidor que pretende que o tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c28d4-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="c28d4-107">Pode instalar o serviço de mobilidade Olá manualmente ou utilizar uma instalação de push de Olá recuperação de Site processar servidor quando a replicação está ativada ou utilizando uma ferramenta como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="c28d4-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="c28d4-108">Se utilizar a instalação push do serviço Olá está instalado no servidor de Olá ao ativar a replicação.</span><span class="sxs-lookup"><span data-stu-id="c28d4-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="c28d4-109">Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c28d4-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="c28d4-110">Instalar manualmente</span><span class="sxs-lookup"><span data-stu-id="c28d4-110">Install manually</span></span>

1. <span data-ttu-id="c28d4-111">Verifique Olá [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para a instalação manual.</span><span class="sxs-lookup"><span data-stu-id="c28d4-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="c28d4-112">Siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para a instalação manual através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="c28d4-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="c28d4-113">Se preferir tooinstall Olá linha de comandos, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="c28d4-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="c28d4-114">Instalar a partir do servidor de processos de Olá</span><span class="sxs-lookup"><span data-stu-id="c28d4-114">Install from hello process server</span></span>

<span data-ttu-id="c28d4-115">Se pretender toopush hello do servidor de processos de Olá a instalação do serviço de mobilidade quando ativar a replicação para uma máquina, precisa de uma conta que pode ser utilizada pela máquina do Olá processo servidor tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="c28d4-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="c28d4-116">conta de Olá só é utilizada para a instalação de push Olá.</span><span class="sxs-lookup"><span data-stu-id="c28d4-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="c28d4-117">Se ainda não criou uma conta, o que pretende utilizar estas diretrizes:</span><span class="sxs-lookup"><span data-stu-id="c28d4-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="c28d4-118">Pode utilizar um domínio ou conta local</span><span class="sxs-lookup"><span data-stu-id="c28d4-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="c28d4-119">Para o Windows, se não estiver a utilizar uma conta de domínio, terá de toodisable controlo de acesso de utilizador remoto no computador local Olá.</span><span class="sxs-lookup"><span data-stu-id="c28d4-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="c28d4-120">toodo, Olá registar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar a entrada de DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.</span><span class="sxs-lookup"><span data-stu-id="c28d4-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="c28d4-121">Se pretender que entrada de registo de Olá tooadd para Windows de um CLI, escreva:</span><span class="sxs-lookup"><span data-stu-id="c28d4-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="c28d4-122">Para Linux conta Olá deve ser a raiz no servidor de Linux Olá origem.</span><span class="sxs-lookup"><span data-stu-id="c28d4-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="c28d4-123">Em seguida, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se pretender que o serviço de mobilidade Olá toopush em VMs do Windows ou Linux em execução.</span><span class="sxs-lookup"><span data-stu-id="c28d4-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="c28d4-124">Outros métodos de instalação</span><span class="sxs-lookup"><span data-stu-id="c28d4-124">Other installation methods</span></span>

- <span data-ttu-id="c28d4-125">[Saiba mais sobre](site-recovery-install-mobility-service-using-sccm.md) instalar o serviço de mobilidade Olá utilizando o Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="c28d4-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="c28d4-126">[Saiba mais sobre](site-recovery-automate-mobility-service-install.md) instalação com o Automation DSC do Azure.</span><span class="sxs-lookup"><span data-stu-id="c28d4-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c28d4-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c28d4-127">Next steps</span></span>

<span data-ttu-id="c28d4-128">Aceda demasiado[passo 10: Ativar a replicação](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c28d4-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
