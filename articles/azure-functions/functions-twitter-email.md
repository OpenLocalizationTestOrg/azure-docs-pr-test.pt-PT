---
title: "Criar uma função que se integra com Azure Logic Apps | Microsoft Docs"
description: "Crie uma função que se integra com Azure Logic Apps e serviços cognitivos Azure categorizar sentimento tweet e enviar notificações quando os dados de sentimento é fraco."
services: functions, logic-apps, cognitive-services
keywords: "fluxo de trabalho, aplicações na cloud, serviços cloud, processos empresariais, integração de sistemas, integração de aplicações empresariais, EAI"
documentationcenter: 
author: ggailey777
manager: cfowler
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 12/08/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8137892c4360a6b55cfe48d62226c2421a791d5e
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/19/2018
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Criar uma função que se integra com Azure Logic Apps

As funções do Azure integra-se com Azure Logic Apps no Designer de aplicações lógicas. Esta integração permite-lhe utilizar o power informático de funções na orchestrations com outros serviços de terceiros e do Azure. 

Este tutorial mostra como utilizar as funções com Logic Apps e serviços cognitivos da Microsoft no Azure para analisar o sentimento do Twitter publicações. Uma função HTTP acionada categoriza tweets como verde, amarelos ou vermelhos com base na classificação de dados de sentimento. É enviado um e-mail quando é detetado sentimento fraco. 

![primeiros dois passos da aplicação no Designer de aplicação de lógica de imagem](media/functions-twitter-email/designer1.png)

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Crie um recurso de API de serviços cognitivos.
> * Crie uma função que categoriza sentimento tweet.
> * Crie uma aplicação lógica que liga-se ao Twitter.
> * Adicione a deteção de dados de sentimento para a aplicação lógica. 
> * Ligar a aplicação lógica para a função.
> * Envie um e-mail com base na resposta da função.

## <a name="prerequisites"></a>Pré-requisitos

+ Um Active Directory [Twitter](https://twitter.com/) conta. 
+ Um [Outlook.com](https://outlook.com/) conta (para o envio de notificações).
+ Este tópico usa como ponto de partida os recursos criados na função [Criar a primeira função a partir do portal do Azure](functions-create-first-azure-function.md).  
Se ainda não o fez, conclua estes passos agora para criar a sua aplicação de função.

## <a name="create-a-cognitive-services-resource"></a>Crie um recurso de serviços cognitivos

As APIs de serviços cognitivos estão disponíveis no Azure como recursos individuais. Utilize a API de análise de texto para detetar o sentimento de tweets em que está a ser monitorizado.

1. Inicie sessão no [portal do Azure](https://portal.azure.com/).

2. Clique no botão **Novo** localizado no canto superior esquerdo do portal do Azure.

3. Clique em **AI + análise** > **análise de texto API**. Em seguida, utilize as definições conforme especificado na tabela, aceite os termos e verifique **afixar ao dashboard**.

    ![Criar uma página de recurso cognitivos](media/functions-twitter-email/cog_svcs_resource.png)

    | Definição      |  Valor sugerido   | Descrição                                        |
    | --- | --- | --- |
    | **Nome** | MyCognitiveServicesAccnt | Escolha um nome de conta exclusiva. |
    | **Localização** | EUA Oeste | Utilize a localização mais próximo. |
    | **Escalão de preço** | F0 | Começar a utilizar o escalão mais baixo. Se executar fora de chamadas, dimensione para um escalão superior.|
    | **Grupo de recursos** | myResourceGroup | Utilize o mesmo grupo de recursos para todos os serviços neste tutorial.|

4. Clique em **criar** para criar o recurso. Depois de criado, selecione o novo recurso serviços cognitivos afixado ao dashboard. 

5. Na coluna de navegação esquerdo, clique em **chaves**e, em seguida, copie o valor da **chave 1** e guardá-lo. Esta chave é utilizada para ligar a aplicação lógica à sua API serviços cognitivos. 
 
    ![Chaves](media/functions-twitter-email/keys.png)

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-the-function-app"></a>Criar a aplicação de função

Funções fornece uma excelente forma de descarga de tarefas de processamento num fluxo de trabalho logic apps. Este tutorial utiliza uma função de acionada de HTTP para processar as pontuações das classificações de serviços cognitivos tweet sentimento e devolver um valor de categoria.  

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

## <a name="create-an-http-triggered-function"></a>Criar uma função de acionada de HTTP  

1. Expanda a aplicação de funções e clique no botão **+**, junto a **Funções**. Se esta for a primeira função na sua aplicação de funções, selecione **Função personalizada**. É apresentado o conjunto completo de modelos de função.

    ![Página de início rápido das funções no portal do Azure](media/functions-twitter-email/add-first-function.png)

2. No campo de pesquisa, escreva `http` e, em seguida, escolha **c#** para o modelo de Acionador HTTP. 

    ![Escolha o acionador HTTP](./media/functions-twitter-email/select-http-trigger-portal.png)

3. Escreva um **nome** para a função, escolha `Function` para  **[nível de autenticação](functions-bindings-http-webhook.md#http-auth)**e, em seguida, selecione **criar**. 

    ![Criar a função de acionada de HTTP](./media/functions-twitter-email/select-http-trigger-portal-2.png)

    Esta ação cria uma função de script c# utilizando o modelo de Acionador de HTTP. O código aparece numa nova janela como `run.csx`.

4. Substitua os conteúdos do `run.csx` ficheiros com o código seguinte, em seguida, clique em **guardar**:

    ```csharp
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Este código de função devolve uma categoria de cor com base na classificação de dados de sentimento recebida no pedido. 

4. Para testar a função, clique em **testar** no extremo direito expandir o separador de teste. Escreva um valor de `0.2` para o **corpo do pedido**e, em seguida, clique em **executar**. Um valor de **RED** é devolvido no corpo da resposta. 

    ![Testar a função no portal do Azure](./media/functions-twitter-email/test.png)

Agora, tem uma função que categoriza pontuações de sentimento. Em seguida, crie uma aplicação lógica que integra-se a função com o Twitter e cognitivos API dos serviços. 

## <a name="create-a-logic-app"></a>Criar uma aplicação lógica   

1. No portal do Azure, clique em de **novo** botão encontrado no canto superior esquerdo do portal do Azure.

2. Clique em **integração empresarial com** > **aplicação lógica**. Em seguida, utilize as definições conforme especificado na tabela, verificação **afixar ao dashboard**e clique em **criar**.
 
4. Em seguida, escreva um **nome** como `TweetSentiment`, utilize as definições conforme especificado na tabela, aceite os termos e verifique **afixar ao dashboard**.

    ![Criar aplicação lógica no portal do Azure](./media/functions-twitter-email/new_logic_app.png)

    | Definição      |  Valor sugerido   | Descrição                                        |
    | ----------------- | ------------ | ------------- |
    | **Nome** | TweetSentiment | Escolha um nome adequado para a sua aplicação. |
    | **Grupo de recursos** | myResourceGroup | Escolha o mesmo grupo de recursos existente como antes. |
    | **Localização** | EUA Leste | Escolha uma localização perto de si. |    

4. Escolha **afixar ao dashboard**e, em seguida, clique em **criar** para criar a sua aplicação lógica. 

5. Depois da aplicação é criada, clique em sua nova aplicação lógica afixada ao dashboard. Em seguida, no Designer de aplicações lógicas, desloque para baixo e clique em de **aplicação lógica em branco** modelo. 

    ![Modelo de Logic Apps em branco](media/functions-twitter-email/blank.png)

Agora, pode utilizar o Designer de aplicações lógicas para adicionar serviços e acionadores à sua aplicação.

## <a name="connect-to-twitter"></a>Ligar ao Twitter

Em primeiro lugar, crie uma ligação à sua conta do Twitter. A aplicação lógica consulta tweets, que accionam a aplicação para ser executada.

1. No designer, clique em de **Twitter** de serviço e clique em de **quando é registado um tweet novo** acionador. Inicie sessão na sua conta do Twitter e autorizar Logic Apps para utilizar a sua conta.

2. Utilize as definições de Acionador de Twitter conforme especificado na tabela. 

    ![Definições do conector do twitter](media/functions-twitter-email/azure_tweet.png)

    | Definição      |  Valor sugerido   | Descrição                                        |
    | ----------------- | ------------ | ------------- |
    | **Texto de pesquisa** | #Azure | Utilize um hashtag que é popular para gerar novos tweets no intervalo escolhido. Quando utilizar o escalão gratuito e o hashtag é demasiado popular, pode utilizar rapidamente cópias de segurança a quota de transação na sua API serviços cognitivos. |
    | **Frequência** | Minuto | A unidade de frequência utilizada para consultar o Twitter.  |
    | **Interval** | 15 | O tempo decorrido entre pedidos do Twitter, em unidades de frequência. |

3.  Clique em **guardar** para ligar à sua conta do Twitter. 

Agora a aplicação está ligada ao Twitter. Em seguida, ligar a análise de texto para detetar o sentimento de tweets recolhidos.

## <a name="add-sentiment-detection"></a>Adicionar a deteção de dados de sentimento

1. Clique em **novo passo**e, em seguida, **adicionar uma ação**.

    ![Novo passo e, em seguida, adicionar uma ação](media/functions-twitter-email/new_step.png)

2. No **escolher uma ação**, clique em **análise de texto**e, em seguida, clique em de **detetar sentimento** ação.

    ![Detetar Sentimento](media/functions-twitter-email/detect_sent.png)

3. Escreva um nome de ligação tal como `MyCognitiveServicesConnection`, cole a chave para a API de serviços cognitivos guardar e clique em **criar**.  

4. Clique em **texto para analisar** > **Tweet texto**e, em seguida, clique em **guardar**.  

    ![Detetar Sentimento](media/functions-twitter-email/ds_tta.png)

Agora que a deteção de dados de sentimento estiver configurada, pode adicionar uma ligação para a função que consome o resultado de modelo de pontuação de sentimento.

## <a name="connect-sentiment-output-to-your-function"></a>Ligar a saída de dados de sentimento a sua função

1. No Designer de aplicações lógica, clique em **novo passo** > **adicionar uma ação**e, em seguida, clique em **das funções do Azure**. 

2. Clique em **escolher uma função do Azure**, selecione o **CategorizeSentiment** função que criou anteriormente.  

    ![Caixa de função do Azure que mostra escolher uma função do Azure](media/functions-twitter-email/choose_fun.png)

3. No **corpo do pedido**, clique em **pontuação** e, em seguida, **guardar**.

    ![Classificação](media/functions-twitter-email/trigger_score.png)

Agora, a função é acionada quando é enviada uma classificação de dados de sentimento da aplicação lógica. Uma categoria codificado por cores é devolvida para a aplicação lógica pela função. Em seguida, adicionar uma notificação de correio eletrónico que é enviada quando um valor de dados de sentimento do **RED** é devolvido na função. 

## <a name="add-email-notifications"></a>Adicionar notificações por e-mail

A última parte do fluxo de trabalho é acionar um e-mail quando o sentimento é classificado como _RED_. Este tópico utiliza um conector do Outlook.com. Pode efetuar os passos semelhantes para utilizar um conector do Gmail ou Outlook do Office 365.   

1. No Designer de aplicações lógica, clique em **novo passo** > **adicionar uma condição**. 

2. Clique em **escolha um valor**, em seguida, clique em **corpo**. Selecione **é igual ao**, clique em **escolha um valor** e tipo `RED`e clique em **guardar**. 

    ![Adicione uma condição para a aplicação lógica.](media/functions-twitter-email/condition.png)

3. No **VERDADEIRO se**, clique em **adicionar uma ação**, procure `outlook.com`, clique em **enviar um e-mail**e inicie sessão na sua conta do Outlook.com.
    
    ![Escolha uma ação para a condição.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Se não tiver uma conta do Outlook.com, pode escolher outro conector, como o Gmail ou Outlook do Office 365

4. No **enviar um e-mail** ação, utilize as definições de e-mail como especificadas na tabela. 

    ![Configure o e-mail para enviar uma ação de correio eletrónico.](media/functions-twitter-email/send_email.png)

    | Definição      |  Valor sugerido   | Descrição  |
    | ----------------- | ------------ | ------------- |
    | **Para** | Escreva o seu endereço de e-mail | O endereço de correio eletrónico que recebe a notificação. |
    | **Assunto** | Dados de sentimento tweet negativo detetado  | A linha de assunto da notificação de correio eletrónico.  |
    | **Corpo** | Texto de tweet, localização | Clique em de **Tweet texto** e **localização** parâmetros. |

5.  Clique em **Guardar**.

Agora que o fluxo de trabalho estiver concluído, pode ativar a aplicação lógica e ver a função no trabalho.

## <a name="test-the-workflow"></a>Testar o fluxo de trabalho

1. No Designer de aplicação lógica, clique em **executar** para iniciar a aplicação.

2. Na coluna esquerda, clique em **descrição geral** para ver o estado da aplicação lógica. 
 
    ![Estado de execução de aplicação lógica](media/functions-twitter-email/over1.png)

3. (Opcional) Clique das execuções para ver detalhes da execução.

4. Aceda à sua função, consulte os registos e certifique-se de que os valores de dados de sentimento foram recebidos e processados.
 
    ![Ver registos de função](media/functions-twitter-email/sent.png)

5. Quando é detetado um sentimento potencialmente negativo, receberá uma mensagem de e-mail. Se ainda não recebeu uma mensagem de e-mail, pode alterar o código de função para devolver a vermelho sempre:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Depois de ter verificado notificações por e-mail, altere para o código original:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Depois de concluir este tutorial, deve desativar a aplicação lógica. Ao desativar a aplicação, poderá evitar a ser cobrados para execuções e utilizando a cópia de segurança as transações na sua API serviços cognitivos.

Agora tem visto como é fácil para integrar funções num fluxo de trabalho Logic Apps.

## <a name="disable-the-logic-app"></a>Desativar a aplicação lógica

Para desativar a aplicação lógica, clique em **descrição geral** e, em seguida, clique em **desativar** na parte superior do ecrã. Isto interrompe a aplicação de lógica de execução e incorrer em custos sem eliminar a aplicação. 

![Registos de funções](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Passos Seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Crie um recurso de API de serviços cognitivos.
> * Crie uma função que categoriza sentimento tweet.
> * Crie uma aplicação lógica que liga-se ao Twitter.
> * Adicione a deteção de dados de sentimento para a aplicação lógica. 
> * Ligar a aplicação lógica para a função.
> * Envie um e-mail com base na resposta da função.

Avançar para o próximo tutorial para saber como criar uma API sem servidor para a sua função.

> [!div class="nextstepaction"] 
> [Criar uma API sem servidor com as Funções do Azure](functions-create-serverless-api.md)

Para saber mais sobre Logic Apps, consulte o artigo [Azure Logic Apps](../logic-apps/logic-apps-overview.md).

