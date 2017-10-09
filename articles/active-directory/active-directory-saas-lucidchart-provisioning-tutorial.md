---
title: "Tutorial: Configurar LucidChart para aprovisionamento de utilizadores automática no Azure Active Directory | Microsoft Docs"
description: "Saiba como tooconfigure do Azure Active Directory tooautomatically aprovisionar e aprovisionar desativação do utilizador contas tooLucidChart."
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="6874f-103">Tutorial: Configurar LucidChart para aprovisionamento de utilizadores automática</span><span class="sxs-lookup"><span data-stu-id="6874f-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="6874f-104">o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no LucidChart e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="6874f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6874f-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6874f-105">Prerequisites</span></span>

<span data-ttu-id="6874f-106">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6874f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="6874f-107">Um inquilino do Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="6874f-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="6874f-108">Um inquilino LucidChart com Olá [plano empresarial](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou melhor ativado</span><span class="sxs-lookup"><span data-stu-id="6874f-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="6874f-109">Uma conta de utilizador no LucidChart com permissões de administrador</span><span class="sxs-lookup"><span data-stu-id="6874f-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="6874f-110">Atribuir utilizadores tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="6874f-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="6874f-111">Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações.</span><span class="sxs-lookup"><span data-stu-id="6874f-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="6874f-112">No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado.</span><span class="sxs-lookup"><span data-stu-id="6874f-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="6874f-113">Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos do Azure AD representam Olá os utilizadores que precisam de acesso tooyour LucidChart aplicação.</span><span class="sxs-lookup"><span data-stu-id="6874f-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="6874f-114">Depois de decidir, pode atribuir estas aplicações de LucidChart tooyour utilizadores ao seguir as instruções de Olá aqui:</span><span class="sxs-lookup"><span data-stu-id="6874f-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="6874f-115">Atribuir um utilizador ou grupo tooan de aplicações</span><span class="sxs-lookup"><span data-stu-id="6874f-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="6874f-116">Sugestões importantes para atribuir utilizadores tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="6874f-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="6874f-117">Recomenda-se que um único utilizador do Azure AD é atribuído tooLucidChart tootest Olá aprovisionamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="6874f-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="6874f-118">Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="6874f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="6874f-119">Ao atribuir um tooLucidChart de utilizador, tem de selecionar o Olá **utilizador** função, ou outra válida específicas da aplicação função (se disponível) na caixa de diálogo de atribuição de Olá.</span><span class="sxs-lookup"><span data-stu-id="6874f-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="6874f-120">Olá **predefinido acesso** função não funciona para o aprovisionamento e estes utilizadores são ignorados.</span><span class="sxs-lookup"><span data-stu-id="6874f-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="6874f-121">Configurar tooLucidChart de aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="6874f-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="6874f-122">Esta secção orienta-o ligar a API de aprovisionamento da conta de utilizador do seu tooLucidChart do Azure AD e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuída LucidChart com base na atribuição de utilizadores e grupos no Azure AD .</span><span class="sxs-lookup"><span data-stu-id="6874f-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="6874f-123">Pode também optar por tooenabled baseados em SAML Single Sign-On para LucidChart, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6874f-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6874f-124">O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.</span><span class="sxs-lookup"><span data-stu-id="6874f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="6874f-125">Configurar conta de utilizador automática aprovisionamento tooLucidChart no Azure AD</span><span class="sxs-lookup"><span data-stu-id="6874f-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="6874f-126">No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.</span><span class="sxs-lookup"><span data-stu-id="6874f-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="6874f-127">Se já tiver configurado LucidChart para o início de sessão único, procure a instância do LucidChart utilizando o campo de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="6874f-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="6874f-128">Caso contrário, selecione **adicionar** e procure **LucidChart** na Galeria de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="6874f-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="6874f-129">Selecione LucidChart os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.</span><span class="sxs-lookup"><span data-stu-id="6874f-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="6874f-130">Selecione a sua instância do LucidChart, em seguida, selecione Olá **aprovisionamento** separador.</span><span class="sxs-lookup"><span data-stu-id="6874f-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="6874f-131">Conjunto Olá **modo de aprovisionamento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="6874f-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Aprovisionamento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="6874f-133">Em Olá **credenciais de administrador** secção, Olá entrada **segredo Token** gerado pela conta do seu LucidChart (pode encontrar o token de Olá na sua conta: **equipa**  >  **Integração de aplicações** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="6874f-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Aprovisionamento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="6874f-135">No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se a aplicação de LucidChart tooyour.</span><span class="sxs-lookup"><span data-stu-id="6874f-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="6874f-136">Se falhar a ligação de Olá, certifique-se de que a conta de LucidChart possui permissões de administrador e repita o passo 5.</span><span class="sxs-lookup"><span data-stu-id="6874f-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="6874f-137">Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e a caixa de verificação de Olá de verificação "enviar uma notificação por e-mail quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="6874f-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="6874f-138">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6874f-138">Click **Save**.</span></span> 

9. <span data-ttu-id="6874f-139">Na secção de mapeamentos Olá, selecione **sincronizar utilizadores do Azure Active Directory tooLucidChart**.</span><span class="sxs-lookup"><span data-stu-id="6874f-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="6874f-140">No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="6874f-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="6874f-141">Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador LucidChart para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="6874f-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="6874f-142">Selecione Olá guardar botão toocommit quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="6874f-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="6874f-143">tooenable Olá serviço aprovisionamento do Azure AD para LucidChart, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção</span><span class="sxs-lookup"><span data-stu-id="6874f-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="6874f-144">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6874f-144">Click **Save**.</span></span> 

<span data-ttu-id="6874f-145">Esta operação inicia a sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooLucidChart no Olá utilizadores e a secção de grupos.</span><span class="sxs-lookup"><span data-stu-id="6874f-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="6874f-146">a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="6874f-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="6874f-147">Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço.</span><span class="sxs-lookup"><span data-stu-id="6874f-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="6874f-148">Para obter mais informações sobre como os registos de aprovisionamento do tooread Olá do Azure AD, consulte [relatórios sobre o aprovisionamento da conta de utilizador automáticas](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="6874f-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6874f-149">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6874f-149">Additional resources</span></span>

* [<span data-ttu-id="6874f-150">Gerir o aprovisionamento da conta de utilizador para aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="6874f-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="6874f-151">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6874f-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="6874f-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6874f-152">Next steps</span></span>

* [<span data-ttu-id="6874f-153">Saiba como tooreview os registos e obter relatórios sobre o aprovisionamento de atividade</span><span class="sxs-lookup"><span data-stu-id="6874f-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
