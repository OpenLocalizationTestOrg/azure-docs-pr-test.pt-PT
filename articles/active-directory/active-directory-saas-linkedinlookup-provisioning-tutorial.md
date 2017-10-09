---
title: "Tutorial: Configurar LinkedIn pesquisa para o aprovisionamento de utilizadores automática no Azure Active Directory | Microsoft Docs"
description: "Saiba como tooconfigure do Azure Active Directory tooautomatically aprovisionar e aprovisionar desativação do utilizador contas tooLinkedIn pesquisa."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="89ed5-103">Tutorial: Configurar LinkedIn pesquisa para o aprovisionamento de utilizadores automática</span><span class="sxs-lookup"><span data-stu-id="89ed5-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="89ed5-104">o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform na pesquisa do LinkedIn e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="89ed5-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Lookup and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="89ed5-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89ed5-105">Prerequisites</span></span>

<span data-ttu-id="89ed5-106">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="89ed5-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="89ed5-107">Um inquilino do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89ed5-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="89ed5-108">Um inquilino LinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="89ed5-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="89ed5-109">Uma conta de administrador na pesquisa do LinkedIn com acesso toohello LinkedIn do Centro de contas</span><span class="sxs-lookup"><span data-stu-id="89ed5-109">An administrator account in LinkedIn Lookup with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="89ed5-110">Azure Active Directory se integra com pesquisa de LinkedIn com Olá [SCIM](http://www.simplecloud.info/) protocolo.</span><span class="sxs-lookup"><span data-stu-id="89ed5-110">Azure Active Directory integrates with LinkedIn Lookup using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-lookup"></a><span data-ttu-id="89ed5-111">Atribuir utilizadores tooLinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="89ed5-111">Assigning users tooLinkedIn Lookup</span></span>

<span data-ttu-id="89ed5-112">Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações.</span><span class="sxs-lookup"><span data-stu-id="89ed5-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="89ed5-113">No contexto de Olá de aprovisionamento da conta de utilizador automáticas, serão sincronizados apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ed5-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="89ed5-114">Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="89ed5-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Lookup.</span></span> <span data-ttu-id="89ed5-115">Depois de decidir, pode atribuir tooLinkedIn estes utilizadores pesquisa ao seguir as instruções de Olá aqui:</span><span class="sxs-lookup"><span data-stu-id="89ed5-115">Once decided, you can assign these users tooLinkedIn Lookup by following hello instructions here:</span></span>

[<span data-ttu-id="89ed5-116">Atribuir um utilizador ou grupo tooan de aplicações</span><span class="sxs-lookup"><span data-stu-id="89ed5-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a><span data-ttu-id="89ed5-117">Sugestões importantes para atribuir utilizadores tooLinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="89ed5-117">Important tips for assigning users tooLinkedIn Lookup</span></span>

*   <span data-ttu-id="89ed5-118">Recomenda-se que um único utilizador do Azure AD ser atribuídos Olá tootest pesquisa de tooLinkedIn aprovisionamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="89ed5-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Lookup tootest hello provisioning configuration.</span></span> <span data-ttu-id="89ed5-119">Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="89ed5-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="89ed5-120">Ao atribuir uma pesquisa de tooLinkedIn do utilizador, tem de selecionar Olá **utilizador** função na caixa de diálogo de atribuição de Olá.</span><span class="sxs-lookup"><span data-stu-id="89ed5-120">When assigning a user tooLinkedIn Lookup, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="89ed5-121">função de "Acesso predefinida" Olá não funciona para o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="89ed5-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a><span data-ttu-id="89ed5-122">Configurar tooLinkedIn pesquisa de aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="89ed5-122">Configuring user provisioning tooLinkedIn Lookup</span></span>

<span data-ttu-id="89ed5-123">Esta secção orienta-o ligar a conta de utilizador do seu Azure AD tooLinkedIn pesquisa SCIM aprovisionamento API e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar o utilizador atribuído contas no LinkedIn pesquisa com base no utilizador e grupo atribuição no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ed5-123">This section guides you through connecting your Azure AD tooLinkedIn Lookup's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="89ed5-124">Pode também optar por tooenabled baseados em SAML Single Sign-On para a pesquisa de LinkedIn, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="89ed5-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Lookup, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="89ed5-125">O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementam entre si.</span><span class="sxs-lookup"><span data-stu-id="89ed5-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a><span data-ttu-id="89ed5-126">conta de utilizador automáticas tooconfigure aprovisionamento tooLinkedIn pesquisa no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="89ed5-126">tooconfigure automatic user account provisioning tooLinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="89ed5-127">primeiro passo de Olá é tooretrieve seu token de acesso LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="89ed5-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="89ed5-128">Se for um administrador de empresa, pode aprovisionar um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="89ed5-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="89ed5-129">No seu centro de contas, aceda demasiado**definições &gt; definições globais** e abra Olá **SCIM configuração** painel.</span><span class="sxs-lookup"><span data-stu-id="89ed5-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="89ed5-130">Se está a aceder ao centro de contas de Olá diretamente em vez de através de uma ligação, pode chegá-la utilizando Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="89ed5-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="89ed5-131">Inicie sessão no Centro de tooAccount.</span><span class="sxs-lookup"><span data-stu-id="89ed5-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="89ed5-132">Selecione **Admin &gt; definições de administrador** .</span><span class="sxs-lookup"><span data-stu-id="89ed5-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="89ed5-133">Clique em **avançadas integrações** na barra lateral esquerdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="89ed5-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="89ed5-134">São direcionados toohello do Centro de contas.</span><span class="sxs-lookup"><span data-stu-id="89ed5-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="89ed5-135">Clique em **+ Adicionar nova configuração de SCIM** e siga o procedimento de Olá preenchendo em cada campo.</span><span class="sxs-lookup"><span data-stu-id="89ed5-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="89ed5-136">Quando autoassign licenças não estiver ativada, significa que apenas os dados de utilizador estão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="89ed5-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="89ed5-138">Quando a atribuição de autolicense estiver ativada, terá de toonote a instância da aplicação e tipo de licença.</span><span class="sxs-lookup"><span data-stu-id="89ed5-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="89ed5-139">São atribuídas as licenças num provenientes do primeiro, primeiro servir base até que todas as licenças de Olá são executadas.</span><span class="sxs-lookup"><span data-stu-id="89ed5-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="89ed5-141">Clique em **gerar token**.</span><span class="sxs-lookup"><span data-stu-id="89ed5-141">Click **Generate token**.</span></span> <span data-ttu-id="89ed5-142">Deverá ver o seu ecrã de token de acesso em Olá **token de acesso** campo.</span><span class="sxs-lookup"><span data-stu-id="89ed5-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="89ed5-143">Guarde a sua área de transferência de token tooyour de acesso ou o computador antes de deixarem a página Olá.</span><span class="sxs-lookup"><span data-stu-id="89ed5-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="89ed5-144">Em seguida, inicie sessão no toohello [portal do Azure](https://portal.azure.com)e procure toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.</span><span class="sxs-lookup"><span data-stu-id="89ed5-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="89ed5-145">Se já tiver configurado o LinkedIn pesquisa para o início de sessão único, procure a instância de pesquisa de LinkedIn com o campo de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="89ed5-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using hello search field.</span></span> <span data-ttu-id="89ed5-146">Caso contrário, selecione **adicionar** e procure **LinkedIn pesquisa** na Galeria de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="89ed5-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in hello application gallery.</span></span> <span data-ttu-id="89ed5-147">Selecione LinkedIn pesquisa de resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.</span><span class="sxs-lookup"><span data-stu-id="89ed5-147">Select LinkedIn Lookup from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="89ed5-148">Selecione a sua instância do LinkedIn pesquisa, em seguida, selecione Olá **aprovisionamento** separador.</span><span class="sxs-lookup"><span data-stu-id="89ed5-148">Select your instance of LinkedIn Lookup, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="89ed5-149">Conjunto Olá **modo de aprovisionamento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="89ed5-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="89ed5-151">Preencha Olá seguintes campos em **credenciais de administrador** :</span><span class="sxs-lookup"><span data-stu-id="89ed5-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="89ed5-152">No Olá **URL de inquilino** campo, introduza https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="89ed5-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="89ed5-153">No Olá **segredo Token** campo, introduza o token de acesso de Olá gerados no passo 1 e clique em **Testar ligação** .</span><span class="sxs-lookup"><span data-stu-id="89ed5-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="89ed5-154">Deverá ver uma notificação de sucesso no lado de upperright Olá do seu portal.</span><span class="sxs-lookup"><span data-stu-id="89ed5-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="89ed5-155">Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e marque Olá caixa de verificação abaixo.</span><span class="sxs-lookup"><span data-stu-id="89ed5-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="89ed5-156">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="89ed5-156">Click **Save**.</span></span> 

14) <span data-ttu-id="89ed5-157">No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador e grupo Olá que serão sincronizados a partir do Azure AD tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="89ed5-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Lookup.</span></span> <span data-ttu-id="89ed5-158">Tenha em atenção que Olá atributos selecionados como **correspondência** propriedades será toomatch utilizadas contas de utilizador de Olá e grupos na pesquisa do LinkedIn para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="89ed5-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="89ed5-159">Selecione Olá guardar botão toocommit quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="89ed5-159">Select hello Save button toocommit any changes.</span></span>

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="89ed5-161">tooenable Olá serviço aprovisionamento do Azure AD para a pesquisa de LinkedIn, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção</span><span class="sxs-lookup"><span data-stu-id="89ed5-161">tooenable hello Azure AD provisioning service for LinkedIn Lookup, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="89ed5-162">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="89ed5-162">Click **Save**.</span></span> 

<span data-ttu-id="89ed5-163">Isto iniciará a sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooLinkedIn procura na secção de utilizadores e grupos de Olá.</span><span class="sxs-lookup"><span data-stu-id="89ed5-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Lookup in hello Users and Groups section.</span></span> <span data-ttu-id="89ed5-164">Tenha em atenção que a sincronização inicial Olá irá demorar mais longo tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="89ed5-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="89ed5-165">Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço na sua aplicação de pesquisa de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="89ed5-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="89ed5-166">Recursos Adicionais</span><span class="sxs-lookup"><span data-stu-id="89ed5-166">Additional Resources</span></span>

* [<span data-ttu-id="89ed5-167">Gerir o aprovisionamento da conta de utilizador para aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="89ed5-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="89ed5-168">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89ed5-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
