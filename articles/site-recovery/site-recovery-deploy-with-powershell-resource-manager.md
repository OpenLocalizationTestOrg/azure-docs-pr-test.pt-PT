---
title: aaaReplicate VMs de Hyper-V com o PowerShell e do Azure Resource Manager | Microsoft Docs
description: "Automatizar a replicação de VMs de Hyper-V tooAzure Olá com o Azure Site Recovery com o PowerShell e do Azure Resource Manager."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="70066-103">Replicar entre máquinas de virtuais de Hyper-V no local e o Azure utilizando o PowerShell e o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70066-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70066-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="70066-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="70066-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70066-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="70066-106">Portal Clássico</span><span class="sxs-lookup"><span data-stu-id="70066-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="70066-107">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="70066-107">Overview</span></span>
<span data-ttu-id="70066-108">O Azure Site Recovery contribui tooyour continuidade e desastre recuperação estratégia de negócios através da orquestração da replicação, ativação pós-falha e recuperação de máquinas virtuais num número de cenários de implementação.</span><span class="sxs-lookup"><span data-stu-id="70066-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="70066-109">Para obter uma lista completa dos cenários de implementação, consulte Olá [descrição geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70066-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="70066-110">O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70066-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="70066-111">Poder funcionar com dois tipos de módulos: Olá módulo Azure perfil ou o módulo do Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="70066-112">Cmdlets do PowerShell da recuperação de site, disponíveis com o Azure PowerShell para o Azure Resource Manager, ajudar a proteger e recuperar os seus servidores no Azure.</span><span class="sxs-lookup"><span data-stu-id="70066-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="70066-113">Este artigo descreve como toouse Windows PowerShell, juntamente com o Azure Resource Manager, toodeploy tooconfigure de recuperação de sites e orquestrar tooAzure de proteção do servidor.</span><span class="sxs-lookup"><span data-stu-id="70066-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="70066-114">exemplo de Olá utilizado neste artigo mostra-lhe como tooprotect, efetuar a ativação pós-falha e recuperar máquinas virtuais no tooAzure anfitrião Hyper-V, utilizando o Azure PowerShell com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="70066-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="70066-115">Olá cmdlets do PowerShell da recuperação de Site atualmente permitem-lhe Olá tooconfigure seguintes: uma tooanother de site do Virtual Machine Manager, um tooAzure de site do Virtual Machine Manager e um tooAzure de site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="70066-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="70066-116">Não precisa de toobe um toouse especialista de PowerShell neste artigo, mas é necessário toounderstand Olá conceitos básicos, tais como módulos, cmdlets e sessões.</span><span class="sxs-lookup"><span data-stu-id="70066-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="70066-117">Para obter mais informações sobre o Windows PowerShell, veja a [Introdução ao Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="70066-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="70066-118">Também pode ler mais sobre [utilizar o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="70066-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="70066-119">Parceiros da Microsoft que fazem parte do programa de fornecedor de solução em nuvem (CSP) Olá podem configurar e gerir a proteção de servidores dos seus clientes respetivas CSP subscrições dos clientes tootheir (subscrições de inquilino).</span><span class="sxs-lookup"><span data-stu-id="70066-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="70066-120">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="70066-120">Before you start</span></span>
<span data-ttu-id="70066-121">Certifique-se de que tem os pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="70066-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="70066-122">A [Microsoft Azure](https://azure.microsoft.com/) conta.</span><span class="sxs-lookup"><span data-stu-id="70066-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="70066-123">Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70066-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="70066-124">Além disso, pode ler sobre [preços do Microsoft Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="70066-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="70066-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="70066-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="70066-126">Para obter informações sobre esta versão e como tooinstall-lo, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="70066-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="70066-127">Olá [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) módulos.</span><span class="sxs-lookup"><span data-stu-id="70066-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="70066-128">Pode obter versões mais recentes do Olá estes módulos do Olá [galeria do PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="70066-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="70066-129">Este artigo ilustra como toouse Azure Powershell com o Azure Resource Manager tooconfigure e gerir a proteção dos seus servidores.</span><span class="sxs-lookup"><span data-stu-id="70066-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="70066-130">exemplo de Olá utilizado neste artigo mostra-lhe como tooprotect uma máquina virtual, em execução num anfitrião Hyper-V, tooAzure.</span><span class="sxs-lookup"><span data-stu-id="70066-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="70066-131">Olá, os seguintes pré-requisitos é exemplo toothis específico.</span><span class="sxs-lookup"><span data-stu-id="70066-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="70066-132">Para um conjunto mais completo de requisitos para Olá vários cenários de recuperação de sites, consulte a documentação de toohello relativas toothat cenário.</span><span class="sxs-lookup"><span data-stu-id="70066-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="70066-133">Um anfitrião de Hyper-V com Windows Server 2012 R2 ou Microsoft Hyper-V Server 2012 R2 que contém uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="70066-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="70066-134">Servidores de Hyper-V ligados toohello Internet, diretamente ou através de um proxy.</span><span class="sxs-lookup"><span data-stu-id="70066-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="70066-135">Olá máquinas virtuais que pretende tooprotect deve estar em conformidade com [pré-requisitos de Máquina Virtual](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="70066-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="70066-136">Passo 1: Iniciar sessão tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="70066-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="70066-137">Abra uma consola do PowerShell e execute este comando toosign no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="70066-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="70066-138">cmdlet de Olá aparece uma página web que irá pedir que introduza as credenciais da conta.</span><span class="sxs-lookup"><span data-stu-id="70066-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="70066-139">Em alternativa, também pode incluir as credenciais da conta como um parâmetro toohello `Login-AzureRmAccount` cmdlet, utilizando Olá `-Credential` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="70066-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="70066-140">Se estiver a trabalhar em nome de um inquilino de parceiro CSP, especificar cliente Olá como um inquilino, utilizando o respetivo nome de domínio primário tenantID ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="70066-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="70066-141">Uma conta pode ter várias subscrições, pelo que deve associar subscrição Olá pretende toouse com a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="70066-142">Certifique-se de que a sua subscrição está registada toouse hello fornecedores do Azure para os serviços de recuperação e de recuperação de Site, utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="70066-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="70066-143">No resultado Olá estes comandos, se hello **RegistrationState** estiver definido demasiado**registada**, pode avançar tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="70066-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="70066-144">Caso contrário, deve registar o fornecedor em falta Olá na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="70066-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="70066-145">tooregister hello o fornecedor do Azure para a recuperação de sites e serviços de recuperação, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="70066-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="70066-146">Certifique-se de que os fornecedores de Olá registado com êxito utilizando Olá os seguintes comandos: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="70066-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="70066-147">Passo 2: Configurar Olá que cofre dos serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="70066-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="70066-148">Crie um grupo de recursos do Azure Resource Manager, nos quais irá criar cofre Olá ou utilizar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="70066-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="70066-149">Pode criar um novo grupo de recursos utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="70066-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="70066-150">em que a variável de Olá $ResourceGroupName contém o nome de Olá Olá do grupo de recursos que pretende toocreate e variável Olá $Geo contém Olá Azure região em que grupo de recursos de Olá toocreate (por exemplo, "sul do Brasil").</span><span class="sxs-lookup"><span data-stu-id="70066-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="70066-151">Pode obter uma lista de grupos de recursos na sua subscrição utilizando Olá `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70066-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="70066-152">Crie um novo cofre de serviços de recuperação do Azure da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="70066-153">Pode obter uma lista de cofres existentes utilizando Olá `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70066-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="70066-154">Se desejar operações tooperform cofres de recuperação de Site criados utilizando o portal clássico Olá ou o módulo de gestão de serviço do Azure PowerShell Olá, pode obter uma lista de cofres de tais utilizando Olá `Get-AzureRmSiteRecoveryVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70066-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="70066-155">Deve criar um novo cofre de serviços de recuperação para todas as operações de novo.</span><span class="sxs-lookup"><span data-stu-id="70066-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="70066-156">cofres de recuperação de Site Olá que criou anteriormente são suportadas, mas não tem funcionalidades mais recentes Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="70066-157">Passo 3: Definir Olá contexto do Cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="70066-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="70066-158">Definir o contexto de cofre Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="70066-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="70066-159">Passo 4: Criar um site de Hyper-V e gerar uma nova chave de registo do cofre para o site de Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="70066-160">Crie um novo site de Hyper-V da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="70066-161">Este cmdlet é iniciado um site de Olá de toocreate de tarefa de recuperação de sites e devolve um objeto de tarefa de recuperação de sites.</span><span class="sxs-lookup"><span data-stu-id="70066-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="70066-162">Aguarde Olá tarefa toocomplete e certifique-se de que essa tarefa Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="70066-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="70066-163">Pode obter o objeto da tarefa Olá e, deste modo, verifique o estado atual do Olá da tarefa de Olá, utilizando o cmdlet Get-AzureRmSiteRecoveryJob de Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="70066-164">Gerar e transferir uma chave de registo para o site de Olá, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="70066-165">Olá cópia transferido toohello chave Hyper-V anfitrião.</span><span class="sxs-lookup"><span data-stu-id="70066-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="70066-166">Terá de site de toohello Olá tooregister chave Olá Hyper-V anfitrião.</span><span class="sxs-lookup"><span data-stu-id="70066-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="70066-167">Passo 5: Instalar o fornecedor do Azure Site Recovery Olá e Azure Recovery Services Agent no seu anfitrião de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="70066-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="70066-168">Transferir o instalador Olá para a versão mais recente do Olá do fornecedor de Olá de [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="70066-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="70066-169">Instalador de Olá execução no anfitrião do Hyper-V e no fim de Olá da instalação de Olá continuar passo de registo toohello.</span><span class="sxs-lookup"><span data-stu-id="70066-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="70066-170">Quando solicitado, forneça Olá transferir chave de registo do site e conclua o registo do site de toohello de anfitrião de Hyper-V Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="70066-171">Certifique-se de que alojam Olá Hyper-V é site toohello registado utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="70066-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="70066-172">Passo 6: Criar uma política de replicação e associe-o contentor de proteção de Olá</span><span class="sxs-lookup"><span data-stu-id="70066-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="70066-173">Crie uma política de replicação da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="70066-174">Olá de verificação devolvido tooensure de tarefa que a criação de política de replicação de Olá for bem sucedida.</span><span class="sxs-lookup"><span data-stu-id="70066-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="70066-175">Olá conta de armazenamento especificada deve estar na mesma região do Azure como o seu Cofre de serviços de recuperação de Olá e deve ter o georreplicação ativada.</span><span class="sxs-lookup"><span data-stu-id="70066-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="70066-176">Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (clássica).</span><span class="sxs-lookup"><span data-stu-id="70066-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="70066-177">Se Olá especificada a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Azure Resource Manager), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="70066-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="70066-178">Obter Olá proteção contentor correspondente toohello site, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="70066-179">Inicie associação Olá do contentor de proteção de Olá com a política de replicação de Olá, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="70066-180">$Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-política $Policy - PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="70066-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="70066-181">Aguarde Olá associação tarefa toocomplete e certifique-se de que foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="70066-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="70066-182">Passo 7: Ativar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="70066-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="70066-183">Obter Olá proteção entidade correspondente toohello VM pretende tooprotect, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="70066-184">Começar a proteger a máquina virtual de Olá, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="70066-185">Olá conta de armazenamento especificada deve estar na mesma região do Azure como o seu Cofre de serviços de recuperação de Olá e deve ter o georreplicação ativada.</span><span class="sxs-lookup"><span data-stu-id="70066-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="70066-186">Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (clássica).</span><span class="sxs-lookup"><span data-stu-id="70066-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="70066-187">Se Olá especificada a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Azure Resource Manager), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="70066-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="70066-188">Se Olá VM estiver a proteger tem mais de um disco tooit anexado, especifique o disco do sistema operativo Olá utilizando Olá *OSDiskName* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="70066-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="70066-189">Aguarde Olá tooreach de máquinas virtuais num estado protegido após a replicação inicial Olá.</span><span class="sxs-lookup"><span data-stu-id="70066-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="70066-190">Isto pode demorar algum tempo, dependendo de fatores como a quantidade de Olá de toobe dados replicado e Olá tooAzure de largura de banda disponível e a montante.</span><span class="sxs-lookup"><span data-stu-id="70066-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="70066-191">Estado da tarefa Olá e StateDescription são atualizados da seguinte forma após Olá VM atingir um estado protegido.</span><span class="sxs-lookup"><span data-stu-id="70066-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="70066-192">Atualize propriedades de recuperação, tais como Olá tamanho de função da VM e rede interface cartões tooupon ativação pós-falha Olá rede Azure tooattach Olá da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="70066-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="70066-193">Passo 8: Executar uma ativação pós-falha de teste</span><span class="sxs-lookup"><span data-stu-id="70066-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="70066-194">Execute uma tarefa de ativação pós-falha de teste, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="70066-195">Certifique-se que teste Olá que é criada a VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="70066-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="70066-196">(tarefa de ativação pós-falha de teste de Olá estiver suspenso, depois de criar a VM de teste de Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="70066-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="70066-197">tarefa de Olá conclui a limpeza artefacts Olá criado após retomar a tarefa de Olá, conforme ilustrado no passo seguinte Olá.)</span><span class="sxs-lookup"><span data-stu-id="70066-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="70066-198">Olá completa de teste de ativação pós-falha, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="70066-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="70066-199">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="70066-199">Next Steps</span></span>
<span data-ttu-id="70066-200">[Leia mais](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="70066-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
