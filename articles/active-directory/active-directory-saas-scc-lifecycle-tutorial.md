---
title: "Tutorial: Integração do Azure Active Directory com o ciclo de vida SCC | Microsoft Docs"
description: "Saiba como toouse SCC ciclo de vida com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="72aba-103">Tutorial: Integração do Azure Active Directory com SCC ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="72aba-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="72aba-104">o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e SCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="72aba-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="72aba-105">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="72aba-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="72aba-106">Uma subscrição do Azure válida</span><span class="sxs-lookup"><span data-stu-id="72aba-106">A valid Azure subscription</span></span>
* <span data-ttu-id="72aba-107">Um ciclo de vida SCC-início de sessão único (SSO) ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="72aba-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="72aba-108">Depois de concluir este tutorial, Olá utilizadores do Azure AD que atribuiu tooSCC ciclo de vida será toosingle capaz de início de sessão na aplicação Olá no site da sua empresa SCC ciclo de vida (serviço fornecedor iniciada pelo início de sessão) ou utilizar Olá [introdução Painel de acesso de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="72aba-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="72aba-109">cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="72aba-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="72aba-110">Ativar a integração de aplicações de Olá para SCC ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="72aba-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="72aba-111">Configurar início de sessão único (SSO)</span><span class="sxs-lookup"><span data-stu-id="72aba-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="72aba-112">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="72aba-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="72aba-113">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="72aba-113">Assigning users</span></span>

<span data-ttu-id="72aba-114">![Cenário](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "cenário")</span><span class="sxs-lookup"><span data-stu-id="72aba-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="72aba-115">Ativar a integração de aplicação Olá para SCC ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="72aba-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="72aba-116">o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable para SCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="72aba-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="72aba-117">**integração de aplicações de Olá tooenable para ciclo de vida SCC, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="72aba-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="72aba-118">No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="72aba-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="72aba-119">![Do Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "do Active Directory")</span><span class="sxs-lookup"><span data-stu-id="72aba-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="72aba-120">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="72aba-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="72aba-121">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="72aba-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="72aba-122">![Aplicações](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "aplicações")</span><span class="sxs-lookup"><span data-stu-id="72aba-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="72aba-123">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="72aba-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="72aba-124">![Adicionar aplicação](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Adicionar aplicação")</span><span class="sxs-lookup"><span data-stu-id="72aba-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="72aba-125">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="72aba-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="72aba-126">![Adicionar uma aplicação de gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "adicionar uma aplicação de gallerry")</span><span class="sxs-lookup"><span data-stu-id="72aba-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="72aba-127">No Olá **caixa pesquisa**, tipo **SCC ciclo de vida**.</span><span class="sxs-lookup"><span data-stu-id="72aba-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="72aba-128">![Galeria de aplicações](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galeria de aplicações")</span><span class="sxs-lookup"><span data-stu-id="72aba-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="72aba-129">No painel de resultados de Olá, selecione **SCC ciclo de vida**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="72aba-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="72aba-130">![Ciclo de vida SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC ciclo de vida")</span><span class="sxs-lookup"><span data-stu-id="72aba-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="72aba-131">Configurar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="72aba-131">Configure single sign-on</span></span>

<span data-ttu-id="72aba-132">o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooSCC ciclo de vida à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.</span><span class="sxs-lookup"><span data-stu-id="72aba-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="72aba-133">**tooconfigure único início de sessão, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="72aba-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="72aba-134">No Olá portal clássico do Azure, no Olá **SCC ciclo de vida** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá * * configurar início de sessão único * * caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72aba-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="72aba-135">![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="72aba-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="72aba-136">No Olá **como seria, como os utilizadores toosign no tooSCC ciclo de vida** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="72aba-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="72aba-137">![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="72aba-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="72aba-138">No Olá **URL da aplicação configurar** página, numa Olá **URL de início de sessão** caixa de texto, tipo Olá URL utilizado pelo seu toosign de utilizadores no tooyour aplicação SCC ciclo de vida utilizando Olá seguir o padrão "*https:// bs1.scc.com/lc7/Welcome/Customer/PICTtest.aspx*"e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="72aba-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="72aba-139">![Configurar o URL da aplicação](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="72aba-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="72aba-140">No Olá **configurar o início de sessão único no ciclo de vida SCC** página, clique em **transferir metadados**e, em seguida, guarde o ficheiro de metadados localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="72aba-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="72aba-141">![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="72aba-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="72aba-142">Reencaminhe esse tooSCC de ficheiro de metadados equipa de suporte do ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="72aba-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="72aba-143">O início de sessão único tem toobe ativado por Olá SCC ciclo de vida a equipa de suporte.</span><span class="sxs-lookup"><span data-stu-id="72aba-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="72aba-144">No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72aba-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="72aba-145">![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="72aba-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="72aba-146">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="72aba-146">Configure user provisioning</span></span>

<span data-ttu-id="72aba-147">Na ordem tooenable do Azure AD os utilizadores toolog no ciclo de vida SCC, têm de ser aprovisionados para SCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="72aba-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="72aba-148">Não há nenhum item de ação para tooconfigure aprovisionamento de utilizadores tooSCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="72aba-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="72aba-149">Quando um toolog de tentativas de utilizador atribuído no ciclo de vida SCC, uma conta de ciclo de vida SCC é criada automaticamente se necessário.</span><span class="sxs-lookup"><span data-stu-id="72aba-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="72aba-150">Pode utilizar quaisquer outras SCC ciclo de vida utilizador conta criação ferramentas ou APIs fornecidas pelo SCC ciclo de vida tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="72aba-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="72aba-151">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="72aba-151">Assign users</span></span>
<span data-ttu-id="72aba-152">tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.</span><span class="sxs-lookup"><span data-stu-id="72aba-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="72aba-153">**tooassign utilizadores tooSCC ciclo de vida, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="72aba-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="72aba-154">Olá portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="72aba-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="72aba-155">No Olá * * SCC ciclo de vida * * página de integração de aplicações, clique em **atribuir utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="72aba-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="72aba-156">![Atribuir utilizadores](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "atribuir utilizadores")</span><span class="sxs-lookup"><span data-stu-id="72aba-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="72aba-157">Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.</span><span class="sxs-lookup"><span data-stu-id="72aba-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="72aba-158">![Sim](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="72aba-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="72aba-159">Se quiser tootest as definições de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="72aba-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="72aba-160">Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="72aba-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

