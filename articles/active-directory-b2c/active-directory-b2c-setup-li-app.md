---
title: "Azure Active Directory B2C: Configuração LinkedIn | Microsoft Docs"
description: "Fornecer tooconsumers de inscrição e o início de sessão com contas de LinkedIn nas aplicações que estejam protegidas pelo Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="b0fec-103">Azure Active Directory B2C: Forneça tooconsumers de inscrição e o início de sessão com contas do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b0fec-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="b0fec-104">Criar uma aplicação LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b0fec-104">Create a LinkedIn application</span></span>
<span data-ttu-id="b0fec-105">toouse LinkedIn como um fornecedor de identidade no Azure Active Directory (Azure AD) B2C, tem de toocreate uma aplicação LinkedIn e fornecer com parâmetros corretos Olá.</span><span class="sxs-lookup"><span data-stu-id="b0fec-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="b0fec-106">É necessário um toodo de conta LinkedIn isto.</span><span class="sxs-lookup"><span data-stu-id="b0fec-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="b0fec-107">Se não tiver uma, pode obtê-lo em [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="b0fec-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="b0fec-108">Aceda toohello [site LinkedIn programadores](https://www.developer.linkedin.com/) e inicie sessão com as credenciais da conta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b0fec-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="b0fec-109">Clique em **aplicações My** no Olá barra de menu superior e, em seguida, clique em **Criar aplicação**.</span><span class="sxs-lookup"><span data-stu-id="b0fec-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nova aplicação](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="b0fec-111">No Olá **criar uma nova aplicação** formulário, preencha as informações relevantes Olá (**nome da empresa**, **nome**, **Descrição**, **URL da aplicação logótipo**, **utilização de aplicações**, **URL do site**, **E-Mail profissionais** e **telefone da empresa**).</span><span class="sxs-lookup"><span data-stu-id="b0fec-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="b0fec-112">Concordo toohello **LinkedIn termos de utilização da API** e clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="b0fec-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - registo de aplicação](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="b0fec-114">Copie os valores de Olá de **ID de cliente** e **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="b0fec-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="b0fec-115">(Pode encontrá-los em **chaves de autenticação**.) Terá de ambos os parâmetros tooconfigure LinkedIn como um fornecedor de identidade no seu inquilino.</span><span class="sxs-lookup"><span data-stu-id="b0fec-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b0fec-116">**Segredo do cliente** é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="b0fec-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="b0fec-117">Introduza `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no Olá **autorizado URLs de redirecionamento** campo (em **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="b0fec-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="b0fec-118">Substitua **{inquilino}** com o nome do seu inquilino (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b0fec-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="b0fec-119">Clique em **adicionar**e, em seguida, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="b0fec-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="b0fec-120">Olá **{inquilino}** valor diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b0fec-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - configuração de aplicação](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b0fec-122">Configurar LinkedIn como um fornecedor de identidade no seu inquilino</span><span class="sxs-lookup"><span data-stu-id="b0fec-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b0fec-123">Siga estes passos demasiado[navegue painel de funcionalidades de toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0fec-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b0fec-124">No painel de funcionalidades de Olá B2C, clique em **fornecedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="b0fec-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b0fec-125">Clique em **+ adicionar** , Olá parte superior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0fec-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b0fec-126">Forneça um amigável **nome** para configuração do fornecedor de identidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0fec-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b0fec-127">Por exemplo, introduza "LI".</span><span class="sxs-lookup"><span data-stu-id="b0fec-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="b0fec-128">Clique em **tipo de fornecedor de identidade**, selecione **LinkedIn**e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0fec-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="b0fec-129">Clique em **configurar este fornecedor de identidade** e introduza Olá ID de cliente e o segredo do cliente de Olá LinkedIn aplicação que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b0fec-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="b0fec-130">Clique em **OK** e, em seguida, clique em **criar** toosave a configuração do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b0fec-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

