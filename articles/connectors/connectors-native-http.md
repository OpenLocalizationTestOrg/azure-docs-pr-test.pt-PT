---
title: "aaaCommunicate com qualquer ponto final através de HTTP - Azure Logic Apps | Microsoft Docs"
description: "Criar as logic apps que podem comunicar com qualquer ponto final através de HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>Introdução ao hello ação de HTTP

Com a ação de HTTP Olá, pode expandir fluxos de trabalho para a sua organização e comunicar o ponto final de tooany através de HTTP.

Pode:

* Crie lógica fluxos de trabalho da aplicação que ativar (acionador) quando um site que gere fica inativo.
* Comunicar tooany endpoint através de HTTP tooextend os fluxos de trabalho noutros serviços.

tooget iniciado utilizando a ação de Olá HTTP numa aplicação lógica, consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Utilize o trigger de Olá HTTP
Um acionador é um evento que pode ser o fluxo de trabalho do toostart utilizados Olá que está definido uma aplicação lógica. [Saiba mais sobre acionadores](connectors-overview.md).

Eis um exemplo de sequência de como tooset segurança Olá HTTP acionar no Olá Designer de aplicação lógica.

1. Adicione o acionador HTTP Olá na sua aplicação lógica.
2. Preencha os parâmetros de Olá para o ponto final de Olá HTTP que pretende que o toopoll.
3. Modificar o intervalo de periodicidade Olá na frequência deve consultar.

   aplicação de lógica de Olá agora desencadeado com qualquer conteúdo que é devolvido durante a verificação de cada.

   ![Acionador HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Como funciona o acionador HTTP Olá

acionador HTTP Olá envia um ponto final da chamada tooHTTP num intervalo periódico. Por predefinição, os códigos de resposta HTTP são inferior a 300 faz com que um toorun de aplicação lógica. toospecify se a aplicação de lógica de Olá deve acionados, pode editar a aplicação de lógica de Olá na vista de código e adicionar uma condição que avalia após Olá chamada HTTP. Eis um exemplo de um acionador HTTP que é acionado quando Olá devolveu o código de estado é maior que ou igual a demasiado`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Detalhes completos sobre os parâmetros de Acionador de Olá HTTP estão disponíveis no [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Utilize a ação de Olá HTTP

Uma ação é uma operação que é efetuada pelo fluxo de trabalho de Olá que está definido uma aplicação lógica. 
[Saiba mais sobre as ações](connectors-overview.md).

1. Escolha **novo passo** > **adicionar uma ação**.
3. Na caixa de pesquisa de ação de Olá, escreva **http** ações de Olá HTTP toolist.
   
    ![Selecione a ação de Olá HTTP](./media/connectors-native-http/using-action-1.png)

4. Adicione os parâmetros necessários para a chamada de Olá HTTP.
   
    ![Olá concluída a ação de HTTP](./media/connectors-native-http/using-action-2.png)

5. Na barra de ferramentas estruturador de Olá, clique em **guardar**. A aplicação lógica é guardada e publicada (ativada) em Olá mesmo tempo.

## <a name="http-trigger"></a>Acionador HTTP
Seguem-se detalhes Olá para o acionador de Olá que suporte este conector. conector HTTP Olá tem um acionador.

| Acionador | Descrição |
| --- | --- |
| HTTP |Faz uma chamada HTTP e devolve o conteúdo da resposta Olá. |

## <a name="http-action"></a>Ação de HTTP
Seguem-se detalhes Olá para a ação de Olá que suporte este conector. conector HTTP Olá tem uma ação possíveis.

| Ação | Descrição |
| --- | --- |
| HTTP |Faz uma chamada HTTP e devolve o conteúdo da resposta Olá. |

## <a name="http-details"></a>Detalhes HTTP
Olá tabelas seguintes descrevem Olá necessários e opcionais campos de entrada para a ação de Olá e detalhes saída correspondente Olá associadas através da ação de Olá.

#### <a name="http-request"></a>Pedido de HTTP
Olá seguem-se os campos de entrada para a ação de Olá, o que faz um pedido de saída de HTTP.
A * significa que é um campo obrigatório.

| Nome a apresentar | Nome da propriedade | Descrição |
| --- | --- | --- |
| Método * |Método |Olá HTTP verbo toouse |
| URI * |URI |Olá URI de pedido de Olá HTTP |
| Cabeçalhos |Cabeçalhos |Um objeto JSON de tooinclude de cabeçalhos HTTP |
| Corpo |Corpo |Olá corpo do pedido HTTP |
| Autenticação |Autenticação |Os detalhes na Olá [autenticação](#authentication) secção |

<br>

#### <a name="output-details"></a>Detalhes de saída
Olá seguem-se detalhes de saída para Olá resposta de HTTP.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Cabeçalhos |objeto |Cabeçalhos de resposta |
| Corpo |objeto |Objeto de resposta |
| Código de estado |Int |Código de estado HTTP |

## <a name="authentication"></a>Autenticação
funcionalidade de Logic Apps Olá permite-lhe toouse diferentes tipos de autenticação nos pontos finais HTTP. Pode utilizar esta autenticação com Olá **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, e  **[HTTP Webhook](connectors-native-webhook.md)**  conectores. Olá, os seguintes tipos de autenticação é configurável:

* [Autenticação básica](#basic-authentication)
* [Autenticação de certificado de cliente](#client-certificate-authentication)
* [Autenticação do Azure Active Directory (Azure AD) OAuth](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Autenticação básica

Olá seguinte objeto de autenticação é necessária para a autenticação básica.
A * significa que é um campo obrigatório.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Tipo * |tipo |Tipo de autenticação (tem de ser `Basic` para a autenticação básica) |
| Nome de utilizador * |o nome de utilizador |Tooauthenticate de nome de utilizador |
| Palavra-passe * |palavra-passe |Palavra-passe tooauthenticate |

> [!TIP]
> Se pretender toouse uma palavra-passe não pode ser obtida a partir da definição de Olá, utilize um `securestring` parâmetro e Olá `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).

Por exemplo:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Autenticação de certificados de cliente

Olá seguinte objeto de autenticação é necessário para autenticação de certificados de cliente. A * significa que é um campo obrigatório.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Tipo * |tipo |Olá, tipo de autenticação (tem de ser `ClientCertificate` para certificados de cliente SSL) |
| PFX * |PFX |Olá com codificação Base64 conteúdo Olá Personal Information (Exchange PFX) ficheiro |
| Palavra-passe * |palavra-passe |Olá palavra-passe tooaccess Olá ficheiro PFX |

> [!TIP]
> um parâmetro que não seja legível na definição de Olá depois de guardar a aplicação de lógica de Olá toouse, pode utilizar um `securestring` parâmetro e Olá `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).

Por exemplo:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Autenticação do Azure AD OAuth
Olá seguinte objeto de autenticação é necessário para autenticação do Azure AD OAuth. A * significa que é um campo obrigatório.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Tipo * |tipo |Olá, tipo de autenticação (tem de ser `ActiveDirectoryOAuth` para o Azure AD OAuth) |
| Inquilino * |Inquilino |Olá identificador de inquilino para o inquilino Olá do Azure AD |
| Público-alvo * |público-alvo |recurso de Olá que está a pedir toouse de autorização. Por exemplo: `https://management.core.windows.net/` |
| Cliente ID * |ID de cliente |Olá identificador de cliente para a aplicação Olá do Azure AD |
| Segredo * |segredo |segredo Olá hello do cliente de que está a solicitar o token de Olá |

> [!TIP]
> Pode utilizar um `securestring` parâmetro e Olá `@parameters()` [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs) toouse um parâmetro que não seja legível na definição de Olá depois de guardar.
> 
> 

Por exemplo:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Passos seguintes
Agora, experimente a plataforma de Olá e [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md). Pode explorar Olá outros conectores disponíveis em Logic Apps observando nosso [lista APIs](apis-list.md).

