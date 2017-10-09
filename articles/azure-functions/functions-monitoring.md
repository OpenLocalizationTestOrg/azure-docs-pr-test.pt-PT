---
title: "aaaMonitoring das funções do Azure | Microsoft Docs"
description: "Saiba como toomonitor as suas funções do Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Monitorizar as Funções do Azure

## <a name="overview"></a>Descrição geral 


Olá **Monitor** separador para cada função permite-lhe tooreview cada execução de uma função.

![Separador de monitor de funções do Azure](./media/functions-monitoring/monitor-tab.png) 

Clicar uma execução permite-lhe tooreview Olá duração, dados de entrada, erros e ficheiros de registo associados. Isto é útil de depuração e as suas funções de otimização do desempenho.


> [!IMPORTANT]
> Quando utilizar Olá [consumo plano de alojamento](functions-overview.md#pricing) para as funções do Azure, Olá **monitorização** mosaico no painel de descrição geral de aplicação de função Olá não apresentará quaisquer dados. Isto acontece porque a plataforma de Olá dinamicamente dimensiona e gere instâncias de computação por si, pelo que estas métricas não são significativas um plano de consumo. utilização de Olá toomonitor das suas aplicações de função, em vez disso, deve utilizar orientações Olá neste artigo.
> 
> Olá seguinte captura de ecrã mostra um exemplo:
> 
> ![No painel de recursos principais do Olá de monitorização](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>A monitorização em tempo real

A monitorização em tempo real está disponível clicando **fluxo de eventos em direto** conforme mostrado abaixo. 

![Em direto a opção de fluxo de eventos para o separador de monitor de Olá](./media/functions-monitoring/monitor-tab-live-event-stream.png)

fluxo de eventos em direto de Olá irá ser graphed num novo separador do browser, conforme mostrado abaixo. 

![Exemplo de fluxo do evento em direto](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Não há um problema conhecido que pode fazer com que a sua toobe de toofail dados preenchido. Se isto ocorrer, poderá ser necessário tooclose Olá browser separador contentora Olá evento em direto fluxo e, em seguida, clique em **fluxo de eventos em direto** novamente tooallow-tooproperly preencher os dados de fluxo de eventos. 

fluxo de eventos em direto de Olá será graph Olá estatísticas para a sua função os seguintes:

* Execuções iniciadas por segundo
* Execuções concluídas por segundo
* Execuções falhadas por segundo
* Tempo de execução média em milissegundos.

Estas estatísticas são em tempo real, mas Olá real graphing de dados de execução de Olá pode ter cerca de 10 segundos de latência.






## <a name="monitoring-log-files-from-a-command-line"></a>Monitorização de ficheiros de registo de uma linha de comandos


Pode transmitir ficheiros de registo tooa sessão de linha de comandos numa estação de trabalho local utilizando Olá Interface de linha de comandos do Azure (CLI) ou o PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Monitorização de ficheiros de registo de aplicação de função com Olá CLI do Azure

tooget iniciado, [instalar Olá CLI do Azure](../cli-install-nodejs.md)

Registo na sua conta do Azure utilizando Olá seguintes comandos, ou qualquer uma das Olá outras opções abrangidas, [tooAzure de Olá CLI do Azure de início de sessão](../xplat-cli-connect.md).

    azure login

Modo de gestão de serviço de CLI do Azure (ASM) do tooenable de comando seguinte Olá de utilização:.

    azure config mode asm

Se tiver várias subscrições, utilize Olá seguir toolist comandos suas subscrições e conjunto Olá atual subscrição toohello subscrição que contém a aplicação de função.

    azure account list
    azure account set <subscriptionNameOrId>

Olá comando seguinte irá transmitir ficheiros de registo de Olá da sua linha de comandos de toohello de aplicação de função:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Monitorização de ficheiros de registo de aplicação de função com o PowerShell

tooget iniciado, [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

Adicione a sua conta do Azure executando Olá os seguintes comandos:

    PS C:\> Add-AzureAccount

Se tiver várias subscrições, pode listá-los por nome com Olá os seguintes comandos toosee se Olá correto de subscrição é Olá atualmente selecionado com base no `IsCurrent` propriedade:

    PS C:\> Get-AzureSubscription

Se precisar de tooset Olá subscrição ativa toohello um que contém a aplicação de função, utilize Olá os seguintes comandos:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Fluxo Olá registos tooyour sessão do PowerShell com Olá os seguintes comandos:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Para obter mais informações consulte demasiado[como: transmitir os registos para aplicações web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá os seguintes recursos:

* [Uma função de teste](functions-test-a-function.md)
* [Uma função de escala](functions-scale.md)

