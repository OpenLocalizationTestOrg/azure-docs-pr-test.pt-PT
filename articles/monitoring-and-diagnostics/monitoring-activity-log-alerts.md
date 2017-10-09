---
title: alertas de registo de atividade aaaCreate | Microsoft Docs
description: "Seja notificado através de SMS, o webhook e o e-mail quando determinados eventos ocorrem no registo de atividade Olá."
author: johnkemnetz
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Criar alertas de registo de atividade

## <a name="overview"></a>Descrição geral
Alertas de registo de atividade são alertas que ativar quando ocorre a um novo registo de eventos de atividade que corresponde a condições de Olá especificadas no alerta Olá. São recursos do Azure, pelo que pode ser criadas utilizando um modelo Azure Resource Manager. Também podem ser criados, atualizar ou eliminados no Olá portal do Azure. Este artigo apresenta alguns conceitos de Olá atrás de alertas de registo de atividade. Em seguida, mostra como toouse Olá tooset portal do Azure, um alerta sobre eventos de registo de atividade.

Normalmente, pode cria alertas de registo de atividade tooreceive notificações quando:

* Alterações específicas ocorrerem em recursos na sua subscrição do Azure, muitas vezes, âmbito tooparticular grupos de recursos ou recursos. Por exemplo, poderá pretender toobe notificado quando qualquer máquina virtual na myProductionResourceGroup é eliminada. Em alternativa, pode querer toobe notificado se quaisquer novas funções são atribuídas tooa utilizador na sua subscrição.
* Ocorre um evento de estado de funcionamento do serviço. Eventos de estado de funcionamento de serviço incluem a notificação de incidentes e eventos de manutenção que se aplicam tooresources na sua subscrição.

Em ambos os casos, um alerta de registo de atividade monitoriza apenas eventos na subscrição Olá no qual Olá é criado um alerta.

Pode configurar um alerta de registo de atividade com base em qualquer propriedade de nível superior do objeto JSON Olá para um registo de eventos de atividade. No entanto, o portal de Olá mostra as opções mais comuns de Olá:

- **Categoria**: administrativo, serviço de estado de funcionamento, dimensionamento automático e recomendação. Para obter mais informações, consulte [descrição geral do registo de atividade do Azure de Olá](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn mais informações sobre eventos de estado de funcionamento do serviço, consulte [receber alertas de registo de atividade em notificações de serviço](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Grupo de recursos**
- **Recurso**
- **Tipo de recurso**
- **Nome da operação**: nome de operação de controlo de acesso baseado em funções do Resource Manager Olá.
- **Nível**: Olá nível de gravidade do evento de Olá (verboso, informativo, aviso, erro ou crítico).
- **Estado**: Estado Olá do evento de Olá, normalmente iniciada, falhou ou foi concluída com êxito.
- **Evento iniciadas pelo**: também conhecido como Olá "autor da chamada." endereço de correio eletrónico hello ou do Azure Active Directory identificador de Olá utilizador que executou a operação de Olá.

>[!NOTE]
>Tem de especificar pelo menos, duas Olá precedente critérios do alerta, com a ser uma categoria de Olá. Não pode criar um alerta que activa sempre que é criado um evento nos registos de atividade Olá.
>
>

Quando um alerta de registo de atividade é ativado, utiliza uma ação de grupo toogenerate ações ou notificações. Um grupo de ação é um conjunto reutilizável de recetores de notificação, tais como endereços de correio eletrónico, números de telefone de URLs de webhook ou SMS. recetores Olá podem ser referenciadas a partir de vários alertas toocentralize e os canais de notificação de grupo. Quando definir o alerta de registo de atividade, tem duas opções. Pode:

* Utilize um grupo de ação existente no seu alerta de registo de atividade. 
* Crie um novo grupo de ação. 

toolearn mais informações sobre grupos de ação, consulte [criar e gerir grupos de ação no portal do Azure de Olá](monitoring-action-groups.md).

toolearn mais informações sobre notificações de estado de funcionamento do serviço, consulte [receber alertas de registo de atividade em notificações do Estado de funcionamento do serviço](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Criar um alerta um evento de registo de atividade com um novo grupo de ação utilizando Olá portal do Azure
1. No Olá [portal](https://portal.azure.com), selecione **Monitor**.

    ![Olá serviço "Monitor de"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. No Olá **registo de atividade** secção, selecione **alertas**.

    ![separador de "Alertas" Olá](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Selecione **Adicionar alerta de registo de atividade**e preencha os campos de Olá.

4. Introduza um nome na Olá **nome de alerta de registo de atividade** caixa e selecione um **Descrição**.

    ![Olá comando "Adicionar o alerta de registo de atividade"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Olá **subscrição** caixa autofills com a sua subscrição atual. Esta subscrição está Olá um no qual o grupo ação Olá é guardado. recurso de alerta de Olá está implementado toothis subscrição e monitores atividade eventos de registo do mesmo.

    ![caixa de diálogo de "Adicionar o alerta de registo de atividade" Olá](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Selecione Olá **grupo de recursos** no qual Olá alerta recurso é criado. Não se trata de grupo de recursos de Olá que é monitorizado por alerta Olá. Em vez disso, é grupo de recursos de olá onde está localizado o recurso de alerta de Olá.

7. Opcionalmente, selecione um **categoria de evento** toomodify Olá filtros adicionais que são apresentados. Para eventos administrativos, filtros de Olá incluem **grupo de recursos**, **recursos**, **tipo de recurso**, **nome da operação**, **Nível**, **estado**, e **eventos iniciadas pelo**. Estes valores identificam os eventos este alerta deve monitorizar.

    >[!NOTE]
    >Tem de especificar pelo menos uma das Olá precedente critérios do alerta. Não pode criar um alerta que activa sempre que é criado um evento nos registos de atividade Olá.
    >
    >

8. Introduza um nome na Olá **nome do grupo de ação** caixa e introduza um nome na Olá **nome abreviado** caixa. nome abreviado Olá é utilizado em vez de um nome de grupo ação completa, quando as notificações são enviadas através deste grupo.

9.  Defina uma lista de ações, fornecendo a ação de Olá:

    a. **Nome**: introduza o nome da ação de Olá, alias ou identificador.

    b. **Tipo de ação**: selecione SMS, o e-mail ou o webhook.

    c. **Detalhes**: com base no tipo de ação de Olá, introduza um número de telefone, o endereço de e-mail ou o webhook URI.

10. Selecione **OK** alerta de Olá toocreate.

alerta de Olá demora alguns minutos toofully se propague e, em seguida, ficar ativo. Este é acionado quando novos eventos correspondem aos critérios de alerta de Olá.

Para obter mais informações, consulte [esquema de webhook compreender Olá utilizada nos alertas do registo de atividade](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>grupo definido nestes passos em ação Olá é reutilizável como um grupo de ação existente para todas as definições de alerta futuras.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Criar um alerta um evento de registo de atividade para um grupo de ação existente utilizando Olá portal do Azure
1. Siga os passos 1 a 7 no Olá anterior secção toocreate o alerta de registo de atividade.

2. Em **notificar através de**, selecione Olá **existentes** botão do grupo de ação. Selecione um grupo de ação existente na lista de Olá.

3. Selecione **OK** alerta de Olá toocreate.

alerta de Olá demora alguns minutos toofully se propague e, em seguida, ficar ativo. Este é acionado quando novos eventos correspondem aos critérios de alerta de Olá.

## <a name="manage-your-alerts"></a>Gerir os alertas

Depois de criar um alerta, é visível na secção de alertas de Olá do painel de Monitor de Olá. Selecione o alerta de Olá que pretende toomanage para:

* Editá-lo.
* Elimine-o.
* Desactivar ou activar, se pretender parar de tootemporarily ou retomar a receção de notificações de alerta de Olá.

## <a name="next-steps"></a>Passos seguintes
- Obter um [descrição geral dos alertas](monitoring-overview-alerts.md).
- Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).
- Olá revisão [esquema de webhook alerta de registo de atividade](monitoring-activity-log-alerts-webhook.md).
- Saiba mais sobre [grupos ação](monitoring-action-groups.md).  
- Saiba mais sobre [notificações de estado de funcionamento do serviço](monitoring-service-notifications.md).
- Criar um [toomonitor alerta de registo de atividade, todas as operações de motor de dimensionamento automático na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Criar um [toomonitor alerta de registo de atividade, todas as operações de escala-na/escalável de dimensionamento automático falhou na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
