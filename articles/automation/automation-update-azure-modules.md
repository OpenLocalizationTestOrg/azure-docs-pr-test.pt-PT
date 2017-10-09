---
title: "aaaUpdate Azure módulos na automatização do Azure | Microsoft Docs"
description: "Este artigo descreve como pode atualizar agora comuns módulos do PowerShell do Azure fornecidos por predefinição na automatização do Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="3293e-103">Como tooupdate módulos do Azure PowerShell na automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="3293e-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="3293e-104">módulos do Azure PowerShell mais comuns do Olá são fornecidos por predefinição em cada conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="3293e-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="3293e-105">atualizações da equipa do Azure de Olá Olá módulos do Azure regularmente, na conta de automatização de Olá fornecemos uma forma para si módulos de Olá tooupdate na conta de Olá quando existem novas versões do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="3293e-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="3293e-106">Porque os módulos são atualizados regularmente por grupo de produtos Olá, as alterações podem ocorrer com cmdlets de Olá incluído, que poderá afetar negativamente os runbooks, dependendo do tipo de Olá de alteração, tais como mudar o nome de um parâmetro ou completamente a descontinuar a um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3293e-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="3293e-107">tooavoid afetar os runbooks e Olá processos automatizar, recomenda-se vivamente que testar e validar antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="3293e-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="3293e-108">Se não tiver uma conta de automatização dedicada pretendida para esta finalidade, considere criar um, para que possa testar muitos cenários diferentes e permutações durante o desenvolvimento de Olá dos seus runbooks, em alterações de tooiterative adição tais como a atualização Olá Módulos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3293e-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="3293e-109">Depois de resultados de Olá são validados e ter aplicado as alterações necessárias, continuar com a coordenação de migração de Olá de todos os runbooks que necessário modificação e efetuar a atualização de Olá, conforme descrito abaixo na produção.</span><span class="sxs-lookup"><span data-stu-id="3293e-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="3293e-110">Atualizar os módulos do Azure</span><span class="sxs-lookup"><span data-stu-id="3293e-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="3293e-111">Módulos de Olá painel da sua conta da automatização é uma opção chamada **os módulos do Azure Update**.</span><span class="sxs-lookup"><span data-stu-id="3293e-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="3293e-112">É sempre ativada.</span><span class="sxs-lookup"><span data-stu-id="3293e-112">It is always enabled.</span></span><br><br> <span data-ttu-id="3293e-113">![Atualizar a opção de módulos do Azure no painel de módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="3293e-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="3293e-114">Clique em **os módulos do Azure Update** e será apresentada uma notificação de confirmação que pede-lhe se pretende toocontinue.</span><span class="sxs-lookup"><span data-stu-id="3293e-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="3293e-115">![Atualizar notificação de módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="3293e-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="3293e-116">Clique em **Sim** e processo de atualização do módulo Olá irá começar.</span><span class="sxs-lookup"><span data-stu-id="3293e-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="3293e-117">processo de atualização de Olá demora Olá de tooupdate 15 a 20 minutos seguintes módulos:</span><span class="sxs-lookup"><span data-stu-id="3293e-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="3293e-118">Azure</span><span class="sxs-lookup"><span data-stu-id="3293e-118">Azure</span></span>
  * <span data-ttu-id="3293e-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="3293e-119">Azure.Storage</span></span>
  * <span data-ttu-id="3293e-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="3293e-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="3293e-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="3293e-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="3293e-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="3293e-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="3293e-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="3293e-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="3293e-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="3293e-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="3293e-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="3293e-125">AzureRm.Storage</span></span>

    <span data-ttu-id="3293e-126">Se os módulos de Olá já estiverem segurança toodate, em seguida, o processo de Olá será concluído dentro de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="3293e-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="3293e-127">Quando tiver concluído o processo de atualização de Olá será notificado.</span><span class="sxs-lookup"><span data-stu-id="3293e-127">When hello update process completes you will be notified.</span></span><br><br> ![Atualizar o estado de atualização de módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="3293e-129">A automatização do Azure irá utilizar módulos mais recentes Olá na sua conta de automatização quando uma nova tarefa agendada é executada.</span><span class="sxs-lookup"><span data-stu-id="3293e-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="3293e-130">Se utilizar os cmdlets destes módulos do PowerShell do Azure na sua toomanage runbooks Azure recursos e irão tooperform este processo de atualização de todos os meses ou, por isso, tooassure tiver Olá módulos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="3293e-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3293e-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3293e-131">Next steps</span></span>

* <span data-ttu-id="3293e-132">toolearn mais informações sobre os módulos de integração e como toocreate módulos personalizados toofurther integrar automatização com outros sistemas, serviços ou soluções, consulte [módulos de integração](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="3293e-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="3293e-133">Considere a utilização de integração de controlo de origem [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gerir e controlar as versões do seu portefólio automatização de runbook e a configuração.</span><span class="sxs-lookup"><span data-stu-id="3293e-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
