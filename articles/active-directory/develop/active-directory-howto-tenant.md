---
title: aaaHow tooget um inquilino do Azure AD | Microsoft Docs
description: "Como tooget um Azure Active Directory de inquilino para registar e criar aplicações."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Como inquilino tooget um Azure Active Directory
No Azure Active Directory (Azure AD), uma organização é representada por um [inquilino](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).  É uma instância dedicada do Olá serviço Azure AD que uma organização recebe e possui quando se inscreve num serviço de nuvem da Microsoft, tais como o Azure, o Microsoft Intune ou o Office 365.  Cada inquilino do Azure AD é distinto e separado dos outros inquilinos do Azure AD.  

Um inquilino aloja os utilizadores Olá da empresa e Olá informações sobre os mesmos - as respetivas palavras-passe, dados de perfil de utilizador, permissões e assim sucessivamente.  Também contém grupos, aplicações e outras informações relativas a tooan organização e a respetiva segurança.

toosign de utilizadores do Azure AD tooallow na aplicação tooyour, tem de registar a aplicação de um inquilino do seu próprio.  A publicação de uma aplicação num inquilino do Azure AD é **absolutamente gratuita**.  Na verdade, a maior parte dos programadores cria vários inquilinos e aplicações com o objetivo de experimentar, desenvolver e testar.  As organizações que subscrevem e consomem a aplicação podem optar por toopurchase licenças se pretenderem tootake partido das funcionalidades avançadas do diretório.

Por isso, como deve proceder para obter um inquilino do Azure AD?  Olá processo poderá ser um pouco diferente se a:

* [Tiver já uma subscrição do Office 365](#use-an-existing-office-365-subscription)
* [Tiver já uma subscrição do Azure associada a uma Conta Microsoft](#use-an-msa-azure-subscription)
* [Tiver já uma subscrição do Azure associada a uma conta da organização](#use-an-organizational-azure-subscription)
* [Ter nenhum dos Olá acima & pretende toostart a partir do zero](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Utilizar uma subscrição do Office 365 existente
Se tiver uma subscrição existente do Office 365, já tem um inquilino do Azure AD! Pode iniciar sessão toohello [portal do Azure](https://portal.azure.com) com o Office 365 conta e começar a utilizar o Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Utilizar uma subscrição do Azure MSA
Se já tiver uma subscrição do Azure com a sua conta individual da Microsoft, já possui um inquilino!  Quando inicia sessão no toohello [Portal do Azure](https://portal.azure.com), automaticamente serão registados no inquilino do tooyour predefinido. São toouse livre este inquilino como Consulte ajustar - mas poderá ser útil toocreate uma conta de administrador organizacional.

toodo por isso, siga estes passos.  Em alternativa, poderá desejar toocreate um novo inquilino e criar um administrador nesse inquilino seguindo um processo semelhante.

1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com) com a sua conta individual
2. Navegue toohello secção "Do Azure Active Directory" portal Olá (localizado na barra de navegação esquerda Olá, em **mais serviços**)
3. Esta automaticamente deve ser iniciada no toohello "Diretório predefinido", caso contrário, pode mudar diretórios clicando em seu nome de conta no canto superior direito Olá.
4. De Olá **tarefas rápida** secção, escolha **adicionar um utilizador**.
5. No formulário Adicionar utilizador de Olá, forneça Olá os detalhes:

   * Nome: (escolher um valor adequado)
   * Nome de Utilizador: (escolher um nome de utilizador para este administrador)
   * Perfil: (preencher os valores apropriados Olá para o nome próprio, último nome do título de trabalho e departamento)
   * Função: Administrador Global
6. Quando tiver concluído Olá Adicionar formulário do utilizador e receber Olá palavra-passe temporária novo utilizador administrativo Olá, ser toorecord se esta palavra-passe pois terá toologin com este novo utilizador na palavra-passe Olá de toochange de ordem. Também pode enviar a palavra-passe de Olá diretamente toohello utilizador através de uma mensagem de correio eletrónico alternativa.
7. Clique em **criar** novo utilizador do toocreate Olá.
8. toochange Olá palavra-passe temporária, iniciar sessão [https://login.microsoftonline.com](https://login.microsoftonline.com) com este novo utilizador da conta e altere a palavra-passe Olá quando solicitado.

## <a name="use-an-organizational-azure-subscription"></a>Utilizar uma subscrição organizacional do Azure
Se já tiver uma subscrição do Azure com a sua conta organizacional, já possui um inquilino!  No Olá [Portal do Azure](https://portal.azure.com), encontrará um inquilino quando navega demasiado "Mais serviços" e "Do Azure Active Directory".  São toouse livre este inquilino como ver ajustar.

## <a name="start-from-scratch"></a>Começar do zero
Se todos os Olá acima não fizer qualquer sentido tooyou, não se preocupe.  Visite simplesmente [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign para o Azure com uma nova organização.  Depois de concluir o processo de Olá, terá o seu próprio inquilino do Azure AD com o nome de domínio de Olá que escolheu durante a cópia de segurança.  No Olá [Portal do Azure](https://portal.azure.com), pode encontrar o seu inquilino ao navegar demasiado "Do Azure Active Directory" na Olá navegação esquerda

Como parte do processo de Olá de inscrição no Azure, será necessário tooprovide detalhes de cartão de crédito.  Pode continuar com confiança, não lhe será cobrado nada por publicar aplicações no Azure AD ou por criar novos inquilinos.
