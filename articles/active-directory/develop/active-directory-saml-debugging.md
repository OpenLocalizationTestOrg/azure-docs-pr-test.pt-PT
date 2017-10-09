---
title: "aaaHow toodebug baseados em SAML único início de sessão tooapplications no Azure Active Directory | Microsoft Docs"
description: "Saiba como toodebug baseados em SAML único início de sessão tooapplications no Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="67c1e-103">Como toodebug baseados em SAML único início de sessão tooapplications no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67c1e-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="67c1e-104">Quando a depuração uma integração de aplicações baseados em SAML, é frequentemente útil toouse uma ferramenta como o [Fiddler](http://www.telerik.com/fiddler) toosee Olá pedido SAML, resposta SAML Olá e Olá real SAML token emitido toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="67c1e-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="67c1e-105">Ao examinar o token SAML Olá, pode Certifique-se de que todos os Olá necessita de atributos, Olá nome de utilizador no requerente do Olá SAML e Olá emissor URI são vem conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="67c1e-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="67c1e-106">Olá resposta do Azure AD que contém o token SAML Olá é normalmente Olá que ocorre após um redirecionamento HTTP 302 de https://login.windows.net e está configurado toohello enviado **URL de resposta** da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="67c1e-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="67c1e-107">Pode ver o token SAML Olá ao selecionar esta linha e, em seguida, selecionar Olá **Inspetores > Web Forms** separador no painel à direita Olá.</span><span class="sxs-lookup"><span data-stu-id="67c1e-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="67c1e-108">A partir daí, faça duplo clique Olá **SAMLResponse** valor e selecione **enviar tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="67c1e-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="67c1e-109">Em seguida, selecione **de Base64** de Olá **transformar** menu toodecode Olá token e ver o respetivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="67c1e-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="67c1e-110">**Tenha em atenção**: pedido de conteúdo de Olá toosee este HTTP, Fiddler pode solicitar-lhe tooconfigure a desencriptação de tráfego HTTPS, o que precisa de toodo.</span><span class="sxs-lookup"><span data-stu-id="67c1e-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="67c1e-111">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="67c1e-111">Related Articles</span></span>
* [<span data-ttu-id="67c1e-112">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67c1e-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="67c1e-113">Configurar único início de sessão tooapplications que não estejam na Galeria de aplicações do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="67c1e-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="67c1e-114">Como tooCustomize as afirmações emitidas no hello SAML Token para aplicações de Pre-Integrated</span><span class="sxs-lookup"><span data-stu-id="67c1e-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png