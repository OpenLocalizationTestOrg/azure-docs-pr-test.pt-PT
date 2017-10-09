---
title: "aaaHow toodetermine o início de sessão único método toouse | Microsoft Docs"
description: "Compreender Olá único início de sessão modos suportados pelo Azure AD e como toopick Olá, que toochoose para uma aplicação que está interessado."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Como toodetermine o início de sessão único método toouse

Este artigo ajudá-lo toounderstand Olá único início de sessão modos suportados pelo Azure AD e como toopick Olá, que toochoose para uma aplicação que está interessado.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>O início de sessão único e o aprovisionamento modos suportados pelos tipos de aplicação específica

tabela de Olá abaixo descreve Olá diferentes-início de sessão único e o aprovisionamento modos suportados por cada Olá acima tipos de aplicações. Pode utilizar esta tabela toohelp toounderstand que aplicação terá de tooadd toosupport um objetivo específico.

  ![Tabela de tipos da Ásia-Pacífico](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Como toochoose um modo de início de sessão único

Olá suportado **de sessão único-** modos de aplicações do Azure AD estão listados abaixo.

-   **Azure AD-início de sessão único desativada** – escolha do Azure AD-início de sessão único desativada **modo de início de sessão único** se são ainda não está preparado toointegrate esta aplicação com o início de sessão com o Azure AD ou está simplesmente a testá-lo

-   **Ligado início de sessão** – escolha Olá [ligado início de sessão](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de início de sessão único** se tiver uma aplicação que já está ligada um único início de sessão solução existente, ou se pretender apenas toopublish simples de ligação para os seus utilizadores no respetivo [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [iniciador da aplicação do Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Baseado em palavra-passe de início de sessão** – escolha Olá [baseada em palavra-passe de início de sessão](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de início de sessão único** se a aplicação apresenta um campo de nome de utilizador e palavra-passe HTML e quiser toostore que nome de utilizador e palavra-passe segura toobe reproduzido toohello aplicação mais tarde

-   **Baseados em SAML início de sessão** – escolha Olá [baseados em SAML início de sessão](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) baseada em funções da aplicação toospecific de início de sessão único modo se a aplicação suporta protocolos SAML ou o OpenID Connect hello, ou se quiser toobe toomap capaz de utilizadores nas regras que define na sua SAML afirmações *(**Nota:** esta opção não está disponível quando o proxy da aplicação Olá está configurado para uma aplicação) *

-   **Com base no cabeçalho de início de sessão** – Escolha esta [com base no cabeçalho de início de sessão](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) único início de sessão se tiver uma aplicação utilizando PingAccess que suporta o cabeçalho de HTTP basear o modo autenticação que pretende tooperform início de sessão único em demasiado *(**Nota:** esta opção só está disponível quando o proxy da aplicação Olá e PingAccess está configurado para uma aplicação) *

-   **Autenticação integrada do Windows** – escolha Olá [autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) início de sessão único modo quando a exposição de uma aplicação de WIA no local que pretende tooperform início de sessão único em demasiado*(*  *Nota:** esta opção só está disponível quando o proxy da aplicação Olá está configurado para uma aplicação) *

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Modos de início de sessão único para aplicações desenvolvidas por personalizada

Aplicações tiver personalizado desenvolvido através de Olá [aplicações desenvolvidas por personalizada](#_Custom-Developed_Applications) experiência também suportam adicionais único início de sessão modos não enumerados acima. Estas incluem:

-   [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) com base em início de sessão

-   [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) com base em início de sessão

-   [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) com base em início de sessão

-   [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) com base em início de sessão

Olá leitura [guia para programadores do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn mais informações sobre como aplicação toocreate um desenvolvidas personalizada que suporte estas único modos de início de sessão.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Como tooset uma aplicação do único modo de início de sessão

do tooset uma aplicação **de sessão único-** modo, siga Olá instruções abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

   * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecionar aplicação Olá pretende tooconfigure-início de sessão único

7.  Quando carrega a aplicação Olá, clique em **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

## <a name="next-steps"></a>Passos seguintes
[Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação](active-directory-application-proxy-sso-using-kcd.md)

