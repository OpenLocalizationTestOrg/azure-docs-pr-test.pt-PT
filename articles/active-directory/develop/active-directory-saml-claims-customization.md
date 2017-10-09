---
title: "afirmações de aaaCustomizing emitidas no token SAML Olá para aplicações previamente integradas no Azure Active Directory | Microsoft Docs"
description: "Saiba como toocustomize Olá as afirmações emitidas no Olá token SAML para aplicações previamente integradas no Azure Active Directory"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Personalizar afirmações emitidas em Olá token SAML para aplicações previamente integradas no Azure Active Directory
Hoje o Azure Active Directory suporta milhares de aplicações previamente integradas no Olá Galeria de aplicações do Azure AD, incluindo mais 360 que suporta o início de sessão único através do protocolo de Olá SAML 2.0. Quando um utilizador efetua a autenticação de aplicação tooan através do Azure AD utilizando SAML, do Azure AD envia uma aplicação de token toohello (através de um HTTP POST). E, em seguida, a aplicação Olá valida e utiliza Olá token toolog Olá utilizador em vez de pedir um nome de utilizador e palavra-passe. Estes tokens SAML contém informações sobre o utilizador Olá conhecido como "afirmações".

Na identidade-enunciar, uma "reclamação" informações de Estados de um fornecedor de identidade sobre um utilizador no interior do token de Olá que emitem para esse utilizador. No [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), estes dados normalmente estão contidos no Olá declaração de atributo de SAML. Olá ID exclusivo do utilizador é normalmente representado na Olá que SAML requerente também denominada como identificador de nome.

Por predefinição, o Azure Active Directory emite uma aplicação de token tooyour SAML que contém uma afirmação NameIdentifier, com um valor de nome de utilizador Olá (também conhecidas como nome principal do utilizador), no Azure AD. Este valor pode identificar exclusivamente o utilizador Olá. token SAML Olá também contém as afirmações adicionais que contém o endereço de correio eletrónico do utilizador Olá, nome próprio e apelido.

tooview ou editar Olá as afirmações emitidas no Olá aplicação de token toohello SAML, application Olá aberto no portal do Azure. Em seguida, selecione Olá **ver e editar todos os outros atributos de utilizador** caixa de verificação no Olá **atributos de utilizador** secção da aplicação Olá.

![Secção de atributos de utilizador][1]

Existem duas razões possíveis por que razão poderá necessitar de afirmações de Olá de tooedit emitidas no token SAML Olá:
* aplicação Olá foi escrita toorequire outro conjunto de afirmação URIs ou valores de afirmação.
* aplicação de Olá tiver sido implementada de forma que requer Olá NameIdentifier afirmação toobe algo que não seja o nome de utilizador Olá (também conhecidas como nome principal do utilizador) armazenados no Azure Active Directory.

Pode editar qualquer um dos valores de afirmação Olá predefinidos. Selecione a linha de afirmação de Olá na tabela de atributos de tokens de SAML Olá. Esta ação abre Olá **Editar atributo** secção e, em seguida, pode editar o nome de afirmação, o valor e o espaço de nomes associado Olá afirmação.

![Editar atributo de utilizador][2]

Pode também remover afirmações (que não seja NameIdentifier) utilizando o menu de contexto de Olá, abre-se ao clicar no Olá **...**  ícone.  Também pode adicionar nova afirmações utilizando Olá **adicionar atributo** botão.

![Editar atributo de utilizador][3]

## <a name="editing-hello-nameidentifier-claim"></a>Editar Olá NameIdentifier afirmação
problema de Olá toosolve onde a aplicação Olá tiver sido implementada com um nome de utilizador diferente, clique em Olá **identificador de utilizador** pendente no Olá **atributos de utilizador** secção. Esta ação apresenta uma caixa de diálogo com várias opções diferentes:

![Editar atributo de utilizador][4]

Na lista pendente Olá, selecione **user.mail** tooset Olá NameIdentifier afirmação de endereço de correio eletrónico do utilizador Olá toobe no diretório de Olá. Em alternativa, selecione **user.onpremisessamaccountname** SAM nome do utilizador toohello tooset da conta que tenha sido sincronizados a partir no local do Azure AD.

Também pode utilizar Olá especial **ExtractMailPrefix()** sufixo de domínio do função tooremove Olá do endereço de correio eletrónico Olá, nome da conta do SAM ou nome principal de utilizador de Olá. Extrai só Olá primeira parte utilizador Olá que está a ser transmitidos através de nome (por exemplo, "joe_smith" em vez de joe_smith@contoso.com).

![Editar atributo de utilizador][5]

Tem agora também adicionámos Olá **join()** Olá toojoin de função verificar domínio com o valor do identificador de utilizador de Olá. Quando seleciona a função de join() Olá Olá **identificador de utilizador** primeiro selecione Olá identificador de utilizador como, como o nome do principal utilizador ou endereço de e-mail e, em seguida, no Olá, segundo a pendente, selecione o domínio verificado. Se selecionar o endereço de correio eletrónico Olá com o domínio verificado Olá, em seguida, do Azure AD extrai Olá nome de utilizador do primeiro valor joe_smith Olá de joe_smith@contoso.com e o acrescenta com contoso.onmicrosoft.com. Consulte o seguinte exemplo de Olá:

![Editar atributo de utilizador][6]

## <a name="adding-claims"></a>A adição de afirmações
Ao adicionar uma afirmação, pode especificar o nome do atributo Olá (que estritamente não necessita de toofollow um padrão URI de acordo com a especificação SAML Olá). Definir Olá valor tooany atributo de utilizador que está armazenado no diretório de Olá.

![Adicione o atributo de utilizador][7]

Por exemplo, terá de toosend departamento Olá que Olá utilizador pertence tooin respetiva organização como uma afirmação (como, vendas). Introduza o nome de afirmação de Olá conforme esperado pela aplicação Olá e, em seguida, selecione **user.department** como valor de Olá.

> [!NOTE]
> Se para um utilizador especificado não existir nenhum valor armazenado para um atributo selecionado, em seguida, esse afirmação não é a ser emitida no token de Olá.

> [!TIP]
> Olá **user.onpremisesecurityidentifier** e **user.onpremisesamaccountname** só são suportadas quando a sincronização dos dados de utilizador no local do Active Directory utilizando Olá [Azure Ferramentas do AD Connect](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Afirmações restritas

Existem algumas restritas afirmações no SAML. Se adicionar estas afirmações, em seguida, do Azure AD não envie estas afirmações. Seguem-se Olá SAML restringe o conjunto de afirmações:

    | Tipo de afirmação (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/Expiration |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/Expired |
    | http://schemas.microsoft.com/Identity/Claims/accesstoken |
    | http://schemas.microsoft.com/Identity/Claims/openid2_id |
    | http://schemas.microsoft.com/Identity/Claims/identityprovider |
    | http://schemas.microsoft.com/Identity/Claims/objectidentifier |
    | http://schemas.microsoft.com/Identity/Claims/PUID |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/NameIdentifier [MR1] |
    | http://schemas.microsoft.com/Identity/Claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/AuthenticationInstant |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/AuthenticationMethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/Claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/Groups |
    | http://schemas.microsoft.com/Claims/Groups.Link |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/role |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/Claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/Claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/Claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/Claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/Identity/Claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/Authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/SID |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/UPN |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/GroupSID |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/SPN |
    | http://schemas.microsoft.com/ws/2008/06/Identity/Claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/Identity/Claims/SCOPE |

## <a name="next-steps"></a>Passos seguintes
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](../active-directory-apps-index.md)
* [Configurar único início de sessão tooapplications que não estejam na Galeria de aplicações do Azure Active Directory Olá](../active-directory-saas-custom-apps.md)
* [Resolução de problemas baseados em SAML Single Sign-On](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png