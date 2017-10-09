---
title: aaaHow toocreate APIs na API Management do Azure
description: Saiba como toocreate e configure APIs na API Management do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Como toocreate APIs na API Management do Azure
Uma API na API Management representa um conjunto de operações que podem ser invocados por aplicações cliente. Novas APIs são criadas no portal do publicador Olá e, em seguida, Olá pretendido operações são adicionadas. Assim que forem adicionadas operações Olá, Olá API é adicionada tooa produto e pode ser publicado. Depois de uma API for publicada, pode ser subscrito tooand utilizado pelos programadores.

Este guia mostra o primeiro passo de Olá no processo de Olá: como toocreate e configurar uma nova API na API Management. Para obter mais informações sobre a adição de operações e publicar um produto, consulte [como tooadd operações tooan API] [ How tooadd operations tooan API] e [como toocreate e publicar um produto] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Criar uma nova API
As APIs são criadas e configuradas no portal do publicador Olá. tooaccess Olá clique portal, publicador **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management.

![Portal do publicador][api-management-management-console]

> Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **adicionar API**.

![Criar API][api-management-create-api]

Olá utilize **Adicionar nova API** janela tooconfigure Olá nova API.

![Adicionar nova API][api-management-add-new-api]

Olá seguintes campos é utilizados tooconfigure Olá nova API.

* **Nome da Web API** fornece um nome único e descritivo para Olá API. Será apresentado em portais de programador e o publicador Olá.
* **URL do serviço Web** referências Olá implementar Olá API de serviço HTTP. API de gestão reencaminha pedidos toothis endereço.
* **Sufixo do URL da API Web** é anexado toohello URL base do serviço de gestão de Olá API. URL de base de Olá é comum para todos os APIs alojadas por uma instância de serviço de API Management. Gestão de API distingue APIs pelo respetivo sufixo e, por conseguinte, o sufixo de Olá tem de ser exclusivo para cada API para um determinado publicador.
* **Esquema de URL de API Web** determina quais protocolos podem ser utilizados tooaccess Olá API. HTTPs é especificado por predefinição.
* toooptionally adicionar este novo tooa produto da API, clique em Olá **produtos (opcionais)** pendente e escolha um produto. Este passo pode ser repetida múltiplas vezes tooadd Olá API toomultiple produtos.

Depois de Olá pretendido valores estão configurados, clique em **guardar**. Assim que for criado Olá nova API, hello página de resumo para a API de Olá é apresentada no portal do publicador Olá.

![Resumo da API][api-management-api-summary]

## <a name="configure-api-settings"></a>As definições da API de configurar
Pode utilizar Olá **definições** separador tooverify e editar Olá configuração de uma API. **Nome da Web API**, **URL do serviço Web**, e **sufixo do URL da API Web** são inicialmente definido quando Olá API é criado e pode ser modificado aqui. **Descrição** fornece uma descrição opcional e **esquema de URL de API Web** determina quais protocolos podem ser utilizados tooaccess Olá API.

![Definições da API][api-management-api-settings]

autenticação de gateway tooconfigure por hello back-end do serviço implementar Olá API, selecione Olá **segurança** Olá separador **com credenciais** pendente pode ser utilizado tooconfigure **HTTP básico** ou **certificados de cliente** autenticação. autenticação básica toouse HTTP, basta introduzir credenciais de Olá assim o desejar. Para obter informações sobre como utilizar a autenticação de certificado de cliente, consulte [como serviços de back-end toosecure utilizando o cliente de certificado de autenticação na API Management do Azure][How toosecure back-end services using client certificate authentication in Azure API Management].

Olá **segurança** separador também pode ser utilizado tooconfigure **autorização do utilizador** utilizando OAuth 2.0. Para obter mais informações, consulte [como programador tooauthorize contas com OAuth 2.0 na API Management do Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Definições de autenticação básica][api-management-api-settings-credentials]

Clique em **guardar** toosave quaisquer alterações que efetuar toohello as definições da API.

## <a name="next-steps"> </a>Passos seguintes
Assim que é criada uma API e definições de Olá configuradas, passos Olá são tooadd Olá operações toohello API, adicionar Olá API tooa produto e publicá-lo para que fique disponível para programadores. Para obter mais informações, consulte Olá seguintes artigos.

* [Como tooadd operações tooan API][How tooadd operations tooan API]
* [Como toocreate e publicar um produto][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
