---
title: conector de aaaSMTP no Azure Logic Apps | Microsoft Docs
description: "Crie aplicações lógicas com o App service do Azure. Ligar tooSMTP toosend e-mail."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Começar a utilizar o conector de SMTP Olá
Ligar tooSMTP toosend e-mail.

toouse [qualquer conector](apis-list.md), terá primeiro de toocreate uma aplicação lógica. Pode começar a utilizar pelo [criar uma aplicação lógica agora](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Ligar tooSMTP
Antes da aplicação lógica pode aceder a qualquer serviço, terá primeiro de toocreate um *ligação* toohello serviço. A [ligação](connectors-overview.md) fornece conectividade entre uma aplicação lógica e outro serviço. Por exemplo, tooconnect tooSMTP, primeiro precisa de um SMTP *ligação*. toocreate uma ligação, introduza as credenciais de Olá que normalmente utiliza o serviço de Olá tooaccess ligar. Por isso, no exemplo de Olá SMTP, introduza nome da ligação Olá credenciais tooyour, o endereço do servidor SMTP e o utilizador início de sessão informações toocreate Olá ligação tooSMTP.  

### <a name="create-a-connection-toosmtp"></a>Criar uma ligação tooSMTP
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Utilizar um acionador de SMTP
Um acionador é um evento que pode ser o fluxo de trabalho do Olá toostart utilizados definido numa aplicação lógica. [Saiba mais sobre acionadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Neste exemplo, porque SMTP não tem um acionador próprios, iremos utilizar Olá **Salesforce - quando é criado um objecto** acionador. Este acionador ativa quando é criado um novo objeto no Salesforce. Para o nosso exemplo, iremos definir-forma a que sempre que é criado um novo fabrico no Salesforce, um *enviar correio eletrónico* ação ocorre através do conector de Olá SMTP com uma notificação de Olá novas oportunidades potenciais a ser criada.

1. Introduza *salesforce* na caixa de pesquisa de Olá no designer de aplicações de lógica de Olá, em seguida, selecione Olá **Salesforce - quando é criado um objecto** acionador.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Olá **quando é criado um objecto** controlo é apresentado.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Selecione Olá **tipo de objeto** , em seguida, selecione *levar* da lista de Olá de objetos. Neste passo, é com a indicação de que está a criar um acionador que irá notificar a sua aplicação lógica sempre que é criado um novo fabrico no Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. acionador Olá foi criado.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Utilizar uma ação de SMTP
Uma ação é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica. [Saiba mais sobre as ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Agora que hello acionador foi adicionado, siga estas ação tooadd um SMTP passos que irá ocorrer quando é criado um novo fabrico no Salesforce.

1. Selecione **+ novo passo** ação de Olá tooadd gostaria tootake quando é criada uma antecedência de novo.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Selecione **adicionar uma ação**. Esta caixa de pesquisa de Olá abre onde pode procurar qualquer ação gostaria de tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Introduza *smtp* toosearch para ações de tooSMTP relacionados.  
4. Selecione **SMTP - enviar correio eletrónico** como Olá ação tootake quando antecedência novo Olá é criada. Bloco de controlo de ação de Olá abre. Terá tooestablish a ligação de smtp no bloco de estruturador Olá se não o fez, anteriormente.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Introduza as informações do e-mail pretendido no Olá **SMTP - enviar correio eletrónico** bloco.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Guarde o trabalho na ordem tooactivate o fluxo de trabalho.  

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Mais conectores
Voltar atrás toohello [lista APIs](apis-list.md).
