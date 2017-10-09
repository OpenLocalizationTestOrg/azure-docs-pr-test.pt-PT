---
title: "aaaCreate e gerir grupos de ação na Olá portal do Azure | Microsoft Docs"
description: "Saiba como toocreate e gerir grupos de ação na Olá portal do Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Criar e gerir grupos de ação na Olá portal do Azure
## <a name="overview"></a>Descrição geral ##
Este artigo mostra como toocreate e gerir grupos de ação na Olá portal do Azure.

Pode configurar uma lista de ações com grupos de ação. Estes grupos, em seguida, podem ser utilizados quando definir alertas do registo de atividade. Estes grupos, em seguida, podem ser reutilizados por cada alerta de registo de atividade que definir, garantindo que Olá mesmas ações efetuadas sempre que é acionada o alerta de registo de atividade Olá.

Um grupo de ação pode ter segurança too10 de cada tipo de ação. Cada ação é constituída por Olá seguintes propriedades:

* **Nome**: um identificador exclusivo dentro do grupo de ação de Olá.  
* **Tipo de ação**: enviar um SMS, envie um e-mail ou chamar um webhook.  
* **Detalhes**: Olá correspondente número de telefone, o endereço de e-mail ou o webhook URI.

Para obter informações sobre como toouse do Azure Resource Manager modelos tooconfigure ação grupos, consulte [modelos de Gestor de recursos do grupo de ação](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Criar um grupo de ação utilizando Olá portal do Azure ##
1. No Olá [portal](https://portal.azure.com), selecione **Monitor**. Olá **Monitor** painel consolida todas as suas monitorização definições e dados de uma vista.

    ![Olá serviço "Monitor de"](./media/monitoring-action-groups/home-monitor.png)
2. No Olá **registo de atividade** secção, selecione **grupos ação**.

    ![separador de "Grupos de ação" Olá](./media/monitoring-action-groups/action-groups-blade.png)
3. Selecione **adicionar grupo de ação**e preencha os campos de Olá.

    ![Olá comando "Adicionar grupo de ação"](./media/monitoring-action-groups/add-action-group.png)
4. Introduza um nome na Olá **nome do grupo de ação** caixa e introduza um nome na Olá **nome abreviado** caixa. nome abreviado Olá é utilizado em vez de um nome de grupo ação completa, quando as notificações são enviadas através deste grupo.

      ![caixa de diálogo Olá adicionar ação grupo"](./media/monitoring-action-groups/action-group-define.png)

5. Olá **subscrição** caixa autofills com a sua subscrição atual. Esta subscrição está Olá um no qual o grupo ação Olá é guardado.

6. Selecione Olá **grupo de recursos** a ação de Olá grupo é guardado.

7. Defina uma lista de ações, fornecendo cada ação:

    a. **Nome**: introduza um identificador exclusivo para esta ação.

    b. **Tipo de ação**: selecione SMS, o e-mail ou o webhook.

    c. **Detalhes**: com base no tipo de ação de Olá, introduza um número de telefone, o endereço de e-mail ou o webhook URI.

8. Selecione **OK** grupo de ação de Olá toocreate.

## <a name="manage-your-action-groups"></a>Gerir os grupos de ação ##
Depois de criar um grupo de ação, é visível na Olá **grupos ação** secção Olá **Monitor** painel. Selecione o grupo de ação de Olá que pretende toomanage para:

* Adicionar, editar ou remover as ações.
* Elimine grupo de ação de Olá.

## <a name="next-steps"></a>Passos seguintes ##
* Saiba mais sobre [SMS alerta comportamento](monitoring-sms-alert-behavior.md).  
* Obter um [compreensão do esquema de webhook alerta de registo de atividade Olá](monitoring-activity-log-alerts-webhook.md).  
* Saiba mais sobre [limitação de taxa](monitoring-alerts-rate-limiting.md) em alertas. 
* Obter um [descrição geral dos alertas de registo de atividade](monitoring-overview-alerts.md)e saber como tooreceive alertas.  
* Saiba como demasiado[configurar alertas sempre que uma notificação de estado de funcionamento do serviço é publicada](monitoring-activity-log-alerts-on-service-notifications.md).
