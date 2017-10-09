---
title: "alertas de aaaCreate para serviços do Azure - PowerShell | Microsoft Docs"
description: "Acionar mensagens de correio eletrónico, notificações, os URLs de Web sites chamada (webhooks) ou automatização quando forem cumpridas condições Olá que especificar."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Criar métricas alertas no Monitor do Azure para serviços do Azure - PowerShell
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Descrição geral
Este artigo mostra como tooset cópias de segurança do Azure métrica alertas utilizando o PowerShell.  

Pode receber um alerta com base na monitorização métricas para ou eventos nos seus serviços do Azure.

* **Valores métricos** - hello acionadores de alertas quando o valor de Olá de uma métrica especificada atravesse um limiar atribuir em qualquer direção. Ou seja, aciona ambas quando Olá primeiro condição e, em seguida, posteriormente quando condição que é já não está a ser cumprido.    
* **Eventos de registo de atividade** -pode acionar um alerta num *cada* eventos ou apenas quando ocorre um determinados eventos. mais informações sobre alertas de registo de atividade toolearn [clique aqui](monitoring-activity-log-alerts.md)

Pode configurar uma métrica toodo alerta Olá a seguir quando aciona:

* enviar o administrador de serviços de toohello de notificações de e-mail e coadministradores
* envie correio eletrónico tooadditional e-mails que especificar.
* Chamar um webhook
* iniciar a execução de um runbook do Azure (apenas a partir do portal do Azure Olá)

Pode configurar e obter informações sobre regras de alerta utilizando

* [Portal do Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interface de linha de comandos (CLI)](insights-alerts-command-line-interface.md)
* [API de REST de Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Para obter informações adicionais, pode sempre escrever ```Get-Help``` e, em seguida, Olá pretende obter ajuda no comando do PowerShell.

## <a name="create-alert-rules-in-powershell"></a>Criar regras de alertas no PowerShell
1. Inicie sessão no tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Obter uma lista de subscrições Olá que tem disponíveis. Certifique-se de que estão a funcionar com a subscrição correta Olá. Se não estiver, defina-o direito de toohello um utilizando um resultado de Olá `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. as regras existentes toolist num grupo de recursos, utilize Olá os seguintes comandos:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate uma regra, terá de toohave várias partes importantes de informações pela primeira vez.

  * Olá **ID de recurso** para o recurso de Olá pretende tooset um alerta para
  * Olá **as definições de métrica** disponíveis para esse recurso

     Olá tooget unidirecional ID de recurso é toouse Olá portal do Azure. Pressupondo que já foi criado o recurso de Olá, selecione-o no portal de Olá. Em seguida, no painel seguinte da Olá, selecione *propriedades* em Olá *definições* secção. **ID de recurso** é um campo no painel seguinte Olá. Outra forma é toouse Olá [Explorador de recursos do Azure](https://resources.azure.com/).

     É um ID de recurso de exemplo para uma aplicação web

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Pode utilizar `Get-AzureRmMetricDefinition` lista de Olá tooview de todas as definições de métricas para um recurso específico.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Olá exemplo seguinte gera uma tabela com o nome de métrica de Olá e Olá unidade para esse métrica.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Está disponível uma lista completa das opções disponíveis para o Get-AzureRmMetricDefinition executando Get-MetricDefinitions.
5. Olá os seguintes conjuntos de exemplo, um alerta no recurso web site. Olá alerta acionadores sempre que recebe consistentemente qualquer tráfego de 5 minutos e novamente quando não recebe nenhum tráfego de 5 minutos.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook ou enviar correio eletrónico quando um alerta é acionado, primeiro crie e-mail Olá e/ou webhooks. Em seguida, criar de imediato regra Olá posteriormente com Olá - tag de ações e conforme mostrado no seguinte exemplo de Olá. Não é possível associar webhook ou e-mails com já criou regras através do PowerShell.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify que os alertas não foi criados corretamente ao observar a regras individuais Olá.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Elimine os alertas. Estes comandos, elimine as regras de Olá criadas anteriormente neste artigo.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Passos seguintes
* [Obter uma descrição geral da monitorização do Azure](monitoring-overview.md) , incluindo os tipos de Olá de informações que pode recolher e monitorizar.
* Saiba mais sobre [configurar webhooks alertas](insights-webhooks-alerts.md).
* Saiba mais sobre [configurar alertas de eventos de registo de atividade](monitoring-activity-log-alerts.md).
* Saiba mais sobre [Runbooks de automatização do Azure](../automation/automation-starting-a-runbook.md).
* Obter um [descrição geral de recolha de registos de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência do seu serviço.
* Obter um [descrição geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake se o serviço está disponível e reativa.
