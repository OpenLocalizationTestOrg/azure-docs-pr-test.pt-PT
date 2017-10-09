---
title: "aaaAdd condições e iniciar os fluxos de trabalho - Azure Logic Apps | Microsoft Docs"
description: "Controla a forma como fluxos de trabalho são executados no Azure Logic Apps adicionando lógica condicional, acionadores, ações e parâmetros."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>Utilizar funcionalidades das Logic Apps

Num [tópico anterior](../logic-apps/logic-apps-create-a-logic-app.md), que criou a sua primeira aplicação lógica. toocontrol fluxo de trabalho da sua aplicação lógica, pode especificar diferentes caminhos para sua toorun de aplicação lógica e demasiado como processar os dados em matrizes, coleções e lotes. Pode incluir estes elementos no seu fluxo de trabalho de aplicação lógica:

* Condições e [comutador instruções](../logic-apps/logic-apps-switch-case.md) permitem a sua aplicação lógica executar ações diferentes com base em se forem cumpridas condições específicas.

* [Ciclos](../logic-apps/logic-apps-loops-and-scopes.md) permitem a sua aplicação lógica executar passos repetidamente. Por exemplo, pode repetir ações através de uma matriz ao utilizar um **For_each** ciclo. Ou pode repetir ações até que a condição é cumprida quando utiliza um **até** ciclo.

* [Âmbitos](../logic-apps/logic-apps-loops-and-scopes.md) permitem agrupar série de ações em conjunto, por exemplo, o processamento de exceções tooimplement.

* [Debatching](../logic-apps/logic-apps-loops-and-scopes.md) permite que a sua aplicação lógica iniciar os fluxos de trabalho separados para os itens numa matriz quando utilizar Olá **SplitOn** comando.

Este tópico apresenta alguns outros conceitos para criar uma aplicação lógica:

* Código de vista tooedit uma aplicação lógica existente
* Opções de início de um fluxo de trabalho

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Condições: Passos de execução apenas depois de reunião, uma condição

toohave a sua aplicação lógica executar passos apenas quando os dados satisfazem critérios específicos, pode adicionar uma condição que compara os dados no fluxo de trabalho Olá contra campos específicos ou valores.

Por exemplo, suponha que tem uma aplicação lógica que envia demasiadas mensagens de correio eletrónico para publicações no feed RSS de um Web site. Pode adicionar uma condição para que a sua aplicação lógica envia correio eletrónico apenas quando publicar Olá nova categoria específica de tooa pertence.

1. No Olá [portal do Azure](https://portal.azure.com), localize e abra a sua aplicação lógica no Designer de aplicação lógica.

2. Adicione uma localização de fluxo de trabalho do toohello a condição que pretende. 

   condição de Olá tooadd entre passos existentes no fluxo de trabalho do app do lógica de Olá, mova o ponteiro de Olá através de seta de olá onde pretende que a condição de Olá tooadd. 
   Escolha Olá **sinal** (**+**), em seguida, escolha **adicionar uma condição**. Por exemplo:

   ![Adicionar condição toologic aplicação](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Se quiser tooadd uma condição no fim de Olá do seu fluxo de trabalho atual, aceda toohello inferior da sua aplicação lógica e escolha **+ novo passo**.

3. Agora defina condição Olá. Especificar o campo de origem de Olá que pretende que o tooevaluate, Olá operação tooperform e o valor de destino Olá ou campo. tooadd existente campos tooyour condição, escolha Olá **lista de conteúdo dinâmica adicionar**.

   Por exemplo:

   ![Editar condição no modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Segue-se a condição concluída Olá:

   ![Condição concluída](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > condição de Olá toodefine no código, escolha **editar no modo avançado**. Por exemplo:
   > 
   > ![Editar condição no código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. Em **se Sim** e **não se**, adicionar Olá passos tooperform com base em se Olá condição é cumprida.

   Por exemplo:

   ![Condição com Sim e não existem caminhos](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Pode arrastar ações existentes para Olá **se Sim** e **não se** caminhos.

5. Quando tiver terminado, guarde a aplicação lógica.

Agora receber e-mails apenas quando Olá cronologia satisfaz a condição.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Repetir ações através de uma lista com forEach

ciclo de forEach Olá Especifica um toorepeat de matriz uma ação ao longo. Se não for uma matriz, o fluxo de Olá falha. Por exemplo, se tiver action1 devolve uma matriz de mensagens e quiser toosend cada mensagem, pode incluir esta declaração de forEach nas propriedades de Olá a ação:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Editar definição de código Olá para uma aplicação lógica

Embora tenham Olá Designer de aplicação lógica, pode editar diretamente o código de Olá que define uma aplicação lógica.

1. Na barra de comando Olá, escolha **Code vista**.

    Um editor de completo abre-se e mostra a definição de Olá editasse.

    ![Vista de código](media/logic-apps-use-logic-app-features/codeview.png)

    No editor de texto Olá, pode copiar e colar qualquer número de ações na Olá mesma aplicação de lógica ou entre as logic apps. 
    Pode também facilmente adicionar ou remover secções todos a definição de Olá, e também pode partilhar as definições com outras pessoas.

2. Escolha as edições de toosave **guardar**.

## <a name="parameters"></a>Parâmetros

Algumas capacidades de Logic Apps estão disponíveis apenas na vista de código, por exemplo, os parâmetros. Os parâmetros tornam mais fácil tooreuse valores em toda a sua aplicação lógica. Por exemplo, se tiver um endereço de e-mail que pretende utilizar nas várias ações, deve definir esse endereço de e-mail como um parâmetro.

Os parâmetros são ideais para extrair os valores que são muito provavelmente toochange. São particularmente úteis quando necessitar de parâmetros de toooverride em ambientes diferentes. toolearn como parâmetros de toooverride com base no ambiente, consulte [criar definições da aplicação lógica](../logic-apps/logic-apps-author-definitions.md) e [documentação da REST API](https://docs.microsoft.com/rest/api/logic).

Este exemplo mostra como tooupdate sua aplicação lógica existente para que possa utilizar os parâmetros de termo de consulta Olá.

1. Na vista de código, determinar Olá `parameters : {}` de objeto e adicionar um `currentFeedUrl` objeto:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Aceda toohello `When_a_feed-item_is_published` ação, localizar Olá `queries` secção e substitua o valor de consulta Olá com:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin dois ou mais cadeias, também pode utilizar Olá `concat` função. 
    Por exemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona Olá mesmo como Olá acima.

3.  Quando tiver terminado, escolha **guardar**. 

    Agora pode alterar o feed através da transmissão de um URL diferente através de Olá RSS do Web site Olá `currentFeedURL` objeto.

Saiba mais sobre [como definições da aplicação lógica tooauthor](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Iniciar os fluxos de trabalho de aplicação de lógica

Ter diferentes opções para iniciar o fluxo de trabalho Olá definido na sua aplicação lógica. Pode sempre iniciar uma fluxo de trabalho a pedido no Olá [portal do Azure].

### <a name="recurrence-triggers"></a>Acionadores de periodicidade

Um acionador de recorrência é executada com intervalo que especificou. Quando o acionador de Olá tem lógica condicional, acionador Olá determina se o fluxo de trabalho Olá tem toorun. Um acionador indica deve executar o fluxo de trabalho Olá devolvendo um `200` código de estado. Quando o fluxo de trabalho Olá não necessita de toorun, acionador Olá devolve um `202` código de estado.

### <a name="callback-using-rest-apis"></a>Chamada de retorno com REST APIs

toostart um fluxo de trabalho, os serviços podem chamar um ponto final da aplicação lógica. toostart este tipo de lógica aplicação a pedido, escolha **executar agora** na barra de comandos Olá. Consulte [iniciar os fluxos de trabalho chamando lógica pontos finais de aplicação como acionadores](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[portal do Azure]: https://portal.azure.com

## <a name="next-steps"></a>Passos seguintes

* [Instruções de comutador](../logic-apps/logic-apps-switch-case.md) 
* [Ciclos, âmbitos e divisões](../logic-apps/logic-apps-loops-and-scopes.md)
* [Criar definições de aplicação lógica](../logic-apps/logic-apps-author-definitions.md)