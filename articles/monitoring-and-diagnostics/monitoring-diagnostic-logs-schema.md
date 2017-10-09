---
title: "aaaAzure serviços de suportado de registos de diagnóstico e de esquemas | Microsoft Docs"
description: "Compreenda Olá suportado serviços e esquema de eventos para os registos de diagnóstico do Azure."
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
ms.author: johnkem
ms.openlocfilehash: a3cbf5267e1bd0dc257f4fb4f42c323644046a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Serviços suportados, esquemas e categorias de registos de diagnóstico do Azure

[Os registos de diagnóstico de recursos do Azure](monitoring-overview-of-diagnostic-logs.md) são registos emitidos pelos recursos do Azure que descrevem a operação de Olá desse recurso. Estes registos são o tipo de recurso específico. Neste artigo, vamos descrevem conjunto Olá do esquema de serviços e eventos suportado para eventos emitidos por cada serviço. Este artigo também inclui uma lista completa das categorias de registo disponível por tipo de recurso.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Suportado e esquemas de serviços para os registos de diagnóstico de recursos
esquema de Olá para registos de diagnóstico de recurso varia consoante categoria Olá de registo e de recursos.   

| Serviço | Esquema & Docs |
| --- | --- |
| Gestão de API | Esquema não está disponível. |
| Gateways da Aplicação |[Registo de diagnóstico para o Gateway de aplicação](../application-gateway/application-gateway-diagnostics.md) |
| Automatização do Azure |[Análise de registos para a automatização do Azure](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Registo de diagnóstico de lote do Azure](../batch/batch-diagnostics.md) |
| Informações de cliente | Esquema não está disponível. |
| Rede de Entrega de Conteúdos | Esquema não está disponível. |
| CosmosDB | Esquema não está disponível. |
| Data Lake Analytics |[Accessing diagnostics logs for Azure Data Lake Analytics (Aceder aos registos de diagnóstico do Azure Data Lake Analytics)](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| Data Lake Store |[Aceder a registos de diagnóstico para o Azure Data Lake Store](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Event Hubs |[Registos de diagnóstico dos Event Hubs do Azure](../event-hubs/event-hubs-diagnostic-logs.md) |
| Cofre de Chaves |[Registo do Cofre de Chaves do Azure](../key-vault/key-vault-logging.md) |
| Load balancer |[Log Analytics para o Balanceador de Carga do Azure](../load-balancer/load-balancer-monitor-log.md) |
| Aplicações Lógicas |[Esquema de controlo personalizado B2B de Aplicações Lógicas](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Grupos de Segurança de Rede |[Análise de registos para grupos de segurança de rede (NSGs) (Log analytics for network security groups (NSGs))](../virtual-network/virtual-network-nsg-manage-log.md) |
| Serviços de Recuperação | Esquema não está disponível.|
| Pesquisa |[Ativar e utilizar a análise de tráfego de pesquisa](../search/search-traffic-analytics.md) |
| Gestão de Servidores | Esquema não está disponível. |
| Service Bus |[Registos de diagnóstico de Service Bus do Azure](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Stream Analytics |[Registos de diagnóstico de tarefa](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |

## <a name="supported-log-categories-per-resource-type"></a>Suportado categorias de registo por tipo de recurso
|Tipo de Recurso|Categoria|Nome a apresentar categoria|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|Os registos relacionado tooApiManagement Gateway|
|Microsoft.Automation/automationAccounts|JobLogs|Registos da tarefa|
|Microsoft.Automation/automationAccounts|JobStreams|Fluxos de trabalho|
|Microsoft.Automation/automationAccounts|DscNodeStatus|Estado do nó DSC|
|Microsoft.Batch/batchAccounts|ServiceLog|Registos do serviço|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Obtém Olá as métricas de ponto final de Olá, por exemplo, a largura de banda, saída, etc.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|Auditoria|Registos de Auditoria|
|Microsoft.DataLakeAnalytics/accounts|Pedidos|Registos de pedido|
|Microsoft.DataLakeStore/accounts|Auditoria|Registos de Auditoria|
|Microsoft.DataLakeStore/accounts|Pedidos|Registos de pedido|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Registos de arquivo|
|Microsoft.EventHub/namespaces|OperationalLogs|Registos operacionais|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Registos de escala automática|
|Microsoft.KeyVault/vaults|AuditEvent|Registos de Auditoria|
|Microsoft.Logic/workflows|WorkflowRuntime|Eventos de diagnóstico de tempo de execução do fluxo de trabalho|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Eventos de registo de conta de integração|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Eventos do grupo de segurança de rede|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Contador de regras do grupo de segurança de rede|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Eventos de alerta de Balanceador de carga|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|Estado de funcionamento de sonda de Balanceador de carga|
|Network/applicationgateways|ApplicationGatewayAccessLog|Registo de acesso do Gateway de aplicação|
|Network/applicationgateways|ApplicationGatewayPerformanceLog|Registo de desempenho do Gateway de aplicação|
|Network/applicationgateways|ApplicationGatewayFirewallLog|Registo de Firewall de Gateway de aplicação|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Cópia de segurança do Azure, dados de relatórios|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Tarefas de recuperação de sites do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Eventos de recuperação de sites do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Recuperação de sites do Azure replicado itens|
|Microsoft.Search/searchServices|OperationLogs|Registos de operações|
|Microsoft.ServiceBus/namespaces|OperationalLogs|Registos operacionais|
|Microsoft.StreamAnalytics/streamingjobs|Execução|Execução|
|Microsoft.StreamAnalytics/streamingjobs|Criação|Criação|

## <a name="next-steps"></a>Passos Seguintes

* [Saiba mais sobre os registos de diagnóstico](monitoring-overview-of-diagnostic-logs.md)
* [Os registos de diagnóstico de recursos de sequência demasiado**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Alterar definições de diagnóstico do recurso utilizando Olá API de REST de Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analisar os registos do armazenamento do Azure com a análise de registos](../log-analytics/log-analytics-azure-storage.md)
