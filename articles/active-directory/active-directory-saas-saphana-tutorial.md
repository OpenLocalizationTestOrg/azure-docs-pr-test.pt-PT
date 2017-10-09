---
title: "Tutorial: Integração do Azure Active Directory com SAP HANA | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="7c801-103">Tutorial: Integração do Azure Active Directory com SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7c801-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="7c801-104">Neste tutorial, saiba como toointegrate SAP HANA com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c801-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c801-105">A integração de SAP HANA com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="7c801-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c801-106">Pode controlar no Azure AD que tenha acesso tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="7c801-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="7c801-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSAP HANA (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c801-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c801-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c801-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7c801-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c801-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c801-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c801-110">Prerequisites</span></span>

<span data-ttu-id="7c801-111">integração do Azure AD com SAP HANA tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7c801-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="7c801-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c801-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c801-113">Um SAP HANA-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="7c801-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="7c801-114">Instância de um HANA em execução em qualquer IaaS público, no local, as VMs do Azure ou instâncias de grande SAP no Azure</span><span class="sxs-lookup"><span data-stu-id="7c801-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="7c801-115">Olá XSA administração Web Interface, bem como Studio HANA instalada na instância do Olá HANA.</span><span class="sxs-lookup"><span data-stu-id="7c801-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="7c801-116">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7c801-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="7c801-117">Teste integração Olá primeiro no desenvolvimento ou teste ambiente da aplicação Olá e, em seguida, ambiente de produção de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="7c801-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="7c801-118">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7c801-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c801-119">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7c801-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c801-120">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c801-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c801-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7c801-121">Scenario description</span></span>
<span data-ttu-id="7c801-122">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7c801-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c801-123">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="7c801-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c801-124">A adição de SAP HANA de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="7c801-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="7c801-125">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="7c801-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="7c801-126">A adição de SAP HANA de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="7c801-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="7c801-127">tooconfigure Olá integração de SAP HANA com o Azure AD, é necessário tooadd SAP HANA Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="7c801-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c801-128">**tooadd SAP HANA da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7c801-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c801-129">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7c801-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="7c801-131">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7c801-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c801-132">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7c801-132">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="7c801-134">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c801-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="7c801-136">Na caixa de pesquisa de Olá, escreva **SAP HANA**, selecione **SAP HANA** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="7c801-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Olá nova aplicação](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c801-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="7c801-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c801-139">Nesta secção, configure e teste do Azure AD-início de sessão único com SAP HANA com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7c801-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7c801-140">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá SAP HANA é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c801-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="7c801-141">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá SAP HANA tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7c801-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="7c801-142">SAP HANA, atribuir valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="7c801-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7c801-143">tooconfigure e teste do Azure AD-início de sessão único com SAP HANA, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7c801-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c801-144">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7c801-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c801-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c801-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c801-146">**[Criar um utilizador de teste de SAP HANA](#creating-a-sap-hana-test-user)**  -toohave um homólogo de Britta Simon no SAP HANA que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="7c801-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c801-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7c801-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c801-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="7c801-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c801-149">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7c801-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c801-150">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7c801-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="7c801-151">**tooconfigure do Azure AD-início de sessão único com SAP HANA, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7c801-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c801-152">No Olá portal do Azure, no Olá **SAP HANA** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="7c801-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="7c801-154">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7c801-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="7c801-156">No Olá **SAP HANA domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7c801-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="7c801-158">a.</span><span class="sxs-lookup"><span data-stu-id="7c801-158">a.</span></span> <span data-ttu-id="7c801-159">No Olá **identificador** caixa de texto, tipo como:`HA100`</span><span class="sxs-lookup"><span data-stu-id="7c801-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="7c801-160">b.</span><span class="sxs-lookup"><span data-stu-id="7c801-160">b.</span></span> <span data-ttu-id="7c801-161">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="7c801-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c801-162">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="7c801-162">These values are not real.</span></span> <span data-ttu-id="7c801-163">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7c801-164">Contacte [equipa de suporte de SAP HANA cliente](https://cloudplatform.sap.com/contact.html) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="7c801-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="7c801-165">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="7c801-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="7c801-167">Se o certificado não está ativo, em seguida, torne-a ativa clicando Olá "disponibilizar novo certificado active" caixa de verificação no Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c801-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="7c801-168">Aplicação de SAP HANA espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="7c801-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7c801-169">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="7c801-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="7c801-170">Aqui iremos ter mapeado os Olá **identificador de utilizador** com **ExtractMailPrefix()** função do **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="7c801-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="7c801-171">Isto permite que o valor de prefixo Olá de e-mail do utilizador Olá que é Olá ID exclusivo do utilizador.</span><span class="sxs-lookup"><span data-stu-id="7c801-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="7c801-172">Esta é enviada toohello aplicação de SAP HANA em cada resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="7c801-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="7c801-174">No Olá **atributos de utilizador** secção em Olá **de sessão único-** diálogo:</span><span class="sxs-lookup"><span data-stu-id="7c801-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="7c801-175">a.</span><span class="sxs-lookup"><span data-stu-id="7c801-175">a.</span></span> <span data-ttu-id="7c801-176">No Olá **identificador de utilizador** na lista pendente, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="7c801-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="7c801-177">b.</span><span class="sxs-lookup"><span data-stu-id="7c801-177">b.</span></span> <span data-ttu-id="7c801-178">No Olá **correio** na lista pendente, selecione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="7c801-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="7c801-179">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="7c801-179">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="7c801-181">tooconfigure-início de sessão único em **SAP HANA** lado, o início de sessão tooyour **HANA XSA Web consola** navegando toohello respetivo-ponto final de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7c801-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="7c801-182">Na configuração predefinida de Olá, Olá URL redireciona o ecrã início de sessão do Olá pedido tooa, que requer credenciais de Olá um autenticado SAP HANA da base de dados utilizador toocomplete Olá início de sessão do processo de.</span><span class="sxs-lookup"><span data-stu-id="7c801-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="7c801-183">Olá utilizador inicia sessão tem de ter privilégios de Olá tooperform necessárias tarefas de administração de SAML.</span><span class="sxs-lookup"><span data-stu-id="7c801-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="7c801-184">Na Interface de Web XSA Olá, navegue demasiado**fornecedor de identidade** e a partir daí, clique em Olá **"+"** -botão no Olá parte inferior do painel do Olá ecrã toodisplay Olá adicionar informações do fornecedor de identidade e executar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7c801-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Adicione o fornecedor de identidade](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="7c801-186">a.</span><span class="sxs-lookup"><span data-stu-id="7c801-186">a.</span></span> <span data-ttu-id="7c801-187">No Olá **adicionar informações do fornecedor de identidade** painel, colar Olá conteúdo Olá XML de metadados, que transferiu do portal do Azure para Olá **metadados** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7c801-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Adicionar as definições do fornecedor de identidade](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="7c801-189">b.</span><span class="sxs-lookup"><span data-stu-id="7c801-189">b.</span></span> <span data-ttu-id="7c801-190">Se o conteúdo de Olá do documento XML Olá é válido, Olá análise processo extrai Olá tooinsert de informações necessárias para Olá **requerente, o ID de entidade e o emissor** campos no Olá geral dados ecrã área e Olá campos de URL no Olá Destino ecrã área, por exemplo,  **Base URL e o URL de SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="7c801-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Adicionar as definições do fornecedor de identidade](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="7c801-192">c.</span><span class="sxs-lookup"><span data-stu-id="7c801-192">c.</span></span> <span data-ttu-id="7c801-193">Na caixa de nome de Olá de Olá geral dados ecrã área, introduza um nome para o fornecedor de identidade de SAML SSO Olá novo.</span><span class="sxs-lookup"><span data-stu-id="7c801-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="7c801-194">nome de Olá de Olá SAML IDP é obrigatória e tem de ser exclusivo; -aparece na lista de Olá de IDPs SAML disponível que é apresentada se selecionar SAML como método de autenticação de Olá para SAP HANA XS toouse de aplicações, por exemplo, na área de ecrã de autenticação Olá da ferramenta de administração de artefacto XS Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="7c801-195">Guarde Olá os detalhes do Olá novo fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="7c801-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="7c801-196">Escolha **guardar** toosave Olá detalhes do fornecedor de identidade Olá e adicione Olá novo SAML toohello lista de IDP de conhecidos IDPs de SAML.</span><span class="sxs-lookup"><span data-stu-id="7c801-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![botão Guardar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="7c801-198">No Studio HANA dentro das propriedades do sistema de Olá de Olá **configuração** separador, apenas filtrar definições por **saml** e ajustar Olá **assertion_timeout** de **10 seg** demasiado**seg 120**.</span><span class="sxs-lookup"><span data-stu-id="7c801-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![definição de assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="7c801-200">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="7c801-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7c801-201">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7c801-202">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c801-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c801-203">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c801-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c801-204">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c801-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="7c801-206">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7c801-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c801-207">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7c801-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c801-209">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="7c801-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c801-211">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão de adição de Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c801-213">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7c801-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c801-215">a.</span><span class="sxs-lookup"><span data-stu-id="7c801-215">a.</span></span> <span data-ttu-id="7c801-216">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c801-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c801-217">b.</span><span class="sxs-lookup"><span data-stu-id="7c801-217">b.</span></span> <span data-ttu-id="7c801-218">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7c801-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c801-219">c.</span><span class="sxs-lookup"><span data-stu-id="7c801-219">c.</span></span> <span data-ttu-id="7c801-220">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="7c801-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7c801-221">d.</span><span class="sxs-lookup"><span data-stu-id="7c801-221">d.</span></span> <span data-ttu-id="7c801-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7c801-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="7c801-223">Criar um utilizador de teste de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7c801-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="7c801-224">tooenable do Azure AD os utilizadores toolog no tooSAP HANA, estes têm de ser aprovisionados para SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7c801-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="7c801-225">SAP HANA suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.</span><span class="sxs-lookup"><span data-stu-id="7c801-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7c801-226">Se precisar de um utilizador de toocreate manualmente, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7c801-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="7c801-227">Pode alterar autenticação externa Olá utilizada pelo utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="7c801-228">Os utilizadores externos são autenticados utilizando um sistema externo, por exemplo um sistema de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="7c801-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="7c801-229">Para obter informações detalhadas sobre as identidades externas, contacte o seu [administrador de domínio](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="7c801-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="7c801-230">Abra Olá [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como administrador e ativar hello utilizador de base de dados para SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="7c801-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![Criar utilizador](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="7c801-232">Marcas de escala Olá caixa de verificação invisível toohello esquerda do **SAML** e siga Olá configurar ligação.</span><span class="sxs-lookup"><span data-stu-id="7c801-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="7c801-233">Clique em **adicionar** tooadd Olá SAML IDP e clique em **OK** selecionar Olá IDP de SAML adequado.</span><span class="sxs-lookup"><span data-stu-id="7c801-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="7c801-234">Adicionar Olá **identidade externas** (ex.</span><span class="sxs-lookup"><span data-stu-id="7c801-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="7c801-235">BrittaSimon aqui) ou escolha **"Qualquer"** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c801-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="7c801-236">Se não estiver marcada "Qualquer" caixa de verificação, em seguida, tem de nome de utilizador de Olá no HANA tooexactly correspondência Olá nome de Olá utilizador no Olá UPN antes de sufixo de domínio Olá (ou seja, BrittaSimon@contoso.com iria ficar BrittaSimon no HANA).</span><span class="sxs-lookup"><span data-stu-id="7c801-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="7c801-237">Para fins de teste, atribuir todos os **"XS"** utilizador toohello de funções.</span><span class="sxs-lookup"><span data-stu-id="7c801-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![atribuir funções](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="7c801-239">Deverá dar-essas permissões adequadas para os casos de utilização apenas.</span><span class="sxs-lookup"><span data-stu-id="7c801-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="7c801-240">Guarde o utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7c801-241">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c801-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7c801-242">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7c801-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="7c801-244">**tooassign Britta Simon tooSAP HANA, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7c801-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c801-245">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7c801-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="7c801-247">Na lista de aplicações de Olá, selecione **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="7c801-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Atribua o utilizador](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="7c801-249">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7c801-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202] 

4. <span data-ttu-id="7c801-251">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="7c801-251">Click **Add** button.</span></span> <span data-ttu-id="7c801-252">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c801-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="7c801-254">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="7c801-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c801-255">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c801-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c801-256">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c801-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c801-257">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7c801-257">Testing single sign-on</span></span>

<span data-ttu-id="7c801-258">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7c801-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7c801-259">Ao clicar em mosaico de SAP HANA Olá no painel de acesso de Olá, deve obter a aplicação de SAP HANA tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="7c801-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="7c801-260">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c801-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c801-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7c801-261">Additional resources</span></span>

* [<span data-ttu-id="7c801-262">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c801-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c801-263">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c801-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

