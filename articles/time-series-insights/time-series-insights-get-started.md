---
title: "aaaCreate um ambiente de informações de séries de tempo do Azure | Microsoft Docs"
description: "Neste tutorial, ficará a saber como toocreate ambiente de séries de tempo, ligue-a origem de evento tooan e pronto tooanalyze os dados de eventos em minutos."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Criar um novo ambiente de informações de séries de tempo no Olá portal do Azure

O ambiente do Time Series Insights é um recurso do Azure com capacidade de receção e armazenamento. Os clientes aprovisionar ambientes através do portal do Azure de Olá com capacidade de Olá necessário.

## <a name="steps-toocreate-hello-environment"></a>Ambiente de Olá passos toocreate

Siga estes passos toocreate seu ambiente:

1.  Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2.  Clique em Olá sinal de adição ("+"), na parte superior Olá esquerda canto.
3.  Procure "Insights de séries de tempo" na caixa de pesquisa de Olá.

  ![Criar ambiente de informações de séries de tempo de Olá](media/get-started/getstarted-create-environment1.png)

4.  Selecione "Time Series Insights", clique em "Criar".

  ![Criar grupo de recursos de informações de séries de tempo de Olá](media/get-started/getstarted-create-environment2.png)

5.  Especifique o nome do ambiente. Este nome irá representar o ambiente de Olá no [Explorador de séries de tempo](https://insights.timeseries.azure.com).
6.  Selecione uma subscrição. Escolha uma que contenha a origem do evento. Informações de séries de tempo pode deteção automática do Azure IoT Hub e Olá de recursos de Hub de eventos existentes na mesma subscrição.
7.  Selecione ou crie um grupo de recursos. Um grupo de recursos é uma coleção de recursos do Azure utilizados em conjunto.
8.  Selecione uma localização de alojamento. os centros de dados de mover tooavoid em dados, escolha a localização que contém a origem de evento.
9.  Selecione um escalão de preço.
10. Selecione a capacidade. Pode alterar a capacidade de um ambiente após a criação.
11. Crie o seu ambiente. Também pode afixar o dashboard de toohello ambiente para facilitar o acesso sempre que iniciar sessão.

  ![Criar Olá Insights de séries de tempo pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Passos seguintes

* [Definir políticas de acesso de dados](time-series-insights-data-access.md) tooaccess ambiente na [Portal de informações de séries de tempo](https://insights.timeseries.azure.com)
* [Criar uma origem de eventos](time-series-insights-add-event-source.md)
* [Enviar eventos](time-series-insights-send-events.md) toohello origem de evento
