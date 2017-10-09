---
title: "aaaAzure solução Cofre de chaves no Log Analytics | Microsoft Docs"
description: "Pode utilizar a solução do Cofre de chaves do Azure de Olá no tooreview de análise de registos que registos do Cofre de chaves do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Soluções de análise do Cofre de chaves do Azure na análise de registos

![Símbolo do Cofre de chaves](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Pode utilizar solução Cofre de chaves do Azure de Olá tooreview de análise de registos do Azure chave de cofre AuditEvent registos.

solução de Olá toouse, terá de tooenable o registo de diagnóstico do Cofre de chaves do Azure e Olá direta a área de trabalho de análise de registos de tooa do diagnóstico. Não é necessário toowrite Olá registos tooAzure o Blob storage.

> [!NOTE]
> Em Janeiro de 2017, Olá suportados forma de envio de registos da tooLog Cofre de chaves que Analytics foi alterado. Mostra se a solução do Cofre de chaves de Olá estiver a utilizar *(preterido)* título Olá, referem-se demasiado[migrar da solução de Cofre de chaves antiga Olá](#migrating-from-the-old-key-vault-solution) para obter os passos precisa de toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Instalar e configurar a solução de Olá
Utilizar Olá seguir instruções tooinstall e configure a solução do Cofre de chaves do Azure de Olá:

1. Ativar a solução do Cofre de chaves do Azure Olá de [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).
2. Ativar o diagnóstico de registo para toomonitor de recursos do Cofre de chaves Olá, utilizando qualquer um dos Olá [portal](#enable-key-vault-diagnostics-in-the-portal) ou [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Ativar o diagnóstico do Cofre de chaves no portal de Olá

1. No portal do Azure Olá, navegue toomonitor de recurso do Cofre de chaves toohello
2. Selecione *registos de diagnóstico* Olá tooopen seguir página

   ![imagem de mosaico do Cofre de chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Clique em *ative os diagnósticos* Olá tooopen seguir página

   ![imagem de mosaico do Cofre de chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. Clique em tooturn diagnósticos, *no* em *Estado*
5. Clique em Olá caixa de verificação *enviar tooLog análise*
6. Selecione uma área de trabalho de análise de registos existente ou crie uma área de trabalho
7. tooenable *AuditEvent* registos, clique em Olá caixa de verificação em registo
8. Clique em *guardar* tooenable o registo de Olá de diagnóstico tooLog análise

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Ativar o diagnóstico do Cofre de chaves utilizando o PowerShell
Olá seguinte script do PowerShell fornece um exemplo de como toouse `Set-AzureRmDiagnosticSetting` tooenable diagnóstico de registo para o Cofre de chaves:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Reveja os detalhes de recolha de dados do Cofre de chaves do Azure
Solução do Cofre de chaves do Azure recolhe registos de diagnóstico diretamente a partir de Olá Cofre de chaves.
Não é necessário toowrite Olá registos tooAzure o Blob storage e sem agente é necessário para a recolha de dados.

Olá tabela seguinte mostra os métodos de recolha de dados e outros detalhes sobre como os dados são recolhidos para o Cofre de chaves do Azure.

| Plataforma | Direcionar o agente | Agente do System Center Operations Manager de sistemas | Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | sobre chegada |

## <a name="use-azure-key-vault"></a>Utilizar o Azure Key Vault
Depois de [instalar Olá solução](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), ver os dados do Cofre de chaves de Olá clicando Olá **Cofre de chaves do Azure** mosaico de Olá **descrição geral** página de análise de registos.

![imagem de mosaico do Cofre de chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Depois de clicar em Olá **descrição geral** mosaico, pode ver resumos dos seus registos e, em seguida, explore no toodetails para Olá seguintes categorias:

* Volume de todas as operações do Cofre de chaves ao longo do tempo
* Falha de volumes de operação ao longo do tempo
* Latência média de operacional operação
* Qualidade de serviço para as operações com o número de Olá de operações que demorar mais de 1000 ms e uma lista de operações que demorar mais de 1000 ms

![imagem do dashboard do Cofre de chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![imagem do dashboard do Cofre de chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>detalhes de tooview em nenhuma operação
1. No Olá **descrição geral** página, clique em Olá **Cofre de chaves do Azure** mosaico.
2. No Olá **Cofre de chaves do Azure** dashboard, reveja as informações de resumo de Olá dos painéis de Olá e, em seguida, clique numa tooview informações detalhadas sobre-la na página de pesquisa de registo Olá.

    Em qualquer uma das páginas de pesquisa de registo Olá, pode ver os resultados por tempo, os resultados detalhados e o histórico de pesquisa de registo. Também pode filtrar por resultados de Olá facetas toonarrow.

## <a name="log-analytics-records"></a>Registos do Log Analytics
Olá solução Cofre de chaves do Azure analisa os registos que tenham um tipo de **KeyVaults** que são recolhidos de [AuditEvent registos](../key-vault/key-vault-logging.md) no diagnóstico do Azure.  Propriedades para estes registos são no Olá a tabela seguinte:  

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*AzureDiagnostics* |
| SourceSystem |*Azure* |
| CallerIpAddress |Endereço IP do cliente de Olá que efetuou o pedido de Olá |
| Categoria | *AuditEvent* |
| CorrelationId |Um GUID opcional que hello do cliente pode passar toocorrelate registos do lado do cliente com os registos do lado do serviço (Cofre de chaves). |
| DurationMs |Tempo que demorou pedido de REST API do tooservice Olá, em milissegundos. Neste momento não inclui a latência de rede, para que o tempo de Olá que medir do lado do cliente de Olá poderá não corresponder a este período de tempo. |
| httpStatusCode_d |Código de estado HTTP devolvido pelo pedido de Olá (por exemplo, *200*) |
| id_s |ID exclusivo do pedido de Olá |
| identity_claim_appid_g | GUID para o id da aplicação Olá |
| OperationName |Nome de operação de Olá, conforme documentado no [registo do Cofre de chaves do Azure](../key-vault/key-vault-logging.md) |
| OperationVersion |Versão de REST API solicitada pelo cliente de Olá (por exemplo *2015-06-01*) |
| requestUri_s |URI de pedido de Olá |
| Recurso |Nome do Cofre de chaves Olá |
| ResourceGroup |Grupo de recursos do Cofre de chaves Olá |
| ResourceId |ID do Recurso do Azure Resource Manager Para os registos do Cofre de chaves, este é o ID de recurso do Olá Cofre de chaves. |
| ResourceProvider |*MICROSOFT. KEYVAULT* |
| ResourceType | *COFRES* |
| ResultSignature |Estado de HTTP (por exemplo, *OK*) |
| ResultType |Resultado do pedido de REST API (por exemplo, *êxito*) |
| SubscriptionId |ID de subscrição do Azure da subscrição Olá contendo Olá Cofre de chaves |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Migrar a partir de solução de Cofre de chaves antiga Olá
Em Janeiro de 2017, Olá suportados forma de envio de registos da tooLog Cofre de chaves que Analytics foi alterado. Estas alterações fornecem Olá seguintes vantagens:
+ Os registos são escritos diretamente tooLog análise sem Olá necessário toouse uma conta de armazenamento
+ A menor latência de tempo de Olá quando os registos são gerados toothem estejam disponíveis no Log Analytics
+ Menos passos de configuração
+ Um formato comum para todos os tipos de diagnóstico do Azure

Olá toouse atualizado solução:

1. [Configurar toobe de diagnóstico enviado diretamente tooLog análise do Cofre de chaves](#enable-key-vault-diagnostics-in-the-portal)  
2. Ativar a solução do Olá Cofre de chaves do Azure utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá Galeria de soluções](log-analytics-add-solutions.md)
3. Atualizar qualquer consultas guardadas, dashboards ou alertas toouse Olá novo tipo de dados
  + Tipo é alterar de: KeyVaults tooAzureDiagnostics. Pode utilizar Olá ResourceType toofilter tooKey registos do cofre.
  - Em vez de: `Type=KeyVaults`, utilize`Type=AzureDiagnostics ResourceType=VAULTS`
  + Campos: (nomes de campo são sensível a maiúsculas e minúsculas)
  - Para qualquer campo que têm um sufixo de \_s, \_d, ou \_g no nome de Olá, alteração Olá primeiro caráter toolower maiúsculas e minúsculas
  - Para qualquer campo que têm um sufixo de \_Nã no nome, dados de Olá é dividido em campos individuais com base nos nomes de campo Olá aninhado. Por exemplo, Olá UPN do autor da chamada Olá é armazenado num campo`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - TooCallerIPAddress CallerIpAddress campo alterado
   - Campo RemoteIPCountry já não está presente
4. Remover Olá *análise do Cofre de chave (preterido)* solução. Se estiver a utilizar o PowerShell, utilize`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Recolher os dados antes de alteração de Olá não estiver visível na solução nova Olá. Pode continuar tooquery para esta utilizando dados Olá tipo antigo e nomes de campo.

## <a name="troubleshooting"></a>Resolução de problemas
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados do Cofre de chaves do Azure.
