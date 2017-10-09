---
title: "Tutorial: Integração do Azure Active Directory com o Dropbox para empresas | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Dropbox para empresas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="8bda2-103">Tutorial: Configurar o Dropbox para empresas para aprovisionamento de utilizadores automática</span><span class="sxs-lookup"><span data-stu-id="8bda2-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="8bda2-104">o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no Dropbox para empresas e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="8bda2-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bda2-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8bda2-105">Prerequisites</span></span>

<span data-ttu-id="8bda2-106">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8bda2-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8bda2-107">Um inquilino do Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="8bda2-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="8bda2-108">Um Dropbox para empresas início de sessão único subscrição ativado.</span><span class="sxs-lookup"><span data-stu-id="8bda2-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="8bda2-109">Uma conta de utilizador no Dropbox para empresas com permissões de administrador de equipa.</span><span class="sxs-lookup"><span data-stu-id="8bda2-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="8bda2-110">Atribuir utilizadores tooDropbox para empresas</span><span class="sxs-lookup"><span data-stu-id="8bda2-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="8bda2-111">Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações.</span><span class="sxs-lookup"><span data-stu-id="8bda2-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8bda2-112">No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado.</span><span class="sxs-lookup"><span data-stu-id="8bda2-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="8bda2-113">Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder tooyour Dropbox para a aplicação de negócio.</span><span class="sxs-lookup"><span data-stu-id="8bda2-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="8bda2-114">Depois de decidir, pode atribuir estes tooyour utilizadores Dropbox para a aplicação de negócio, seguindo as instruções de Olá aqui:</span><span class="sxs-lookup"><span data-stu-id="8bda2-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="8bda2-115">Atribuir um utilizador ou grupo tooan de aplicações</span><span class="sxs-lookup"><span data-stu-id="8bda2-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="8bda2-116">Sugestões importantes para atribuir utilizadores tooDropbox para empresas</span><span class="sxs-lookup"><span data-stu-id="8bda2-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="8bda2-117">Recomenda-se que um único utilizador do Azure AD é atribuído tooDropbox para Olá do negócio tootest aprovisionamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="8bda2-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="8bda2-118">Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="8bda2-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8bda2-119">Ao atribuir um tooDropbox de utilizador para empresas, tem de selecionar uma função de utilizador válido.</span><span class="sxs-lookup"><span data-stu-id="8bda2-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="8bda2-120">função de "Acesso predefinida" Olá não funciona para o aprovisionamento...</span><span class="sxs-lookup"><span data-stu-id="8bda2-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="8bda2-121">Ativar o aprovisionamento automatizado do utilizador</span><span class="sxs-lookup"><span data-stu-id="8bda2-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="8bda2-122">Esta secção orienta-o ligar a sua tooDropbox do Azure AD para a conta de utilizador de negócio API de aprovisionamento e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuído no Dropbox para empresas com base no utilizador e grupo atribuição no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bda2-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="8bda2-123">Pode também optar por tooenabled baseados em SAML Single Sign-On para Dropbox para empresas, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bda2-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8bda2-124">O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.</span><span class="sxs-lookup"><span data-stu-id="8bda2-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="8bda2-125">tooconfigure aprovisionamento da conta utilizador automáticas:</span><span class="sxs-lookup"><span data-stu-id="8bda2-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="8bda2-126">No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.</span><span class="sxs-lookup"><span data-stu-id="8bda2-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="8bda2-127">Se já tiver configurado o Dropbox para empresas para o início de sessão único, procure a instância da Dropbox para empresas com o campo de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="8bda2-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="8bda2-128">Caso contrário, selecione **adicionar** e procure **Dropbox para empresas** na Galeria de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="8bda2-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="8bda2-129">Selecione o Dropbox para empresas dos resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.</span><span class="sxs-lookup"><span data-stu-id="8bda2-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="8bda2-130">Selecione a instância da Dropbox para empresas, em seguida, selecione Olá **aprovisionamento** separador.</span><span class="sxs-lookup"><span data-stu-id="8bda2-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="8bda2-131">Conjunto Olá **modo de aprovisionamento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="8bda2-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="8bda2-133">Em Olá **credenciais de administrador** secção, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="8bda2-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="8bda2-134">É aberta uma Dropbox para a caixa de diálogo de início de sessão de negócio numa nova janela do browser.</span><span class="sxs-lookup"><span data-stu-id="8bda2-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="8bda2-135">No Olá **início de sessão tooDropbox toolink com o Azure AD** caixa de diálogo, início de sessão tooyour Dropbox para o inquilino de negócio.</span><span class="sxs-lookup"><span data-stu-id="8bda2-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="8bda2-136">![Aprovisionamento de utilizadores](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "aprovisionamento de utilizadores")</span><span class="sxs-lookup"><span data-stu-id="8bda2-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="8bda2-137">Certifique-se de que pretende toogive do Azure Active Directory permissão toomake alterações tooyour Dropbox para o inquilino de negócio.</span><span class="sxs-lookup"><span data-stu-id="8bda2-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="8bda2-138">Clique em **permitir**.</span><span class="sxs-lookup"><span data-stu-id="8bda2-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="8bda2-139">![Aprovisionamento de utilizadores](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "aprovisionamento de utilizadores")</span><span class="sxs-lookup"><span data-stu-id="8bda2-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="8bda2-140">No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar tooyour Dropbox para a aplicação de negócio.</span><span class="sxs-lookup"><span data-stu-id="8bda2-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="8bda2-141">Se falhar a ligação de Olá, certifique-se a Dropbox para a conta tem permissões de administração de equipa e tente Olá **"Autorizar"** passo novamente.</span><span class="sxs-lookup"><span data-stu-id="8bda2-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="8bda2-142">Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e marque Olá caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="8bda2-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="8bda2-143">Clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="8bda2-143">Click **Save.**</span></span>

11. <span data-ttu-id="8bda2-144">Na secção de mapeamentos Olá, selecione **tooDropbox sincronizar utilizadores do Azure Active Directory para empresas.**</span><span class="sxs-lookup"><span data-stu-id="8bda2-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="8bda2-145">No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="8bda2-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="8bda2-146">Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador Dropbox para empresas para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="8bda2-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="8bda2-147">Selecione Olá guardar botão toocommit quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="8bda2-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="8bda2-148">tooenable Olá serviço aprovisionamento do Azure AD para Dropbox para empresas, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá secção de definições</span><span class="sxs-lookup"><span data-stu-id="8bda2-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="8bda2-149">Clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="8bda2-149">Click **Save.**</span></span>

<span data-ttu-id="8bda2-150">Iniciar sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooDropbox para empresas no Olá utilizadores e a secção de grupos.</span><span class="sxs-lookup"><span data-stu-id="8bda2-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="8bda2-151">a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="8bda2-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="8bda2-152">Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento para a aplicação de negócio do serviço no seu Dropbox.</span><span class="sxs-lookup"><span data-stu-id="8bda2-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="8bda2-153">Agora, pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="8bda2-153">You can now create a test account.</span></span> <span data-ttu-id="8bda2-154">Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="8bda2-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="8bda2-155">Um ciclo de aprovisionamento de utilizadores concluída com êxito é indicada pelo Estado relacionado.</span><span class="sxs-lookup"><span data-stu-id="8bda2-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="8bda2-156">![Atribuir utilizadores](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "atribuir utilizadores")</span><span class="sxs-lookup"><span data-stu-id="8bda2-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8bda2-157">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8bda2-157">Additional resources</span></span>

* [<span data-ttu-id="8bda2-158">Gerir o aprovisionamento da conta de utilizador para aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="8bda2-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bda2-159">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bda2-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8bda2-160">Configurar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="8bda2-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)