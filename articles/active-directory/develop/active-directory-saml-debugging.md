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
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Como toodebug baseados em SAML único início de sessão tooapplications no Azure Active Directory
Quando a depuração uma integração de aplicações baseados em SAML, é frequentemente útil toouse uma ferramenta como o [Fiddler](http://www.telerik.com/fiddler) toosee Olá pedido SAML, resposta SAML Olá e Olá real SAML token emitido toohello aplicação. Ao examinar o token SAML Olá, pode Certifique-se de que todos os Olá necessita de atributos, Olá nome de utilizador no requerente do Olá SAML e Olá emissor URI são vem conforme esperado.

![][1]

Olá resposta do Azure AD que contém o token SAML Olá é normalmente Olá que ocorre após um redirecionamento HTTP 302 de https://login.windows.net e está configurado toohello enviado **URL de resposta** da aplicação Olá. 

Pode ver o token SAML Olá ao selecionar esta linha e, em seguida, selecionar Olá **Inspetores > Web Forms** separador no painel à direita Olá. A partir daí, faça duplo clique Olá **SAMLResponse** valor e selecione **enviar tooTextWizard**. Em seguida, selecione **de Base64** de Olá **transformar** menu toodecode Olá token e ver o respetivo conteúdo.

**Tenha em atenção**: pedido de conteúdo de Olá toosee este HTTP, Fiddler pode solicitar-lhe tooconfigure a desencriptação de tráfego HTTPS, o que precisa de toodo.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](../active-directory-apps-index.md)
* [Configurar único início de sessão tooapplications que não estejam na Galeria de aplicações do Azure Active Directory Olá](../active-directory-saas-custom-apps.md)
* [Como tooCustomize as afirmações emitidas no hello SAML Token para aplicações de Pre-Integrated](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png