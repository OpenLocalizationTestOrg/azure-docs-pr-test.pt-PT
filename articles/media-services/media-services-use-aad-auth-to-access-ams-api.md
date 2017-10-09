---
title: "aaaAccess API de serviços de suporte de dados do Azure com a autenticação do Azure Active Directory | Microsoft Docs"
description: "Saiba mais sobre conceitos e passos tootake toouse Azure Active Directory (Azure AD) tooauthenticate acesso toohello API de serviços de suporte de dados do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Aceder Olá API de serviços de suporte de dados do Azure com a autenticação do Azure AD
 
Olá API de serviços de suporte de dados do Azure é uma API RESTful. Pode utilizar este tooperform operações nos recursos de suporte de dados utilizando uma API REST ou ao utilizar SDKs do cliente disponíveis. Media Services do Azure oferece um SDK do cliente de Media Services para Microsoft .NET. toobe autorizado tooaccess recursos de Media Services e Olá API dos serviços de suporte de dados, tem primeiro de ser autenticado. 

Os Media Services suportam [Azure Active Directory (Azure AD)-autenticação com base no](../active-directory/active-directory-whatis.md). Olá serviço REST de suporte de dados do Azure requer que o utilizador Olá ou aplicação que faz com que os pedidos de API de REST de Olá têm ambos Olá **contribuinte** ou **proprietário** função tooaccess Olá recursos. Para obter mais informações, consulte [introdução ao controlo de acesso baseado em funções no portal do Azure de Olá](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Atualmente, os Media Services suportam o modelo de autenticação do serviço de controlo de acesso do Azure Olá. No entanto, a autorização de controlo de acesso vai ser preterida no dia 1 de Junho de 2018. Recomendamos que migre o modelo de autenticação toohello do Azure AD logo que possível.

Este documento fornece uma descrição geral de como tooaccess Olá API dos serviços de suporte de dados através de REST ou de APIs de .NET.

## <a name="access-control"></a>Controlo de acesso

Para Olá toosucceed de pedido de REST de suporte de dados do Azure, o utilizador chamada Olá tem de ter uma função de contribuinte ou proprietário para Olá está a tentar tooaccess de conta de Media Services.  
Apenas um utilizador com função de proprietário Olá pode dar suporte de dados (conta) de recursos de acesso toonew os utilizadores ou aplicações. função de contribuinte Olá pode aceder a recursos de suporte de dados de Olá apenas.
Pedidos não autorizados falharam com o código de estado de 401. Se vir este código de erro, verifique se o utilizador tem Olá contribuinte ou função de proprietário atribuído da conta de Media Services do utilizador Olá. Pode verificar isto no Olá portal do Azure. Procure a sua conta de media e, em seguida, clique em Olá **controlo de acesso** separador. 

![Separador de controlo de acesso](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Tipos de autenticação 
 
Quando utiliza a autenticação do Azure AD com Media Services do Azure, tem duas opções de autenticação:

- **Autenticação de utilizador**. Autentica uma pessoa que está a utilizar Olá aplicação toointeract com recursos de Media Services. aplicação interativa do Olá deve primeiro solicitar utilizador Olá credenciais do utilizador Olá. Um exemplo é uma aplicação de consola de gestão utilizada pelas tarefas de codificação de toomonitor de utilizadores autorizados ou live transmissão em fluxo. 
- **Autenticação principal de serviço**. Autenticar-se um serviço. As aplicações que utilizam frequentemente este método de autenticação são aplicações que executem serviços de daemon, serviços de camada média ou tarefas agendadas. Os exemplos são as web apps, aplicações de função, as logic apps, API e micro-serviços.

### <a name="user-authentication"></a>Autenticação de utilizador 

As aplicações que devem utilizar o método de autenticação de utilizador Olá são gestão ou de monitorização de aplicações nativas: as aplicações móveis, as aplicações do Windows e aplicações de consola. Este tipo de solução é útil quando pretender que uma interação humana com o serviço de Olá dos Olá os seguintes cenários:

- Dashboard de monitorização para os trabalhos de codificação.
- Dashboard de monitorização para os fluxos em direto.
- Aplicação de gestão de recursos de tooadminister desktop ou mobile utilizadores numa conta de Media Services.

> [!NOTE]
> Este método de autenticação não deve ser utilizado para aplicações direcionadas para o consumidor. 

Uma aplicação nativa tem de primeiro adquirir um token de acesso do Azure AD e, em seguida, utilizá-lo quando fizer a API de REST de serviços de suporte de dados toohello pedidos HTTP. Adicione cabeçalho de pedido de token toohello de acesso de Olá. 

Olá diagrama a seguir mostra um fluxo de autenticação da aplicação interativa típica: 

![Diagrama de aplicações nativas](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

Olá precedente diagrama, Olá números representam o fluxo de Olá de pedidos de Olá por ordem cronológica.

> [!NOTE]
> Quando utilizar o método de autenticação de utilizador Olá, todas as aplicações partilham Olá URI de redirecionamento do mesmo ID de cliente de aplicação nativa (predefinição) e a aplicação nativa. 

1. Solicita credenciais um utilizador.
2. Pedir um token de acesso do Azure AD com Olá os seguintes parâmetros:  

    * Azure AD ponto final de inquilino.

        é possível obter as informações de inquilinos Olá de Olá portal do Azure. Coloque o cursor sobre nome Olá do utilizador com sessão iniciada Olá no canto superior direito Olá.
    * URI do recurso dos Media Services. 

        Este URI é Olá mesmo para contas de serviços de suporte de dados que se encontrem no Olá mesmo ambiente do Azure (por exemplo, https://rest.media.azure.net).

    * ID de cliente de serviços de suporte de dados (nativo) de aplicação.
    * URI de redirecionamento da aplicação de Media Services (nativo).
    * URI para serviços de suporte de dados REST do recurso.
        
        Olá URI representa o ponto final de API de REST Olá (por exemplo, https://test03.restv2.westus.media.azure.net/api/).

    tooget valores para estes parâmetros, consulte [utilizar definições de autenticação do Azure tooaccess portal do Azure AD Olá](media-services-portal-get-started-with-aad.md) utilizando a opção de autenticação de utilizador Olá.

3. o token de acesso de Olá do Azure AD é enviado toohello cliente.
4. cliente de Olá envia um pedido toohello API de REST de suporte de dados do Azure com o token de acesso de Olá do Azure AD.
5. cliente de Olá recebe de volta dados Olá dos serviços de suporte de dados.

Para obter informações sobre como os pedidos de toouse do Azure AD authentication toocommunicate com REST utilizando o SDK do cliente de .NET dos Media Services Olá, consulte [tooaccess de autenticação de utilização do Azure AD Olá API dos serviços de suporte de dados com o .NET](media-services-dotnet-get-started-with-aad.md). 

Se não estiver a utilizar o SDK do cliente de .NET dos Media Services Olá, tem de criar manualmente um pedido de token de acesso do Azure AD através da utilização de parâmetros de Olá descritos no passo 2. Para obter mais informações, consulte [como toouse Olá do Azure AD Authentication Library tooget Olá token do Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Autenticação do principal de serviço

As aplicações que utilizam frequentemente este método de autenticação são as aplicações que executam os serviços de camada média e tarefas agendadas: web apps, aplicações de função, as logic apps, APIs e micro-serviços. Este método de autenticação também é adequado para aplicações interativas na qual poderá toouse um recursos de toomanage da conta de serviço.

Quando utiliza os cenários do consumidor de toobuild do método de autenticação principal do Olá serviço, autenticação, normalmente, é processada na camada de média de Olá (através de alguns API) e não diretamente numa aplicação móvel ou ambiente de trabalho. 

toouse este método, criar uma aplicação do Azure AD e serviço principal no seu próprio inquilino. Depois de criar aplicação Olá, dê Olá aplicação contribuinte ou proprietário função acesso toohello conta dos Media Services. Pode fazer isto numa Olá portal do Azure, utilizando a CLI do Azure, ou com um script do PowerShell. Também pode utilizar uma aplicação do Azure AD existente. Pode registar e gerir a sua aplicação Azure AD e o principal de serviço [no portal do Azure de Olá](media-services-portal-get-started-with-aad.md). Também pode fazer isto utilizando [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) ou [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Aplicações de camada média](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Depois de criar a aplicação do Azure AD, pode obter valores para Olá seguintes definições. Necessitar destes valores para a autenticação:

- ID de cliente 
- Segredo do cliente 

Em Olá precedente figura, Olá números representam fluxo Olá de pedidos de Olá por ordem cronológica:
    
1. Uma aplicação de camada média (web API ou aplicação web) solicita um token de acesso do Azure AD que tenha Olá os seguintes parâmetros:  

    * Azure AD ponto final de inquilino.

        é possível obter as informações de inquilinos Olá de Olá portal do Azure. Coloque o cursor sobre nome Olá do utilizador com sessão iniciada Olá no canto superior direito Olá.
    * URI do recurso dos Media Services. 

        Este URI é Olá mesmo para contas de serviços de suporte de dados que estão localizadas em Olá mesmo ambiente do Azure (por exemplo, https://rest.media.azure.net).

    * URI para serviços de suporte de dados REST do recurso.

        Olá URI representa o ponto final de API de REST Olá (por exemplo, https://test03.restv2.westus.media.azure.net/api/).

    * Os valores de aplicação do Azure AD: Olá ID de cliente e o segredo do cliente.
    
    tooget valores para estes parâmetros, consulte [utilizar definições de autenticação do Azure tooaccess portal do Azure AD Olá](media-services-portal-get-started-with-aad.md) utilizando a opção de autenticação principal de serviço Olá.

2. o token de acesso de Olá do Azure AD é enviado toohello de camada média.
4. camada média Olá envia o pedido toohello API de REST de suporte de dados do Azure com um token do Azure AD Olá.
5. camada média Olá recebe de volta dados Olá dos serviços de suporte de dados.

Para obter mais informações sobre como os pedidos de toouse do Azure AD authentication toocommunicate com REST utilizando o SDK do cliente de .NET dos Media Services Olá, consulte [tooaccess de autenticação de utilização do Azure AD API de serviços de suporte de dados do Azure com o .NET](media-services-dotnet-get-started-with-aad.md). 

Se não estiver a utilizar o SDK do cliente de .NET dos Media Services Olá, tem de criar manualmente um pedido de token do Azure AD através da utilização de parâmetros descritos no passo 1. Para obter mais informações, consulte [como toouse Olá do Azure AD Authentication Library tooget Olá token do Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Resolução de problemas

Exceção: "Olá o servidor remoto devolveu um erro: não autorizado (401)."

Solução: Para Olá REST de serviços de suporte de dados pedido toosucceed, utilizador chamada Olá tem de ser uma função de contribuinte ou proprietário Olá está a tentar tooaccess de conta de Media Services. Para obter mais informações, consulte Olá [controlo de acesso](media-services-use-aad-auth-to-access-ams-api.md#access-control) secção.

## <a name="resources"></a>Recursos

Olá seguintes artigos-se descrições gerais de conceitos de autenticação do Azure AD: 

- [Cenários de autenticação endereçados através do Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Adicionar, atualizar ou remover uma aplicação no Azure AD](../active-directory/develop/active-directory-integrating-applications.md)
- [Configurar e gerir o controlo de acesso baseado em funções utilizando o PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Passos seguintes

* Utilizar o portal do Azure de Olá demasiado[acesso do Azure AD authentication tooconsume API de serviços de suporte de dados do Azure](media-services-portal-get-started-with-aad.md).
* Utilizar a autenticação do Azure AD demasiado[aceder à API de serviços de suporte de dados do Azure com o .NET](media-services-dotnet-get-started-with-aad.md).

