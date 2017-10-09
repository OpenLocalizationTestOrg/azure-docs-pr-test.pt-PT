---
title: "autenticação de Account Microsoft tooconfigure aaaHow para a sua aplicação de serviços aplicacionais"
description: "Saiba como autenticação de Account Microsoft tooconfigure para a sua aplicação de serviços de aplicações."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Como tooconfigure o início de sessão de Account Microsoft de toouse de aplicação do serviço de aplicações
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure App Service do Azure toouse Account Microsoft como um fornecedor de autenticação. 

## <a name="register-microsoft-account"></a>Registar a sua aplicação com a conta Microsoft
1. Inicie sessão no toohello [portal do Azure]e navegue tooyour aplicação. Copiar o **URL**que mais tarde, utiliza tooconfigure a aplicação com Account Microsoft.
2. Navegue toohello [aplicações My] página em Olá Microsoft Account Developer Center e inicie sessão com a sua conta Microsoft, se necessário.
3. Clique em **adicionar uma aplicação**, em seguida, escreva um nome de aplicação e, em **Criar aplicação**.
4. Tome nota do Olá **ID da aplicação**, uma vez que irá precisar dele mais tarde. 
5. Em "Plataformas", clique em **adicionar plataforma** e selecione "Web".
6. Em "URI de redirecionamento" alimentação Olá ponto final para a sua aplicação, em seguida, clique em **guardar**. 
   
   > [!NOTE]
   > O redirecionamento URI é Olá URL da aplicação acrescentada com o caminho de Olá, */.auth/login/microsoftaccount/callback*. Por exemplo, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Certifique-se de que está a utilizar o esquema HTTPS de Olá.
   
7. Em "Segredos de aplicação", clique em **gerar a nova palavra-passe**. Tome nota do valor de Olá que aparece. Depois de deixar a página Olá, não será novamente apresentado.

    > [!IMPORTANT]
    > palavra-passe de Olá é uma credencial de segurança importantes. Não partilhe palavra-passe de Olá com ninguém e distribui-lo dentro de uma aplicação de cliente.

## <a name="secrets"></a>Tooyour de informações de adicionar a conta do Microsoft aplicação de serviço de aplicações
1. Novamente no Olá [portal do Azure], navegue até tooyour aplicação, clique em **definições** > **autenticação / autorização**.
2. Se Olá autenticação / autorização funcionalidade não está ativada, mude- **no**.
3. Clique em **conta Microsoft**. Colar Olá ID da aplicação e a palavra-passe os valores que obteve anteriormente e, opcionalmente ativar qualquer âmbitos que requer a sua aplicação. Em seguida, clique em **OK**.
   
    ![][1]
   
    Por predefinição, o serviço de aplicações fornece autenticação mas não a restringir o conteúdo de site de tooyour acesso autorizado e APIs. Tem de autorizar os utilizadores no seu código de aplicação.
4. (Opcional) toorestrict acesso tooyour site tooonly, os utilizadores autenticados pelo conta Microsoft, defina **ação tootake quando o pedido não é autenticado** demasiado**Account Microsoft**. Isto requer que todos os pedidos de ser autenticados e todos os pedidos não autenticados são direcionados tooMicrosoft conta para autenticação.
5. Clique em **Guardar**.

Agora, está pronto toouse Account Microsoft para a autenticação na sua aplicação.

## <a name="related-content"></a>Relacionados com o conteúdo
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[aplicações My]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portal do Azure]: https://portal.azure.com/
