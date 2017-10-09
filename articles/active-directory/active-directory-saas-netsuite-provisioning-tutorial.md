---
title: "Tutorial: Integração do Azure Active Directory com Netsuite | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="0cbff-103">Tutorial: Configurar Netsuite para aprovisionamento de utilizadores automática</span><span class="sxs-lookup"><span data-stu-id="0cbff-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="0cbff-104">o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no Netsuite e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="0cbff-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cbff-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0cbff-105">Prerequisites</span></span>

<span data-ttu-id="0cbff-106">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0cbff-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="0cbff-107">Um inquilino do Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="0cbff-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0cbff-108">Um Netsuite início de sessão único subscrição ativado.</span><span class="sxs-lookup"><span data-stu-id="0cbff-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="0cbff-109">Uma conta de utilizador no Netsuite com permissões de administrador de equipa.</span><span class="sxs-lookup"><span data-stu-id="0cbff-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="0cbff-110">Atribuir utilizadores tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="0cbff-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="0cbff-111">Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações.</span><span class="sxs-lookup"><span data-stu-id="0cbff-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0cbff-112">No contexto de Olá de aprovisionamento da conta de utilizador automático, são sincronizados apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cbff-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="0cbff-113">Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos do Azure AD representam Olá os utilizadores que precisam de acesso tooyour Netsuite aplicação.</span><span class="sxs-lookup"><span data-stu-id="0cbff-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="0cbff-114">Depois de decidir, pode atribuir estas aplicações de Netsuite tooyour utilizadores ao seguir as instruções de Olá aqui:</span><span class="sxs-lookup"><span data-stu-id="0cbff-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="0cbff-115">Atribuir um utilizador ou grupo tooan de aplicações</span><span class="sxs-lookup"><span data-stu-id="0cbff-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="0cbff-116">Sugestões importantes para atribuir utilizadores tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="0cbff-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="0cbff-117">Recomenda-se que um único utilizador do Azure AD é atribuído tooNetsuite tootest Olá aprovisionamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="0cbff-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="0cbff-118">Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0cbff-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0cbff-119">Ao atribuir um tooNetsuite de utilizador, tem de selecionar uma função de utilizador válido.</span><span class="sxs-lookup"><span data-stu-id="0cbff-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="0cbff-120">função de "Acesso predefinida" Olá não funciona para o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="0cbff-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="0cbff-121">Ativar o aprovisionamento de utilizador</span><span class="sxs-lookup"><span data-stu-id="0cbff-121">Enable User Provisioning</span></span>

<span data-ttu-id="0cbff-122">Esta secção orienta-o ligar a API de aprovisionamento da conta de utilizador do seu tooNetsuite do Azure AD e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuída Netsuite com base na atribuição de utilizadores e grupos no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cbff-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="0cbff-123">Pode também optar por tooenabled baseados em SAML Single Sign-On para Netsuite, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0cbff-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0cbff-124">O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.</span><span class="sxs-lookup"><span data-stu-id="0cbff-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="0cbff-125">Aprovisionamento de conta do utilizador de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="0cbff-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="0cbff-126">o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory tooNetsuite de contas.</span><span class="sxs-lookup"><span data-stu-id="0cbff-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="0cbff-127">No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.</span><span class="sxs-lookup"><span data-stu-id="0cbff-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="0cbff-128">Se já tiver configurado Netsuite para o início de sessão único, procure a instância do Netsuite utilizando o campo de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="0cbff-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="0cbff-129">Caso contrário, selecione **adicionar** e procure **Netsuite** na Galeria de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cbff-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="0cbff-130">Selecione Netsuite os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.</span><span class="sxs-lookup"><span data-stu-id="0cbff-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="0cbff-131">Selecione a sua instância do Netsuite, em seguida, selecione Olá **aprovisionamento** separador.</span><span class="sxs-lookup"><span data-stu-id="0cbff-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="0cbff-132">Conjunto Olá **modo de aprovisionamento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="0cbff-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamento](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="0cbff-134">Em Olá **credenciais de administrador** secção, forneça Olá seguintes definições de configuração:</span><span class="sxs-lookup"><span data-stu-id="0cbff-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="0cbff-135">a.</span><span class="sxs-lookup"><span data-stu-id="0cbff-135">a.</span></span> <span data-ttu-id="0cbff-136">No Olá **nome de utilizador de Admin** caixa de texto, tipo um Netsuite conta nome que tem Olá **administrador de sistema** perfil no Netsuite.com atribuído.</span><span class="sxs-lookup"><span data-stu-id="0cbff-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="0cbff-137">b.</span><span class="sxs-lookup"><span data-stu-id="0cbff-137">b.</span></span> <span data-ttu-id="0cbff-138">No Olá **palavra-passe de administrador** caixa de texto, tipo Olá palavra-passe desta conta.</span><span class="sxs-lookup"><span data-stu-id="0cbff-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="0cbff-139">No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se a aplicação de Netsuite tooyour.</span><span class="sxs-lookup"><span data-stu-id="0cbff-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="0cbff-140">No Olá **correio eletrónico de notificação** campo, introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro de aprovisionamento e marque Olá caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="0cbff-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="0cbff-141">Clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="0cbff-141">Click **Save.**</span></span>

9. <span data-ttu-id="0cbff-142">Na secção de mapeamentos Olá, selecione **tooNetsuite sincronizar utilizadores do Azure Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="0cbff-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="0cbff-143">No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="0cbff-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="0cbff-144">Tenha em atenção que Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador Netsuite para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="0cbff-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="0cbff-145">Selecione Olá guardar botão toocommit quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="0cbff-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="0cbff-146">tooenable Olá serviço aprovisionamento do Azure AD para Netsuite, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá secção de definições</span><span class="sxs-lookup"><span data-stu-id="0cbff-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="0cbff-147">Clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="0cbff-147">Click **Save.**</span></span>

<span data-ttu-id="0cbff-148">Iniciar sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooNetsuite no Olá utilizadores e a secção de grupos.</span><span class="sxs-lookup"><span data-stu-id="0cbff-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="0cbff-149">Tenha em atenção que a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="0cbff-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="0cbff-150">Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço na sua aplicação Netsuite.</span><span class="sxs-lookup"><span data-stu-id="0cbff-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="0cbff-151">Agora, pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="0cbff-151">You can now create a test account.</span></span> <span data-ttu-id="0cbff-152">Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="0cbff-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0cbff-153">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0cbff-153">Additional resources</span></span>

* [<span data-ttu-id="0cbff-154">Gerir o aprovisionamento da conta de utilizador para aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="0cbff-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cbff-155">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cbff-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0cbff-156">Configurar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0cbff-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)