---
title: "Exemplos de início rápido aaaAzure Monitor CLI 1.0. | Microsoft Docs"
description: "Comandos de exemplo CLI 1.0 para funcionalidades de monitorização do Azure. Monitor do Azure é um serviço do Microsoft Azure que permite as notificações de alerta toosend, chamada web URLs com base nos valores de dados de telemetria configurado e serviços de Cloud de dimensionamento automático, as máquinas virtuais e aplicações Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Exemplos de início rápido 1.0 Monitor plataforma CLI do Azure
Este artigo apresenta o exemplo toohelp de comandos de interface de linha de comandos (CLI) pode aceder às funcionalidades de monitorização do Azure. Monitor do Azure permite-lhe tooAutoScale serviços em nuvem, as máquinas virtuais e aplicações Web e toosend as notificações de alerta ou chamada web URLs com base nos valores de dados de telemetria configurado.

> [!NOTE]
> Monitor do Azure é o nome novo Olá que foi chamado "Informações do Azure" até 25th de Setembro de 2016. No entanto, Olá espaços de nomes e, consequentemente, os comandos de Olá abaixo contém ainda insights"Olá".
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Se ainda não instalou Olá CLI do Azure, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md). Se não estiver familiarizado com a CLI do Azure, pode ler mais sobre-lo no [Olá utilize CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../xplat-cli-azure-resource-manager.md).

No Windows, instale npm a partir de Olá [Web site do Node.js](https://nodejs.org/). Depois de concluir a instalação de Olá, com CMD.exe com privilégios de executar como administrador, execute o seguinte Olá a partir da pasta de olá onde npm está instalado:

```console
npm install azure-cli --global
```

Em seguida, navegue até tooany/localização da pasta que pretende e escreva Olá da linha de comandos:

```console
azure help
```

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure
Step-by-Olá primeiro passo é toologin tooyour conta do Azure.

```console
azure login
```

Depois de executar este comando, tem toosign em através de instruções de Olá no ecrã de Olá. Posteriormente, para ver a conta, TenantId e predefinido ID da subscrição. Todos os comandos funcionam no contexto de Olá da sua subscrição predefinida.

detalhes de Olá toolist da sua subscrição atual, utilize Olá os seguintes comandos.

```console
azure account show
```

toochange trabalho contexto tooa subscrição diferente, Olá utilize os seguintes comandos.

```console
azure account set "subscription ID or subscription name"
```

toouse o Azure Resource Manager e o Monitor de Azure os comandos, terá de toobe no modo Azure Resource Manager.

```console
azure config mode arm
```

tooview uma lista de todos os comandos suportados do Monitor do Azure, execute o seguinte Olá.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Ver o registo de atividade para uma subscrição
tooview uma lista de eventos de registo de atividade, efetue o seguinte de Olá.

```console
azure insights logs list [options]
```

Tente Olá seguir tooview todas as opções disponíveis.

```console
azure insights logs list -help
```

Eis um exemplo registos toolist por um resourceGroup

```console
azure insights logs list --resourceGroup "myrg1"
```

Registos de toolist de exemplo pelo autor da chamada

```console
azure insights logs list --caller "myname@company.com"
```

Registos de toolist de exemplo pelo autor da chamada num tipo de recurso, dentro de uma data de início e de fim

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Trabalhar com alertas
Pode utilizar informações de Olá Olá secção toowork com alertas.

### <a name="get-alert-rules-in-a-resource-group"></a>Obter as regras de alerta num grupo de recursos
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Criar uma regra de alerta métrica
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Criar regra de alerta do teste Web
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Eliminar uma regra de alerta
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Perfis de registo
Utilize as informações de Olá toowork esta secção com perfis de registo.

### <a name="get-a-log-profile"></a>Obter um perfil de registo
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Adicionar um perfil de registo sem retenção
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Remover um perfil de registo
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Adicionar um perfil de registo com retenção
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Adicionar um perfil de registo com retenção e EventHub
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnóstico
Utilize as informações de Olá toowork nesta secção, com definições de diagnóstico.

### <a name="get-a-diagnostic-setting"></a>Obter uma definição de diagnóstico
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Desativar a definição de diagnóstico
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Ativar uma definição de diagnóstico sem retenção
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Dimensionamento Automático
Utilize as informações de Olá toowork nesta secção, com definições de dimensionamento automático. É necessário toomodify estes exemplos.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Obter definições de dimensionamento automático para um grupo de recursos
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Obter definições de dimensionamento automático por nome de um grupo de recursos
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Configurar as definições de auotoscale
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
