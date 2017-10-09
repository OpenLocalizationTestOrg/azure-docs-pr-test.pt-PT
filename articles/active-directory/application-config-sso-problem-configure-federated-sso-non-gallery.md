---
title: "configuração federada-início de sessão único para uma aplicação não Galeria de aaaProblem | Microsoft Docs"
description: "Resolver alguns dos problemas comuns de Olá que poderão surgir quando configurar aplicação SAML personalizada federado único início de sessão tooyour que não está listada no Olá Galeria de aplicações do Azure AD"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Configuração federada-início de sessão único para uma aplicação não galeria do problema

Se ocorrer um problema ao configurar uma aplicação. Certifique-se de que seguiu todos os passos de Olá artigo Olá [configurar único início de sessão tooapplications que não estejam na Galeria de aplicações do Azure Active Directory Olá.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Não é possível adicionar outra instância da aplicação Olá

tooadd uma segunda instância de uma aplicação, terá de toobe capaz de:

-   Configure um identificador exclusivo para a segunda instância de Olá. Não será Olá tooconfigure capaz de identificador do mesmo utilizado para a primeira instância de Olá.

-   Configure um certificado diferente que Olá utilizada para Olá primeira instância.

Se hello aplicação não suporta qualquer um dos Olá acima. Em seguida, não será capaz de tooconfigure uma segunda instância.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Onde definir o formato do Olá EntityID (identificador de utilizador)

Não ter o formato de EntityID (utilizador Identifier) de Olá de tooselect consegue que do Azure AD envia toohello aplicação resposta Olá após a autenticação de utilizador.

Formato de Olá selecione AD do Azure para o atributo de NameID Olá (identificador de utilizador) com base no valor de Olá selecionado ou Olá formato pedido por aplicação Olá Olá SAML AuthRequest. Para obter mais informações, visite artigo Olá [protocolo SAML de início de sessão único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na secção de Olá NameIDPolicy,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Onde posso obter metadados da aplicação Olá ou o certificado do Azure AD

metadados da aplicação Olá toodownload ou o certificado do Azure AD, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

   * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá tiver configurado o início de sessão único.

7.  Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

8.  Aceda demasiado**certificado de assinatura de SAML** secção, em seguida, clique em **transferir** valor da coluna. Dependendo do que aplicação Olá necessita de configurar o início de sessão único, consulte o toodownload de opção Olá Olá XML de metadados ou Olá certificado.

Azure AD não fornece uma metadados de Olá tooget URL. Olá metadados só podem ser obtidos como um ficheiro XML.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Não sabe como toocustomize SAML afirmações enviadas tooan aplicação

toolearn como afirmações de atributo do toocustomize Olá SAML enviada tooyour aplicação, consulte [afirmações mapeamento no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.

## <a name="next-steps"></a>Passos seguintes
[Gestão de aplicações com o Azure Active Directory](active-directory-enable-sso-scenario.md)
