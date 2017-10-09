---
title: "Azure Active Directory B2C: Configuração LinkedIn | Microsoft Docs"
description: "Fornecer tooconsumers de inscrição e o início de sessão com contas de LinkedIn nas aplicações que estejam protegidas pelo Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active Directory B2C: Forneça tooconsumers de inscrição e o início de sessão com contas do LinkedIn
## <a name="create-a-linkedin-application"></a>Criar uma aplicação LinkedIn
toouse LinkedIn como um fornecedor de identidade no Azure Active Directory (Azure AD) B2C, tem de toocreate uma aplicação LinkedIn e fornecer com parâmetros corretos Olá. É necessário um toodo de conta LinkedIn isto. Se não tiver uma, pode obtê-lo em [https://www.linkedin.com/](https://www.linkedin.com/).

1. Aceda toohello [site LinkedIn programadores](https://www.developer.linkedin.com/) e inicie sessão com as credenciais da conta LinkedIn.
2. Clique em **aplicações My** no Olá barra de menu superior e, em seguida, clique em **Criar aplicação**.
   
    ![LinkedIn - nova aplicação](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. No Olá **criar uma nova aplicação** formulário, preencha as informações relevantes Olá (**nome da empresa**, **nome**, **Descrição**, **URL da aplicação logótipo**, **utilização de aplicações**, **URL do site**, **E-Mail profissionais** e **telefone da empresa**).
4. Concordo toohello **LinkedIn termos de utilização da API** e clique em **submeter**.
   
    ![LinkedIn - registo de aplicação](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Copie os valores de Olá de **ID de cliente** e **segredo do cliente**. (Pode encontrá-los em **chaves de autenticação**.) Terá de ambos os parâmetros tooconfigure LinkedIn como um fornecedor de identidade no seu inquilino.
   
   > [!NOTE]
   > **Segredo do cliente** é uma credencial de segurança importantes.
   > 
   > 
6. Introduza `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no Olá **autorizado URLs de redirecionamento** campo (em **OAuth 2.0**). Substitua **{inquilino}** com o nome do seu inquilino (por exemplo, contoso.onmicrosoft.com). Clique em **adicionar**e, em seguida, clique em **atualização**. Olá **{inquilino}** valor diferencia maiúsculas de minúsculas.
   
    ![LinkedIn - configuração de aplicação](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Configurar LinkedIn como um fornecedor de identidade no seu inquilino
1. Siga estes passos demasiado[navegue painel de funcionalidades de toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no Olá portal do Azure.
2. No painel de funcionalidades de Olá B2C, clique em **fornecedores de identidade**.
3. Clique em **+ adicionar** , Olá parte superior do painel de Olá.
4. Forneça um amigável **nome** para configuração do fornecedor de identidade de Olá. Por exemplo, introduza "LI".
5. Clique em **tipo de fornecedor de identidade**, selecione **LinkedIn**e clique em **OK**.
6. Clique em **configurar este fornecedor de identidade** e introduza Olá ID de cliente e o segredo do cliente de Olá LinkedIn aplicação que criou anteriormente.
7. Clique em **OK** e, em seguida, clique em **criar** toosave a configuração do LinkedIn.

