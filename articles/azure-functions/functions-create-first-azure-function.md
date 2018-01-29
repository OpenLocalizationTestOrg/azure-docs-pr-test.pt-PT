---
title: "Criar a sua primeira função a partir do portal do Azure | Microsoft Docs"
description: "Saiba como criar a sua primeira Função do Azure para execução sem servidor através do portal do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/17/2017
ms.author: glenga
ms.custom: mvc, devcenter
ms.openlocfilehash: 754ca6e5297c3be9166efa7a40a5ba3714911c99
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/12/2018
---
# <a name="create-your-first-function-in-the-azure-portal"></a>Criar a sua primeira função no portal do Azure

As Funções do Azure permitem-lhe executar o seu código num ambiente [sem servidor](https://azure.microsoft.com/overview/serverless-computing/), sem que tenha de criar primeiro uma VM ou publicar uma aplicação Web. Neste tópico, aprenda a utilizar as Funções para criar uma função “hello world” no portal do Azure.

![Criar uma aplicação de função no portal do Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sign-in-to-azure"></a>Iniciar sessão no Azure

Abra o portal do Azure. Para fazê-lo, inicie a sessão no [portal do Azure](https://portal.azure.com/) com a sua conta do Azure.

## <a name="create-a-function-app"></a>Criar uma aplicação de função

Precisa de uma aplicação Function App para alojar a execução das suas funções. As aplicações App Function permitem-lhe agrupar funções como unidades lógicas para uma gestão, implementação e partilha de recursos mais fácil. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Em seguida, vai criar uma função na aplicação Function App nova.

## <a name="create-function"></a>Criar uma função acionada por HTTP

1. Expanda a aplicação Function App nova e clique no botão **+**, junto a **Functions**.

2.  Na página **Começar rapidamente**, clique em **WebHook + API**, clique em **Escolher uma linguagem** para a função e clique em **Criar esta função**. 
   
    ![Início rápido de funções no portal do Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

É criada uma função na linguagem que escolheu com o modelo de função acionada por HTTP. Este tópico mostra uma função de script do C# no portal, mas pode criar uma função em qualquer [idioma suportado](supported-languages.md). 

Agora, pode enviar um pedido HTTP para executar a função nova.

## <a name="test-the-function"></a>Testar a função

1. Na sua nova função, clique em **</> Obter URL da função** no canto superior direito, selecione **predefinição (tecla de Função)** e, em seguida, clique em **Copiar**. 

    ![Copiar o URL da função a partir do portal do Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Cole o URL da função na barra de endereço do navegador. Adicione o valor da cadeia de consulta `&name=<yourname>` ao final deste URL e prima a tecla `Enter` no teclado para executar o pedido. Deverá ver a resposta devolvida pela função apresentada no browser.  

    Segue-se um exemplo de resposta no browser Edge (outros browsers podem incluir o XML apresentado):

    ![Resposta da função no browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    O URL do pedido inclui uma chave que é necessária, por predefinição, para aceder à sua função através de HTTP.   

3. Quando a sua função é executada, são escritas informações de rastreio nos registos. Para ver a saída de rastreio da execução anterior, regresse à função no portal e clique na seta, na parte inferior do ecrã, para expandir os **Registos**. 

   ![Visualizador de registo de funções no portal do Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passos seguintes

Criou uma aplicação App Function com uma função acionada por HTTP simples.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações, veja [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Enlaces de HTTP e webhook das Funções do Azure).



