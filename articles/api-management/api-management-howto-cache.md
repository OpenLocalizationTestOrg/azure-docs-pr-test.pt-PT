---
title: "aaaAdd colocação em cache tooimprove desempenho na API Management do Azure | Microsoft Docs"
description: "Saiba como carregar a latência de Olá tooimprove, o consumo de largura de banda e o serviço web para chamadas de serviço de API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Adicionar a colocação em cache tooimprove desempenho na API Management do Azure
É possível configurar as operações da API Management para colocar as respostas em cache. A colocação de respostas em cache pode reduzir significativamente a latência da API, o consumo de largura de banda e a carga do serviço Web para os dados que não são alterados com frequência.

Este guia mostra como resposta tooadd colocação em cache para a API e configurar políticas para as operações de API eco de exemplo de Olá. Em seguida, pode chamar a operação a Olá de Olá programador portal tooverify em cache em ação.

> [!NOTE]
> Para obter informações sobre a colocação em cache de itens por chave utilizando expressões de política, consulte [Colocação em cache personalizada na API Management do Azure](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Passos seguinte Olá neste guia, tem de ter uma instância de serviço de API Management com uma API e um produto configurado. Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.

## <a name="configure-caching"> </a>Configurar uma operação para colocação em cache
Neste passo, irá rever Olá colocação em cache as definições de Olá **recurso GET (em cache)** operação de exemplo de Olá API eco.

> [!NOTE]
> Cada instância de serviço de API Management está pré-configurada com uma API eco que pode ser utilizado tooexperiment com e saber mais sobre a API Management. Para obter mais informações, consulte [Introdução à Gestão de API do Azure][Get started with Azure API Management].
> 
> 

tooget iniciado, clique em **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management. Isto leva-o portal do publicador da API Management toohello.

![Portal do publicador][api-management-management-console]

Clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **API eco**.

![API Eco][api-management-echo-api]

Clique em Olá **operações** separador e, em seguida, clique em Olá **recurso GET (em cache)** operação a partir da Olá **operações** lista.

![Operações da API Eco][api-management-echo-api-operations]

Clique em Olá **colocação em cache** Olá tooview de separador colocação em cache as definições para esta operação.

![Separador Colocação em cache][api-management-caching-tab]

tooenable colocação em cache para uma operação, selecione de Olá **ativar** caixa de verificação. Neste exemplo, a colocação em cache está ativada.

Cada resposta da operação é codificada, com base nos valores de Olá no Olá **variação por parâmetros de cadeia de consulta** e **variação por cabeçalhos** campos. Se quiser toocache várias respostas com base nos parâmetros de cadeia de consulta ou nos cabeçalhos, pode configurá-las nestes dois campos.

**Duração** Especifica o intervalo de expiração de Olá das respostas hello em cache. Neste exemplo, o intervalo de Olá é **3600** segundos, que é equivalente tooone hora.

Utilizar a colocação em cache de configuração neste exemplo de Olá, Olá primeiro pedido toohello **recurso GET (em cache)** operação devolve uma resposta do serviço de back-end Olá. Esta resposta serão colocadas em cache, codificada por Olá especificado parâmetros de cadeia de consulta e de cabeçalhos. As chamadas subsequentes operação toohello, com correspondentes aos parâmetros, terá de Olá colocadas em cache resposta devolvida, até que o intervalo de duração da cache Olá expirou.

## <a name="caching-policies"></a>Olá de rever as políticas de colocação em cache
Neste passo, consulte Olá colocação em cache as definições de Olá **recurso GET (em cache)** operação de exemplo de Olá API eco.

Quando as definições de colocação em cache são configuradas para uma operação no Olá **colocação em cache** separador colocação em cache as políticas são adicionadas para a operação de Olá. Estas políticas podem ser visualizadas e editá-lo no editor de políticas de Olá.

Clique em **políticas** de Olá **API Management** menu Olá esquerda e, em seguida, selecione **API eco / recurso (em cache) GET** de Olá **operação**na lista pendente.

![Operação de âmbito da política][api-management-operation-dropdown]

Esta ação apresenta as políticas de Olá para esta operação no editor de políticas de Olá.

![Editor de políticas da API Management][api-management-policy-editor]

definição de política de Olá para esta operação inclui Olá as políticas que definem Olá configuração de colocação em cache que foram revistas utilizando Olá **colocação em cache** separador no passo anterior Olá.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Toohello as alterações efetuadas políticas no editor de políticas de Olá a colocação em cache será refletido na Olá **colocação em cache** separador de uma operação e vice-versa.
> 
> 

## <a name="test-operation"></a>Chamar uma operação e testar Olá colocação em cache
Olá toosee colocação em cache em ação, podemos chamar a operação de Olá partir do portal de programador Olá. Clique em **portal do programador** no menu superior direito Olá.

![Portal do programador][api-management-developer-portal-menu]

Clique em **APIs** no Olá menu superior e, em seguida, selecione **API eco**.

![API Eco][api-management-apis-echo-api]

> Se tiver apenas uma API configurada ou visível tooyour conta, em seguida, clicar em APIs leva-o diretamente toohello operações dessa API.
> 
> 

Selecione Olá **recurso GET (em cache)** operação e, em seguida, clique em **abrir a consola**.

![Abrir consola][api-management-open-console]

consola de Olá permite-lhe tooinvoke operações diretamente a partir do portal do programador Olá.

![Consola][api-management-console]

Mantenha os valores predefinidos de Olá para **param1** e **param2**.

Selecione Olá chave pretendida Olá **chave de subscrição** na lista pendente. Se a sua conta tiver apenas uma subscrição, esta já estará selecionada.

Introduza **sampleheader: value1** no Olá **cabeçalhos de pedido** caixa de texto.

Clique em **HTTP Get** e tome nota do Olá cabeçalhos de resposta.

Introduza **sampleheader: value2** no Olá **cabeçalhos de pedido** caixa de texto e, em seguida, clique em **HTTP Get**.

Tenha em atenção que o valor de Olá **sampleheader** ainda **value1** na resposta Olá. Experimente alguns valores diferentes e tenha em atenção que Olá resposta em cache da primeira chamada de Olá é devolvida.

Introduza **25** para Olá **param2** campo e, em seguida, clique em **HTTP Get**.

Tenha em atenção que o valor de Olá **sampleheader** Olá resposta é agora **value2**. Porque os resultados da operação Olá são codificados por cadeia de consulta, a resposta em cache anterior Olá não foi devolvida.

## <a name="next-steps"> </a>Passos seguintes
* Para obter mais informações sobre as políticas de colocação em cache, consulte [políticas de colocação em cache] [ Caching policies] no Olá [referência de política de gestão de API][API Management policy reference].
* Para obter informações sobre a colocação em cache de itens por chave utilizando expressões de política, consulte [Colocação em cache personalizada na API Management do Azure](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
