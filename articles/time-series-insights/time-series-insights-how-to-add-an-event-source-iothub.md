---
title: "aaaHow tooadd um ambiente de informações de séries de tempo do Azure tooyour de origem de evento de IoT Hub | Microsoft Docs"
description: "Este tutorial abrange como tooadd um evento de origem que está ligado tooan ambiente do IoT Hub tooyour Insights de séries de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Como tooadd uma origem de evento do IoT Hub

Este tutorial abrange como toouse Olá tooadd portal do Azure uma origem de evento que lê a partir de um ambiente do IoT Hub tooyour Insights de séries de tempo.

## <a name="prerequisites"></a>Pré-requisitos

Criar um IoT Hub e estiver a escrever tooit de eventos. Para obter mais informações sobre os Hubs IoT, consulte <https://azure.microsoft.com/services/iot-hub/>

> [Grupos de consumidores] Cada origem de evento Insights de séries de tempo tem toohave seu próprio grupo de consumidores dedicado que não seja partilhado com quaisquer outros consumidores. Se a leitores múltiplos consumam eventos a partir do mesmo grupo de consumidores de Olá, todos os leitores são toosee provável falhas. Para obter mais informações, consulte Olá [guia para programadores do IoT Hub](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Escolher uma opção de importar

Olá as definições de origem do evento Olá podem ser introduzidas manualmente ou um IoT hub pode ser selecionado a partir de hubs de IoT Olá que estão disponível tooyou.
No Olá **opção de importar** Seletor, escolha uma das seguintes opções de Olá:

* Forneça definições de IoT Hub manualmente
* Utilizar o IoT Hub a partir de subscrições disponíveis

### <a name="select-an-available-iot-hub"></a>Selecione um IoT Hub disponíveis

Olá tabela seguinte explica cada opção no separador de nova origem de evento Olá com a respetiva descrição ao selecionar um IoT Hub disponível como uma origem de evento:

| NOME DA PROPRIEDADE | DESCRIÇÃO |
| --- | --- |
| Nome da origem de evento | nome de Olá da sua origem de evento. Este nome tem de ser exclusivo no seu ambiente de informações de séries de tempo.
| Origem | Escolha **IoT Hub** toocreate uma origem de evento do IoT Hub.
| Id de subscrição | Selecione a subscrição de Olá no qual este hub IoT foi criado.
| Nome do hub IoT | Selecione o nome de Olá do Olá IoT Hub.
| Nome da política do IoT hub | Selecione a política de acesso Olá partilhado, o que pode ser encontrada no Olá separador de definições do IoT Hub. Cada política de acesso partilhado tem um nome, as permissões que define e chaves de acesso. Olá partilhado a política de acesso para a origem de evento *tem* ter **serviço ligar** permissões.
| Grupo de consumidores do hub IoT | Olá grupo de consumidores tooread eventos a partir de Olá IoT Hub. É altamente recomendado toouse um grupo de consumidores dedicado para a origem de evento.

### <a name="provide-iot-hub-settings-manually"></a>Forneça definições de IoT Hub manualmente

Olá tabela seguinte explica cada propriedade no separador de nova origem de evento Olá com a respetiva descrição ao introduzir as definições manualmente:

| NOME DA PROPRIEDADE | DESCRIÇÃO |
| --- | --- |
| Nome da origem de evento | nome de Olá da sua origem de evento. Este nome tem de ser exclusivo no seu ambiente de informações de séries de tempo.
| Origem | Escolha **IoT Hub** toocreate uma origem de evento do IoT Hub.
| Id de subscrição | subscrição Olá no qual este hub IoT foi criado.
| Grupo de recursos | subscrição Olá no qual este hub IoT foi criado.
| Nome do hub IoT | nome de Olá do seu IoT Hub. Quando criou o seu hub IoT, também lhe atribuiu um nome específico
| Nome da política do IoT hub | Olá partilhado política de acesso, que pode ser criada em Olá separador de definições do IoT Hub. Cada política de acesso partilhado tem um nome, as permissões que define e chaves de acesso. Olá partilhado a política de acesso para a origem de evento *tem* ter **serviço ligar** permissões.
| Chave de política do IoT hub | a chave de acesso partilhado Olá utilizada espaço de nomes do Service Bus do tooauthenticate acesso toohello. Tipo Olá chave primária ou secundária aqui.
| Grupo de consumidores do hub IoT | Olá grupo de consumidores tooread eventos a partir de Olá IoT Hub. É altamente recomendado toouse um grupo de consumidores dedicado para a origem de evento.

## <a name="next-steps"></a>Passos seguintes

1. Adicionar um ambiente de tooyour de política de acesso de dados [dados definir políticas de acesso](time-series-insights-data-access.md)
1. Aceder ao seu ambiente no Olá [Portal de informações de séries de tempo](https://insights.timeseries.azure.com)
