---
title: "aaaWork com os proxies de funções do Azure | Microsoft Docs"
description: "Descrição geral de como toouse Proxies de funções do Azure"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Trabalhar com os Proxies de funções do Azure (pré-visualização)

> [!NOTE] 
> Proxies de funções do Azure está atualmente em pré-visualização. É gratuito enquanto na pré-visualização, mas funções padrão faturação aplica-se tooproxy execuções. Para obter mais informações, consulte [preços de funções do Azure](https://azure.microsoft.com/pricing/details/functions/).

Este artigo explica como tooconfigure e funcionam com os Proxies de funções do Azure. Com esta funcionalidade, pode especificar pontos finais na sua aplicação de função que são implementados por outro recurso. Pode utilizar estes toobreak proxies uma API de grandes dimensões em várias aplicações de função (como uma arquitetura de microsserviço), enquanto ainda apresentar uma único superfície de API para os clientes.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Ativar as funções do Azure Proxies

Proxies não estão ativadas por predefinição. Pode criar proxies enquanto Olá funcionalidade está desativada, mas não executará. tooenable proxies Olá seguintes:

1. Abra Olá [portal do Azure], e, em seguida, aceda a aplicação de função tooyour.
2. Selecione **as definições de aplicação de função**.
3. Comutador **ativar Proxies de funções do Azure (pré-visualização)** demasiado**no**.

Também pode regressar aqui o tempo de execução do tooupdate Olá proxy à novas funcionalidades ficam disponíveis.


## <a name="create"></a>Criar um proxy

Esta secção mostra como toocreate um proxy em Olá portal das funções.

1. Abra Olá [portal do Azure], e, em seguida, aceda a aplicação de função tooyour.
2. No painel esquerdo Olá, selecione **novo proxy**.
3. Forneça um nome para o proxy.
4. Configurar o ponto final de Olá que é exposto nesta aplicação de função especificando Olá **modelo de rota** e **métodos de HTTP**. Estes parâmetros comportar-se de acordo com as regras de toohello para [HTTP acionadores].
5. Conjunto Olá **URL back-end** tooanother endpoint. Este ponto final pode ser uma função na outra aplicação de função, ou pode ser qualquer outra API. Olá valor não necessita de toobe estática e pode fazer referência a [definições da aplicação] e [parâmetros do pedido de cliente original Olá].
6. Clique em **Criar**.

O proxy agora existe como um novo ponto final na sua aplicação de função. A partir de uma perspetiva do cliente, é equivalente tooan HttpTrigger nas funções do Azure. Pode experimentar o seu novo proxy ao copiar Olá URL de Proxy e testá-lo com o cliente HTTP favorito.

## <a name="modify-requests-responses"></a>Modificar pedidos e respostas

Com os Proxies de funções do Azure, pode modificar pedidos tooand respostas de back-end Olá. Estes transformações podem utilizar variáveis, tal como definido no [utilizar variáveis].

### <a name="modify-backend-request"></a>Modificar o pedido de back-end Olá

Por predefinição, o pedido de back-end Olá é inicializado como uma cópia do pedido original Olá. Além disso toosetting Olá back-end URL, pode efetuar alterações toohello HTTP, cabeçalhos sendo que os parâmetros de cadeia de consulta. Olá modificados valores podem referenciar [definições da aplicação] e [parâmetros do pedido de cliente original Olá].

Atualmente, não há nenhum experiência do portal para modificar pedidos de back-end. toolearn como tooapply esta capacidade de proxies.json, consulte o artigo [definir um objeto de requestOverrides].

### <a name="modify-response"></a>Modificar a resposta Olá

Por predefinição, a resposta do cliente Olá foi inicializada como uma cópia da resposta de back-end Olá. Pode efetuar o código de estado de resposta de toohello a alterações, frase de razão, os cabeçalhos e corpo. Olá modificados valores podem referenciar [definições da aplicação], [parâmetros do pedido de cliente original Olá], e [parâmetros da resposta de back-end Olá].

Atualmente, não há nenhum experiência do portal para modificar as respostas. toolearn como tooapply esta capacidade de proxies.json, consulte o artigo [definir um objeto de responseOverrides].

## <a name="using-variables"></a>Utilizar variáveis

configuração de Olá para um proxy não precisa de toobe estático. Pode condição-toouse variáveis do pedido original Olá, resposta de back-end Olá ou as definições da aplicação.

### <a name="request-parameters"></a>Parâmetros do pedido de referência

Pode utilizar os parâmetros do pedido como entradas de propriedade de URL de back-end toohello ou como parte de modificar os pedidos e respostas. Alguns parâmetros podem estar vinculados a partir do modelo de rota Olá especificado na configuração de base proxy Olá e outros utilizadores podem ter a partir das propriedades de pedido de entrada Olá.

#### <a name="route-template-parameters"></a>Parâmetros do modelo de rota
Os parâmetros que são utilizados no modelo de rota Olá se toobe disponível referenciada por nome. os nomes dos parâmetros de Olá são colocados entre chavetas ({}).

Por exemplo, se um proxy, tem um modelo de rota, tal como `/pets/{petId}`, Olá URL de back-end pode incluir valor Olá `{petId}`, como no `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Se o modelo de rota Olá termina num caráter universal, tais como `/api/{*restOfPath}`, Olá valor `{restOfPath}` é uma representação de cadeia de Olá restantes segmentos de caminho do pedido de entrada Olá.

#### <a name="additional-request-parameters"></a>Parâmetros do pedido adicionais
Além disso toohello encaminhar os parâmetros do modelo, Olá os seguintes valores pode ser utilizado em valores de configuração:

* **{request.method}** : Olá método HTTP que é utilizado no pedido original Olá.
* **{request.headers. \<HeaderName\>}**: um cabeçalho que pode ser lidos na pedido original Olá. Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá que pretende que o tooread. Se o cabeçalho de Olá não está incluído no pedido de Olá, o valor de Olá será uma cadeia vazia Olá.
* **{request.querystring. \<ParameterName\>}**: um parâmetro de cadeia de consulta que pode ser lidos na pedido original Olá. Substitua  *\<ParameterName\>*  com o nome de Olá do parâmetro de Olá que pretende que o tooread. Se o parâmetro de Olá não está incluído no pedido de Olá, o valor de Olá será uma cadeia vazia Olá.

### <a name="response-parameters"></a>Parâmetros de resposta de back-end de referência

Parâmetros de resposta podem ser utilizados como parte de modificação de cliente de toohello Olá resposta. Olá, os seguintes valores pode ser utilizado valores de configuração:

* **{backend.response.statusCode}** : Olá código de estado HTTP que é devolvido numa resposta de back-end Olá.
* **{backend.response.statusReason}** : frase de razão Olá HTTP, que é devolvido numa resposta de back-end Olá.
* **{backend.response.headers. \<HeaderName\>}**: um cabeçalho que pode ser lidos na resposta do Olá back-end. Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá pretende tooread. Se o cabeçalho de Olá não está incluído no pedido de Olá, o valor de Olá será uma cadeia vazia Olá.

### <a name="use-appsettings"></a>Definições da aplicação de referência

Também pode referenciar [definições da aplicação definidas para a aplicação de função Olá](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) por envolvente nome da definição Olá com sinais de percentagem (%).

Por exemplo, um URL de back-end de *https://%ORDER_PROCESSING_HOST%/api/orders* teria aos "% ORDER_PROCESSING_HOST %" substituída pelo valor Olá da definição de ORDER_PROCESSING_HOST Olá.

> [!TIP] 
> Utilize as definições da aplicação para os anfitriões de back-end, se tiver múltiplas implementações ou ambientes de teste. Dessa forma, pode certificar-se que sempre estamos a falar toohello direito novamente terminar nesse ambiente.

## <a name="advanced-configuration"></a>Configuração avançada

proxies de Olá configuradas por si são armazenados num ficheiro proxies.json, que está localizado na raiz de Olá de um diretório de aplicação de função. Pode editar este ficheiro manualmente e implementá-lo como parte da sua aplicação quando utilizar qualquer um dos Olá [métodos de implementação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) que suporta as funções. funcionalidade de Olá tem de ser [ativada](#enable) para Olá ficheiro toobe processado. 

> [!TIP] 
> Se não configurou um dos métodos de implementação de Olá, também pode trabalhar com o ficheiro de proxies.json Olá no portal de Olá. Aplicação de função tooyour aceda, selecione **funcionalidades da plataforma**e, em seguida, selecione **Editor do serviço de aplicações**. Ao fazê-lo, pode ver a estrutura de Olá de ficheiro completo da sua aplicação de função e, em seguida, efetuar alterações.

Proxies.JSON é definido por um objeto de proxies, que é composto por proxies com nome e as respetivas definições. Opcionalmente, se o seu editor de o suportar, pode referenciar um [esquema JSON](http://json.schemastore.org/proxies) para conclusão de código. Um ficheiro de exemplo aspeto que poderá ter Olá seguinte:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Cada proxy tem um nome amigável, tais como *proxy1* no Olá anterior exemplo. objeto de definição de proxy Olá correspondente é definido pela Olá seguintes propriedades:

* **matchCondition**: necessário – um objeto definir pedidos de Olá acionam a execução de Olá deste proxy. Contém duas propriedades que são partilhadas com [HTTP acionadores]:
    * _métodos_: uma matriz de métodos de Olá HTTP Olá proxy responde a. Se não for especificado, o proxy de Olá responde tooall métodos de HTTP na rota Olá.
    * _rota_: necessário – define o modelo de rota Olá, controlar qual pedido URLs o proxy responde a. Ao contrário no acionadores HTTP, não há nenhum valor predefinido.
* **backendUri**: Olá URL do pedido de Olá Olá recursos de back-end toowhich deve ser efetuado. Este valor pode referenciar as definições da aplicação e os parâmetros do pedido de cliente Olá original. Se esta propriedade não for incluída, as funções do Azure responde com uma HTTP 200 OK.
* **requestOverrides**: um objeto que define o pedido de back-end de toohello transformações. Consulte [definir um objeto de requestOverrides].
* **responseOverrides**: um objeto que define a resposta de cliente de toohello transformações. Consulte [definir um objeto de responseOverrides].

> [!NOTE] 
> propriedade de rota Olá Proxies de funções do Azure não honrar a propriedade de routePrefix Olá da configuração do anfitrião Olá funções. Se quiser tooinclude um prefixo como /api, tem de ser incluído na propriedade de rota Olá.

### <a name="requestOverrides"></a>Definir um objeto de requestOverrides

objeto de requestOverrides Olá define as alterações efetuadas toohello pedido quando recursos de back-end Olá é chamado. objeto de Olá é definido pela Olá seguintes propriedades:

* **backend.Request.Method**: Olá método HTTP que foi utilizado toocall Olá de back-end.
* **backend.Request.QueryString. \<ParameterName\>**: um parâmetro de cadeia de consulta que pode ser definido para Olá chamada toohello de back-end. Substitua  *\<ParameterName\>*  com o nome de Olá do parâmetro de Olá que pretende que o tooset. Se for fornecida uma cadeia vazia Olá parâmetro Olá não está incluído no pedido de back-end Olá.
* **backend.Request.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para Olá chamada toohello de back-end. Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá que pretende que o tooset. Se fornecer uma cadeia vazia Olá, cabeçalho Olá não está incluído no pedido de back-end Olá.

Valores podem referenciar as definições da aplicação e os parâmetros do pedido de cliente Olá original.

Um exemplo de configuração aspeto que poderá ter Olá seguinte:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>Definir um objeto de responseOverrides

objeto de requestOverrides Olá define as alterações efetuadas toohello resposta que passou toohello back-cliente. objeto de Olá é definido pela Olá seguintes propriedades:

* **response.statusCode**: toobe de código de estado de Olá HTTP devolvido toohello cliente.
* **response.statusReason**: toobe de frase de razão Olá HTTP devolvido toohello cliente.
* **Response.body**: representação de cadeia Olá de Olá corpo toobe devolvido toohello cliente.
* **Response.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para o cliente de toohello Olá resposta. Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá que pretende que o tooset. Se fornecer uma cadeia vazia Olá, o cabeçalho de Olá não está incluído na resposta Olá.

Valores podem referenciar as definições da aplicação, parâmetros do pedido de cliente original Olá e os parâmetros da resposta de back-end Olá.

Um exemplo de configuração aspeto que poderá ter Olá seguinte:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> Neste exemplo, corpo Olá está a ser definido diretamente, por isso, não `backendUri` propriedade é necessária. exemplo de Olá mostra como pode utilizar os Proxies de funções do Azure para mocking APIs.

[portal do Azure]: https://portal.azure.com
[HTTP acionadores]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definir um objeto de requestOverrides]: #requestOverrides
[definir um objeto de responseOverrides]: #responseOverrides
[definições da aplicação]: #use-appsettings
[utilizar variáveis]: #using-variables
[parâmetros do pedido de cliente original Olá]: #request-parameters
[parâmetros da resposta de back-end Olá]: #response-parameters
