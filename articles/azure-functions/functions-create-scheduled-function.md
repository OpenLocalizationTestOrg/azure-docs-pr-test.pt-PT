---
title: "aaaCreate uma função que é executada com base numa agenda no Azure | Microsoft Docs"
description: "Saiba como toocreate uma função no Azure que é executada com base numa agenda que definir."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Criar uma função no Azure que é acionada por um temporizador

Saiba como toouse das funções do Azure toocreate uma função que executa com base numa agenda que definir.

![Criar aplicação de função no Olá portal do Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial:

+ Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Criar uma aplicação de Funções do Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicação Function App criada com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

Em seguida, crie uma função na nova aplicação de função Olá.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Criar uma função acionada por temporizador

1. Expanda a sua aplicação de função e clique em Olá  **+**  no botão seguinte demasiado**funções**. Se esta for a primeira função de Olá na sua aplicação de função, selecione **função personalizada**. Esta ação apresenta o conjunto completo de Olá dos modelos de função.

    ![Página de início rápido de funções no Olá portal do Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Selecione Olá **TimerTrigger** modelo para o idioma pretendido. Em seguida, utilize definições de Olá conforme especificado na tabela de Olá:

    ![Crie uma função de temporizador acionada Olá portal do Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Definição | Valor sugerido | Descrição |
    |---|---|---|
    | **Dar um nome à função** | TimerTriggerCSharp1 | Define o nome de Olá da sua função de temporizador acionado. |
    | **[Agenda](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Um campo seis [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que agendas toorun sua função de cada minuto. |

2. Clique em **Criar**. É criada uma função na linguagem que escolheu e que é executada todos os minutos.

3. Certifique-se a execução através da visualização de informações de rastreio escritas toohello registos.

    ![As funções de início de sessão Visualizador Olá portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Agora, pode alterar a agenda da função de Olá para que seja executado com menos frequência, por exemplo, uma vez a cada hora. 

## <a name="update-hello-timer-schedule"></a>Atualizar o agendamento de temporizador Olá

1. Expanda a função e clique em **Integrar**. Este é onde definir entrada e saída enlaces para a sua função e também definir agenda Olá. 

2. Introduza um valor para **Agenda** novo de `0 0 */1 * * *` e clique em **Guardar**.  

![As funções de atualizar o agendamento de temporizador no Olá portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Tem agora uma função que é executada uma vez por hora. 

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passos seguintes

Criou uma função que é executada com base numa agenda.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações sobre os acionadores de temporizadores, veja [Schedule code execution with Azure Functions](functions-bindings-timer.md) (Agendar a execução de código com as Funções do Azure).