---
title: "aaaHow tooconfigure Google autenticação para a sua aplicação de serviços aplicacionais"
description: "Saiba como tooconfigure Google autenticação para a sua aplicação de serviços de aplicações."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Como tooconfigure o início de sessão de Google de toouse de aplicação do serviço de aplicações
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure App Service do Azure toouse Google como um fornecedor de autenticação.

procedimento de Olá toocomplete neste tópico, tem de ter uma conta do Google que tenha um endereço de correio eletrónico verificado. toocreate uma nova conta do Google, aceda demasiado[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Registar a aplicação com o Google
1. Inicie sessão no toohello [portal do Azure]e navegue tooyour aplicação. Copiar o **URL**, que utiliza a aplicação do Google tooconfigure posterior.
2. Navegue toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) Web site, inicie sessão com as credenciais da conta Google, clique em **criar projeto**, forneça um **nome do projeto**, em seguida, clique em  **Criar**.
3. Em **APIs sociais** clique **Google + API** e, em seguida, **ativar**.
4. No Olá à esquerda de navegação, **credenciais** > **ecrã de consentimento do OAuth**, em seguida, selecione o **endereço de correio eletrónico**, introduza um **denomedeproduto**e clique em **guardar**.
5. No Olá **credenciais** separador, clique em **criar credenciais** > **ID de cliente OAuth**, em seguida, selecione **aplicação Web**.
6. Colar hello do serviço de aplicações **URL** que copiou anteriormente para **autorizado origens de JavaScript**, em seguida, cole o redirecionamento URI para **autorizado o URI de redirecionamento**. Olá redirecionamento URI é Olá URL da aplicação acrescentada com o caminho de Olá, */.auth/login/google/callback*. Por exemplo, `https://contoso.azurewebsites.net/.auth/login/google/callback`. Certifique-se de que está a utilizar o esquema HTTPS de Olá. Em seguida, clique em **Criar**.
7. No seguinte ecrã de Olá, tome nota dos valores de hello do cliente de Olá segredo de cliente e o ID.

    > [!IMPORTANT]
    > segredo do cliente Olá é uma credencial de segurança importantes. Não partilhe este segredo com ninguém e distribui-lo dentro de uma aplicação de cliente.


## <a name="secrets"></a>Aplicação do Google adicionar informações tooyour
1. Novamente no Olá [portal do Azure], navegue até tooyour aplicação. Clique em **definições**e, em seguida, **autenticação / autorização**.
2. Se Olá autenticação / autorização funcionalidade não está ativada, ative o comutador de Olá demasiado**no**.
3. Clique em **Google**. Cole valores de ID de aplicação e o segredo de aplicação Olá que obteve anteriormente e, opcionalmente ativar qualquer âmbitos que requer a sua aplicação. Em seguida, clique em **OK**.
   
   ![][1]
   
   Por predefinição, o serviço de aplicações fornece autenticação mas não a restringir o conteúdo de site de tooyour acesso autorizado e APIs. Tem de autorizar os utilizadores no seu código de aplicação.
4. (Opcional) toorestrict acesso tooyour site tooonly, os utilizadores autenticados pelo Google, defina **ação tootake quando o pedido não é autenticado** demasiado**Google**. Isto requer que todos os pedidos de ser autenticados e todos os pedidos não autenticados são tooGoogle redirecionado para a autenticação.
5. Clique em **Guardar**.

Agora, está pronto toouse Google para autenticação na sua aplicação.

## <a name="related-content"></a>Relacionados com o conteúdo
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal do Azure]: https://portal.azure.com/

