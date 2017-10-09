---
title: "aplicações de tooon local de acesso aaaConditional - do Azure AD | Microsoft Docs"
description: "Abrange como tooset configurar o acesso condicional para aplicações publicar toobe acedido remotamente através de Proxy de aplicações do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Trabalhar com acesso condicional no Proxy de aplicações do Azure AD

>[!NOTE]
>Este artigo aplica-se toohello portal clássico do Azure, que está a ser retirado. Recomendamos que utilize Olá [portal do Azure](https://portal.azure.com). No portal do Azure Olá, o Proxy de aplicações, as aplicações têm Olá mesmo funcionalidades de acesso condicional como a quaisquer outras aplicações SaaS. toolearn mais informações sobre o acesso condicional, consulte [introdução ao acesso condicional no Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Pode configurar o acesso regras toogrant acesso condicional tooapplications publicadas com o Proxy da aplicação. Permite-lhe:

* Exigir a autenticação multifator por aplicação
* Exigir autenticação multifator apenas quando os utilizadores não estão no local de trabalho
* Bloquear os utilizadores acedam a aplicações de Olá quando não estão no local de trabalho

Estas regras podem ser aplicados tooall utilizadores e grupos ou apenas toospecific utilizadores e grupos. Por predefinição Olá regra aplica a tooall utilizadores com acesso toohello aplicação. No entanto, regra Olá também pode ser restrito toousers que são membros dos grupos de segurança especificados.  

As regras de acesso são avaliadas quando um utilizador acede a uma aplicação federada que utiliza o OAuth 2.0, OpenID Connect, SAML ou WS-Federation. Além disso, as regras de acesso são avaliadas com OAuth 2.0 e o OpenID Connect quando um token de atualização é tooacquire utilizado um token de acesso.

## <a name="conditional-access-prerequisites"></a>Pré-requisitos de acesso condicional
* Subscrição tooAzure Active Directory Premium
* Um inquilino do Azure Active Directory federado ou gerido
* Inquilinos federados exigem autenticação multifator (MFA)  
    ![Configurar regras de acesso - requer autenticação multifator](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Configurar por aplicação multi-factor authentication
1. Inicie sessão como administrador no Olá portal clássico do Azure.
2. Aceda tooActive diretório e selecione o diretório de Olá em que pretende tooenable Proxy de aplicações.
3. Clique em **aplicações** e desloque-se para baixo toohello **as regras de acesso** secção. secção de regras de acesso de Olá só é apresentado para aplicações publicadas através do Proxy de aplicações que utilizam autenticação federada.
4. Ativar regra de Olá selecionando **ativar as regras de acesso** demasiado**no**.
5. Especifique Olá utilizadores e grupos toowhom Olá regras aplicam-se. Olá utilize **adicionar grupo** botão tooselect um ou mais grupos que se aplica a regra de acesso de Olá toowhich. Esta caixa de diálogo também pode ser utilizados tooremove selecionado grupos.  Quando as regras de Olá são toogroups tooapply selecionado, são impostas quais regras de acesso Olá apenas para utilizadores que pertencem tooone de Olá especificado grupos de segurança.  

   * grupos de segurança de exclusão tooexplicitly da regra de Olá, verifique **exceto** e especifique um ou mais grupos. Os utilizadores que são membros de um grupo no Olá, exceto lista não são tooperform necessária a autenticação multifator.  
   * Se um utilizador tiver sido configurado para utilizar a funcionalidade de autenticação multifator Olá por utilizador, esta definição tem precedência sobre Olá regras de autenticação multifator da aplicação. Um utilizador que foi configurado para a autenticação multifator por utilizador é tooperform necessária a autenticação multifator, mesmo que tenham sido excluídos a partir de regras de autenticação multifator da aplicação Olá. Saiba mais sobre [definições de autenticação e por utilizador do multi-factor](../multi-factor-authentication/multi-factor-authentication.md).
6. Selecione a regra de acesso de Olá que pretende tooset:

   * **Exigir a autenticação multifator**: os utilizadores a aplicam as regras de acesso de toowhom são toocomplete necessária a autenticação multifator antes de aceder Olá aplicação toowhich Olá regra aplica-se.
   * **Requer multi-factor authentication quando não está no trabalho**: os utilizadores ao tentar tooaccess aplicação Olá um endereço IP fidedigno não serão tooperform necessária a autenticação multifator. Olá fidedigno intervalos de endereços IP podem ser configurados na página de definições de autenticação multifator Olá.
   * **Bloquear o acesso quando não está no trabalho**: utilizadores tentar tooaccess Olá aplicação fora da rede empresarial não será capaz de tooaccess aplicação de Olá.

## <a name="configuring-mfa-for-federation-services"></a>Configurar a MFA para os serviços de Federação
Para inquilinos federados, autenticação multifator (MFA) pode ser efetuada pelo Azure Active Directory ou ao hello do AD FS server local. Por predefinição, o MFA ocorre em qualquer página alojada pelo Azure Active Directory. tooconfigure MFA no local, execute o Windows PowerShell e utilize Olá – SupportsMFA propriedade tooset Olá módulo do Azure AD.

Olá exemplo seguinte mostra como tooenable no local MFA utilizando Olá [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) no inquilino do Olá contoso.com:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

Na adição toosetting este sinalizador, Olá federado inquilino do AD FS instância tem de ser configurado tooperform multi-factor authentication. Siga as instruções de Olá para [implementar o Microsoft Azure a autenticação multifator no local](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Consultar também
* [Trabalhar com aplicações com suporte para afirmações](active-directory-application-proxy-claims-aware-apps.md)
* [Publicar aplicações com o Proxy de aplicações](active-directory-application-proxy-publish.md)
* [Ativar o início de sessão único](active-directory-application-proxy-sso-using-kcd.md)
* [Publicar aplicações com o seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)

Para obter notícias mais recentes Olá e atualizações, consulte Olá [blogue do Proxy da aplicação](http://blogs.technet.com/b/applicationproxyblog/)
