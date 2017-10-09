---
title: "aaaGet começar a utilizar segurança com a monitorização do Azure, funções e permissões | Microsoft Docs"
description: "Saiba como funções incorporadas e permissões toorestrict do Monitor de Azure toouse aceder aos recursos toomonitoring."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Introdução à segurança com a monitorização do Azure, funções e permissões
Tem de várias equipas toostrictly limitá toomonitoring aceder a dados e definições. Por exemplo, se tiver os membros da equipa que trabalham exclusivamente no monitorização (engenheiros de suporte, os engenheiros de devops) ou se utilizar um fornecedor de serviço geridas, poderá ser útil toogrant-lhes aceder tooonly dados de monitorização ao restringir os respetivos toocreate de capacidade, modificar, ou Elimine recursos. Este artigo mostra como tooquickly aplicar um incorporada monitorização RBAC função tooa utilizador no Azure ou criar a sua própria função personalizada para um utilizador que tem permissões de monitorização limitadas. -Descreve considerações de segurança para os seus recursos relacionados com o Monitor do Azure, em seguida, e como pode limitar o acesso toohello dados contêm.

## <a name="built-in-monitoring-roles"></a>Monitorização de funções incorporadas
Funções incorporadas do Monitor do Azure são toohelp concebida limite acesso tooresources numa subscrição permitindo os responsáveis pela monitorização de infraestrutura tooobtain e configurar dados de Olá que precisam. Monitor do Azure fornece duas funções out of box: A monitorização leitor e contribuinte de monitorização.

### <a name="monitoring-reader"></a>Leitor de monitorização
Pessoas atribuídas a função de leitor de monitorização de Olá podem ver todos os dados de monitorização de uma subscrição, mas não é possível modificar qualquer recurso ou editar quaisquer recursos relacionados toomonitoring de definições. Esta função é adequada para os utilizadores numa organização, tais como engenheiros de suporte ou operações que necessitam de toobe capaz de:

* Ver os dashboards de monitorização no portal de Olá e criar os seus próprios dashboards de monitorização privadas.
* A consulta utilizando Olá com base nas métricas [API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn931930.aspx), [cmdlets do PowerShell](insights-powershell-samples.md), ou [CLI de várias plataformas](insights-cli-samples.md).
* Consulta Olá utilizando o portal de Olá, API de REST de Monitor do Azure, os cmdlets do PowerShell ou CLI de várias plataformas de registo de atividade.
* Olá vista [definições de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) para um recurso.
* Olá vista [registo perfil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) para uma subscrição.
* Ver definições de dimensionamento automático.
* Atividade de alerta de vista e as definições.
* Aceder a dados do Application Insights e ver dados AI análise.
* Procurar dados de área de trabalho de análise de registos (OMS), incluindo dados de utilização para a área de trabalho Olá.
* Ver grupos de gestão de análise de registos (OMS).
* Obter o esquema de pesquisa do Olá análise de registos (OMS).
* Lista de pacotes de intelligence de análise de registos (OMS).
* Obter e executar a análise de registos (OMS) pesquisas guardadas.
* Obter a configuração de armazenamento da análise de registos (OMS) Olá.

> [!NOTE]
> Esta função não conceda acesso de leitura toolog dados que foi hub de eventos de transmissão em fluxo tooan ou armazenados numa conta do storage. [Consulte abaixo](#security-considerations-for-monitoring-data) para obter informações sobre como configurar o acesso a recursos toothese.
> 
> 

### <a name="monitoring-contributor"></a>Monitorização contribuinte
As pessoas atribuídas Olá contribuinte de monitorização de função pode visualizar todos os dados de monitorização de uma subscrição e criar ou modificar as definições de monitorização, mas não é possível modificar quaisquer outros recursos. Esta função é um superconjunto da função de leitor de monitorização de Olá e é adequada para os membros da equipa de monitorização ou fornecedores de serviço gerida que, além disso toohello permissões acima, também necessitam de toobe conseguir da organização:

* Publica os dashboards de monitorização como um dashboard partilhado.
* Definir [definições de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) para um resource.*
* Conjunto Olá [registo perfil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) para um subscription.*
* Defina a atividade de alerta e as definições.
* Crie testes web do Application Insights e componentes.
* Área de trabalho de análise de registos (OMS) de lista de chaves partilhadas.
* Ativar ou desativar a análise de registos (OMS) intelligence pacotes.
* Criar e eliminar e executar a análise de registos (OMS) pesquisas guardadas.
* Criar e eliminar configuração de armazenamento da análise de registos (OMS) Olá.

* tem também separadamente ser concedido ao utilizador permissão ListKeys Olá destino recursos (armazenamento conta ou event hub espaço de nomes) tooset um perfil de registo ou a definição de diagnóstico.

> [!NOTE]
> Esta função não conceda acesso de leitura toolog dados que foi hub de eventos de transmissão em fluxo tooan ou armazenados numa conta do storage. [Consulte abaixo](#security-considerations-for-monitoring-data) para obter informações sobre como configurar o acesso a recursos toothese.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>As permissões e funções do RBAC personalizadas de monitorização
Se Olá acima funções incorporadas não satisfazer as necessidades de exato de Olá da sua equipa, pode [criar uma função personalizada do RBAC](../active-directory/role-based-access-control-custom-roles.md) com permissões mais granulares. Seguem-se Olá operações comuns do RBAC de Monitor do Azure com as respetivas descrições.

| Operação | Descrição |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, escrita, eliminar] |Regras de alertas de leitura/escrita/eliminar. |
| Microsoft.Insights/AlertRules/Incidents/Read |Lista de incidentes (histórico Olá de regra de alerta que está a ser acionado) para regras de alertas. Isto aplica-se apenas toohello portal. |
| Microsoft.Insights/AutoscaleSettings/[Read, escrita, eliminar] |Definições de dimensionamento automático de leitura/escrita/eliminar. |
| Microsoft.Insights/DiagnosticSettings/[Read, escrita, eliminar] |Definições de diagnóstico de leitura/escrita/eliminar. |
| Microsoft.Insights/eventtypes/digestevents/Read |Esta permissão é necessária para os utilizadores que precisam de aceder a registos de tooActivity através do portal Olá. |
| Microsoft.Insights/eventtypes/values/Read |Lista de eventos de registo de atividade (eventos de gestão) numa subscrição. Esta permissão é aplicável tooboth acesso programático e portal toohello registo de atividade. |
| Microsoft.Insights/LogDefinitions/Read |Esta permissão é necessária para os utilizadores que precisam de aceder a registos de tooActivity através do portal Olá. |
| Microsoft.Insights/MetricDefinitions/Read |Ler as definições de métrica (lista de tipos de métricas disponíveis para um recurso). |
| Microsoft.Insights/Metrics/Read |Ler métricas para um recurso. |

> [!NOTE]
> Acesso tooalerts, definições de diagnóstico e métricas para um recurso requer que o utilizador Olá tem o tipo de recurso de toohello de acesso de leitura e âmbito desse recurso. Criar ("escrita") um perfil de definição ou o registo de diagnóstico que arquivos tooa armazenamento conta ou fluxos tooevent hubs requer Olá utilizador tooalso permissão ListKeys no recurso de destino Olá.
> 
> 

Por exemplo, utilizando Olá acima tabela pode criar uma função RBAC personalizada para um "leitor do registo de atividade" como esta:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Considerações de segurança para dados de monitorização
Dados de monitorização — particularmente ficheiros de registo — pode conter informações confidenciais, tais como endereços IP ou nomes de utilizador. Dados de monitorização do Azure é fornecido em três formulários básicos:

1. Olá registo de atividade, que descreve a todas as ações de controlo plane na sua subscrição do Azure.
2. Registos de diagnóstico, que são emitidos por um recurso de registos.
3. Métricas que são emitidas pelo recursos.

Todas as três dos seguintes tipos de dados podem ser armazenadas numa conta de armazenamento ou transmissão em fluxo tooEvent Hub, que são recursos do Azure para fins gerais. Uma vez que estes são os recursos para fins gerais, criar, eliminar e aceder às mesmas são uma operação com privilégios normalmente reservada para um administrador. Sugerimos que utilize Olá seguintes práticas para utilização indevida de tooprevent relacionadas com a monitorização de recursos:

* Utilize uma conta de armazenamento dedicada único para os dados de monitorização. Se precisar de tooseparate dados de monitorização em várias contas do storage, nunca partilhar a utilização de uma conta de armazenamento entre monitorização e não-monitorização de dados, como esta inadvertidamente podem dar a quem só precisa de aceder aos dados de toomonitoring (ex. um SIEM de terceiros) aceder aos dados de monitorização de toonon.
* Utilize um único, dedicado barramento de serviço ou o Hub de eventos espaço de nomes em todas as definições de diagnóstico para Olá pelo mesmo motivo conforme apresentado acima.
* Limitar as contas de acesso a armazenamento relacionadas com toomonitoring ou event hubs ao mantê-los num grupo de recursos separado, e [utilizar âmbito](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) nas funções de monitorização toolimit acesso tooonly nesse grupo de recursos.
* Nunca Olá ListKeys permissão concedida para contas de armazenamento ou os hubs de eventos no âmbito da subscrição quando um utilizador necessita apenas de aceder a dados toomonitoring. Em vez disso, atribuir estas permissões toohello utilizador um recurso ou grupo de recursos (se tiver um grupo de recursos dedicado monitorização) âmbito.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Limitar as contas de armazenamento relacionadas com toomonitoring de acesso
Quando um utilizador ou aplicação precisa de aceder aos dados de toomonitoring numa conta do storage, deve [gerar um SAS de conta](https://msdn.microsoft.com/library/azure/mt584140.aspx) na conta de armazenamento de Olá que contém dados de monitorização com o armazenamento de tooblob acesso só de leitura de nível de serviço. No PowerShell, este poderá ter o seguinte aspeto:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

Em seguida, pode conceder entidade de token toohello Olá que necessita de tooread partir dessa conta de armazenamento e pode listar e ler a partir de todos os blobs nessa conta de armazenamento.

Em alternativa, se precisar de toocontrol esta permissão com RBAC, pode conceder Olá essa entidade permissão Microsoft.Storage/storageAccounts/listkeys/action essa conta de armazenamento específico. Isto é necessário para os utilizadores que necessitam de toobe capaz de tooset uma diagnóstico definição ou de registo perfil tooarchive tooa conta de armazenamento. Por exemplo, pode criar Olá seguinte função RBAC personalizada para um utilizador ou aplicação que necessita apenas de tooread de uma conta de armazenamento:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Olá ListKeys permissão permite que as chaves de conta de armazenamento primário e secundário toolist Olá Olá utilizador. Estas chaves conceder utilizador Olá todas assinadas permissões (ler, escrever, blobs de criar, eliminar blobs, etc.) em todas assinadas serviços (blob, fila, tabela, o ficheiro) nessa conta de armazenamento. Recomendamos que utilize um SAS de conta descrito acima, sempre que possível.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Limitar os hubs de eventos relacionados com toomonitoring de acesso
Um padrão semelhante pode ser seguido com os event hubs, mas tem primeiro toocreate uma regra de autorização de escutar dedicada. Se quiser toogrant acesso tooan aplicação que necessita apenas de hubs de eventos relacionados com toomonitoring toolisten, Olá a seguir:

1. Crie uma política de acesso partilhado no Olá eventos hub(s) que foram criadas para dados de monitorização com apenas afirmações de escuta de transmissão em fluxo. Pode fazê-lo no portal de Olá. Por exemplo, pode chamar-"monitoringReadOnly." Se for possível, deverá toogive que chave diretamente toohello consumidor e ignorar o passo seguinte Olá.
2. Se precisar de consumidor Olá toobe tooget capaz de Olá chave ad-hoc, conceda a ação do Olá utilizador Olá ListKeys para esse hub de eventos. Isto também é necessário para os utilizadores que precisam de toobe capaz de tooset uma definição de diagnóstico ou inicie os hubs de tooevent do perfil toostream. Por exemplo, poderá criar uma regra RBAC:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Passos seguintes
* [Leia sobre RBAC e permissões no Gestor de recursos](../active-directory/role-based-access-control-what-is.md)
* [Descrição geral de Olá de leitura de monitorização no Azure](monitoring-overview.md)

