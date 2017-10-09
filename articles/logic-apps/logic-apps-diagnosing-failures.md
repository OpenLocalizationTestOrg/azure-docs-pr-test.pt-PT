---
title: falhas de aaaDiagnose - Azure Logic Apps | Microsoft Docs
description: "Comuns toounderstand de formas em que as logic apps estão a falhar"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Diagnosticar falhas de aplicação lógica
Se surgirem problemas ou falhas com as logic apps, existem alguns abordagens podem ajudar a compreender melhor onde são feitos falhas Olá.  

## <a name="azure-portal-tools"></a>Ferramentas de portais do Azure
Olá portal do Azure fornece várias ferramentas toodiagnose cada aplicação lógica em cada passo.

### <a name="trigger-history"></a>Histórico de Acionador

Cada aplicação lógica tem pelo menos um acionador. Se reparar em que as aplicações não são acionando, procure primeiro no histórico de Acionador de Olá para obter mais informações. Pode aceder ao histórico de Acionador de Olá no painel principal do Olá lógica app'ss.

![Localizar o histórico de Acionador de Olá][1]

histórico de Acionador de Olá apresenta uma lista de todas as tentativas de Acionador que efetuou a sua aplicação lógica. Pode clicar em cada toodrill de tentativa de Acionador para detalhes de Olá, especificamente, as entradas ou saídas Olá tentativa de Acionador gerado. Se encontrar acionadores falhadas, selecione a tentativa de Acionador de Olá e escolha Olá **saídas** ligação tooreview qualquer erro gerado mensagens, por exemplo, as credenciais de FTP que não são válidas.

Olá Estados diferentes, que poderá ver são:

* **Ignorado**. ponto final de Olá foi consultado toocheck para dados e recebeu uma resposta que não estavam disponíveis dados.
* **Foi concluída com êxito**. acionador Olá recebeu uma resposta que estavam disponíveis dados. Este estado poderá resultar de um acionador manual, um acionador de recorrência ou um acionador de consulta. Este estado é normalmente acompanhado Olá **Fired** Estado, mas poderá não ser se tiver uma condição ou o comando SplitOn na vista de código que não foi satisfeita.
* **Não foi possível**. Foi gerado um erro.

#### <a name="start-a-trigger-manually"></a>Inicie manualmente um acionador

Se pretender toocheck de aplicação de lógica de Olá para um acionador disponível imediatamente sem aguardar a próxima periodicidade de Olá, clique em **selecione acionador** no painel principal de Olá tooforce uma verificação. Por exemplo, ao clicar nesta ligação com um acionador Dropbox faz com que Olá fluxo de trabalho tooimmediately consulta Dropbox para novos ficheiros.

### <a name="run-history"></a>histórico de execução

Cada acionador fired resulta numa execução. Pode aceder a informações de execução a partir do painel principal Olá, que contém vários detalhes que podem ajudar a compreender o que aconteceu durante o fluxo de trabalho Olá.

![Localizar Olá histórico de execução][2]

Uma execução apresentará um dos seguintes Estados de Olá:

* **Foi concluída com êxito**. Todas as ações com êxito. Se Ocorreu uma falha, falha de que foi processada por uma ação que ocorreram mais tarde no fluxo de trabalho Olá. Ou seja, falha de Olá foi processada por uma ação que foi definida toorun após uma falha na ação.
* **Não foi possível**. Pelo menos uma ação tido uma falha que não foi processada por uma ação mais tarde no Olá fluxo de trabalho.
* **Cancelada**. fluxo de trabalho Olá estava a ser executado, mas foi recebido um pedido de cancelamento.
* **Executar**. fluxo de trabalho Olá está atualmente em execução. Este estado pode ocorrer para fluxos de trabalho otimizados ou devido a Olá atual plano de preços. Para obter mais informações, consulte [limites de ação na página de preços de Olá](https://azure.microsoft.com/pricing/details/app-service/plans/). Configurar o diagnóstico (gráficos de Olá que são apresentados em Olá histórico de execução) também pode fornecer informações sobre quaisquer eventos de limitação que ocorrem.

Quando está a visualizar um histórico de execução, pode desagregar para obter mais detalhes.  

#### <a name="trigger-outputs"></a>Saídas de Acionador

Acionador produz Mostrar dados de Olá que provém de Acionador de Olá. Estes saídas podem ajudá-lo a determinar se todas as propriedades devolvidas conforme esperado.

> [!NOTE]
> Se vir qualquer conteúdo que não compreender, saiba como Azure Logic Apps [processa diferentes tipos de conteúdo](../logic-apps/logic-apps-content-type.md).
> 

![Exemplos de saída do acionador][3]

#### <a name="action-inputs-and-outputs"></a>Ação de entradas e saídas

Pode explorar entradas de Olá e saídas que receberam uma ação. Estes dados são útil para compreender o tamanho de Olá e a forma da área de Olá saídas e também para localizar as mensagens de erro poderão ter sido geradas.

![Ação de entradas e saídas][4]

## <a name="debug-workflow-runtime"></a>Tempo de execução do fluxo de trabalho de depuração

Juntamente com a monitorização entradas Olá, saídas e acionadores de execução, pode adicionar alguns fluxo de trabalho de tooa passos que ajudam na depuração. 
[RequestBin](http://requestb.in) é uma ferramenta poderosa, que pode adicionar como um passo num fluxo de trabalho. Ao utilizar RequestBin, pode configurar um HTTP inspector toodetermine Olá exato tamanho do pedido, a forma e o formato de um pedido HTTP. Pode criar um RequestBin e cole o URL de Olá numa aplicação lógica ação de HTTP POST com conteúdo do corpo que pretende que tootest, por exemplo, uma expressão ou outro resultado de passo. Depois de executar a aplicação de lógica de Olá, pode atualizar o seu toosee RequestBin como pedido Olá foi incorretamente quando gerados a partir do motor do Olá Logic Apps.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
