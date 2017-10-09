---
title: "O Azure Active Directory B2C: Adicionar ADFS como um fornecedor de identidade através de políticas personalizadas"
description: "Um tooarticle como sobre como configurar 2016 do AD FS utilizando o protocolo SAML e as políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="254f3-103">O Azure Active Directory B2C: Adicionar ADFS como um fornecedor de identidade através de políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="254f3-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="254f3-104">Este artigo mostra como tooenable início de sessão para os utilizadores da conta do AD FS através da utilização de Olá de [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="254f3-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="254f3-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="254f3-105">Prerequisites</span></span>

<span data-ttu-id="254f3-106">Olá concluir os passos em Olá [introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="254f3-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="254f3-107">Estes passos incluem:</span><span class="sxs-lookup"><span data-stu-id="254f3-107">These steps include:</span></span>

1.  <span data-ttu-id="254f3-108">Criar uma confiança de entidade Confiadora de ADFS.</span><span class="sxs-lookup"><span data-stu-id="254f3-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="254f3-109">Adicionar Olá ADFS confiança de entidade Confiadora certificado tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="254f3-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="254f3-110">A adicionar a política de tooa do fornecedor de afirmações.</span><span class="sxs-lookup"><span data-stu-id="254f3-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="254f3-111">Conta ADFS Olá registar journey de utilizador de tooa do fornecedor de afirmações.</span><span class="sxs-lookup"><span data-stu-id="254f3-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="254f3-112">Carregamento Olá tooan de política do Azure AD B2C inquilino e testá-lo.</span><span class="sxs-lookup"><span data-stu-id="254f3-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="254f3-113">toocreate uma confiança da entidade Confiadora com suporte para afirmações</span><span class="sxs-lookup"><span data-stu-id="254f3-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="254f3-114">toouse ADFS como um fornecedor de identidade no Azure Active Directory (Azure AD) B2C, tem de toocreate um ADFS confiança da entidade Confiadora e fornecer com parâmetros corretos Olá.</span><span class="sxs-lookup"><span data-stu-id="254f3-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="254f3-115">tooadd uma nova entidade confiadora confiar utilizando Olá AD FS snap-in de gestão e configurar manualmente as definições de Olá, efetuar Olá segue o procedimento num servidor de Federação.</span><span class="sxs-lookup"><span data-stu-id="254f3-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="254f3-116">A associação **administradores**, ou equivalente, no computador local Olá toocomplete necessários mínimos de Olá este procedimento.</span><span class="sxs-lookup"><span data-stu-id="254f3-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="254f3-117">Reveja os detalhes sobre como utilizar contas apropriadas Olá e associações a grupos em [locais e grupos predefinidos do domínio](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="254f3-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="254f3-118">No Gestor de servidor, clique em **ferramentas**e, em seguida, selecione **ADFS gestão**.</span><span class="sxs-lookup"><span data-stu-id="254f3-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="254f3-119">Clique em **adicionar confiança da entidade Confiadora**.</span><span class="sxs-lookup"><span data-stu-id="254f3-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="254f3-120">![Adicionar confiança da entidade Confiadora](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="254f3-121">No Olá **boas-vindas** página, escolha **com suporte para afirmações** e clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="254f3-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="254f3-122">![Na página de boas-vindas Olá, escolha com suporte para afirmações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="254f3-123">No Olá **selecionar origem de dados** página, clique em **introduzir dados sobre a entidade confiadora Olá manualmente**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="254f3-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="254f3-124">![Introduzir dados sobre a entidade confiadora Olá](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="254f3-125">No Olá **Especificar nome a apresentar** , escreva um nome na **nome a apresentar**, em **notas** escreva uma descrição para esta confiança da entidade confiadora e, em seguida, clique em **seguinte** .</span><span class="sxs-lookup"><span data-stu-id="254f3-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="254f3-126">![Especifique o nome a apresentar e notas](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="254f3-127">Opcional.</span><span class="sxs-lookup"><span data-stu-id="254f3-127">Optional.</span></span> <span data-ttu-id="254f3-128">Se tiver um certificado de encriptação de tokens opcional, em seguida, no Olá **configurar certificado** página, clique em **procurar** toolocate o ficheiro de certificado e, em seguida, clique em **seguinte** .</span><span class="sxs-lookup"><span data-stu-id="254f3-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="254f3-129">![Configurar o certificado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="254f3-130">No Olá **configurar URL** página, selecione de Olá **ativar o suporte para protocolo SAML 2.0 WebSSO de Olá** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="254f3-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="254f3-131">Em **URL de serviço SAML 2.0 SSO da entidade Confiadora**, escreva o URL do ponto final de serviço do Olá Security Assertion Markup Language (SAML) para esta confiança da entidade confiadora e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="254f3-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="254f3-132">Para Olá **URL de serviço SAML 2.0 SSO da entidade Confiadora**, cole Olá `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="254f3-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="254f3-133">Substitua {inquilino} com o nome do seu inquilino (por exemplo, contosob2c.onmicrosoft.com) e substitua Olá {política} com o nome da política extensões (por exemplo, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="254f3-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="254f3-134">nome da política Olá é Olá uma política de signup_or_signin herda, neste caso é: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="254f3-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="254f3-135">Por exemplo Olá URL pode ser: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="254f3-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![URL do serviço SAML 2.0 SSO de entidade confiadora](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="254f3-137">No Olá **configurar identificadores** página, especifique Olá mesmo URL que o passo anterior Olá, clique em **adicionar** tooadd-los toohello lista e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="254f3-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="254f3-138">![Entidade confiadora identificadores de confiança de entidade](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="254f3-139">No Olá **escolha política de controlo de acesso** selecionar uma política e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="254f3-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="254f3-140">![Escolha a política de controlo de acesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="254f3-141">No Olá **pronto tooAdd confiança** página, reveja as definições de Olá e, em seguida, clique em **seguinte** toosave informações sobre a confiança da entidade confiadora.</span><span class="sxs-lookup"><span data-stu-id="254f3-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="254f3-142">![Guardar as informações de confiança de entidade entidade confiadora](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="254f3-143">No Olá **concluir** página, clique em **fechar**, esta ação apresenta automaticamente Olá **editar regras de afirmação** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="254f3-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="254f3-144">![Editar regras de afirmação](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="254f3-145">Clique em **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="254f3-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="254f3-146">![Adicionar nova regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="254f3-147">No **modelo de regra de afirmação**, selecione **enviar atributos LDAP como afirmações**.</span><span class="sxs-lookup"><span data-stu-id="254f3-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="254f3-148">![Selecione enviar atributos LDAP como regra de modelo de afirmações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="254f3-149">Fornecer **nome da regra de afirmação**.</span><span class="sxs-lookup"><span data-stu-id="254f3-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="254f3-150">Para Olá **arquivo de atributos** selecione **selecione Active Directory** adicionar Olá seguintes afirmações, em seguida, clique em **concluir** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="254f3-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="254f3-151">![Defina as propriedades de regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="254f3-152">No Gestor de servidor, selecione **confianças da entidade Confiadora** , em seguida, selecione a confiança da entidade confiadora Olá que criou e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="254f3-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="254f3-153">![Entidade confiadora propriedades de edição de terceiros](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="254f3-154">Olá uma entidade confiadora clique de janela de propriedades a confiança (B2C demonstração) de terceiros **assinatura** separador e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="254f3-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="254f3-155">![Assinatura de conjunto](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="254f3-156">Adicione o certificado de assinatura (ficheiro .cert, sem chave privada).</span><span class="sxs-lookup"><span data-stu-id="254f3-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Adicionar o certificado de assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="254f3-158">Na janela de propriedades de fidedignidade (B2C demonstração) Olá entidade confiadora terceiros clique **avançadas** separador e alterar Olá **o algoritmo hash seguro** demasiado**SHA-1**, clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="254f3-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="254f3-159">![Definir o algoritmo de hash seguro tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="254f3-160">Adicionar Olá ADFS conta aplicação chave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="254f3-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="254f3-161">A Federação com contas ADFS requer um segredo do cliente de AD FS tootrust de conta do Azure AD B2C em nome da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="254f3-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="254f3-162">É necessário toostore o certificado do AD FS no seu inquilino do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="254f3-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="254f3-163">Aceda inquilino tooyour do Azure AD B2C e selecione **definições do B2C** > **Framework de experiência de identidade**</span><span class="sxs-lookup"><span data-stu-id="254f3-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="254f3-164">Selecione **política chaves** tooview Olá as chaves disponíveis no seu inquilino.</span><span class="sxs-lookup"><span data-stu-id="254f3-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="254f3-165">Clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="254f3-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="254f3-166">Para **opções**, utilize **carregar**.</span><span class="sxs-lookup"><span data-stu-id="254f3-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="254f3-167">Para **nome**, utilize `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="254f3-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="254f3-168">prefixo de Olá `B2C_1A_` podem ser adicionados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="254f3-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="254f3-169">No carregamento do ficheiro Olá, * * selecionar o ficheiro de. pfx do certificado com chave privada.</span><span class="sxs-lookup"><span data-stu-id="254f3-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="254f3-170">Nota: este certificado (com a chave privada de Olá) deve ser Olá mesmo mais emitido e utilizado para Olá ADFS entidade confiadora.</span><span class="sxs-lookup"><span data-stu-id="254f3-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="254f3-171">![Carregar política chave](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="254f3-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="254f3-172">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="254f3-172">Click **Create**</span></span>
8.  <span data-ttu-id="254f3-173">Confirme que criou a chave de Olá `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="254f3-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="254f3-174">Adicionar um fornecedor de afirmações na política de extensão</span><span class="sxs-lookup"><span data-stu-id="254f3-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="254f3-175">Se pretender que os utilizadores toosign utilizando a conta do AD FS, precisa de toodefine ADFS conta como um fornecedor de afirmações.</span><span class="sxs-lookup"><span data-stu-id="254f3-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="254f3-176">Por outras palavras, terá de toospecify um ponto final que o Azure AD B2C comunica com.</span><span class="sxs-lookup"><span data-stu-id="254f3-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="254f3-177">ponto final de Olá fornece um conjunto de afirmações que são utilizados pelo Azure AD B2C tooverify que foi autenticado um utilizador específico.</span><span class="sxs-lookup"><span data-stu-id="254f3-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="254f3-178">Definir o ADFS como um fornecedor de afirmações, adicionando `<ClaimsProvider>` nó no seu ficheiro de política de extensão:</span><span class="sxs-lookup"><span data-stu-id="254f3-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="254f3-179">Abra o ficheiro de política de extensão de Olá (TrustFrameworkExtensions.xml) do diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="254f3-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="254f3-180">Se precisar de um editor de XML, [tente Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma simples.</span><span class="sxs-lookup"><span data-stu-id="254f3-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="254f3-181">Determinar Olá `<ClaimsProviders>` secção</span><span class="sxs-lookup"><span data-stu-id="254f3-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="254f3-182">Adicionar Olá seguinte fragmento XML em Olá `ClaimsProviders` elemento e substitua `identityProvider` com o seu DNS (valor arbitrário que indica o seu domínio) e guarde-Olá.</span><span class="sxs-lookup"><span data-stu-id="254f3-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="254f3-183">Registar tooSign de fornecedor de afirmações do Olá ADFS conta se ou iniciar sessão no journey de utilizador</span><span class="sxs-lookup"><span data-stu-id="254f3-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="254f3-184">Neste momento, o fornecedor de identidade Olá foi configurado.</span><span class="sxs-lookup"><span data-stu-id="254f3-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="254f3-185">No entanto, não está disponível em nenhum dos Olá sessão-up/início de sessão ecrãs.</span><span class="sxs-lookup"><span data-stu-id="254f3-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="254f3-186">Agora tem tooadd Olá ADFS identidade fornecedor tooyour utilizador da conta `SignUpOrSignIn` journey de utilizador.</span><span class="sxs-lookup"><span data-stu-id="254f3-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="254f3-187">toomake-la disponível, criamos um duplicado de um existente journey de utilizador do modelo.</span><span class="sxs-lookup"><span data-stu-id="254f3-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="254f3-188">Em seguida, iremos modificá-lo para que inclui o fornecedor de identidade do ADFS Olá:</span><span class="sxs-lookup"><span data-stu-id="254f3-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="254f3-189">Abra o ficheiro de base de Olá da sua política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="254f3-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="254f3-190">Determinar Olá `<UserJourneys>` elemento e cópia Olá todo o conteúdo de `<UserJourneys>` nós.</span><span class="sxs-lookup"><span data-stu-id="254f3-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="254f3-191">Abra o ficheiro de extensão de Olá (por exemplo, TrustFrameworkExtensions.xml) e determinar Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="254f3-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="254f3-192">Se não existir elemento Olá, adicione um.</span><span class="sxs-lookup"><span data-stu-id="254f3-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="254f3-193">Colar o conteúdo completo de Olá de `<UserJournesy>` nó que copiou como subordinado de Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="254f3-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="254f3-194">Botão de Olá de apresentação</span><span class="sxs-lookup"><span data-stu-id="254f3-194">Display hello button</span></span>
<span data-ttu-id="254f3-195">Olá `<ClaimsProviderSelections>` elemento define lista Olá das opções de seleção de fornecedor de afirmações e a sua ordem.</span><span class="sxs-lookup"><span data-stu-id="254f3-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="254f3-196">`<ClaimsProviderSelection>`elemento está no botão do fornecedor de identidade tooan semelhante numa página sessão-up/início de sessão.</span><span class="sxs-lookup"><span data-stu-id="254f3-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="254f3-197">Se adicionar um `<ClaimsProviderSelection>` elemento para a conta do AD FS, um novo botão aparece quando um utilizador lands na página Olá.</span><span class="sxs-lookup"><span data-stu-id="254f3-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="254f3-198">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="254f3-198">tooadd this element:</span></span>

1.  <span data-ttu-id="254f3-199">Determinar Olá `<UserJourney>` nó que inclui `Id="SignUpOrSignIn"` no journey de utilizador de Olá que copiou.</span><span class="sxs-lookup"><span data-stu-id="254f3-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="254f3-200">Localizar Olá `<OrchestrationStep>` nó que inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="254f3-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="254f3-201">Adicione o seguinte fragmento XML em `<ClaimsProviderSelections>` nó:</span><span class="sxs-lookup"><span data-stu-id="254f3-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="254f3-202">Ligação Olá botão tooan ação</span><span class="sxs-lookup"><span data-stu-id="254f3-202">Link hello button tooan action</span></span>

<span data-ttu-id="254f3-203">Agora que tem um botão no local, terá de toolink-tooan ação.</span><span class="sxs-lookup"><span data-stu-id="254f3-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="254f3-204">Olá, neste caso, é ação para o Azure AD B2C toocommunicate com ADFS conta tooreceive um token.</span><span class="sxs-lookup"><span data-stu-id="254f3-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="254f3-205">Ligação Olá botão tooan ação associando perfil técnica Olá para o fornecedor de afirmações do ADFS conta:</span><span class="sxs-lookup"><span data-stu-id="254f3-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="254f3-206">Determinar Olá `<OrchestrationStep>` que inclua `Order="2"` no Olá `<UserJourney>` nós.</span><span class="sxs-lookup"><span data-stu-id="254f3-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="254f3-207">Adicione o seguinte fragmento XML em `<ClaimsExchanges>` nó:</span><span class="sxs-lookup"><span data-stu-id="254f3-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="254f3-208">Certifique-se Olá `Id` tem Olá mesmo valor da `TargetClaimsExchangeId` no Olá anterior a secção.</span><span class="sxs-lookup"><span data-stu-id="254f3-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="254f3-209">Certifique-se `TechnicalProfileReferenceId` é definir perfil técnica toohello que criou anteriormente (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="254f3-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="254f3-210">Carregar o inquilino de tooyour Olá política</span><span class="sxs-lookup"><span data-stu-id="254f3-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="254f3-211">No Olá [portal do Azure](https://portal.azure.com), mudar para Olá [contexto do seu inquilino do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra Olá **do Azure AD B2C** painel.</span><span class="sxs-lookup"><span data-stu-id="254f3-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="254f3-212">Selecione **identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="254f3-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="254f3-213">Abra Olá **todas as políticas** painel.</span><span class="sxs-lookup"><span data-stu-id="254f3-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="254f3-214">Selecione **carregar política**.</span><span class="sxs-lookup"><span data-stu-id="254f3-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="254f3-215">Verifique **substituir a política de Olá, se existir** caixa.</span><span class="sxs-lookup"><span data-stu-id="254f3-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="254f3-216">**Carregar** TrustFrameworkExtensions.xml e certifique-se de que não falha a validação de Olá</span><span class="sxs-lookup"><span data-stu-id="254f3-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="254f3-217">Testar a política personalizada do Olá utilizando o executar agora</span><span class="sxs-lookup"><span data-stu-id="254f3-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="254f3-218">Abra **definições do Azure AD B2C** e aceda demasiado**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="254f3-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="254f3-219">Abra **B2C_1A_signup_signin**, Olá entidade confiadora política personalizada de terceiros (RP) que carregou.</span><span class="sxs-lookup"><span data-stu-id="254f3-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="254f3-220">Selecione **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="254f3-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="254f3-221">Deve ser capaz de toosign sessão com a conta ADFS.</span><span class="sxs-lookup"><span data-stu-id="254f3-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="254f3-222">[Opcional] Registar journey de utilizador ao editar tooProfile do fornecedor de afirmações Olá ADFS conta</span><span class="sxs-lookup"><span data-stu-id="254f3-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="254f3-223">Poderá ser útil fornecedor de identidade de conta ADFS Olá tooadd também tooyour utilizador `ProfileEdit` journey de utilizador.</span><span class="sxs-lookup"><span data-stu-id="254f3-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="254f3-224">toomake-la disponível, iremos repetir Olá últimos dois passos:</span><span class="sxs-lookup"><span data-stu-id="254f3-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="254f3-225">Botão de Olá de apresentação</span><span class="sxs-lookup"><span data-stu-id="254f3-225">Display hello button</span></span>
1.  <span data-ttu-id="254f3-226">Abra o ficheiro de extensão de Olá da sua política (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="254f3-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="254f3-227">Determinar Olá `<UserJourney>` nó que inclui `Id="ProfileEdit"` no journey de utilizador de Olá que copiou.</span><span class="sxs-lookup"><span data-stu-id="254f3-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="254f3-228">Localizar Olá `<OrchestrationStep>` nó que inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="254f3-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="254f3-229">Adicione o seguinte fragmento XML em `<ClaimsProviderSelections>` nó:</span><span class="sxs-lookup"><span data-stu-id="254f3-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="254f3-230">Ligação Olá botão tooan ação</span><span class="sxs-lookup"><span data-stu-id="254f3-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="254f3-231">Determinar Olá `<OrchestrationStep>` que inclua `Order="2"` no Olá `<UserJourney>` nós.</span><span class="sxs-lookup"><span data-stu-id="254f3-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="254f3-232">Adicione o seguinte fragmento XML em `<ClaimsExchanges>` nó:</span><span class="sxs-lookup"><span data-stu-id="254f3-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="254f3-233">Testar a política de edição de perfil personalizada do Olá utilizando o executar agora</span><span class="sxs-lookup"><span data-stu-id="254f3-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="254f3-234">Abra **definições do Azure AD B2C** e aceda demasiado**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="254f3-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="254f3-235">Abra **B2C_1A_ProfileEdit**, Olá entidade confiadora política personalizada de terceiros (RP) que carregou.</span><span class="sxs-lookup"><span data-stu-id="254f3-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="254f3-236">Selecione **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="254f3-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="254f3-237">Deve ser capaz de toosign sessão com a conta ADFS.</span><span class="sxs-lookup"><span data-stu-id="254f3-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="254f3-238">Transferir ficheiros de política concluída Olá</span><span class="sxs-lookup"><span data-stu-id="254f3-238">Download hello complete policy files</span></span>
<span data-ttu-id="254f3-239">Opcional: Recomendamos que crie o seu cenário de utilizar os seus próprios ficheiros de política personalizada depois de concluir Olá introdução com as políticas personalizadas guiá.</span><span class="sxs-lookup"><span data-stu-id="254f3-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="254f3-240">Ficheiros de política de exemplo para referência apenas</span><span class="sxs-lookup"><span data-stu-id="254f3-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
