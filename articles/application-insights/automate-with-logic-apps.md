---
title: aaaAutomate Azure Application Insights processa utilizando as Logic Apps.
description: "Saiba como rapidamente pode automatizar processos repetíveis, adicionando a aplicação de lógica de tooyour do Olá Application Insights conector."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Automatizar processos de Application Insights utilizando as Logic Apps

Localizar sozinho repetidamente executar Olá mesmas consultas no seu toocheck de dados de telemetria se o serviço está a funcionar corretamente? É procura o tooautomate estas consultas para localizar tendências e anomalias e, em seguida, criar os seus fluxos de trabalho em torno deles? conector do Azure Application Insights (pré-visualização) Olá para aplicações lógicas é ferramenta certa Olá para esta finalidade.

Esta integração, pode automatizar processos várias sem ter de escrever uma única linha de código. Pode criar uma aplicação lógica com Olá Application Insights conector tooquickly automatizar qualquer processo do Application Insights. 

Pode adicionar, bem como as ações adicionais. funcionalidade de Logic Apps Olá do App Service do Azure disponibiliza a centenas de ações. Por exemplo, utilizando uma aplicação lógica, pode automaticamente enviar uma notificação por e-mail ou criar um erro no Visual Studio Team Services. Também pode utilizar um dos Olá muitas disponíveis [modelos](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp acelerar o processo de Olá de criar a sua aplicação lógica. 

## <a name="create-a-logic-app-for-application-insights"></a>Criar uma aplicação lógica para o Application Insights

Neste tutorial, saiba como toocreate uma aplicação lógica que utiliza Olá análise autocluster algoritmo toogroup atributos nos dados de Olá para uma aplicação web. fluxo de Olá envia automaticamente resultados Olá por e-mail, apenas um exemplo de como pode utilizar o Application Insights Analytics e Logic Apps em conjunto. 

### <a name="step-1-create-a-logic-app"></a>Passo 1: Criar uma aplicação lógica
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No Olá **novo** painel, selecione **Web + móvel**e, em seguida, selecione **aplicação lógica**.

    ![Nova janela de aplicação lógica](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Passo 2: Criar um acionador para a sua aplicação lógica
1. No Olá **Designer de aplicação lógica** janela em **começar com um acionador comuns**, selecione **periodicidade**.

    ![Janela do estruturador de aplicação lógica](./media/automate-with-logic-apps/logicapp2.png)

2. No Olá **frequência** caixa, selecione **dia** e, em seguida, no Olá **intervalo** caixa, escreva **1**.

    ![Designer de aplicação lógica "Recurrence" janela](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Passo 3: Adicionar uma ação do Application Insights
1. Clique em **novo passo**e, em seguida, clique em **adicionar uma ação**.

2. No Olá **escolher uma ação** caixa de pesquisa, escreva **Azure Application Insights**.

3. Em **ações**, clique em **pré-visualização de consulta do Azure Application Insights – análise visualizar**.

    !["Escolher uma ação" janela do Designer de aplicação lógica](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Passo 4: Ligar o recurso do Application Insights tooan

toocomplete neste passo, precisará de uma ID da aplicação e uma chave de API para o seu recurso. Pode obtê-los de Olá portal do Azure, conforme mostrado no Olá diagrama a seguir:

![ID da aplicação Olá portal do Azure](./media/automate-with-logic-apps/appid.png) 

Forneça um nome para a ligação, o ID da aplicação Olá e a chave de API de Olá.

![Janela de ligação de fluxo de Designer da aplicação lógica](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Passo 5: Especificar Olá consulta de análise e tipo de gráfico
No seguinte exemplo de Olá, consulta Olá seleciona Olá falhada pedidos dentro Olá último dia e está correlacionada com exceções que ocorreram como parte da operação de Olá. Análise de está correlacionada com pedidos de Olá falhou, com base no identificador de operation_Id Olá. consulta de Olá segmenta, em seguida, resultados de Olá utilizando Olá autocluster algoritmo. 

Quando criar as suas próprias consultas, certifique-se de que estão a funcionar corretamente no Analytics antes de o adicionar tooyour fluxo.

1. No Olá **consulta** caixa, adicione a seguinte consulta de análise de Olá: 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. No Olá **tipo de gráfico** caixa, selecione **Html tabela**.

    ![Janela de configuração de consulta de análise](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Passo 6: Configurar o e-mail de toosend de aplicação de lógica de Olá

1. Clique em **novo passo**e, em seguida, selecione **adicionar uma ação**.

2. Na caixa de pesquisa de Olá, escreva **Outlook do Office 365**.

3. Clique em **Office 365 Outlook – enviar um e-mail**.

    ![Seleção de Outlook do Office 365](./media/automate-with-logic-apps/flow2b.png)

4. No Olá **enviar um e-mail** janela, Olá a seguir:

   a. Escreva o endereço de e-mail Olá do destinatário Olá.

   b. Escreva um assunto de correio eletrónico de Olá.

   c. Clique em qualquer local no Olá **corpo** caixa e, em seguida, no Olá dinâmica conteúdo menu que se abre no Olá direito, selecione **corpo**.

   d. Clique em **Mostrar opções avançadas**.

      ![Configuração do Outlook do Office 365](./media/automate-with-logic-apps/flow5.png)

5. No menu de conteúdo dinâmico de Olá, Olá seguintes:

    a. Selecione **nome do anexo**.

    b. Selecione **anexo conteúdo**.
    
    c. No Olá **é HTML** caixa, selecione **Sim**.

      ![Ecrã de configuração de e-mail do Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Passo 7: Guardar e testar a sua aplicação lógica
* Clique em **guardar** toosave as suas alterações.

Pode aguardar a aplicação de lógica Olá acionador toorun Olá, ou pode executar imediatamente aplicação de lógica de Olá selecionando **executar**.

![Ecrã de criação de aplicação lógica](./media/automate-with-logic-apps/step7.png)

Quando é executada a sua aplicação lógica, os destinatários Olá especificado na lista de correio eletrónico Olá irão receber um e-mail que se assemelha Olá seguinte:

![Mensagem de correio eletrónico de aplicação lógica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre como criar [as consultas de análises](app-insights-analytics-using.md).
- Saiba mais sobre [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





