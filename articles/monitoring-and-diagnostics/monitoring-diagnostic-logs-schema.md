---
title: "Registos de diagnóstico do Azure, esquemas e serviços suportados | Microsoft Docs"
description: "Compreenda o esquema de serviços e eventos suportado para os registos de diagnóstico do Azure."
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
ms.date: 1/24/2018
ms.author: johnkem
ms.openlocfilehash: 3e2b5305b969c96e6b14122af03da9249373094a
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/25/2018
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Serviços suportados, esquemas e categorias de registos de diagnóstico do Azure

[Os registos de diagnóstico de recursos do Azure](monitoring-overview-of-diagnostic-logs.md) são registos emitidos pelos recursos do Azure que descrevem a operação desse recurso. Estes registos são o tipo de recurso específico. Neste artigo, vamos descrevem o conjunto de serviços suportados e o esquema de eventos para eventos emitidos por cada serviço. Este artigo também inclui uma lista completa das categorias de registo disponível por tipo de recurso.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Suportado e esquemas de serviços para os registos de diagnóstico de recursos
O esquema para os registos de diagnóstico de recurso varia consoante a categoria de registo e de recursos.   

| Serviço | Esquema & Docs |
| --- | --- |
| Analysis Services | Esquema não está disponível. |
| Gestão de API | [Registos de diagnóstico de gestão de API](../api-management/api-management-howto-use-azure-monitor.md#diagnostic-logs) |
| Gateways da Aplicação |[Registo de diagnóstico para o Gateway de aplicação](../application-gateway/application-gateway-diagnostics.md) |
| Automatização do Azure |[Análise de registos para a automatização do Azure](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Registo de diagnóstico de lote do Azure](../batch/batch-diagnostics.md) |
| Informações do Cliente | Esquema não está disponível. |
| Rede de Entrega de Conteúdos | Esquema não está disponível. |
| CosmosDB | [Registo do Cosmos BD do Azure](../cosmos-db/logging.md) |
| Data Lake Analytics |[Accessing diagnostics logs for Azure Data Lake Analytics (Aceder aos registos de diagnóstico do Azure Data Lake Analytics)](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| Data Lake Store |[Aceder a registos de diagnóstico para o Azure Data Lake Store](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Event Hubs |[Registos de diagnóstico dos Event Hubs do Azure](../event-hubs/event-hubs-diagnostic-logs.md) |
| IoT Hub | [Operações de IoT Hub](../iot-hub/iot-hub-monitor-resource-health.md#use-azure-monitor) |
| Cofre de Chaves |[Registo do Cofre de Chaves do Azure](../key-vault/key-vault-logging.md) |
| Load balancer |[Log Analytics para o Balanceador de Carga do Azure](../load-balancer/load-balancer-monitor-log.md) |
| Aplicações Lógicas |[Esquema de controlo personalizado B2B de Aplicações Lógicas](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Grupos de Segurança de Rede |[Análise de registos para grupos de segurança de rede (NSGs) (Log analytics for network security groups (NSGs))](../virtual-network/virtual-network-nsg-manage-log.md) |
| Proteção contra DDOS | Esquema não está disponível. |
| Serviços de Recuperação | [Modelo de dados para cópia de segurança do Azure](../backup/backup-azure-reports-data-model.md)|
| Pesquisa |[Ativar e utilizar a análise de tráfego de pesquisa](../search/search-traffic-analytics.md) |
| Gestão de Servidores | Esquema não está disponível. |
| Service Bus |[Registos de diagnóstico de Service Bus do Azure](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| SQL Database | [Registo de diagnóstico de base de dados SQL do Azure](../sql-database/sql-database-metrics-diag-logging.md) |
| Stream Analytics |[Registos de diagnóstico de tarefa](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |
| Redes Virtuais | Esquema não está disponível. |

## <a name="supported-log-categories-per-resource-type"></a>Suportado categorias de registo por tipo de recurso
|Tipo de Recurso|Categoria|Nome a apresentar categoria|
|---|---|---|
|Microsoft.AnalysisServices/servers|Motor|Motor|
|Microsoft.AnalysisServices/servers|Serviço|Serviço|
|Microsoft.ApiManagement/service|GatewayLogs|Registos relacionados com o Gateway de ApiManagement|
|Microsoft.Automation/automationAccounts|JobLogs|Registos da tarefa|
|Microsoft.Automation/automationAccounts|JobStreams|Fluxos de trabalho|
|Microsoft.Automation/automationAccounts|DscNodeStatus|Estado do nó DSC|
|Microsoft.Batch/batchAccounts|ServiceLog|Registos do serviço|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Obtém as métricas do ponto final, por exemplo, largura de banda, saída, etc.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataFactory/factories|ActivityRuns|Registo de execuções de atividade do pipeline|
|Microsoft.DataFactory/factories|PipelineRuns|Registo de execução de pipeline|
|Microsoft.DataFactory/factories|TriggerRuns|Registo de execução do acionador|
|Microsoft.DataLakeAnalytics/accounts|Auditoria|Registos de Auditoria|
|Microsoft.DataLakeAnalytics/accounts|Pedidos|Registos de pedido|
|Microsoft.DataLakeStore/accounts|Auditoria|Registos de Auditoria|
|Microsoft.DataLakeStore/accounts|Pedidos|Registos de pedido|
|Microsoft.Devices/IotHubs|Ligações|Ligações|
|Microsoft.Devices/IotHubs|DeviceTelemetry|Telemetria do dispositivo|
|Microsoft.Devices/IotHubs|C2DCommands|Comandos de C2D|
|Microsoft.Devices/IotHubs|DeviceIdentityOperations|Operações de identidade de dispositivo|
|Microsoft.Devices/IotHubs|FileUploadOperations|Operações de carregamento de ficheiros|
|Microsoft.Devices/IotHubs|Rotas|Rotas|
|Microsoft.Devices/IotHubs|D2CTwinOperations|D2CTwinOperations|
|Microsoft.Devices/IotHubs|C2DTwinOperations|Operações de duplo C2D|
|Microsoft.Devices/IotHubs|TwinQueries|Consultas de duplo|
|Microsoft.Devices/IotHubs|JobsOperations|Operações de tarefas|
|Microsoft.Devices/IotHubs|DirectMethods|Métodos diretos|
|Microsoft.Devices/provisioningServices|DeviceOperations|Operações de dispositivo|
|Microsoft.Devices/provisioningServices|ServiceOperations|Operações de serviço|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.DocumentDB/databaseAccounts|MongoRequests|MongoRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Registos de arquivo|
|Microsoft.EventHub/namespaces|OperationalLogs|Registos operacionais|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Registos de escala automática|
|Microsoft.KeyVault/vaults|AuditEvent|Registos de Auditoria|
|Microsoft.Logic/workflows|WorkflowRuntime|Eventos de diagnóstico de runtime de fluxo de trabalho|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Conta de Integração para controlar eventos|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Eventos do grupo de segurança de rede|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Contador de regras do grupo de segurança de rede|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupFlowEvent|Eventos de fluxo de regra de grupo de segurança de rede|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Eventos de alerta de Balanceador de carga|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|Estado de funcionamento de sonda de Balanceador de carga|
|Microsoft.Network/publicIPAddresses|DDoSProtectionNotifications|Notificações de proteção DDoS|
|Microsoft.Network/virtualNetworks|VMProtectionAlerts|Alertas de proteção de VM|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Registo de acesso do Gateway de aplicação|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Registo de desempenho do Gateway de aplicação|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Registo de Firewall de Gateway de aplicação|
|Microsoft.Network/virtualNetworkGateways|GatewayDiagnosticLog|Registos de diagnóstico do gateway|
|Microsoft.Network/virtualNetworkGateways|TunnelDiagnosticLog|Registos de diagnóstico de túnel|
|Microsoft.Network/virtualNetworkGateways|RouteDiagnosticLog|Registos de diagnóstico de rota|
|Microsoft.Network/trafficManagerProfiles|ProbeHealthStatusEvents|Evento de resultados de estado de funcionamento de sonda de Gestor de tráfego|
|Microsoft.Network/expressRouteCircuits|GWMCountersTable|Tabela de contadores GWM|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Cópia de segurança do Azure, dados de relatórios|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Tarefas de recuperação de sites do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Eventos de recuperação de sites do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Recuperação de sites do Azure replicado itens|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicationStats|Estatísticas de replicação de recuperação de sites do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryRecoveryPoints|Pontos de recuperação do Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicationDataUploadRate|Taxa de carregamento de dados de replicação de recuperação de sites do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryProtectedDiskDataChurn|Fluxo de dados do disco de protegidos do Azure Site Recovery|
|Microsoft.Search/searchServices|OperationLogs|Registos de Operações|
|Microsoft.ServiceBus/namespaces|OperationalLogs|Registos operacionais|
|Microsoft.Sql/servers/databases|QueryStoreRuntimeStatistics|Estatísticas de tempo de execução do arquivo de consultas|
|Microsoft.Sql/servers/databases|QueryStoreWaitStatistics|Estatísticas de espera de arquivo de consultas|
|Microsoft.Sql/servers/databases|Erros|Erros|
|Microsoft.Sql/servers/databases|DatabaseWaitStatistics|Estatísticas de espera de base de dados|
|Microsoft.Sql/servers/databases|Tempos limite|Tempos limite|
|Microsoft.Sql/servers/databases|Blocos de|Blocos de|
|Microsoft.Sql/servers/databases|SQLInsights|SQL Insights|
|Microsoft.Sql/servers/databases|Auditoria|Registos de Auditoria|
|Microsoft.StreamAnalytics/streamingjobs|Execução|Execução|
|Microsoft.StreamAnalytics/streamingjobs|Criação de conteúdos|Criação de conteúdos|

## <a name="next-steps"></a>Próximos Passos

* [Saiba mais sobre os registos de diagnóstico](monitoring-overview-of-diagnostic-logs.md)
* [Transmitir os registos de diagnóstico de recursos para **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Alterar definições de diagnóstico de recursos através da API de REST de Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analisar os registos do armazenamento do Azure com a análise de registos](../log-analytics/log-analytics-azure-storage.md)
