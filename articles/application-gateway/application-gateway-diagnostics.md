---
title: "aaaMonitor acesso registos, registos de desempenho, estado de funcionamento de back-end e métricas de Gateway de aplicação | Microsoft Docs"
description: "Saiba como tooenable e gerir registos de acesso e registos de desempenho para o Gateway de aplicação"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Estado de funcionamento de back-end, os registos de diagnóstico e métricas de Gateway de aplicação

Ao utilizar o Gateway de aplicação do Azure, pode monitorizar recursos Olá seguintes formas:

* [Estado de funcionamento de back-end](#back-end-health): Gateway de aplicação fornece Olá capacidade toomonitor Olá estado de funcionamento dos servidores Olá Olá conjuntos de back-end através de Olá portal do Azure e através do PowerShell. Também pode encontrar o estado de funcionamento de Olá dos conjuntos de back-end Olá através de registos de diagnóstico de desempenho de Olá.

* [Os registos](#diagnostic-logs): permitir que os registos de desempenho, o acesso, e outro dados toobe guardado ou consumido de um recurso para efeitos de monitorização.

* [Métricas](#metrics): Gateway de aplicação não tem atualmente uma métrica. Esta métrica mede o débito de Olá Olá do gateway de aplicação em bytes por segundo.

## <a name="back-end-health"></a>Estado de funcionamento de back-end

Gateway de aplicação fornece Olá capacidade toomonitor Olá estado de funcionamento dos membros individuais dos conjuntos de back-end Olá através do portal de Olá, PowerShell e Olá interface de linha de comandos (CLI). Também pode encontrar um Estado de funcionamento agregado resumo dos conjuntos de back-end através de registos de diagnóstico de desempenho de Olá. 

relatório de estado de funcionamento de back-end Olá reflete a saída de Olá de instâncias de Olá estado de funcionamento do Gateway de aplicação toohello de sonda back-end. Quando pesquisar é bem-sucedido e Olá novamente fim pode receber tráfego, é considerado em bom estado. Caso contrário, considera-se danificado.

> [!IMPORTANT]
> Se existir um grupo de segurança de rede (NSG) numa sub-rede de Gateway de aplicação, abra a intervalos de portas 65503 65534 na sub-rede de Gateway de aplicação Olá para tráfego de entrada. Estas portas são necessárias para toowork de API do Estado de funcionamento de back-end Olá.


### <a name="view-back-end-health-through-hello-portal"></a>Ver estado de funcionamento de back-end através do portal Olá

No portal de Olá, estado de funcionamento de back-end é fornecido automaticamente. Num gateway de aplicação existente, selecione **monitorização** > **estado de funcionamento de back-end**. 

Cada membro do conjunto de back-end Olá está listado nesta página (quer seja um NIC, IP ou FQDN). Nome do conjunto de back-end, porta, o nome de definições HTTP de back-end e estado de funcionamento são apresentadas. Os valores válidos para o estado de funcionamento são **bom estado de funcionamento**, **mau estado de funcionamento**, e **desconhecido**.

> [!NOTE]
> Se vir um Estado de funcionamento de back-end das **desconhecido**, certifique-se de que esse acesso toohello back-end não está bloqueado por uma regra NSG, uma rota definida pelo utilizador (UDR) ou um DNS na rede virtual Olá personalizado.

![Estado de funcionamento de back-end][10]

### <a name="view-back-end-health-through-powershell"></a>Ver estado de funcionamento de back-end através do PowerShell

Olá código do PowerShell a seguir mostra como o estado de funcionamento do tooview back-end utilizando Olá `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Ver estado de funcionamento de back-end através do Azure CLI 2.0

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Resultados

Olá fragmento a seguir mostra um exemplo de resposta Olá:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Registos de diagnóstico

Pode utilizar diferentes tipos de registos do Azure toomanage e resolver problemas de gateways de aplicação. Pode aceder a algumas destes registos através do portal Olá. Todos os registos podem ser extraídos de Blob storage do Azure e visualizados em diferentes ferramentas, tal como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e o Power BI. Pode saber mais sobre Olá diferentes tipos de registos de Olá lista a seguir:

* **Registo de atividade**: pode utilizar [registos de atividade do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecido como registos de auditoria e registos operacionais) tooview todas as operações que são submetidos tooyour subscrição do Azure e o respetivo estado. Entradas de registo de atividade são recolhidas por predefinição, e pode visualizá-los no Olá portal do Azure.
* **Registo de acesso**: pode utilizar este padrões de acesso de Gateway de aplicação do registo tooview e analisar informações importantes, incluindo Olá invocadora IP, URL pedido, latência de resposta, código de retorno e bytes e terminar. Um registo de acesso é recolhido a cada 300 segundos. Este registo contém um registo por instância de Gateway de aplicação. instância de Gateway de aplicação Olá pode ser identificada pela propriedade de instanceId Olá.
* **Registo de desempenho**: pode utilizar este tooview de registo como instâncias de Gateway de aplicação estiver a efetuar. Este registo captura informações de desempenho para cada instância, incluindo o total de pedidos servidos, débito em bytes, total de pedidos servidos, contagem de pedidos falhados e contagem de instâncias de back-end de bom estado de funcionamento e mau estado de funcionamento. Um registo de desempenho é recolhido a cada 60 segundos.
* **Registo de firewall**: pode utilizar este tooview Olá gerar pedidos de registo que são registados através do modo de deteção ou prevenção de um gateway de aplicação que está configurado com firewall de aplicações web Olá.

> [!NOTE]
> Estão disponíveis apenas para os recursos implementados no modelo de implementação Azure Resource Manager Olá registos. Não é possível utilizar os registos de recursos no modelo de implementação clássica Olá. Para uma melhor compreensão dos modelos de Olá dois, consulte Olá [Gestor de recursos de compreender implementação clássica e](../azure-resource-manager/resource-manager-deployment-model.md) artigo.

Tem três opções para armazenar os registos:

* **Conta de armazenamento**: contas do Storage são melhor utilizadas para os registos quando os registos são armazenados durante um longo período de tempo e revistos quando necessário.
* **Os Event hubs**: os Event hubs são uma excelente opção para integrar com outras informações de segurança e alertas tooget nos seus recursos de ferramentas de gestão de eventos (SEIM).
* **Análise de registo**: análise de registos melhor é utilizada para a monitorização em tempo real gerais da sua aplicação ou ao procurar tendências.

### <a name="enable-logging-through-powershell"></a>Ativar o registo através do PowerShell

Registo de atividade é ativado automaticamente para todos os recursos do Resource Manager. Tem de ativar o acesso e o desempenho toostart de registo a recolher dados de Olá disponíveis através desses registos. tooenable registo Olá utilize os seguintes passos:

1. Tenha em atenção o ID de recurso da sua conta do storage, onde os dados de registo Olá estão armazenados. Este valor é o formato de Olá: /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Storage/storageAccounts/\<denomedecontadostorage\>. Pode utilizar qualquer conta de armazenamento na sua subscrição. Pode utilizar estas informações a Olá toofind portal do Azure.

    ![Portal: ID de recurso conta de armazenamento](./media/application-gateway-diagnostics/diagnostics1.png)

2. Tenha em atenção o ID de recurso do gateway de aplicação para o qual o registo está ativado. Este valor é o formato de Olá: /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Network/applicationGateways/\<gateway de aplicação nome\>. Pode utilizar toofind portal Olá estas informações.

    ![Portal: ID de recurso para o gateway de aplicação](./media/application-gateway-diagnostics/diagnostics2.png)

3. Ative o registo de diagnóstico utilizando Olá seguinte cmdlet do PowerShell:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Registos de atividade não necessitam de uma conta de armazenamento separada. utilização de Olá de armazenamento de acesso e o registo de desempenho incorreu encargos de serviço.

### <a name="enable-logging-through-hello-azure-portal"></a>Ativar o registo através de Olá portal do Azure

1. No Olá portal do Azure, localizar o recurso e clique em **registos de diagnóstico**.

   Gateway de aplicação, estão disponíveis três registos:

   * Registo de acesso
   * Registo de desempenho
   * Registo de firewall

2. recolher dados de toostart, clique em **ative os diagnósticos**.

   ![Ativar o diagnóstico][1]

3. Olá **as definições de diagnóstico** painel fornece definições de Olá para Olá os registos de diagnóstico. Neste exemplo, análise de registos armazena Olá registos. Clique em **configurar** em **Log Analytics** tooconfigure sua área de trabalho. Também pode utilizar um armazenamento conta toosave Olá os registos de diagnóstico e hubs de eventos.

   ![Iniciar o processo de configuração de Olá][2]

4. Escolha uma área de trabalho do Operations Management Suite (OMS) existente ou crie um novo. Este exemplo utiliza um existente.

   ![Opções para áreas de trabalho do OMS][3]

5. Confirme as definições de Olá e clique em **guardar**.

   ![Painel de definições de diagnóstico com seleções][4]

### <a name="activity-log"></a>Registo de atividades

Por predefinição, o Azure gera o registo de atividade Olá. Olá registos são preservados durante 90 dias no arquivo de registos de eventos do Azure Olá. Saiba mais sobre estes registos o lendo Olá [ver eventos e registo de atividade](../monitoring-and-diagnostics/insights-debugging-with-events.md) artigo.

### <a name="access-log"></a>Registo de acesso

registo de acesso de Olá é gerado apenas se tiver ativado, cada instância de Gateway de aplicação, conforme detalhado em Olá precedente passos. dados de Olá são armazenados na conta do storage Olá que especificou quando ativou o registo de Olá. Cada acesso do Gateway de aplicação é registado no formato JSON, conforme mostrado no seguinte exemplo de Olá:


|Valor  |Descrição  |
|---------|---------|
|instanceId     | Esse pedido Olá servidos de instância de Gateway de aplicação.        |
|ClientIP     | IP de origem para o pedido de Olá.        |
|clientPort     | Porta de origem para o pedido de Olá.       |
|httpMethod     | Método HTTP utilizado pelo pedido de Olá.       |
|requestUri     | URI de Olá recebeu o pedido.        |
|RequestQuery     | **Encaminhados por servidor**: instância de conjunto de Back-end que lhe foi enviada o pedido de Olá. </br> **X-AzureApplicationGateway-registo-ID**: ID de correlação utilizada Olá pedido. Pode ser utilizado tootroubleshoot tráfego problemas em servidores de back-end Olá. </br>**Estado do servidor**: código de resposta HTTP recebido de Gateway de aplicação de back-end Olá.       |
|UserAgent     | Agente de utilizador do cabeçalho de pedido de Olá HTTP.        |
|httpStatus     | Código de estado HTTP devolvido toohello cliente do Gateway de aplicação.       |
|httpVersion     | Versão HTTP do pedido de Olá.        |
|receivedBytes     | Tamanho do pacote recebido, em bytes.        |
|sentBytes| Tamanho do pacote enviado, em bytes.|
|timeTaken| Período de tempo (em milissegundos) que leva uma toobe de pedidos processados e respetivos toobe resposta enviada. Esta é calculada como Olá início do intervalo tempo Olá quando o Gateway de aplicação recebe primeiro byte de Olá de um tempo de toohello de pedido HTTP quando resposta Olá enviar a operação depois de concluída. É importante toonote Olá Time-Taken campo normalmente inclui o tempo de Olá que pacotes hello a pedido e resposta são estiverem em deslocação rede Olá. |
|sslEnabled| Indica se os conjuntos de back-end de toohello de comunicação utilizados SSL. Os valores válidos são e desativar.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Registo de desempenho

registo de desempenho de Olá é gerado apenas se tiver ativado, cada instância de Gateway de aplicação, conforme detalhado em Olá precedente passos. dados de Olá são armazenados na conta do storage Olá que especificou quando ativou o registo de Olá. dados de registo de desempenho de Olá são gerados em intervalos de 1 minuto. é registado Olá dados os seguintes:


|Valor  |Descrição  |
|---------|---------|
|instanceId     |  Instância de Gateway de aplicação para o desempenho de dados está a ser gerados. Para um gateway de aplicação de várias instâncias, há uma linha por instância.        |
|healthyHostCount     | Número de anfitriões bom estado de funcionamento no conjunto de back-end Olá.        |
|unHealthyHostCount     | Número de anfitriões mau estado de funcionamento no conjunto de back-end Olá.        |
|requestCount     | Número de pedidos servidos.        |
|latência | Latência (em milissegundos) de pedidos do Olá instância toohello back-end que serve Olá pedidos. |
|failedRequestCount| Número de pedidos falhados.|
|Débito| Débito médio desde o registo do último Olá, medido em bytes por segundo.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Latência é calculada a partir de tempo de Olá ao primeiro byte de Olá de pedido de Olá HTTP está na altura de recebida toohello último byte de Olá de Olá resposta de HTTP é enviado. Olá, de Olá soma do tempo de processamento de Gateway de aplicação plus hello rede custo toohello novamente terminar, juntamente com a hora de Olá Olá back-end demora tooprocess Olá pedido.

### <a name="firewall-log"></a>Registo de firewall

registo de firewall de Olá é gerado apenas se tiver ativado-la para cada gateway de aplicação, conforme detalhado em Olá precedente passos. Este registo também requer que firewall de aplicações web Olá está configurado num gateway de aplicação. dados de Olá são armazenados na conta do storage Olá que especificou quando ativou o registo de Olá. é registado Olá dados os seguintes:


|Valor  |Descrição  |
|---------|---------|
|instanceId     | Instância de Gateway de aplicação para que firewall dados está a ser gerados. Para um gateway de aplicação de várias instâncias, há uma linha por instância.         |
|clientIp     |   IP de origem para o pedido de Olá.      |
|clientPort     |  Porta de origem para o pedido de Olá.       |
|requestUri     | URL do pedido recebido Olá.       |
|ruleSetType     | Tipo de conjunto de regras. o valor disponível Olá é OWASP.        |
|ruleSetVersion     | O conjunto de regras de versão utilizada. Os valores disponíveis são 2.2.9 e 3.0.     |
|ruleId     | ID de regra de Olá acionar eventos.        |
|Mensagem     | Mensagem amigável de utilizador para acionar eventos de Olá. Obter mais detalhes são fornecidos na secção de detalhes de Olá.        |
|Ação     |  Ação tomada pedido Olá. Os valores disponíveis são bloqueado e permitido.      |
|site     | Site para os qual Olá registo foi gerado. Atualmente, apenas Global está listado porque as regras são globais.|
|Detalhes     | Detalhes de Olá acionar eventos.        |
|details.Message     | Descrição da regra de Olá.        |
|details.data     | Dados específicos encontradas pedido dessa regra Olá correspondentes.         |
|details.File     | Ficheiro de configuração que continha regra Olá.        |
|details.line     | Número de linha no ficheiro de configuração de Olá que acionou o evento de Olá.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Ver e analisar o registo de atividade Olá

Pode ver e analisar dados de registo de atividade, utilizando qualquer um dos seguintes métodos de Olá:

* **Ferramentas do Azure**: obter as informações do registo de atividade Olá através do Azure PowerShell, Olá CLI do Azure, Olá API de REST do Azure, ou Olá portal do Azure. Instruções passo a passo para cada método passo são detalhadas no Olá [operações de atividade com o Resource Manager](../azure-resource-manager/resource-group-audit.md) artigo.
* **Power BI**: Se ainda não tiver um [Power BI](https://powerbi.microsoft.com/pricing) conta, pode experimentar, gratuitamente. Ao utilizar Olá [conteúdo de registos de atividade do Azure pack para o Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), pode analisar os dados com dashboards pré-configuradas que podem ser utilizados como está, ou personalizar.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Ver e analisar registos de firewall, desempenho e acesso de Olá

Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) pode recolher ficheiros de registo de eventos e contadores de Olá da sua conta de armazenamento de Blobs. Inclui as visualizações e tooanalyze de capacidades de pesquisa poderosas os seus registos.

Também pode ligar-se a conta de armazenamento tooyour e obter entradas de registo Olá JSON para os registos de acesso e o desempenho. Depois de transferir ficheiros JSON Olá, pode convertê-los tooCSV e visualizá-los no Excel, Power BI ou qualquer outra ferramenta de visualização de dados.

> [!TIP]
> Se estiver familiarizado com conceitos básicos do alterar os valores de constantes e variáveis em c# e o Visual Studio, pode utilizar Olá [iniciar ferramentas de conversor](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis a partir do GitHub.
> 
> 

## <a name="metrics"></a>Métricas

As métricas são uma funcionalidade de certos recursos do Azure, onde pode ver os contadores de desempenho no portal de Olá. Gateway de aplicação, uma métrica está actualmente disponível. Esta métrica é o débito e pode vê-lo no portal de Olá. Procurar tooan gateway de aplicação e clique em **métricas**. os valores de Olá tooview, selecione de débito no Olá **as métricas disponíveis** secção. Olá seguinte imagem, pode ver um exemplo com filtros de Olá que pode utilizar dados de Olá toodisplay em intervalos de tempo diferente.

![Vista de métrica com filtros][5]

toosee uma lista atual de métricas, consulte [suportado métricas com a monitorização do Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Regras de alertas

Pode começar a regras de alertas com base nas métricas para um recurso. Por exemplo, um alerta pode chamar um webhook ou um administrador de e-mail, se o débito de Olá Olá do gateway de aplicação é acima, abaixo ou com um limiar durante um período especificado.

Olá seguinte exemplo explica-lhe criar uma regra de alerta que envia um administrador de tooan e-mail depois de falhas de débito um limiar:

1. Clique em **Adicionar alerta métrica** tooopen Olá **Adicionar regra** painel. Também pode contactar este painel a partir do painel de métricas de Olá.

   ![Botão "Adicionar alerta métrica"][6]

2. No Olá **Adicionar regra** painel, preencha o nome de Olá, condição, notificar secções e clique em **OK**.

   * No Olá **condição** Seletor, selecione um dos valores de Olá quatro: **maior**, **igual ou maior do que**, **menor**, ou  **Menor ou igual a**.

   * No Olá **período** Seletor, selecione um período de 5 minutos too6 horas.

   * Se selecionar **proprietários, contribuintes e leitores de E-Mail**, e-mail Olá pode ser dinâmica com base nos utilizadores de Olá que tenham acesso toothat recursos. Caso contrário, pode fornecer uma lista separada por vírgulas de utilizadores de Olá **administrador adicionais email(s)** caixa.

   ![Adicionar o painel de regra][7]

Se o limiar de Olá é quebrado, chega uma mensagem de e-mail que é semelhante toohello um no Olá seguinte imagem:

![Correio eletrónico para o limiar infringido][8]

É apresentada uma lista de alertas depois de criar um alerta de métrico. Fornece uma descrição geral de todas as regras de alerta de Olá.

![Lista de alertas e regras][9]

toolearn mais informações sobre notificações de alertas, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand mais informações sobre webhooks e como pode utilizá-los com alertas, visite [configurar um webhook num alerta métrico Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Passos seguintes

* Visualizar registos de eventos e contadores utilizando [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).
* [Visualizar o registo de atividade do Azure com Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogue.
* [Ver e analisar registos de atividade do Azure no Power BI e muito mais](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogue.

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
