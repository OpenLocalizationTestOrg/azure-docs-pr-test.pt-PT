---
title: "aaaAzure solução de análise de redes no Log Analytics | Microsoft Docs"
description: "Pode utilizar Olá solução de análise de redes do Azure nos registos de grupo de segurança de rede do Azure tooreview análise de registos e registos do Gateway de aplicação do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Soluções de análise de registos de monitorização da rede do Azure

Análise de registos oferece Olá seguintes soluções para monitorização as redes:
* Monitor de desempenho de rede (NPM) para
 * Estado de funcionamento do monitor Olá da sua rede
* Tooreview de análise de Gateway de aplicação do Azure
 * Registos de Gateway de aplicação do Azure
 * Métricas de Gateway de aplicação do Azure
* Tooreview de análise do grupo de segurança de rede do Azure
 * Registos do grupo de segurança de rede do Azure

## <a name="network-performance-monitor-npm"></a>Monitor de desempenho de rede (NPM)

Olá [Monitor de desempenho de rede](log-analytics-network-performance-monitor.md) solução de gestão é uma solução, que monitoriza o estado de funcionamento de Olá, disponibilidade e acessibilidade de redes de monitorização de rede.  É utilizado toomonitor conectividade entre:

* Nuvem pública e no local
* Os centros de dados e localizações de utilizador (sucursais)
* Sub-redes alojar várias camadas de uma aplicação de várias camadas.

Para obter mais informações, consulte [Monitor de desempenho de rede](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Análise de Gateway de aplicação e o grupo de segurança de rede do Azure
soluções de Olá toouse:
1. Adicionar tooLog de solução de gestão de Olá, a análise e
2. Ative o diagnóstico toodirect Olá diagnóstico tooa Log Analytics área de trabalho. Não é necessário toowrite Olá registos tooAzure o Blob storage.

Pode ativar os diagnósticos e solução correspondente Olá para uma ou ambas Gateway de aplicação e grupos de segurança de rede.

Se não ativar o registo de diagnóstico para um tipo de recurso específico, mas instalar solução Olá, painéis de dashboard Olá para esse recurso em branco e apresentam uma mensagem de erro.

> [!NOTE]
> Em Janeiro de 2017, Olá suportados forma de envio de registos de grupos de segurança de rede e Gateways de aplicação tooLog que Analytics foi alterado. Se vir Olá **análise de rede do Azure (preterido)** solução, consulte demasiado[migrar de solução de análise de redes de antiga Olá](#migrating-from-the-old-networking-analytics-solution) para obter os passos precisa de toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Reveja os detalhes de recolha de dados de rede do Azure
análise de Gateway de aplicação do Azure Olá e soluções de gestão de análise de grupo de segurança de rede Olá recolher registos de diagnóstico diretamente a partir de grupos de segurança de rede e Gateways de aplicação do Azure. Não é necessário toowrite Olá registos tooAzure o Blob storage e sem agente é necessário para a recolha de dados.

Olá tabela seguinte mostra os métodos de recolha de dados e outros detalhes sobre como os dados são recolhidos para análise do grupo de segurança de rede de Olá e de análise de Gateway de aplicação do Azure.

| Plataforma | Direcionar o agente | Agente do System Center Operations Manager de sistemas | Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |Quando tem sessão iniciada |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Solução de análise do Gateway de aplicação do Azure na análise de registos

![Símbolo de análise de Gateway de aplicação do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Olá seguintes os registos é suportada para Gateways de aplicação:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Olá métricas a seguir é suportada para Gateways de aplicação:

* débito de 5 minutos

### <a name="install-and-configure-hello-solution"></a>Instalar e configurar a solução de Olá
Utilizar Olá seguir instruções tooinstall e configure a solução de análise do Gateway de aplicação do Azure Olá:

1. Ativar a solução de análise do Gateway de aplicação do Azure Olá de [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).
2. Ativar o registo de diagnóstico de Olá [Gateways de aplicação](../application-gateway/application-gateway-diagnostics.md) pretende toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Ativar o diagnóstico do Gateway de aplicação do Azure no portal de Olá

1. No portal do Azure Olá, navegue toomonitor de recurso do Gateway de aplicação toohello
2. Selecione *registos de diagnóstico* Olá tooopen seguir página

   ![imagem de recurso de Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Clique em *ative os diagnósticos* Olá tooopen seguir página

   ![imagem de recurso de Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. Clique em tooturn diagnósticos, *no* em *Estado*
5. Clique em Olá caixa de verificação *enviar tooLog análise*
6. Selecione uma área de trabalho de análise de registos existente ou crie uma área de trabalho
7. Clique em Olá caixa de verificação em **registo** para cada um dos Olá registo tipos toocollect
8. Clique em *guardar* tooenable o registo de Olá de diagnóstico tooLog análise

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Ativar o diagnóstico de rede do Azure com o PowerShell

Olá seguinte script do PowerShell fornece um exemplo de como tooenable diagnóstico de registo para gateways de aplicação.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Utilize a análise de Gateway de aplicação do Azure
![imagem do Gateway de aplicação do Azure mosaico de análise](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Depois de clicar em Olá **análise de Gateway de aplicação do Azure** mosaico Olá descrição geral, pode ver resumos dos seus registos e depois pormenorize em toodetails para Olá seguintes categorias:

* Os registos de acesso de Gateway de aplicação
  * Erros de cliente e servidor para os registos de acesso do Gateway de aplicação
  * Pedidos por hora para cada Gateway de aplicação
  * Falha de pedidos por hora para cada Gateway de aplicação
  * Erros pelo agente de utilizador para Gateways de aplicação
* Desempenho do Gateway de aplicação
  * Estado de funcionamento do anfitrião para o Gateway de aplicação
  * Pedidos falhados de percentil máximo e 95th para Gateway de aplicação

![imagem do dashboard de análise do Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagem do dashboard de análise do Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

No Olá **análise de Gateway de aplicação do Azure** dashboard, reveja as informações de resumo de Olá dos painéis de Olá e, em seguida, clique numa tooview informações detalhadas sobre a página de pesquisa de registo de Olá.

Em qualquer uma das páginas de pesquisa de registo Olá, pode ver os resultados por tempo, os resultados detalhados e o histórico de pesquisa de registo. Também pode filtrar por resultados de Olá facetas toonarrow.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Solução de análise do grupo de segurança de rede do Azure na análise de registos

![Símbolo de análise do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Olá seguintes os registos é suportada para grupos de segurança de rede:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Instalar e configurar a solução de Olá
Utilizar Olá seguir instruções tooinstall e configure a solução de análise de redes do Azure Olá:

1. Ativar a solução de análise do grupo de segurança de rede de Azure Olá de [do Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).
2. Ativar o registo de diagnóstico de Olá [grupo de segurança de rede](../virtual-network/virtual-network-nsg-manage-log.md) recursos que pretende toomonitor.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Ativar o diagnóstico de grupo de segurança de rede do Azure no portal de Olá

1. No portal do Azure Olá, navegue toomonitor de recursos do grupo de segurança de rede toohello
2. Selecione *registos de diagnóstico* Olá tooopen seguir página

   ![imagem de recurso do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Clique em *ative os diagnósticos* Olá tooopen seguir página

   ![imagem de recurso do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. Clique em tooturn diagnósticos, *no* em *Estado*
5. Clique em Olá caixa de verificação *enviar tooLog análise*
6. Selecione uma área de trabalho de análise de registos existente ou crie uma área de trabalho
7. Clique em Olá caixa de verificação em **registo** para cada um dos Olá registo tipos toocollect
8. Clique em *guardar* tooenable o registo de Olá de diagnóstico tooLog análise

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Ativar o diagnóstico de rede do Azure com o PowerShell

Olá seguinte script do PowerShell fornece um exemplo de como tooenable diagnóstico de registo para grupos de segurança de rede
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Análise de grupo de segurança de rede de Azure de utilização
Depois de clicar em Olá **análise do grupo de segurança de rede de Azure** mosaico Olá descrição geral, pode ver resumos dos seus registos e depois pormenorize em toodetails para Olá seguintes categorias:

* Grupo de segurança de rede bloqueado fluxos
  * Regras de grupo de segurança de rede com fluxos de bloqueados
  * Endereços MAC com fluxos bloqueados
* Grupo de segurança de rede permitido fluxos
  * Regras de grupo de segurança de rede com fluxos permitidos
  * Endereços MAC com fluxos permitidos

![imagem do dashboard de análise do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagem do dashboard de análise do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

No Olá **análise do grupo de segurança de rede de Azure** dashboard, reveja as informações de resumo de Olá dos painéis de Olá e, em seguida, clique numa tooview informações detalhadas sobre a página de pesquisa de registo de Olá.

Em qualquer uma das páginas de pesquisa de registo Olá, pode ver os resultados por tempo, os resultados detalhados e o histórico de pesquisa de registo. Também pode filtrar por resultados de Olá facetas toonarrow.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Migrar a partir de solução de análise de redes de antiga Olá
Em Janeiro de 2017, Olá suportados forma de envio de registos de Gateways de aplicação do Azure e os grupos de segurança de rede do Azure tooLog que Analytics foi alterado. Estas alterações fornecem Olá seguintes vantagens:
+ Os registos são escritos diretamente tooLog análise sem Olá necessário toouse uma conta de armazenamento
+ A menor latência de tempo de Olá quando os registos são gerados toothem estejam disponíveis no Log Analytics
+ Menos passos de configuração
+ Um formato comum para todos os tipos de diagnóstico do Azure

Olá toouse atualizado soluções:

1. [Configurar toobe de diagnóstico enviado diretamente tooLog análise dos Gateways de aplicação do Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Configurar toobe de diagnóstico enviado tooLog análise diretamente a partir de grupos de segurança de rede do Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Ativar Olá *análise de Gateway de aplicação do Azure* e Olá *análises de grupo de segurança de rede de Azure* solução utilizando Olá processo descrito no [soluções de análise de registos de adicionar de Olá Galeria de soluções](log-analytics-add-solutions.md)
3. Atualizar qualquer consultas guardadas, dashboards ou alertas toouse Olá novo tipo de dados
  + O tipo é tooAzureDiagnostics. Pode utilizar Olá ResourceType toofilter tooAzure rede os registos de.

    | Em vez de: | Utilização: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Para qualquer campo que têm um sufixo de \_s, \_d, ou \_g no nome de Olá, alteração Olá primeiro caráter toolower maiúsculas e minúsculas
   + Para qualquer campo que têm um sufixo de \_Nã no nome, dados de Olá é dividido em campos individuais com base nos nomes de campo Olá aninhado.
4. Remover Olá *redes a análise do Azure (preterido)* solução.
  + Se estiver a utilizar o PowerShell, utilize`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Recolher os dados antes de alteração de Olá não estiver visível na solução nova Olá. Pode continuar tooquery para esta utilizando dados Olá tipo antigo e nomes de campo.

## <a name="troubleshooting"></a>Resolução de problemas
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados de diagnóstico do Azure.
