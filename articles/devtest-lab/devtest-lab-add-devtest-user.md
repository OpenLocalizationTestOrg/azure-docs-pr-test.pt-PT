---
title: "aaaAdd proprietários e os utilizadores no Azure DevTest Labs | Microsoft Docs"
description: "Adicionar utilizadores e proprietários no Azure DevTest Labs utilizando Olá portal do Azure ou o PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="be174-103">Adicionar utilizadores e proprietários no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="be174-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="be174-104">O acesso no Azure DevTest Labs é controlado pelo [controlo de acesso em funções do Azure (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="be174-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="be174-105">Utilizar o RBAC, pode segregar funções na sua equipa no *funções* onde conceder apenas Olá quantidade de acesso necessários toousers tooperform as respetivas tarefas.</span><span class="sxs-lookup"><span data-stu-id="be174-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="be174-106">Três destas funções do RBAC são *proprietário*, *DevTest Labs utilizador*, e *contribuinte*.</span><span class="sxs-lookup"><span data-stu-id="be174-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="be174-107">Neste artigo, saiba o que ações podem ser efetuadas em cada um dos Olá três principais funções do RBAC.</span><span class="sxs-lookup"><span data-stu-id="be174-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="be174-108">A partir daí, saiba como laboratório do tooadd utilizadores tooa - ambos através de Olá portal e através de um script do PowerShell e como os utilizadores de tooadd no Olá ao nível da subscrição.</span><span class="sxs-lookup"><span data-stu-id="be174-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="be174-109">Ações que podem ser executadas em cada função</span><span class="sxs-lookup"><span data-stu-id="be174-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="be174-110">Existem três funções principais que pode atribuir um utilizador:</span><span class="sxs-lookup"><span data-stu-id="be174-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="be174-111">Proprietário</span><span class="sxs-lookup"><span data-stu-id="be174-111">Owner</span></span>
* <span data-ttu-id="be174-112">DevTest Labs utilizador</span><span class="sxs-lookup"><span data-stu-id="be174-112">DevTest Labs User</span></span>
* <span data-ttu-id="be174-113">Contribuinte</span><span class="sxs-lookup"><span data-stu-id="be174-113">Contributor</span></span>

<span data-ttu-id="be174-114">Olá tabela que se segue ilustra as ações de Olá que podem ser efetuadas pelos utilizadores em cada uma destas funções:</span><span class="sxs-lookup"><span data-stu-id="be174-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="be174-115">**Podem efetuar ações os utilizadores com esta função**</span><span class="sxs-lookup"><span data-stu-id="be174-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="be174-116">**DevTest Labs utilizador**</span><span class="sxs-lookup"><span data-stu-id="be174-116">**DevTest Labs User**</span></span> | <span data-ttu-id="be174-117">**Proprietário**</span><span class="sxs-lookup"><span data-stu-id="be174-117">**Owner**</span></span> | <span data-ttu-id="be174-118">**Contribuinte**</span><span class="sxs-lookup"><span data-stu-id="be174-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="be174-119">**Tarefas de laboratório**</span><span class="sxs-lookup"><span data-stu-id="be174-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="be174-120">Adicionar o laboratório de tooa de utilizadores</span><span class="sxs-lookup"><span data-stu-id="be174-120">Add users tooa lab</span></span> |<span data-ttu-id="be174-121">Não</span><span class="sxs-lookup"><span data-stu-id="be174-121">No</span></span> |<span data-ttu-id="be174-122">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-122">Yes</span></span> |<span data-ttu-id="be174-123">Não</span><span class="sxs-lookup"><span data-stu-id="be174-123">No</span></span> |
| <span data-ttu-id="be174-124">Atualizar as definições de custos</span><span class="sxs-lookup"><span data-stu-id="be174-124">Update cost settings</span></span> |<span data-ttu-id="be174-125">Não</span><span class="sxs-lookup"><span data-stu-id="be174-125">No</span></span> |<span data-ttu-id="be174-126">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-126">Yes</span></span> |<span data-ttu-id="be174-127">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-127">Yes</span></span> |
| <span data-ttu-id="be174-128">**Tarefas de base de VM**</span><span class="sxs-lookup"><span data-stu-id="be174-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="be174-129">Adicionar e remover imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="be174-129">Add and remove custom images</span></span> |<span data-ttu-id="be174-130">Não</span><span class="sxs-lookup"><span data-stu-id="be174-130">No</span></span> |<span data-ttu-id="be174-131">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-131">Yes</span></span> |<span data-ttu-id="be174-132">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-132">Yes</span></span> |
| <span data-ttu-id="be174-133">Adicionar, atualizar e eliminar as fórmulas</span><span class="sxs-lookup"><span data-stu-id="be174-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="be174-134">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-134">Yes</span></span> |<span data-ttu-id="be174-135">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-135">Yes</span></span> |<span data-ttu-id="be174-136">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-136">Yes</span></span> |
| <span data-ttu-id="be174-137">Imagens da lista branca Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="be174-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="be174-138">Não</span><span class="sxs-lookup"><span data-stu-id="be174-138">No</span></span> |<span data-ttu-id="be174-139">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-139">Yes</span></span> |<span data-ttu-id="be174-140">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-140">Yes</span></span> |
| <span data-ttu-id="be174-141">**Tarefas VM**</span><span class="sxs-lookup"><span data-stu-id="be174-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="be174-142">Criar VMs</span><span class="sxs-lookup"><span data-stu-id="be174-142">Create VMs</span></span> |<span data-ttu-id="be174-143">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-143">Yes</span></span> |<span data-ttu-id="be174-144">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-144">Yes</span></span> |<span data-ttu-id="be174-145">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-145">Yes</span></span> |
| <span data-ttu-id="be174-146">Iniciar, parar e eliminar as VMs</span><span class="sxs-lookup"><span data-stu-id="be174-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="be174-147">Apenas as VMs criadas por utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="be174-147">Only VMs created by hello user</span></span> |<span data-ttu-id="be174-148">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-148">Yes</span></span> |<span data-ttu-id="be174-149">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-149">Yes</span></span> |
| <span data-ttu-id="be174-150">Atualizar as políticas de VM</span><span class="sxs-lookup"><span data-stu-id="be174-150">Update VM policies</span></span> |<span data-ttu-id="be174-151">Não</span><span class="sxs-lookup"><span data-stu-id="be174-151">No</span></span> |<span data-ttu-id="be174-152">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-152">Yes</span></span> |<span data-ttu-id="be174-153">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-153">Yes</span></span> |
| <span data-ttu-id="be174-154">Adicionar/remover discos de dados do VMs</span><span class="sxs-lookup"><span data-stu-id="be174-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="be174-155">Apenas as VMs criadas por utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="be174-155">Only VMs created by hello user</span></span> |<span data-ttu-id="be174-156">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-156">Yes</span></span> |<span data-ttu-id="be174-157">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-157">Yes</span></span> |
| <span data-ttu-id="be174-158">**Tarefas de artefactos**</span><span class="sxs-lookup"><span data-stu-id="be174-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="be174-159">Adicionar e remover repositórios de artefactos</span><span class="sxs-lookup"><span data-stu-id="be174-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="be174-160">Não</span><span class="sxs-lookup"><span data-stu-id="be174-160">No</span></span> |<span data-ttu-id="be174-161">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-161">Yes</span></span> |<span data-ttu-id="be174-162">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-162">Yes</span></span> |
| <span data-ttu-id="be174-163">Aplicam-se de artefactos</span><span class="sxs-lookup"><span data-stu-id="be174-163">Apply artifacts</span></span> |<span data-ttu-id="be174-164">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-164">Yes</span></span> |<span data-ttu-id="be174-165">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-165">Yes</span></span> |<span data-ttu-id="be174-166">Sim</span><span class="sxs-lookup"><span data-stu-id="be174-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="be174-167">Quando um utilizador cria uma VM, esse utilizador é atribuído automaticamente toohello **proprietário** função de Olá criada a VM.</span><span class="sxs-lookup"><span data-stu-id="be174-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="be174-168">Adicionar um proprietário ou o utilizador ao nível de laboratório de Olá</span><span class="sxs-lookup"><span data-stu-id="be174-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="be174-169">Os proprietários e os utilizadores podem ser adicionados ao nível do laboratório Olá através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="be174-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="be174-170">Isto inclui os utilizadores externos com um [conta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="be174-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="be174-171">Olá, os seguintes passos guiá-lo através do processo de Olá de adição de um laboratório de tooa proprietário ou utilizador no Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="be174-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="be174-172">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="be174-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="be174-173">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="be174-174">Na lista de Olá de laboratórios, selecione laboratório pretendido Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="be174-175">No painel do laboratório de Olá, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="be174-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="be174-176">No Olá **configuração** painel, selecione **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="be174-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="be174-177">No Olá **utilizadores** painel, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="be174-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Adicionar utilizador](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="be174-179">No Olá **selecionar uma função** painel, a função pretendida Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="be174-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="be174-180">Olá secção [ações que podem ser executadas em cada função](#actions-that-can-be-performed-in-each-role) listas Olá várias ações que podem ser efetuadas pelos utilizadores nas funções de proprietário, utilizador de DevTest e contribuinte Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="be174-181">No Olá **adicionar utilizadores** painel, introduza o endereço de correio eletrónico Olá ou nome de utilizador de Olá pretende tooadd na função Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="be174-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="be174-182">Se não é possível localizar o utilizador Olá, uma mensagem de erro explica problema Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="be174-183">Se Olá utilizador for encontrado, esse utilizador é listado e seleccionado.</span><span class="sxs-lookup"><span data-stu-id="be174-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="be174-184">Selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="be174-184">Select **Select**.</span></span>
10. <span data-ttu-id="be174-185">Selecione **OK** tooclose Olá **adicionar acesso** painel.</span><span class="sxs-lookup"><span data-stu-id="be174-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="be174-186">Quando regressar toohello **utilizadores** painel, Olá utilizador foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="be174-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="be174-187">Adicionar um laboratório de tooa utilizador externo através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="be174-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="be174-188">Além disso tooadding utilizadores Olá portal do Azure, pode adicionar um laboratório de tooyour de utilizador externo utilizando um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be174-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="be174-189">Olá simplesmente seguinte o exemplo, modificar os valores de parâmetros de Olá em Olá **valores toochange** comentário.</span><span class="sxs-lookup"><span data-stu-id="be174-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="be174-190">Pode obter Olá `subscriptionId`, `labResourceGroup`, e `labName` valores a partir do painel de laboratório Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="be174-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="be174-191">script de exemplo de Olá parte do princípio de que Olá especificado utilizador foi adicionado como um toohello de convidado do Active Directory e irá falhar se não for esse caso de Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="be174-192">tooadd um utilizador não se encontra na Olá laboratório de tooa do Active Directory, utilize Olá tooassign portal do Azure Olá tooa a função de utilizador, conforme ilustrado na secção de Olá, [adicionar um proprietário ou o utilizador ao nível de laboratório de Olá](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="be174-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="be174-193">Adicionar um proprietário ou o utilizador ao nível da subscrição de Olá</span><span class="sxs-lookup"><span data-stu-id="be174-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="be174-194">Permissões do Azure são propagadas do âmbito de toochild âmbito principal no Azure.</span><span class="sxs-lookup"><span data-stu-id="be174-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="be174-195">Por conseguinte, os proprietários de uma subscrição do Azure que contém laboratórios são automaticamente os proprietários desses laboratórios.</span><span class="sxs-lookup"><span data-stu-id="be174-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="be174-196">Também possuem Olá VMs e outros recursos criados por utilizadores do laboratório de Olá e Olá serviço Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="be174-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="be174-197">Pode adicionar o laboratório de tooa proprietários adicionais através do painel do laboratório de Olá no Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="be174-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="be174-198">No entanto, Olá Adicionar âmbito do proprietário da administração é mais restritos ao âmbito do proprietário da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="be174-199">Por exemplo, Olá adicionada proprietários não têm acesso total toosome Olá de recursos de que são criados na subscrição Olá por Olá serviço DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="be174-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="be174-200">tooadd tooan um proprietário subscrição do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="be174-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="be174-201">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="be174-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="be174-202">Selecione **mais serviços**e, em seguida, selecione **subscrições** da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="be174-203">Selecione a subscrição de Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="be174-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="be174-204">Selecione **acesso** ícone.</span><span class="sxs-lookup"><span data-stu-id="be174-204">Select **Access** icon.</span></span> 
   
    ![Utilizadores de acesso](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="be174-206">No Olá **utilizadores** painel, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="be174-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Adicionar utilizador](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="be174-208">No Olá **selecionar uma função** painel, selecione **proprietário**.</span><span class="sxs-lookup"><span data-stu-id="be174-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="be174-209">No Olá **adicionar utilizadores** painel, introduza o endereço de correio eletrónico Olá ou nome de utilizador de Olá pretende tooadd como um proprietário.</span><span class="sxs-lookup"><span data-stu-id="be174-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="be174-210">Se não é possível localizar o utilizador Olá, receberá uma mensagem de erro explicar problema Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="be174-211">Se for encontrado o utilizador Olá, esse utilizador é apresentado em Olá **utilizador** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="be174-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="be174-212">Selecione o nome de utilizador localizado Olá.</span><span class="sxs-lookup"><span data-stu-id="be174-212">Select hello located user name.</span></span>
9. <span data-ttu-id="be174-213">Selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="be174-213">Select **Select**.</span></span>
10. <span data-ttu-id="be174-214">Selecione **OK** tooclose Olá **adicionar acesso** painel.</span><span class="sxs-lookup"><span data-stu-id="be174-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="be174-215">Quando regressar toohello **utilizadores** painel, Olá utilizador foi adicionado como um proprietário.</span><span class="sxs-lookup"><span data-stu-id="be174-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="be174-216">Este utilizador é agora um proprietário de quaisquer laboratórios criado pertencentes a esta subscrição e, por conseguinte, ser capaz de tooperform tarefas de proprietário.</span><span class="sxs-lookup"><span data-stu-id="be174-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

