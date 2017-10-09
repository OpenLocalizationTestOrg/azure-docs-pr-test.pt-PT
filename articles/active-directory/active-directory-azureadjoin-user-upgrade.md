---
title: "aaaSet segurança de um dispositivo Windows 10 com o Azure AD a partir das definições | Microsoft Docs"
description: "Explica como os utilizadores podem associar tooAzure AD através do menu de definições de Olá."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Configurar um dispositivo Windows 10 com o Azure AD a partir das definições
Se já estiver a utilizar o Windows 7 ou Windows 8 e o computador ou dispositivo tiver sido atualizado tooWindows 10, pode participar tooAzure do Active Directory (Azure AD) através do menu de definições de Olá.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD a partir do menu de definições de Olá
1. De Olá **iniciar** menu, clique em Olá **definições** atalho.
2. De **definições**, selecione **sistema**->**sobre**->**associação do Azure AD**.
   
   <center>
   ![Associação do Azure AD a partir do menu de definições de Olá](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Clique em **continuar** na janela de mensagem de associação do Azure AD Olá.
   
   <center>
   ![Janela de mensagem de associação do Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Forneça as credenciais de início de sessão. Esta experiência de início de sessão irá incluir todos os passos de Olá são toocomplete necessária autenticação. Se fizer parte de um inquilino federado, o administrador irá fornecer-lhe experiência de Federação Olá que está alojada pela sua organização.
   <center>
   ![Forneça as credenciais de início de sessão](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Se a sua organização tiver configurado o multi-factor Authentication do Azure para efetuar a adesão tooAzure AD, forneça o segundo fator de Olá antes de continuar.
6. Clique em **aceitar** no Olá **permitir toobe este dispositivo gerido** ecrã.
7. Deverá ver a mensagem de saudação "o dispositivo está agora associado tooyour organização no Azure AD".

## <a name="additional-information"></a>Informações adicionais
* [Saiba mais sobre os cenários de utilização da Associação do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Associação do Azure AD](active-directory-azureadjoin-setup.md)
* [Autenticar identidades sem palavras-passe através do Microsoft Passport](active-directory-azureadjoin-passport.md)

