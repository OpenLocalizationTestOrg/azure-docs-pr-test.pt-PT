---
title: "aaaOverview de registos de diagnóstico do Azure | Microsoft Docs"
description: "Saiba quais são os registos de diagnóstico do Azure e como pode utilizá-los eventos toounderstand ocorrer dentro de um recurso do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Recolher e consumir dados de registo dos seus recursos do Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>Quais são os registos de diagnóstico de recursos do Azure
**Os registos de diagnóstico ao nível de recursos do Azure** são registos emitidos por um recurso que fornecem dados avançados, frequentes sobre a operação de Olá desse recurso. conteúdo de Olá estes registos varia consoante o tipo de recurso. Por exemplo, os contadores de regra de grupo de segurança de rede e de auditorias do Cofre de chaves são duas categorias de registos de recursos.

Os registos de diagnóstico de nível de recursos sejam diferentes das Olá [registo de atividade](monitoring-overview-activity-logs.md). Olá registo de atividade fornece informações sobre as operações de Olá que foram efetuadas nos recursos na sua subscrição com o Resource Manager, por exemplo, criar uma máquina virtual ou eliminar uma aplicação lógica. Olá registo de atividade é um registo de nível de subscrição. Os registos de diagnóstico de nível de recursos fornecem informações aprofundadas operações que foram efetuadas no recurso de si próprio, por exemplo, obter um segredo do Cofre de chaves.

Os registos de diagnóstico de nível de recursos também diferem dos registos de diagnóstico de nível de SO convidado. Os registos de diagnóstico de SO convidado são esses recolhidos por um agente em execução dentro de uma máquina virtual ou outros suportado o tipo de recurso. Os registos de diagnóstico de nível de recursos requerem não existem dados de recursos específicos agente e captura do Olá plataforma do Azure, enquanto os registos de diagnóstico de nível de SO convidado capturar os dados do sistema de operativo Olá e aplicações em execução numa máquina virtual.

Nem todos os recursos suportam novo tipo de Olá de registos de diagnóstico de recurso descrito aqui. Este artigo contém uma lista de secção que tipos de recursos suportam Olá novo nível de recursos registos de diagnóstico.

![Registos de diagnóstico de recurso vs outros tipos de registos ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>O que pode fazer com os registos de diagnóstico de nível de recursos
Seguem-se algumas das ações de Olá que pode fazer com os registos de diagnóstico de recursos:

![Posicionamento de lógico de registos de diagnóstico de recursos](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Guardá-las tooa [ **conta de armazenamento** ](monitoring-archive-diagnostic-logs.md) de inspeção de auditoria ou manual. Pode especificar Olá retenção tempo (em dias) utilizando **definições de diagnóstico de recurso**.
* [Transmiti-los demasiado**Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) para ingestão por um serviço independente ou uma solução de análise personalizada, tais como o Power BI.
* Analisá-los com [análise de registos do OMS](../log-analytics/log-analytics-azure-storage.md)

Pode utilizar uma conta de armazenamento ou espaço de nomes de Event Hubs que não se encontra em Olá mesma subscrição, conforme Olá um emitir os registos. Olá utilizador configura a definição de Olá tem de ter Olá adequadas RBAC acesso tooboth as subscrições.

## <a name="resource-diagnostic-settings"></a>Definições de diagnóstico de recursos
Registos de diagnóstico de recursos de não-computação recursos estão configurados com as definições de diagnóstico de recursos. **Definições de diagnóstico de recurso** para um controlo de recursos:

* Onde os registos de diagnóstico de recursos e as métricas são enviadas (conta de armazenamento, os Event Hubs, e/ou análise de registos do OMS).
* As categorias de registo são enviadas e se os dados métricos também são enviados.
* Quanto cada categoria de registo deve ser mantida na conta de armazenamento
    - Uma retenção de zero dias significa que os registos são mantidos indefinidamente. Caso contrário, o valor de Olá pode ser qualquer número de dias entre 1 e 2147483647.
    - Se as políticas de retenção estão definidas, mas armazenar os registos numa conta do Storage está desativada (por exemplo, se apenas as opções de Event Hubs ou OMS estão selecionadas), as políticas de retenção de Olá não tem qualquer efeito.
    - As políticas de retenção são aplicado por dia, pelo que a Olá regista o fim do dia (UTC), do dia de Olá que se encontra agora para além da política de retenção de Olá são eliminados. Por exemplo, se tiver uma política de retenção de um dia, no início de Olá de hoje em dia a dia Olá hello registos de ontem de antes do dia de Olá seriam eliminados.

Estas definições são facilmente configuradas através de definições de diagnóstico de Olá para um recurso no portal do Azure de Olá, através de comandos do Azure PowerShell e CLI ou através de Olá [API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Os registos de diagnóstico e métricas de camada de SO convidado Olá de utilização de recursos (por exemplo, VMs ou Service Fabric) de computação de [um mecanismo separado para a configuração e seleção de saídas](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Como tooenable coleção de registos de diagnóstico de recursos
Coleção de registos de diagnóstico de recurso pode ser ativada [como parte da criação de um recurso num modelo do Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) ou depois de criar um recurso da página desse recurso no portal de Olá. Também pode ativar a coleção em qualquer momento utilizando os comandos do Azure PowerShell ou o CLI, ou Olá API de REST de Monitor do Azure.

> [!TIP]
> Estas instruções não aplicadas diretamente tooevery recursos. Consulte as hiperligações de esquema de Olá no Olá parte inferior desta página toounderstand especial os passos que podem ser aplicadas toocertain tipos de recursos.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Ativar a recolha de registos de diagnóstico de recurso no portal de Olá
Pode ativar a coleção de registos de diagnóstico de recurso no Olá Azure portal depois de um recurso foi criado pelo recurso específico de tooa vai ou navegando tooAzure Monitor. tooenable isto através do Azure Monitor:

1. No Olá [portal do Azure](http://portal.azure.com), navegue até tooAzure Monitor e clique em **definições de diagnóstico**

    ![Secção de monitorização do Monitor do Azure](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Opcionalmente filtrar a lista de Olá por tipo de recurso ou grupo de recursos, em seguida, clique no recurso de Olá para o qual gostaria de tooset uma definição de diagnóstico.

3. Se não existem definições de existirem no recurso de Olá que selecionou, são toocreate que lhes é pedida uma definição. Clique em "Ativar o diagnóstico".

   ![Adicionar definição de diagnóstico - sem definições existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Se existirem definições existentes no recurso de Olá, verá uma lista das definições já configurada neste recurso. Clique em "Adicionar definição de diagnóstico".

   ![Adicionar definição de diagnóstico - existente definições](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Atribua a um nome da definição, verifique as caixas de Olá para cada toowhich destino teria como toosend dados e configurar o recurso é utilizado para cada destino. Opcionalmente, defina um número de dias tooretain estes registos utilizando Olá **retenção (dias)** controlos de deslize (apenas aplicável toohello conta destino de armazenamento). Uma retenção de zero dias armazena os registos de Olá indefinidamente.
   
   ![Adicionar definição de diagnóstico - existente definições](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Clique em **Guardar**.

Após alguns instantes, a nova definição é apresentada na lista de definições para este recurso e os registos de diagnóstico são enviados toohello Olá especificado destinos assim que os novos dados de evento são gerados.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Ativar a recolha de registos de diagnóstico de recursos através do PowerShell
coleção de tooenable de registos de diagnóstico de recursos através do Azure PowerShell, Olá utilize os seguintes comandos:

armazenamento de tooenable dos registos de diagnóstico numa conta do storage, utilize este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

ID de conta de armazenamento de Olá Olá ID de recurso para toowhich de conta de armazenamento de Olá pretende toosend Olá registos.

tooenable de transmissão em fluxo os registos de diagnóstico tooan do hub de eventos, utilize este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

ID de regra de barramento de serviço Olá é uma cadeia com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

Enviar tooenable da área de trabalho do Log Analytics do tooa de registos de diagnóstico, utilize este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Pode obter o ID de recurso Olá da sua área de trabalho de análise de registos utilizando Olá os seguintes comandos:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Pode combinar estas tooenable parâmetros várias opções de saída.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Ativar a recolha de registos de diagnóstico de recursos através da CLI
coleção de tooenable de registos de diagnóstico de recursos através de Olá CLI do Azure, utilize Olá os seguintes comandos:

armazenamento de tooenable dos registos de diagnóstico numa conta do Storage, utilize este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

ID de conta de armazenamento de Olá Olá ID de recurso para toowhich de conta de armazenamento de Olá pretende toosend Olá registos.

tooenable de transmissão em fluxo os registos de diagnóstico tooan do hub de eventos, utilize este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

ID de regra de barramento de serviço Olá é uma cadeia com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

Enviar tooenable da área de trabalho do Log Analytics do tooa de registos de diagnóstico, utilize este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Pode combinar estas tooenable parâmetros várias opções de saída.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Ativar a recolha de registos de diagnóstico de recursos através de REST API
definições de diagnóstico toochange utilizando Olá API de REST de Monitor do Azure, consulte [neste documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Gerir definições de diagnóstico de recursos no portal de Olá
Certifique-se de que todos os seus recursos estão configurados com definições de diagnóstico. Navegue demasiado**Monitor** no Olá portal e abra **definições de diagnóstico**.

![Diagnóstico registos painel no portal de Olá](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Poderá ter tooclick mais secção "serviços" toofind Olá Monitor.

Aqui pode ver e filtrar todos os recursos que suportam toosee de definições de diagnóstico, se tiver ativado o diagnóstico. Também pode desagregar toosee se várias definições estão definidas num recurso e verifique que a conta de armazenamento, o espaço de nomes de Event Hubs e/ou as área de trabalho de análise de registos que são enviados dados para.

![Resultados de registos de diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Adicionar que uma definição de diagnóstico aparece Olá vista de definições de diagnóstico, onde pode ativar, desativar ou modificar as definições de diagnóstico para Olá selecionado recursos.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Serviços suportados, categorias e esquemas de registos de diagnóstico de recursos
[Consulte este artigo](monitoring-diagnostic-logs-schema.md) para uma lista completa dos serviços suportados e categorias de registo Olá e esquemas utilizadas por esses serviços.

## <a name="next-steps"></a>Passos seguintes

* [Os registos de diagnóstico de recursos de sequência demasiado**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Alterar definições de diagnóstico do recurso utilizando Olá API de REST de Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analisar os registos do armazenamento do Azure com a análise de registos](../log-analytics/log-analytics-azure-storage.md)
