---
title: recursos de nuvem aaaSecure MFA do Azure e do AD FS | Microsoft Docs
description: "Este é Olá multi-factor authentication página que descreve como tooget utilizar a MFA do Azure e o AD FS na nuvem de Olá."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="a5db1-103">Proteger recursos da nuvem com o Multi-Factor Authentication do Azure e o AD FS</span><span class="sxs-lookup"><span data-stu-id="a5db1-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="a5db1-104">Se a sua organização estiver federada com o Azure Active Directory, utilize o multi-factor Authentication do Azure ou recursos de toosecure de serviços de Federação do Active Directory (AD FS) que sejam acedidos pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5db1-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="a5db1-105">Utilize Olá os seguintes recursos do Azure Active Directory de toosecure de procedimentos com multi-factor Authentication do Azure ou serviços de Federação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5db1-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="a5db1-106">Proteger recursos do Azure AD com o AD FS</span><span class="sxs-lookup"><span data-stu-id="a5db1-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="a5db1-107">toosecure o recurso da nuvem, configure uma regra de afirmações para que os serviços de Federação do Active Directory emite Olá multipleauthn afirmação quando um utilizador efetua a verificação com êxito.</span><span class="sxs-lookup"><span data-stu-id="a5db1-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="a5db1-108">Esta afirmação é transmitida tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="a5db1-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="a5db1-109">Siga este toowalk procedimento passos Olá:</span><span class="sxs-lookup"><span data-stu-id="a5db1-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="a5db1-110">Abra a Gestão do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a5db1-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="a5db1-111">Olá esquerda, selecione **confianças da entidade Confiadora**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="a5db1-112">Clique com o botão direito do rato na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Afirmação**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="a5db1-114">Em Regras de Transformação da Emissão, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="a5db1-116">No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **passar ou filtrar uma afirmação de entrada** de Olá pendente e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="a5db1-118">Dê um nome à sua regra.</span><span class="sxs-lookup"><span data-stu-id="a5db1-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="a5db1-119">Selecione **referências dos métodos de autenticação** como Olá entrada de tipo de afirmação.</span><span class="sxs-lookup"><span data-stu-id="a5db1-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="a5db1-120">Selecione **Passar todos os valores de afirmação**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="a5db1-121">![Assistente para Adicionar Regra de Afirmação de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="a5db1-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="a5db1-122">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-122">Click **Finish**.</span></span> <span data-ttu-id="a5db1-123">Feche a consola de gestão FS Olá AD.</span><span class="sxs-lookup"><span data-stu-id="a5db1-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="a5db1-124">IPs Fidedignos para utilizadores federados</span><span class="sxs-lookup"><span data-stu-id="a5db1-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="a5db1-125">IPs fidedignos permitem aos administradores de verificação de dois passos tooby passagem para endereços IP específicos, ou para os utilizadores federados que tenham pedidos com origem na sua própria intranet.</span><span class="sxs-lookup"><span data-stu-id="a5db1-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="a5db1-126">Olá secções seguintes descrevem como tooconfigure multi-factor Authentication do Azure fidedigna IPs com utilizadores federados e ignorar a verificação quando um pedido tem origem dentro de uma intranet de utilizadores federados.</span><span class="sxs-lookup"><span data-stu-id="a5db1-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="a5db1-127">Isto é conseguido através da configuração do AD FS toouse um pass-through ou filtrar um modelo de afirmação de entrada com Olá tipo de afirmação dentro da rede empresarial.</span><span class="sxs-lookup"><span data-stu-id="a5db1-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="a5db1-128">Este exemplo utiliza o Office 365 para as Confianças de Entidades Confiadoras.</span><span class="sxs-lookup"><span data-stu-id="a5db1-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="a5db1-129">Configurar regras de afirmações Olá do AD FS</span><span class="sxs-lookup"><span data-stu-id="a5db1-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="a5db1-130">Olá primeira coisa toodo é tooconfigure Olá do AD FS afirmações.</span><span class="sxs-lookup"><span data-stu-id="a5db1-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="a5db1-131">Criar duas regras de afirmações, uma para Olá dentro da rede empresarial de afirmações de tipo e uma adicional para manter os utilizadores com sessão iniciados.</span><span class="sxs-lookup"><span data-stu-id="a5db1-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="a5db1-132">Abra a Gestão do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a5db1-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="a5db1-133">Olá esquerda, selecione **confianças da entidade Confiadora**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="a5db1-134">Clique com o botão direito do rato na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Afirmação**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="a5db1-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="a5db1-135">Em Regras de Transformação da Emissão, clique em **Adicionar Regra.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="a5db1-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="a5db1-136">No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **passar ou filtrar uma afirmação de entrada** de Olá pendente e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="a5db1-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="a5db1-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="a5db1-138">No Olá caixa seguinte tooClaim nome da regra, atribua a regra, um nome.</span><span class="sxs-lookup"><span data-stu-id="a5db1-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="a5db1-139">Por exemplo: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="a5db1-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="a5db1-140">Na lista pendente Olá, tooIncoming seguinte tipo de afirmação, selecione **dentro da rede empresarial**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="a5db1-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="a5db1-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="a5db1-142">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-142">Click **Finish**.</span></span>
9. <span data-ttu-id="a5db1-143">Em Regras de Transformação da Emissão, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="a5db1-144">No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **enviar afirmações utilizando uma regra personalizada** de Olá pendente e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="a5db1-145">Na caixa de Olá em nome da regra de afirmação: introduza *manter os utilizadores com sessão iniciada no*.</span><span class="sxs-lookup"><span data-stu-id="a5db1-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="a5db1-146">Na caixa de regra personalizada de Olá, introduza:</span><span class="sxs-lookup"><span data-stu-id="a5db1-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="a5db1-148">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-148">Click **Finish**.</span></span>
14. <span data-ttu-id="a5db1-149">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-149">Click **Apply**.</span></span>
15. <span data-ttu-id="a5db1-150">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-150">Click **Ok**.</span></span>
16. <span data-ttu-id="a5db1-151">Feche a Gestão do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a5db1-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="a5db1-152">Configurar IPs Fidedignos do Multi-Factor Authentication do Azure com Utilizadores Federados</span><span class="sxs-lookup"><span data-stu-id="a5db1-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="a5db1-153">Agora que Olá afirmações estão ativadas, podemos configurar IPs fidedignos.</span><span class="sxs-lookup"><span data-stu-id="a5db1-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="a5db1-154">Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a5db1-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a5db1-155">Olá esquerda, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="a5db1-156">No diretório, selecione o diretório de olá onde pretende tooset configurar IPs fidedignos.</span><span class="sxs-lookup"><span data-stu-id="a5db1-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="a5db1-157">No diretório que selecionou Olá, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="a5db1-158">Na secção de autenticação multifator Olá, clique em **gerir definições do serviço**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="a5db1-159">Na página de definições do serviço de Olá, em IPs fidedignos, selecione **ignorar várias-factor-autenticação para pedidos de utilizadores federados na minha intranet**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="a5db1-161">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-161">Click **save**.</span></span>
8. <span data-ttu-id="a5db1-162">Depois de tem sido aplicadas Olá atualizações, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="a5db1-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="a5db1-163">Já está!</span><span class="sxs-lookup"><span data-stu-id="a5db1-163">That’s it!</span></span> <span data-ttu-id="a5db1-164">Neste momento, os utilizadores federados do Office 365 só devem ter toouse MFA quando uma afirmação tiver origem a partir da intranet de empresa Olá fora.</span><span class="sxs-lookup"><span data-stu-id="a5db1-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
