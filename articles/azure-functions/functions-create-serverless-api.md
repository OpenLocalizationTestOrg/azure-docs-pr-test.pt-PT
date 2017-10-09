---
title: "aaaCreate uma API sem servidor através das funções do Azure | Microsoft Docs"
description: "Como toocreate uma API sem servidor através das funções do Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Criar uma API sem servidor através das funções do Azure

Neste tutorial, ficará a saber como as funções do Azure permite-lhe toobuild APIs altamente dimensionável. As funções do Azure é fornecido com uma coleção de incorporada HTTP acionadores e enlaces que tornam mais fácil tooauthor um ponto final numa variedade de idiomas, incluindo o Node.JS, c# e muito mais. Neste tutorial, irá personalizar um HTTP acionador toohandle as ações específicas na sua conceção de API. Também irá preparar para a crescer a sua API, como o integrar com Proxies de funções do Azure e como configurar mock APIs. Tudo isto é conseguido por cima Olá funções sem servidor ambiente de computação, pelo que não tem tooworry sobre dimensionamento recursos - apenas poder concentrar na sua lógica de API.

## <a name="prerequisites"></a>Pré-requisitos 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

função resultante Olá será utilizada para o resto Olá deste tutorial.

### <a name="sign-in-tooazure"></a>Inicie sessão no tooAzure

Abra Olá portal do Azure. toodo, inicie sessão no demasiado[https://portal.azure.com](https://portal.azure.com) com a sua conta do Azure.

## <a name="customize-your-http-function"></a>Personalizar a sua função HTTP

Por predefinição, a função de acionada por HTTP é configurado tooaccept qualquer método HTTP. Também é um URL predefinido do formulário Olá `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Se seguiu o guia de introdução Olá, em seguida, `<funcname>` provavelmente aspeto semelhante ao seguinte "HttpTriggerJS1". Nesta secção, irá modificar pedidos de tooGET apenas do Olá função toorespond contra `/api/hello` encaminhar em vez disso. 

Navegue tooyour função no Olá portal do Azure. Selecione **integrar** no Olá deixado navegação.

![Personalizar uma função HTTP](./media/functions-create-serverless-api/customizing-http.png)

Utilize as definições de Acionador HTTP especificado na tabela de Olá.

| Campo | Valor da amostra | Descrição |
|---|---|---|
| Métodos de HTTP permitidos | Métodos selecionados | Determinar que métodos HTTP podem ser utilizado tooinvoke esta função |
| Métodos de HTTP selecionados | INTRODUÇÃO | Permite que apenas toobe de métodos HTTP selecionado utilizado tooinvoke esta função |
| Modelo de rota | /Hello | Determina a rota de que é utilizado tooinvoke esta função |

Tenha em atenção que não incluiu Olá `/api` base prefixo de caminho no modelo de rota Olá, como isto é processado por uma definição global.

Clique em **Guardar**.

Pode saber mais sobre como personalizar funções HTTP no [enlaces HTTP de funções do Azure e webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>A API de teste

Em seguida, teste a função toosee-lo a trabalhar com a superfície de API novo Olá.

Navegue página de desenvolvimento de back-toohello ao clicar no nome da função de Olá no Olá deixado navegação.

Clique em **obter URL de função** e copie o URL de Olá. Deverá ver que utiliza Olá `/api/hello` encaminhar agora.

Copie o URL de Olá para um novo separador do browser ou o cliente REST preferencial. Browsers utilizará GET por predefinição.

Execute a função Olá e confirme que está a funcionar. Poderá ter o parâmetro de "name" tooprovide Olá como um código de início rápido Olá de toosatisfy de cadeia de consulta.

Também pode tentar chamar Olá ponto final com outro tooconfirm de método HTTP que função Olá não foi executada. Para tal, terá de toouse um cliente REST, tais como cURL, Postman ou Fiddler.

## <a name="proxies-overview"></a>Descrição geral de proxies

Na secção seguinte, Olá, será de superfície da API através de um proxy. Proxies de funções do Azure é uma funcionalidade de pré-visualização permite-lhe tooforward pedidos tooother recursos. Definir um ponto final de HTTP tal como com o acionador de HTTP, mas em vez de escrever código tooexecute quando esse ponto final é chamado, terá de fornecer uma implementação de remota tooa URL. Isto permite-lhe toocompose API várias origens para uma único superfície de API que é mais fácil para os clientes tooconsume. Isto é particularmente útil se quiser toobuild a API como micro-serviços.

Um ponto proxy de pode tooany HTTP recursos, tais como:
- Funções do Azure 
- API apps no [App Service do Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Os contentores de docker no [do serviço de aplicações no Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Quaisquer outro API alojada

Consulte toolearn mais informações sobre proxies [trabalhar com os Proxies de funções do Azure (pré-visualização)].

## <a name="create-your-first-proxy"></a>Criar o primeiro proxy

Nesta secção, irá criar um novo proxy que funciona como um front-end tooyour API geral. 

### <a name="setting-up-hello-frontend-environment"></a>Configurar o ambiente de front-end Olá

Repita os passos de Olá demasiado[criar uma aplicação de função](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate uma nova aplicação de função na qual irá criar o proxy. Esta nova aplicação irá servir como front-end de Olá para a nossa API e aplicação de função Olá que foram anteriormente editar irá servir como um back-end.

Navegue tooyour nova front-end aplicação de função no portal de Olá.

Selecione **definições**. Em seguida, ative **ativar Proxies de funções do Azure (pré-visualização)** demasiado "em".

Selecione **definições plataforma** e escolha **definições da aplicação**.

Desloque para baixo demasiado**as definições de aplicação** e criar uma nova definição com a chave "HELLO_HOST". Definir o respetivo anfitrião toohello do valor da sua aplicação de função de back-end, tal como `<YourApp>.azurewebsites.net`. Esta é a parte do URL de Olá que copiou anteriormente ao testar a sua função HTTP. Irá referenciar esta definição na configuração de Olá mais tarde.

> [!NOTE] 
> As definições de aplicação são recomendadas para tooprevent de configuração de anfitrião Olá uma dependência de ambiente hard-coded para proxy de Olá. Utilizar as definições de aplicação significa que pode mover a configuração de proxy Olá entre ambientes e definições de aplicação específico do ambiente de Olá serão aplicadas.

Clique em **Guardar**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Criar um proxy no front-end de Olá

Navegue até a aplicação de função de front-end de back-tooyour no portal de Olá.

No painel navegação esquerda Olá, clique Olá juntamente com o início de sessão seguinte '+' demasiado "Proxies (pré-visualização)".

![Criar um proxy](./media/functions-create-serverless-api/creating-proxy.png)

Utilize as definições de proxy conforme especificado na tabela de Olá.

| Campo | Valor da amostra | Descrição |
|---|---|---|
| Nome | HelloProxy | Um nome amigável utilizado apenas para gestão |
| Modelo de rota | Olá/api / | Determina a rota de que é utilizado tooinvoke este proxy |
| URL de back-end | https://%HELLO_HOST%/API/Hello | Especifica o pedido de Olá Olá ponto final toowhich deve ser efetuado |

Tenha em atenção que Proxies fornecem Olá `/api` prefixo do caminho de base e este deve ser incluído no modelo de rota Olá.

Olá `%HELLO_HOST%` sintaxe fará referência a definição de aplicação Olá que criou anteriormente. Olá resolvido que URL irá apontar função original tooyour.

Clique em **Criar**.

Pode experimentar o seu novo proxy ao copiar Olá URL de Proxy e testá-lo no browser Olá ou com o cliente HTTP favorito.

## <a name="create-a-mock-api"></a>Criar uma API mock

Em seguida, irá utilizar um proxy toocreate uma API mock para a sua solução. Isto permite que o desenvolvimento de cliente tooprogress, sem necessitar de back-end de Olá totalmente implementado. Mais tarde no desenvolvimento, pode criar uma nova aplicação de função que suporte esta lógica e redirecionar o tooit de proxy.

toocreate mock esta API, vamos criar um novo proxy, desta vez utilizando o Olá [Editor do serviço de aplicações](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget iniciado, navegue tooyour a aplicação de função no portal de Olá. Selecione **funcionalidades da plataforma** e localizar **Editor do serviço de aplicações**. Clicar em Isto abrirá Olá Editor do serviço de aplicações num novo separador.

Selecione `proxies.json` no Olá deixado navegação. Este é o ficheiro de Olá que armazena a configuração de Olá para todos os seus proxies. Se utilizar um dos Olá [funciona métodos de implementação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), este é o ficheiro Olá irão manter o controlo de origem. toolearn mais informações sobre este ficheiro, consulte [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Se tiver seguido até ao momento, o proxies.json deve aspeto Olá seguinte:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Em seguida irá adicionar a API mock. Substitua o ficheiro proxies.json seguinte Olá:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Esta ação adiciona um novo proxy, "GetUserByName", sem a propriedade de backendUri Olá. Em vez de chamar outro recurso, modifica a resposta de predefinição Olá de Proxies utilizando uma substituição de resposta. Substituições de pedido e resposta também podem ser utilizadas em conjunto com um URL de back-end. Isto é particularmente útil quando a funcionalidade de proxy tooa legado sistema, onde poderá ser necessário toomodify cabeçalhos, parâmetros de consulta, etc. toolearn mais sobre o pedido e resposta substituições, consulte [modificar pedidos e respostas no Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Testar a sua API mock ao chamar Olá `/api/users/{username}` ponto final utilizando um browser ou o cliente REST favorito. Ser tooreplace se _{username}_ com um valor de cadeia representando um nome de utilizador.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, aprendeu como toobuild e personalizar uma API das funções do Azure. Também aprendeu como toobring várias APIs, incluindo mocks, em conjunto como uma superfície de API unificada. Pode utilizar estes toobuild técnicas os APIs de qualquer complexidade, todos os durante a execução em Olá sem servidor computação modelo forneceu as funções do Azure.

Olá referências seguintes podem ser útil como desenvolver ainda mais a API:

- [Enlaces de funções de HTTP e webhook do Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [trabalhar com os Proxies de funções do Azure (pré-visualização)]
- [Documentar uma API de funções do Azure (pré-visualização)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[trabalhar com os Proxies de funções do Azure (pré-visualização)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
