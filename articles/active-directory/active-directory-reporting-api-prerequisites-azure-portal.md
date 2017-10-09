---
title: "API de relatórios aaaPrerequisites tooaccess Olá do Azure AD | Microsoft Docs"
description: "Saiba mais sobre API relatórios do Olá pré-requisitos tooaccess Olá do Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="c2c92-103">API de relatórios pré-requisitos tooaccess Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2c92-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="c2c92-104">Olá [relatório APIs do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) lhe fornecer os dados de toohello acesso programático através de um conjunto de APIs baseado em REST.</span><span class="sxs-lookup"><span data-stu-id="c2c92-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="c2c92-105">Pode chamar estas APIs a partir de várias linguagens e ferramentas de programação.</span><span class="sxs-lookup"><span data-stu-id="c2c92-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c2c92-106">Olá reporting utiliza API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) as APIs do web toohello tooauthorize acesso.</span><span class="sxs-lookup"><span data-stu-id="c2c92-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="c2c92-107">tooget aceder aos dados de relatórios toohello através da API de Olá, precisa toohave uma Olá funções atribuídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2c92-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="c2c92-108">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="c2c92-108">Security Reader</span></span>
- <span data-ttu-id="c2c92-109">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="c2c92-109">Security Admin</span></span>
- <span data-ttu-id="c2c92-110">Administrador global</span><span class="sxs-lookup"><span data-stu-id="c2c92-110">Global Admin</span></span>


<span data-ttu-id="c2c92-111">tooprepare sua toohello acesso API do relatório, tem de:</span><span class="sxs-lookup"><span data-stu-id="c2c92-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="c2c92-112">Registar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="c2c92-112">Register an application</span></span> 
2. <span data-ttu-id="c2c92-113">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="c2c92-113">Grant permissions</span></span> 
3. <span data-ttu-id="c2c92-114">Recolher as definições de configuração</span><span class="sxs-lookup"><span data-stu-id="c2c92-114">Gather configuration settings</span></span> 

<span data-ttu-id="c2c92-115">Para perguntas, problemas ou comentários, consulte [um pedido de suporte de ficheiros](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="c2c92-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="c2c92-116">Registar uma aplicação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2c92-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="c2c92-117">É necessário tooregister uma aplicação, mesmo que se estão a aceder Olá API através de um script do relatório.</span><span class="sxs-lookup"><span data-stu-id="c2c92-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="c2c92-118">Isto dá-lhe um **ID da aplicação**, que é necessário para uma chamada de autorização e permite que os tokens de tooreceive de código.</span><span class="sxs-lookup"><span data-stu-id="c2c92-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="c2c92-119">tooconfigure diretório tooaccess Olá do Azure AD relatórios API, tem de iniciar sessão toohello portal do Azure com uma conta de administrador do Azure que também seja membro de Olá **Administrador Global** função de diretório no seu inquilino do Azure AD .</span><span class="sxs-lookup"><span data-stu-id="c2c92-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2c92-120">As aplicações em execução sob credenciais com privilégios de "admin" como este podem ser muito poderosas, por isso, tenha ser as credenciais de ID/segredo da aplicação do se tookeep Olá segura.</span><span class="sxs-lookup"><span data-stu-id="c2c92-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="c2c92-121">**tooregister uma aplicação do Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="c2c92-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="c2c92-122">No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="c2c92-124">No Olá **do Azure Active Directory** painel, clique em **registos de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="c2c92-126">No Olá **registos de aplicação** painel, na barra de ferramentas de Olá na parte superior do Olá, clique em **novo registo de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="c2c92-128">No Olá **criar** painel, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c2c92-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="c2c92-130">a.</span><span class="sxs-lookup"><span data-stu-id="c2c92-130">a.</span></span> <span data-ttu-id="c2c92-131">No Olá **nome** caixa de texto, tipo `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="c2c92-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="c2c92-132">b.</span><span class="sxs-lookup"><span data-stu-id="c2c92-132">b.</span></span> <span data-ttu-id="c2c92-133">Como **tipo de aplicação**, selecione **aplicação Web / API**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="c2c92-134">c.</span><span class="sxs-lookup"><span data-stu-id="c2c92-134">c.</span></span> <span data-ttu-id="c2c92-135">No Olá **URL de início de sessão** caixa de texto, tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="c2c92-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="c2c92-136">d.</span><span class="sxs-lookup"><span data-stu-id="c2c92-136">d.</span></span> <span data-ttu-id="c2c92-137">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="c2c92-138">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="c2c92-138">Grant permissions</span></span> 

<span data-ttu-id="c2c92-139">o objetivo deste passo Olá é toogrant a aplicação **ler os dados de diretório** permissões toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="c2c92-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="c2c92-141">**toogrant Olá de toouse permissão da aplicação API:**</span><span class="sxs-lookup"><span data-stu-id="c2c92-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="c2c92-142">No Olá **registos de aplicação** painel, na lista de aplicações de Olá, clique em **aplicação API de relatórios**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="c2c92-143">No Olá **aplicação API de relatórios** painel, na barra de ferramentas de Olá na parte superior do Olá, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="c2c92-145">No Olá **definições** painel, clique em **as permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="c2c92-147">No Olá **as permissões necessárias** painel, no Olá **API** lista, clique em **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="c2c92-149">No Olá **ativar o acesso ao** painel, selecione **ler os dados de diretório**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="c2c92-151">Na barra de ferramentas Olá na parte superior do Olá, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="c2c92-153">Recolher as definições de configuração</span><span class="sxs-lookup"><span data-stu-id="c2c92-153">Gather configuration settings</span></span> 
<span data-ttu-id="c2c92-154">Esta secção mostra-lhe como Olá tooget seguintes definições de diretório:</span><span class="sxs-lookup"><span data-stu-id="c2c92-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="c2c92-155">Nome de domínio</span><span class="sxs-lookup"><span data-stu-id="c2c92-155">Domain name</span></span>
* <span data-ttu-id="c2c92-156">ID de cliente</span><span class="sxs-lookup"><span data-stu-id="c2c92-156">Client ID</span></span>
* <span data-ttu-id="c2c92-157">Segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="c2c92-157">Client secret</span></span>

<span data-ttu-id="c2c92-158">Necessitar destes valores quando configurar a API de relatórios de toohello de chamadas.</span><span class="sxs-lookup"><span data-stu-id="c2c92-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="c2c92-159">Obter o nome de domínio</span><span class="sxs-lookup"><span data-stu-id="c2c92-159">Get your domain name</span></span>

<span data-ttu-id="c2c92-160">**tooget seu nome de domínio:**</span><span class="sxs-lookup"><span data-stu-id="c2c92-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="c2c92-161">No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="c2c92-163">No Olá **do Azure Active Directory** painel, clique em **nomes de domínio**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="c2c92-165">Copie o seu nome de domínio na lista de Olá de domínios.</span><span class="sxs-lookup"><span data-stu-id="c2c92-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="c2c92-166">Obter ID de cliente da aplicação</span><span class="sxs-lookup"><span data-stu-id="c2c92-166">Get your application's client ID</span></span>

<span data-ttu-id="c2c92-167">**tooget ID de cliente da aplicação:**</span><span class="sxs-lookup"><span data-stu-id="c2c92-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="c2c92-168">No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="c2c92-170">No Olá **registos de aplicação** painel, na lista de aplicações de Olá, clique em **aplicação API de relatórios**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="c2c92-171">No Olá **aplicação API de relatórios** painel, em Olá **ID da aplicação**, clique em **clique toocopy**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="c2c92-173">Obter o segredo do cliente da aplicação</span><span class="sxs-lookup"><span data-stu-id="c2c92-173">Get your application's client secret</span></span>
<span data-ttu-id="c2c92-174">tooget cliente da sua aplicação secreta, que precisa toocreate uma nova chave e guarde respectivo valor após guardar a nova chave de Olá porque não é possível tooretrieve este valor já mais tarde.</span><span class="sxs-lookup"><span data-stu-id="c2c92-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="c2c92-175">**tooget segredo do cliente da aplicação:**</span><span class="sxs-lookup"><span data-stu-id="c2c92-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="c2c92-176">No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="c2c92-178">No Olá **registos de aplicação** painel, na lista de aplicações de Olá, clique em **aplicação API de relatórios**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="c2c92-179">No Olá **aplicação API de relatórios** painel, na barra de ferramentas de Olá na parte superior do Olá, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="c2c92-181">No Olá **definições** painel, no Olá **APIR acesso** secção, clique em **chaves**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="c2c92-183">No Olá **chaves** painel, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c2c92-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="c2c92-185">a.</span><span class="sxs-lookup"><span data-stu-id="c2c92-185">a.</span></span> <span data-ttu-id="c2c92-186">No Olá **Descrição** caixa de texto, tipo `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="c2c92-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="c2c92-187">b.</span><span class="sxs-lookup"><span data-stu-id="c2c92-187">b.</span></span> <span data-ttu-id="c2c92-188">Como **expira**, selecione **nos 2 anos**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="c2c92-189">c.</span><span class="sxs-lookup"><span data-stu-id="c2c92-189">c.</span></span> <span data-ttu-id="c2c92-190">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c2c92-190">Click **Save**.</span></span>

    <span data-ttu-id="c2c92-191">d.</span><span class="sxs-lookup"><span data-stu-id="c2c92-191">d.</span></span> <span data-ttu-id="c2c92-192">Copie o valor da chave Olá.</span><span class="sxs-lookup"><span data-stu-id="c2c92-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c2c92-193">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="c2c92-193">Next Steps</span></span>
* <span data-ttu-id="c2c92-194">Seria que como tooaccess Olá dados a partir do Azure AD de Olá API do relatório de forma programática?</span><span class="sxs-lookup"><span data-stu-id="c2c92-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="c2c92-195">Veja [introdução Olá API do Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2c92-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="c2c92-196">Se quiser toofind mais informações sobre os relatórios do Azure Active Directory, consulte Olá [do Azure Active Directory guia de relatórios](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c2c92-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

