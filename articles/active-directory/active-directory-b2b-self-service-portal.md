---
title: "portal de inscrição do serviço de aaaSelf para colaboração B2B do Azure Active Directory do | Microsoft Docs"
description: "Colaboração do Azure Active Directory B2B suporta as relações entre empresas ao permitir o acesso de tooselectively de parceiros de negócio a aplicações empresariais"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Portal self-service para inscrição de colaboração B2B do Azure AD

Os clientes podem fazer muito com funcionalidades incorporadas Olá expostas através do nosso administrador de TI [portal do Azure](https://portal.azure.com) e no nosso [painel de acesso de aplicação](https://myapps.microsoft.com) para os utilizadores finais. Mas estamos também em atenção de que as empresas necessitam de fluxo de trabalho do toocustomize Olá integração para B2B utilizadores toofit as necessidades da sua organização. Podem fazê-lo com [nossa API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

Em discussões com os nossos clientes, vemos um comuns tem de aumentar a segurança acima de todos os outros. Olá inviting organização poderá não saber antecedência que Olá colaboradores externos individuais são que precisa de aceder a recursos de tootheir. Pretendessem uma forma para os utilizadores de empresas demasiado inscrevem-se com um conjunto de políticas que Olá inviting controlos da organização. Este cenário é possível através do nosso APIs, pelo que iremos publicado um projeto no Github que criou apenas que: [projeto do Github de exemplo](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Nosso projeto Github demonstra como as organizações podem utilizar os APIs e fornecer uma capacidade de inscrição baseadas em políticas, self-service para os respetivos parceiros confiadores, com regras que determinam aplicações Olá que poderem aceder ao. Os utilizadores do parceiro podem obter acesso tooresources quando precisam, de forma segura, sem necessidade de Olá inviting organização toomanually carregá-los. Pode facilmente implementar o projeto de Olá para uma subscrição do Azure à sua escolha.

## <a name="as-is-code"></a>Como-é código

Lembre-se de que este código é disponibilizado como a utilização de toodemonstrate um exemplo de convite de Olá do Azure Active Directory B2B API. Deve ser personalizada pela sua equipa de desenvolvimento ou de um parceiro e deve ser revisto antes de ser implementado num cenário de produção.

## <a name="next-steps"></a>Passos seguintes

Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:
* [O que é a colaboração B2B do Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como é que os administradores de Azure Active Directory adicionar utilizadores de colaboração do B2B?](active-directory-b2b-admin-add-users.md)
* [Como é que os infotrabalhadores adicionar utilizadores de colaboração do B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de Olá de Olá e-mail de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento e colaboração do Azure AD B2B](active-directory-b2b-licensing.md)
* [Resolução de problemas de colaboração B2B do Azure Active Directory do](active-directory-b2b-troubleshooting.md)
* [Colaboração do Azure Active Directory B2B perguntas mais frequentes (FAQ)](active-directory-b2b-faq.md)
* [Autenticação multifator para os utilizadores da colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar utilizadores de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)