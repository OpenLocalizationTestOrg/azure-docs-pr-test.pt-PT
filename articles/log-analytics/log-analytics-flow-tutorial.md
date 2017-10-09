---
title: aaaAutomate processa do Log Analytics do Azure com o Microsoft Flow
description: "Saiba como pode utilizar o Microsoft Flow tooquickly automatizar processos repetíveis utilizando o conector do Olá Log Analytics do Azure."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Automatizar processos de análise de registos com o conector de Olá Flow da Microsoft
[Microsoft Flow](https://ms.flow.microsoft.com) permite-lhe toocreate automatizada fluxos de trabalho com centenas de ações para uma variedade de serviços. Resultado de uma ação pode ser utilizado como entrada tooanother, permitindo-lhe toocreate integração entre diferentes serviços.  conector do Log Analytics do Azure Olá Microsoft Flow permitem-lhe toobuild fluxos de trabalho que incluem dados obtidos através de pesquisas de registo na análise de registos.

Por exemplo, pode utilizar dados de análise de registos do Microsoft Flow toouse uma notificação por e-mail a partir do Office 365, criar um erro no Visual Studio Team Services ou publicar uma mensagem Slack.  Pode acionar um fluxo de trabalho por um agendamento simple ou a partir de qualquer ação num serviço ligado, tais como quando é recebido um e-mail ou um tweet.  


> [!NOTE]
> conector de Log Analytics do Azure de Olá Microsoft Flow requer a sua área de trabalho toobe atualizado toohello nova análise de registos a linguagem de consulta. Pode saber mais sobre o novo idioma de Olá e obter Olá procedimento tooupgrade sua área de trabalho em [atualizar a sua pesquisa de registo de toonew de área de trabalho do Log Analytics do Azure](log-analytics-log-search-upgrade.md).  

tutorial de Olá neste artigo mostra como toocreate um fluxo que envia automaticamente Olá resultados da pesquisa de análise de registos de registo por e-mail, apenas um exemplo de como pode utilizar a análise de registos Flow da Microsoft. 


## <a name="step-1-create-a-flow"></a>Passo 1: Criar um fluxo
1. A iniciar sessão demasiado[Microsoft Flow](http://flow.microsoft.com)e selecione **flui My**.
2. Clique em **+ criar em branco**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Passo 2: Criar um acionador para o fluxo
1. Clique em **pesquisa centenas de conectores e acionadores**.
2. Tipo **agenda** na caixa de pesquisa de Olá.
3. Selecione **agenda**e, em seguida, selecione **agenda - periodicidade**.
4. No Olá **frequência** selecione **dia** e no Olá **intervalo** box, introduza **1**.<br><br>![Caixa de diálogo de Acionador de Flow Microsoft](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Passo 3: Adicionar uma ação de análise de registos
1. Clique em **+ novo passo**e, em seguida, clique em **adicionar uma ação**.
2. Procurar **Iniciar análise**.
3. Clique em **Log Analytics do Azure – execute a consulta e visualizar os resultados**.<br><br>![Execute a janela de consulta de análise de registos](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Passo 4: Configurar a ação de análise de registos de Olá

1. Especifique os detalhes de Olá para a sua área de trabalho, incluindo Olá ID de subscrição, grupo de recursos e o nome da área de trabalho.
2. Adicionar Olá seguir toohello de consulta de análise de registos **consulta** janela.  Esta é apenas uma consulta de exemplo e pode substituir qualquer outra que devolve dados.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Selecione **HTML tabela** para Olá **tipo de gráfico**.<br><br>![Ação de análise do registo](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Passo 5: Configurar o e-mail de toosend Olá fluxo

1. Clique em **novo passo**e, em seguida, clique em **+ adicionar uma ação**.
2. Procurar **Outlook do Office 365**.
3. Clique em **Office 365 Outlook – enviar um e-mail**.<br><br>![Janela de seleção do Outlook do Office 365](media/log-analytics-flow-tutorial/flow04.png)

4. Especifique o endereço de correio eletrónico Olá de um destinatário no Olá **para** janela e um assunto de correio eletrónico de Olá no **requerente**.
5. Clique em qualquer local no Olá **corpo** caixa.  A **conteúdo dinâmico** é aberta a janela com os valores das ações de anteriores.  
6. Selecione **corpo**.  Este é Olá os resultados da consulta Olá Olá ação de análise de registos.
6. Clique em **Mostrar opções avançadas**.
7. No Olá **é HTML** caixa, selecione **Sim**.<br><br>![Janela de configuração de e-mail do Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Passo 6: Guardar e testar o fluxo
1. No Olá **nome de fluxo** caixa, adicionar um nome para o fluxo e, em seguida, clique em **criar fluxo**.<br><br>![Guardar fluxo](media/log-analytics-flow-tutorial/flow06.png)
2. fluxo de Olá está agora criado e será executado após um dia em que é a agenda de Olá que especificou. 
3. tooimmediately teste Olá fluxo, clique em **executar agora** e, em seguida, **executar fluxo**.<br><br>![Executar o fluxo](media/log-analytics-flow-tutorial/flow07.png)
3. Quando o fluxo de Olá estiver concluída, verifique o correio de Olá de destinatário Olá que especificou.  Deve ter recebido uma mensagem com um corpo semelhante toohello seguinte procedimento:<br><br>![E-mail de exemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [pesquisas de registo na análise de registos](log-analytics-log-search-new.md).
- Saiba mais sobre [Microsoft Flow](https://ms.flow.microsoft.com).



