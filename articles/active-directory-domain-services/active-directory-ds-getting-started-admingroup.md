---
title: "Serviços de domínio do Azure Active Directory: Introdução | Microsoft Docs"
description: "Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="b06e4-103">Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="b06e4-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="b06e4-104">Tarefa 3: configurar o grupo administrativo</span><span class="sxs-lookup"><span data-stu-id="b06e4-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="b06e4-105">Nesta tarefa de configuração, crie um grupo administrativo no diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b06e4-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="b06e4-106">Este grupo administrativo especial denomina *AAD DC administradores*.</span><span class="sxs-lookup"><span data-stu-id="b06e4-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="b06e4-107">Os membros deste grupo recebem permissões administrativas nas máquinas que estão associados a um domínio toohello de domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="b06e4-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="b06e4-108">Em computadores associados a um domínio, este grupo é adicionado toohello grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="b06e4-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="b06e4-109">Além disso, os membros deste grupo podem utilizar o ambiente de trabalho remoto tooconnect remotamente toodomain computadores associados a um.</span><span class="sxs-lookup"><span data-stu-id="b06e4-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="b06e4-110">Não dispõe de permissões de administrador do domínio ou de administrador de empresa Olá domínio gerido que criou utilizando o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="b06e4-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b06e4-111">Nos domínios geridos, estas permissões são reservadas pelo serviço de Olá em não ficam disponíveis toousers no inquilino Olá.</span><span class="sxs-lookup"><span data-stu-id="b06e4-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="b06e4-112">No entanto, pode utilizar o Olá de grupo administrativo especial criada neste tooperform de tarefas de configuração privilegiado algumas operações.</span><span class="sxs-lookup"><span data-stu-id="b06e4-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="b06e4-113">Estas operações incluem a associação a domínio toohello de computadores, que pertence o grupo de administração de toohello em computadores associados a um domínio e a configuração de política de grupo.</span><span class="sxs-lookup"><span data-stu-id="b06e4-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="b06e4-114">Assistente de Olá cria automaticamente o grupo administrativo Olá no diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b06e4-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="b06e4-115">Este grupo é chamado 'AAD DC administradores'.</span><span class="sxs-lookup"><span data-stu-id="b06e4-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="b06e4-116">Se tiver um grupo existente com este nome no diretório do Azure AD, o Assistente de Olá seleciona deste grupo.</span><span class="sxs-lookup"><span data-stu-id="b06e4-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="b06e4-117">Pode configurar a associação ao grupo utilizando Olá **grupo Administrador** página do assistente.</span><span class="sxs-lookup"><span data-stu-id="b06e4-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="b06e4-118">associação ao grupo de tooconfigure, clique em **AAD DC administradores**.</span><span class="sxs-lookup"><span data-stu-id="b06e4-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurar a associação de grupo](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="b06e4-120">Clique em Olá **adicionar membros** botão tooadd utilizadores do seu grupo de administrador do toohello de diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b06e4-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="b06e4-121">Quando tiver terminado, clique em **OK** toomove no toohello **resumo** página do Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="b06e4-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="b06e4-122">No Olá **resumo** página do Assistente de Olá, definições de configuração de Olá revisão do domínio Olá de gerido.</span><span class="sxs-lookup"><span data-stu-id="b06e4-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="b06e4-123">Pode voltar atrás tooany passo do assistente toomake altera o Olá, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b06e4-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="b06e4-124">Quando tiver terminado, clique em **OK** toocreate Olá geridos novo domínio.</span><span class="sxs-lookup"><span data-stu-id="b06e4-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Resumo](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="b06e4-126">Verá uma notificação que mostra o progresso de Olá da sua implementação de serviços de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b06e4-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="b06e4-127">Clique em notificação Olá toosee detalhadas progresso para a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="b06e4-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Notificação - implementação em curso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="b06e4-129">Aprovisionar o seu domínio gerido</span><span class="sxs-lookup"><span data-stu-id="b06e4-129">Provision your managed domain</span></span>
<span data-ttu-id="b06e4-130">processo de Olá de aprovisionamento do seu domínio gerido pode demorar até tooan hora.</span><span class="sxs-lookup"><span data-stu-id="b06e4-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="b06e4-131">Enquanto a implementação está em curso, pode procurar 'Serviços de domínio' Olá **procurar recursos** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b06e4-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="b06e4-132">Selecione **serviços de domínio do Azure AD** do resultado de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="b06e4-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="b06e4-133">Olá **serviços de domínio do Azure AD** painel lista Olá domínio gerido que está a ser aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="b06e4-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Localizar o domínio gerido que está a ser aprovisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="b06e4-135">Clique no nome de Olá de Olá gerido (por exemplo, ' contoso100.com') do domínio toosee mais detalhes sobre o domínio de Olá.</span><span class="sxs-lookup"><span data-stu-id="b06e4-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Serviços de domínio - estado de aprovisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="b06e4-137">Olá **descrição geral** separador mostra esse domínio Olá está atualmente a ser aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="b06e4-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="b06e4-138">Não é possível configurar o domínio Olá de gerido até que esteja totalmente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="b06e4-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="b06e4-139">Esta operação pode demorar tooan hora para a sua toobe domínio gerido totalmente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="b06e4-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="b06e4-140">Serviços de domínio - separador de descrição geral durante Olá estado de aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="b06e4-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="b06e4-141">Quando o domínio gerido Olá esteja totalmente aprovisionado, Olá **descrição geral** separador mostra o estado de domínio de Olá como **executar**.</span><span class="sxs-lookup"><span data-stu-id="b06e4-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Serviços de domínio - separador Descrição geral depois de totalmente aprovisionado](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="b06e4-143">No Olá **propriedades** separador, verá dois endereços IP no qual o domínio estão disponíveis para a rede virtual Olá controladores.</span><span class="sxs-lookup"><span data-stu-id="b06e4-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Serviços de domínio - separador de propriedades depois totalmente aprovisionado](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="b06e4-145">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="b06e4-145">Next step</span></span>
[<span data-ttu-id="b06e4-146">Tarefa 4: atualizar as definições de DNS de Olá de Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b06e4-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
