---
title: "alertas de aaaCreate para serviços do Azure - CLI de várias plataformas | Microsoft Docs"
description: "Acionar mensagens de correio eletrónico, notificações, os URLs de Web sites chamada (webhooks) ou automatização quando forem cumpridas condições Olá que especificar."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Criar métricas alertas no Monitor do Azure para serviços do Azure - CLI de várias plataformas
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Descrição geral
Este artigo mostra como tooset configurar alertas de métricas do Azure utilizando Olá plataforma Interface de linha de comandos (CLI).

> [!NOTE]
> Monitor do Azure é o nome novo Olá que foi chamado "Informações do Azure" até 25th de Setembro de 2016. No entanto, Olá espaços de nomes e, consequentemente, os comandos de Olá abaixo contém ainda insights"Olá".
>
>

Pode receber um alerta com base na monitorização métricas para ou eventos nos seus serviços do Azure.

* **Valores métricos** - hello acionadores de alertas quando o valor de Olá de uma métrica especificada atravesse um limiar atribuir em qualquer direção. Ou seja, aciona ambas quando Olá primeiro condição e, em seguida, posteriormente quando condição que é já não está a ser cumprido.    
* **Eventos de registo de atividade** -pode acionar um alerta num *cada* eventos ou apenas quando ocorre um determinados eventos. mais informações sobre alertas de registo de atividade toolearn [clique aqui](monitoring-activity-log-alerts.md)

Pode configurar uma métrica toodo alerta Olá a seguir quando aciona:

* enviar o administrador de serviços de toohello de notificações de e-mail e coadministradores
* envie correio eletrónico tooadditional e-mails que especificar.
* Chamar um webhook
* iniciar a execução de um runbook do Azure (apenas a partir do portal do Azure neste momento Olá)

Pode configurar e obter informações sobre regras de alerta métricas utilizando

* [Portal do Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interface de linha de comandos (CLI)](insights-alerts-command-line-interface.md)
* [API de REST de Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Pode receber sempre a ajuda para comandos escrevendo um comando e colocando - ajudar no fim de Olá. Por exemplo:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Criar regras de alertas utilizando Olá CLI
1. Efetue Olá pré-requisitos e tooAzure de início de sessão. Consulte [amostras da CLI do Azure Monitor](insights-cli-samples.md). Em suma, instale Olá CLI e executar estes comandos. Podem ajudá-lo a sessão iniciada, mostram que subscrição que está a utilizar e prepará-lo toorun comandos de Monitor do Azure.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. as regras existentes toolist num grupo de recursos, utilize Olá seguir formulário **informações do azure a lista de regras de alertas** *[opções] &lt;resourceGroup&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate uma regra, terá de toohave várias partes importantes de informações pela primeira vez.
  * Olá **ID de recurso** para o recurso de Olá pretende tooset um alerta para
  * Olá **as definições de métrica** disponíveis para esse recurso

     Olá tooget unidirecional ID de recurso é toouse Olá portal do Azure. Pressupondo que já foi criado o recurso de Olá, selecione-o no portal de Olá. Em seguida, no painel seguinte da Olá, selecione *propriedades* em Olá *definições* secção. Olá *ID de recurso* é um campo no painel seguinte Olá. Outra forma é toouse Olá [Explorador de recursos do Azure](https://resources.azure.com/).

     É um id de recurso de exemplo para uma aplicação web

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     uma lista de unidades para as métricas de exemplo de recursos anterior Olá, Olá utilize os seguintes comandos da CLI e as métricas disponíveis de Olá tooget:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* é granularidade Olá de medição de Olá disponíveis (intervalos de 1 minuto). Utilizar diferentes granularidades dá-lhe opções de métricas diferentes.
4. toocreate uma métrica com base na regra de alerta, utilize um comando de Olá seguinte formato:

    **as informações do Azure métrico conjunto de regras de alertas** *[opções] &lt;ruleName&gt; &lt;localização&gt; &lt;resourceGroup&gt; &lt;windowSize &gt; &lt;operador&gt; &lt;limiar&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt; timeAggregationOperator&gt;*

    Olá os seguintes conjuntos de exemplo, um alerta no recurso web site. Olá alerta acionadores sempre que recebe consistentemente qualquer tráfego de 5 minutos e novamente quando não recebe nenhum tráfego de 5 minutos.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook ou enviar correio eletrónico quando um métrico alerta é acionado, primeiro crie e-mail Olá e/ou webhooks. Em seguida, criar regra de Olá imediatamente posteriormente. Não é possível associar webhook ou e-mails com já criou regras utilizando Olá CLI.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Pode verificar que os alertas não foi criados corretamente ao observar uma regra de individuais.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. regras de toodelete, utilize um comando de formulário Olá:

    **informações de eliminação de regras de alertas** [opções] &lt;resourceGroup&gt; &lt;ruleName&gt;

    Estes comandos, elimine as regras de Olá que criou anteriormente neste artigo.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Passos seguintes
* [Obter uma descrição geral da monitorização do Azure](monitoring-overview.md) , incluindo os tipos de Olá de informações que pode recolher e monitorizar.
* Saiba mais sobre [configurar webhooks alertas](insights-webhooks-alerts.md).
* Saiba mais sobre [configurar alertas de eventos de registo de atividade](monitoring-activity-log-alerts.md).
* Saiba mais sobre [Runbooks de automatização do Azure](../automation/automation-starting-a-runbook.md).
* Obter um [descrição geral de recolha de registos de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência do seu serviço.
* Obter um [descrição geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake se o serviço está disponível e reativa.
