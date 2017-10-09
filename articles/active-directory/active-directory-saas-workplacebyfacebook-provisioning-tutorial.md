---
title: "Tutorial: Integração do Azure Active Directory a área de trabalho por Facebook | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e à área de trabalho por Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="b5429-103">Tutorial: Configurar à área de trabalho ao Facebook para aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="b5429-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="b5429-104">o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform na área de trabalho por Facebook e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooWorkplace por Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5429-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b5429-105">Prerequisites</span></span>

<span data-ttu-id="b5429-106">integração do Azure AD a área de trabalho por Facebook tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b5429-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="b5429-107">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5429-107">An Azure AD subscription</span></span>
- <span data-ttu-id="b5429-108">Uma área de trabalho por Facebook início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="b5429-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5429-109">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b5429-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5429-110">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b5429-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5429-111">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b5429-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5429-112">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5429-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="b5429-113">Atribuir utilizadores tooWorkplace por Facebook</span><span class="sxs-lookup"><span data-stu-id="b5429-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="b5429-114">Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações.</span><span class="sxs-lookup"><span data-stu-id="b5429-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b5429-115">No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado.</span><span class="sxs-lookup"><span data-stu-id="b5429-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b5429-116">Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder à área de trabalho de tooyour pela aplicação do Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="b5429-117">Depois de decidir, pode atribuir estes tooyour de utilizadores à área de trabalho através da aplicação do Facebook, seguindo as instruções de Olá aqui:</span><span class="sxs-lookup"><span data-stu-id="b5429-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="b5429-118">Atribuir um utilizador ou grupo tooan de aplicações</span><span class="sxs-lookup"><span data-stu-id="b5429-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="b5429-119">Sugestões importantes para atribuir utilizadores tooWorkplace por Facebook</span><span class="sxs-lookup"><span data-stu-id="b5429-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="b5429-120">Recomenda-se que um único utilizador do Azure AD é atribuído tooWorkplace pelo Facebook tootest Olá aprovisionamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="b5429-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="b5429-121">Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b5429-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b5429-122">Ao atribuir um tooWorkplace de utilizador, Facebook, tem de selecionar uma função de utilizador válido.</span><span class="sxs-lookup"><span data-stu-id="b5429-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="b5429-123">função de "Acesso predefinida" Olá não funciona para o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="b5429-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="b5429-124">Ativar o aprovisionamento de utilizador</span><span class="sxs-lookup"><span data-stu-id="b5429-124">Enable User Provisioning</span></span>

<span data-ttu-id="b5429-125">Esta secção orienta-o ao ligar o tooWorkplace do Azure AD através da API de aprovisionamento da conta de utilizador do Facebook e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuído na área de trabalho por Facebook com base no utilizador e grupo atribuição no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5429-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="b5429-126">Pode também optar por tooenabled baseados em SAML Single Sign-On para a área de trabalho, Facebook, seguindo as instruções de Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5429-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b5429-127">O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.</span><span class="sxs-lookup"><span data-stu-id="b5429-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="b5429-128">conta de utilizador tooconfigure aprovisionamento tooWorkplace por Facebook no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b5429-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="b5429-129">o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizador do Active Directory contas tooWorkplace por Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="b5429-130">Azure suporta de AD Olá capacidade tooautomatically sincronizar detalhes da conta de Olá atribuído tooWorkplace de utilizadores por Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="b5429-131">Esta sincronização automática permite à área de trabalho por necessita que os utilizadores tooauthorize de acesso, antes de dados do Facebook tooget Olá-las de tentar toosign para Olá pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="b5429-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="b5429-132">É também anular Aprovisiona os utilizadores da área de trabalho por Facebook quando foi revogado acesso no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5429-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="b5429-133">No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory** > **aplicações da empresa** > **todas as aplicações** secção.</span><span class="sxs-lookup"><span data-stu-id="b5429-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="b5429-134">Se já tiver configurado a área de trabalho ao Facebook para o início de sessão único, procure a instância da área de trabalho por Facebook utilizando o campo de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="b5429-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="b5429-135">Caso contrário, selecione **adicionar** e procure **à área de trabalho por Facebook** na Galeria de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5429-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="b5429-136">Selecione a área de trabalho por Facebook os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.</span><span class="sxs-lookup"><span data-stu-id="b5429-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b5429-137">Selecione a instância da área de trabalho, Facebook, em seguida, selecione Olá **aprovisionamento** separador.</span><span class="sxs-lookup"><span data-stu-id="b5429-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b5429-138">Conjunto Olá **modo de aprovisionamento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="b5429-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b5429-140">Em Olá **credenciais de administrador** secção, introduza Olá segredo Token e Olá URL de inquilino da sua área de trabalho pelo administrador do Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="b5429-141">No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se à área de trabalho de tooyour pela aplicação do Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="b5429-142">Se falhar a ligação de Olá, certifique-se à sua área de trabalho pela conta do Facebook permissões de administração de equipa.</span><span class="sxs-lookup"><span data-stu-id="b5429-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="b5429-143">Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e marque Olá caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="b5429-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="b5429-144">Clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="b5429-144">Click **Save.**</span></span>

9. <span data-ttu-id="b5429-145">Na secção de mapeamentos Olá, selecione **tooWorkplace sincronizar utilizadores do Azure Active Directory, Facebook.**</span><span class="sxs-lookup"><span data-stu-id="b5429-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="b5429-146">No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooWorkplace por Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="b5429-147">Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá as contas de utilizador na área de trabalho ao Facebook para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="b5429-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="b5429-148">Selecione Olá guardar botão toocommit quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="b5429-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="b5429-149">tooenable Olá serviço aprovisionamento do Azure AD para a área de trabalho, Facebook, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção</span><span class="sxs-lookup"><span data-stu-id="b5429-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="b5429-150">Clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="b5429-150">Click **Save.**</span></span>

<span data-ttu-id="b5429-151">Para obter mais informações sobre como tooconfigure automática de aprovisionamento, consulte [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="b5429-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="b5429-152">Agora, pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="b5429-152">You can now create a test account.</span></span> <span data-ttu-id="b5429-153">Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada tooWorkplace por Facebook.</span><span class="sxs-lookup"><span data-stu-id="b5429-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5429-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b5429-154">Additional resources</span></span>

* [<span data-ttu-id="b5429-155">Gerir o aprovisionamento da conta de utilizador para aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="b5429-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5429-156">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b5429-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b5429-157">Configurar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b5429-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

