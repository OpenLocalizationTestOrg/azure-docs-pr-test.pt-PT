---
title: "aaaAzure SQL da base de dados métricas e registo de diagnóstico | Microsoft Docs"
description: "Saiba mais sobre como configurar a utilização de recursos do SQL Database do Azure resource toostore, conectividade e estatísticas de execução da consulta."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Métricas de base de dados SQL do Azure e o registo de diagnóstico 
Base de dados SQL do Azure pode emitir métricas e registos de diagnóstico para a monitorização mais fácil. Pode configurar a conectividade para um destes recursos do Azure e sessões, funcionários e utilização de recursos de toostore SQL Database do Azure:
- **Armazenamento do Azure**: para arquivar grandes quantidades de telemetria a um preço baixo
- **Hub de eventos do Azure**: para integrar telemetria de SQL Database do Azure com a sua solução de monitorização personalizada ou pipelines frequente
- **Análise de registos do Azure**: para Box Olá solução com o Reporting Services, alertas e mitigar as capacidades de monitorização 

    ![arquitetura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Ativar registo

Métricas e registo de diagnóstico não está ativada por predefinição. Pode ativar e gerir as métricas e registo de diagnóstico utilizando um dos seguintes métodos de Olá:
- Portal do Azure
- PowerShell
- CLI do Azure
- API REST 
- Modelo do Resource Manager

Quando ativar métricas e registo de diagnóstico, terá de toospecify Olá recursos do Azure onde são recolhidos os dados selecionados. Opções disponíveis:
- Log analytics
- Hub de Eventos
- Storage do Azure 

Pode aprovisionar um novo recurso do Azure ou selecione um recurso existente. Depois de selecionar os recursos de armazenamento Olá, terá de toospecify que toocollect de dados. As opções disponíveis incluem:

- **[métricas de 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**  -contém a percentagem de DTU, limite DTU, percentagem de CPU, percentagem de leitura de dados físicos, escrever o registo de percentagem, Successful/falhado/bloqueado por ligações de firewall, a percentagem de sessões, a percentagem de funcionários, armazenamento, a percentagem de armazenamento, a percentagem de armazenamento XTP

Se especificar uma conta de AzureStorage ou Hub de eventos, pode especificar um toospecify de política de retenção os dados que é mais antigos do que um selecionado período de tempo é eliminado. Se especificar a análise de registos, depende da política de retenção de Olá no escalão de preço selecionado Olá. Leia mais sobre [preços de análise de registos](https://azure.microsoft.com/pricing/details/log-analytics/). 

Recomendamos que leia os dois Olá [descrição geral das métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [descrição geral do Azure os registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigos toogain uma compreensão dos não apenas como tooenable registo, mas Olá categorias de métricas e registo suportado pela Olá vários serviços do Azure.

### <a name="azure-portal"></a>Portal do Azure

métricas de tooenable coleção de registos de diagnóstico no Olá portal do Azure, navegue tooyour SQL database do Azure ou a página do conjunto elástico e, em seguida, clique em **definições de diagnóstico**.

   ![Ativar no Olá portal do Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable métricas e registo de diagnóstico com o PowerShell, utilize Olá os seguintes comandos:

- armazenamento de tooenable dos registos de diagnóstico numa conta do Storage, utilize este comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   Olá ID da conta de armazenamento é o id de recurso Olá para toowhich de conta de armazenamento de Olá pretende toosend Olá registos.

- tooenable de transmissão em fluxo de registos de diagnóstico tooan Hub de eventos, utilize este comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Olá ID de regra de barramento de serviço é uma cadeia com este formato:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- Enviar tooenable da área de trabalho do Log Analytics do tooa de registos de diagnóstico, utilize este comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- Pode obter o id de recurso Olá da sua área de trabalho de análise de registos utilizando Olá os seguintes comandos:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

Pode combinar estas tooenable parâmetros várias opções de saída.

### <a name="cli"></a>CLI

tooenable métricas e registo de diagnóstico utilizando Olá CLI do Azure, Olá utilize os seguintes comandos:

- armazenamento de tooenable dos registos de diagnóstico numa conta do Storage, utilize este comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   Olá ID da conta de armazenamento é o id de recurso Olá para toowhich de conta de armazenamento de Olá pretende toosend Olá registos.

- tooenable de transmissão em fluxo de registos de diagnóstico tooan Hub de eventos, utilize este comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Olá ID de regra de barramento de serviço é uma cadeia com este formato:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- Enviar tooenable da área de trabalho do Log Analytics do tooa de registos de diagnóstico, utilize este comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

Pode combinar estas tooenable parâmetros várias opções de saída.

### <a name="rest-api"></a>API REST

Leia sobre como demasiado[alterar definições de diagnóstico com Olá API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Modelo do Resource Manager

Leia sobre como demasiado[ativam as definições de diagnóstico durante a criação de recursos utilizando o modelo do Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Fluxo para análise de registos 
Métricas de base de dados SQL do Azure e os registos de diagnóstico podem transmissão em fluxo para análise de registos utilizando a opção de incorporado "Enviar tooLog análise" Olá, no portal de hello, ou ao ativar a análise de registos na definição de diagnóstico através de cmdlets do PowerShell do Azure, CLI do Azure ou REST de Monitor do Azure API.

### <a name="installation-overview"></a>Descrição geral da instalação

Monitorização frota de SQL Database do Azure é simple com a análise de registos. São necessários três passos:

1.  Criar o recurso de análise de registos
2.  Configurar as métricas de toorecord de bases de dados e registos de diagnóstico para Olá criado análise de registos
3.  Instalar **análise do Azure SQL** solução a partir da galeria na análise de registos

### <a name="create-log-analytics-resource"></a>Criar o recurso de análise de registos

1. Clique em **novo** no menu da esquerda Olá.
2. Clique em **monitorização + gestão**
3. Clique em **análise de registo**
4. Preencha o formulário de análise de registos de Olá com informações adicionais de Olá necessárias: nome de área de trabalho, subscrição, grupo de recursos, localização e escalão de preço.

   ![análise de registos](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>Configurar as métricas de toorecord de bases de dados e registos de diagnóstico

tooconfigure forma mais fácil olá onde as bases de dados grave as métricas é efetuada através de Olá portal do Azure. No Olá portal do Azure, navegue até tooyour recursos de SQL Database do Azure e clique em **as definições de diagnóstico**. 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>Instalar a solução de análise do Azure SQL Olá da Galeria  

1. Depois de Olá recursos de análise de registos é criado e os dados é que fluem para, instale a solução de análise de SQL do Azure. Isto pode ser feito Olá **soluções galeria** que pode encontrar na home page do Olá OMS e no menu de lado de Olá. Na Galeria de Olá, localize e clique em **análise do Azure SQL** solução e clique em **adicionar**.

   ![solução de monitorização](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. Na sua home page do OMS, um novo mosaico chamado **análise do Azure SQL** aparece. Selecionar este mosaico abre o dashboard de análise do Azure SQL Olá.

### <a name="using-azure-sql-analytics-solution"></a>Utilizar a solução de análise SQL do Azure

Análise de SQL do Azure é um dashboard hierárquico que permite-lhe toonavigate através da hierarquia de Olá dos recursos da SQL Database do Azure. Permite esta capacidade é toodo alto nível de monitorização, mas também permite-lhe tooscope o direito de Olá toojust monitorização conjunto de recursos.
Dashboard contêm listas de Olá de diferentes recursos em recursos de Olá selecionado. Por exemplo, para uma subscrição selecionada pode ver Olá todos os servidores, conjuntos elásticos e bases de dados que pertencem toohello selecionada a subscrição. Além disso, para conjuntos elásticos e bases de dados, pode ver as métricas de utilização de recursos Olá desse recurso. Isto inclui gráficos para DTU, CPU, e/s, registo, sessões, os trabalhadores, ligações e armazenamento em GB.

## <a name="stream-into-azure-event-hub"></a>Fluxo para o Hub de eventos do Azure

Métricas de base de dados SQL do Azure e os registos de diagnóstico podem transmissão em fluxo para o Hub de eventos utilizando a opção de incorporado "fluxo tooan event hub" Olá no portal de hello, ou ao ativar o Id de regra de barramento de serviço na definição de diagnóstico através de Cmdlets do PowerShell do Azure, CLI do Azure ou REST de Monitor do Azure API. 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>Que toodo com métricas e registos de diagnóstico no Hub de eventos?
Depois dos dados de Olá selecionado é transmitida em fluxo para o Hub de eventos, são tooenabling próximo um do passo, avançadas cenários de monitorização. Os Event Hubs atuam como Olá "porta da frente" para um pipeline de eventos e, depois dos dados são recolhidos para um Hub de eventos, podem ser transformado e armazenados através de qualquer fornecedor de análise em tempo real ou adaptadores de criação de batches/armazenamento. Os Event Hubs desacoplam a produção de Olá de um fluxo de eventos do consumo desses eventos, Olá para que os consumidores de eventos possam aceder eventos Olá na sua própria agenda. Para obter mais informações sobre o Hub de eventos, consulte:

- [Quais são os Event Hubs do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?
- [Introdução ao Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Seguem-se apenas algumas formas poderá utilizar Olá capacidade de transmissão em fluxo:

-   Ver estado de funcionamento do serviço por transmissão em fluxo "path frequente" dados tooPowerBI - utilizar Event Hubs, o Stream Analytics e o Power BI, pode facilmente transformar os dados de métricas e diagnóstico para quase em tempo real das informações no seus serviços do Azure. Para uma descrição geral de como processar os dados com o Stream Analytics tooset dos Hubs de eventos e utilizar o Power BI como uma saída, consulte [Stream Analytics e o Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Fluxo registos toothird terceiros telemetria e de registo fluxos – utilizar os Hubs de eventos de transmissão em fluxo podem obter as métricas e registos de diagnóstico no toodifferent soluções de análise de registo e monitorização de terceiros. 
-   Crie uma plataforma de registo – e telemetria personalizada se já tiver uma plataforma de telemetria personalizada ou são apenas pensar sobre como criar um, Olá altamente dimensionável de publicação-subscrição natureza dos Event Hubs permite-lhe tooflexibly ingestão de registos de diagnóstico. Consulte [toousing de guia de Dan Rosanova Event Hubs numa plataforma de telemetria de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Fluxo para o armazenamento do Azure

Métricas de base de dados SQL do Azure e os registos de diagnóstico podem ser armazenados no armazenamento do Azure com a opção de "Conta de armazenamento tooa arquivar" incorporada Olá no Olá portal do Azure, ou ao ativar o armazenamento do Azure na definição de diagnóstico através de Cmdlets do PowerShell do Azure, CLI do Azure ou do Azure API de REST do monitor.

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>Esquema de métricas e registos de diagnóstico na conta do storage Olá

Assim que tiver configurado a métricas e recolha de registos de diagnóstico, um contentor de armazenamento é criado na conta de armazenamento de Olá que selecionou quando as primeiras linhas de Olá de dados estão disponíveis. estrutura de Olá destas blobs é:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
Ou, mais simples:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Por exemplo, poderá ser um nome de blob para 1 minuto métricas:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

No caso de pretender toorecord dados Olá Olá conjunto elástico, o nome do blob é um pouco diferente:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>Transferir registos e as métricas do storage do Azure

Consulte [transferir métricas e registos de diagnóstico do armazenamento do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)

## <a name="1-minute-metrics"></a>métricas de 1 minuto

| |  |
|---|---|
|**Recurso**|**Métricas**|
|Base de Dados|Percentagem DTU, DTU utilizado, o limite DTU, percentagem de CPU, percentagem de leitura de dados físicos, escrever o registo de percentagem, Successful/falhado/bloqueado por ligações de firewall, percentagem de sessões, percentagem workers, armazenamento, percentagem de armazenamento, a percentagem de armazenamento XTP, impasses |
|Agrupamento elástico|percentagem de eDTU, eDTU utilizado, o limite de eDTU, percentagem de CPU, percentagem de leitura de dados físicos, registo escrever percentagem, percentagem de sessões, percentagem workers, armazenamento, a percentagem de armazenamento, limite de armazenamento, percentagem de armazenamento XTP |
|||

## <a name="next-steps"></a>Passos seguintes

- Ler ambas Olá [descrição geral das métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [descrição geral do Azure os registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigos toogain uma compreensão dos não apenas como o tooenable registo, mas Olá métricas e categorias de registo suportado pelo Olá em vários serviços do Azure.
- Leia estas toolearn artigos sobre os event hubs:
   - [Quais são os Event Hubs do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?
   - [Introdução ao Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Consulte [transferir métricas e registos de diagnóstico do armazenamento do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
