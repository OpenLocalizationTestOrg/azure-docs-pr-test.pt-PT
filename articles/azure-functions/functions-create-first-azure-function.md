---
title: "aaaCreate a sua primeira função do Olá Portal do Azure | Microsoft Docs"
description: "Saiba como toocreate a sua primeira Azure funcionar para a utilização de execução sem servidor Olá portal do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Criar a sua primeira função no Olá portal do Azure

As funções do Azure permite-lhe executar o seu código num ambiente sem servidor sem ter toofirst criar uma VM ou publicar uma aplicação web. Neste tópico, saiba como toouse funciona toocreate uma função de "Olá mundo" Olá portal do Azure.

![Criar aplicação de função no Olá portal do Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure

Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Criar uma aplicação de função

Tem de ter uma execução de Olá do função aplicação toohost das suas funções. As aplicações App Function permitem-lhe agrupar funções como unidades lógicas para uma gestão, implementação e partilha de recursos mais fácil. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Em seguida, crie uma função na nova aplicação de função Olá.

## <a name="create-function"></a>Criar uma função acionada por HTTP

1. Expanda a nova aplicação de função, em seguida, clique em Olá  **+**  no botão seguinte demasiado**funções**.

2.  No Olá **começar rapidamente** página, selecione **WebHook + API**, **escolher um idioma** para a função e clique em **criar esta função** . 
   
    ![Guia de introdução de funções no Olá portal do Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Uma função é criada no idioma que escolheu utilizando o modelo de Olá para uma função de acionada de HTTP. Pode executar a nova função de Olá ao enviar um pedido HTTP.

## <a name="test-hello-function"></a>Testar a função de Olá

1. Na sua nova função, clique em **</> Obter URL da função**, selecione **predefinição (tecla de função)** e, em seguida, clique em **Copiar**. 

    ![Copie o URL da função Olá do Olá portal do Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Colar Olá função URL na barra de endereço do browser. Acrescentar a cadeia de consulta Olá `&name=<yourname>` toothis URL e prima Olá `Enter` chave no seu pedido de Olá tooexecute teclado. Olá segue-se um exemplo de resposta de Olá devolvida pela função Olá no browser Edge de Olá:

    ![Resposta de função no browser Olá.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    pedido de Olá URL inclui uma chave que é necessário, por predefinição, tooaccess a função através de HTTP.   

3. Quando a função é executada, informações de rastreio são escritas toohello registos. resultados de rastreio de Olá toosee da execução anterior do Olá, regresse a função tooyour no portal de Olá e clique em Olá segurança seta na parte inferior de Olá de Olá ecrã tooexpand **registos**. 

   ![As funções de início de sessão Visualizador Olá portal do Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passos seguintes

Criou uma aplicação App Function com uma função acionada por HTTP simples.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações, veja [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Enlaces de HTTP e webhook das Funções do Azure).



