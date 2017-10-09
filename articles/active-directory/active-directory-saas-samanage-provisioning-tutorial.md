---
title: "Tutorial: Configurar Samanage para aprovisionamento de utilizadores automática no Azure Active Directory | Microsoft Docs"
description: "Saiba como tooconfigure do Azure Active Directory tooautomatically aprovisionar e aprovisionar desativação do utilizador contas tooSamanage."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="e3d9d-103">Tutorial: Configurar Samanage para aprovisionamento de utilizadores automática</span><span class="sxs-lookup"><span data-stu-id="e3d9d-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="e3d9d-104">o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no Samanage e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e3d9d-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3d9d-105">Prerequisites</span></span>

<span data-ttu-id="e3d9d-106">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e3d9d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="e3d9d-107">Um inquilino do Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="e3d9d-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="e3d9d-108">Um inquilino Samanage com Olá [plano profissionais](https://www.samanage.com/pricing/) ou melhor ativado</span><span class="sxs-lookup"><span data-stu-id="e3d9d-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="e3d9d-109">Uma conta de utilizador no Samanage com permissões de administrador</span><span class="sxs-lookup"><span data-stu-id="e3d9d-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="e3d9d-110">Hello do Azure AD aprovisionamento integração depende Olá [API de REST Samanage](https://www.samanage.com/api/), que é equipas tooSamanage disponíveis no Olá Professional planear ou uma melhor.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="e3d9d-111">Atribuir utilizadores tooSamanage</span><span class="sxs-lookup"><span data-stu-id="e3d9d-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="e3d9d-112">Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="e3d9d-113">No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="e3d9d-114">Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos do Azure AD representam Olá os utilizadores que precisam de acesso tooyour Samanage aplicação.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="e3d9d-115">Depois de decidir, pode atribuir estas aplicações de Samanage tooyour utilizadores ao seguir as instruções de Olá aqui:</span><span class="sxs-lookup"><span data-stu-id="e3d9d-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="e3d9d-116">Atribuir um utilizador ou grupo tooan de aplicações</span><span class="sxs-lookup"><span data-stu-id="e3d9d-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="e3d9d-117">Sugestões importantes para atribuir utilizadores tooSamanage</span><span class="sxs-lookup"><span data-stu-id="e3d9d-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="e3d9d-118">Recomenda-se que um único utilizador do Azure AD é atribuído tooSamanage tootest Olá aprovisionamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="e3d9d-119">Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="e3d9d-120">Ao atribuir um tooSamanage de utilizador, tem de selecionar o Olá **utilizador** função, ou outra válida específicas da aplicação função (se disponível) na caixa de diálogo de atribuição de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="e3d9d-121">Olá **predefinido acesso** função não funciona para o aprovisionamento e estes utilizadores são ignorados.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d9d-122">Enquanto funcionalidade adicionada, Olá aprovisionamento do serviço lê quaisquer funções personalizadas definidas na Samanage e importa-los com o Azure AD, onde podem ser seleccionados na caixa de diálogo do Olá selecionar função.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="e3d9d-123">Estas funções serão visíveis na Olá portal do Azure após a ativação Olá aprovisionamento do serviço e um ciclo de sincronização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="e3d9d-124">Configurar tooSamanage de aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="e3d9d-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="e3d9d-125">Esta secção orienta-o ligar a API de aprovisionamento da conta de utilizador do seu tooSamanage do Azure AD e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuída Samanage com base na atribuição de utilizadores e grupos no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="e3d9d-126">Pode também optar por tooenabled baseados em SAML Single Sign-On para Samanage, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3d9d-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e3d9d-127">O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="e3d9d-128">Configure a conta de utilizador automáticas aprovisionamento tooSamanage no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e3d9d-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="e3d9d-129">No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="e3d9d-130">Se já tiver configurado Samanage para o início de sessão único, procure a instância do Samanage utilizando o campo de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="e3d9d-131">Caso contrário, selecione **adicionar** e procure **Samanage** na Galeria de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="e3d9d-132">Selecione Samanage os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="e3d9d-133">Selecione a sua instância do Samanage, em seguida, selecione Olá **aprovisionamento** separador.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="e3d9d-134">Conjunto Olá **modo de aprovisionamento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Aprovisionamento de Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="e3d9d-136">Em Olá **credenciais de administrador** secção, Olá entrada **nome de utilizador de Admin & palavra-passe de administrador** da conta da sua Samanage.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="e3d9d-137">No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se a aplicação de Samanage tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="e3d9d-138">Se falhar a ligação de Olá, certifique-se de que a conta de Samanage possui permissões de administrador e repita o passo 5.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="e3d9d-139">Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e a caixa de verificação de Olá de verificação "enviar uma notificação por e-mail quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="e3d9d-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="e3d9d-140">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-140">Click **Save**.</span></span> 

9. <span data-ttu-id="e3d9d-141">Na secção de mapeamentos Olá, selecione **sincronizar utilizadores do Azure Active Directory tooSamanage**.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="e3d9d-142">No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="e3d9d-143">Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador Samanage para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="e3d9d-144">Selecione Olá guardar botão toocommit quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="e3d9d-145">tooenable Olá serviço aprovisionamento do Azure AD para Samanage, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção</span><span class="sxs-lookup"><span data-stu-id="e3d9d-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="e3d9d-146">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-146">Click **Save**.</span></span> 

<span data-ttu-id="e3d9d-147">Esta operação inicia a sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooSamanage no Olá utilizadores e a secção de grupos.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="e3d9d-148">a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="e3d9d-149">Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço.</span><span class="sxs-lookup"><span data-stu-id="e3d9d-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="e3d9d-150">Para obter mais informações sobre como os registos de aprovisionamento do tooread Olá do Azure AD, consulte [relatórios sobre o aprovisionamento da conta de utilizador automáticas](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="e3d9d-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e3d9d-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e3d9d-151">Additional resources</span></span>

* [<span data-ttu-id="e3d9d-152">Gerir o aprovisionamento da conta de utilizador para aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="e3d9d-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="e3d9d-153">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3d9d-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="e3d9d-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e3d9d-154">Next steps</span></span>

* [<span data-ttu-id="e3d9d-155">Saiba como tooreview os registos e obter relatórios sobre o aprovisionamento de atividade</span><span class="sxs-lookup"><span data-stu-id="e3d9d-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
