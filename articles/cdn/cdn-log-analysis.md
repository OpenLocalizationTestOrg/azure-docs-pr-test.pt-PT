---
title: "análise de aaaLog para o Azure CDN | Microsoft Docs"
description: "Cliente pode ativar a análise de registos para a CDN do Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Registos de diagnóstico para a CDN do Azure

Depois de ativar a CDN para a sua aplicação, irá provavelmente pretender a utilização CDN toomonitor Olá, verifique o estado de funcionamento de Olá do seu entrega e resolver problemas potenciais problemas. CDN do Azure fornece mais capacidades com [análise de núcleo de CDN](cdn-analyze-usage-patterns.md) e [os registos de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>Análise de núcleo CDN
Como um utilizador CDN do Azure atual com o perfil de premium ou standard da Verizon, já estiver tooview capaz de análise de núcleo no portal suplementar Olá acessível através da opção de "Gerir" Olá da Olá portal do Azure. 

## <a name="azure-diagnostic-logs"></a>Registos de diagnóstico do Azure

O Azure com esta nova funcionalidade, pode agora ver análise de núcleo e guardá-las para um ou mais destinos, incluindo:

 - Conta de armazenamento do Azure
 - Azure Event Hubs
 - [Repositório de análise de registos do OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Esta funcionalidade está disponível para todos os pontos finais da CDN que pertencem tooVerizon (Standard e Premium) e perfis da CDN Akamai (Standard).

Registos de diagnóstico permitem-lhe tooexport métricas de utilização básica da sua variedade de tooa de ponto final CDN de origens de modo a que pode aceder aos mesmos de forma personalizada. Por exemplo, pode fazê-lo Olá os seguintes tipos de exportação de dados:

- Exportar o armazenamento de dados tooblob, exportar tooCSV e gerar gráficos no excel.
- Exporte os hubs de tooevent de dados e estar relacionados com a dados a partir de outros serviços do azure.
- Exportar dados toolog análise e ver dados no seu próprio espaço de trabalho do OMS

Olá figura seguinte mostra uma vista de análise de núcleo de CDN típica de dados.

![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Figura 1 - vista de análise de núcleo de CDN*

Olá seguir instruções passa pelo esquema Olá de dados de análise de núcleo Olá, os passos envolvidos na ativar a funcionalidade de Olá, entrega-los toovarious destinos e consumir nestes destinos.

## <a name="enable-logging-with-azure-portal"></a>Ativar o registo com o portal do Azure

> [!NOTE]
> Olá registos de diagnóstico são ativados **desativar** por predefinição. 

Siga os passos de Olá abaixo tooenable registo CDN Core Analytics:

Inicie sessão no toohello [portal do Azure](http://portal.azure.com). Se ainda não tiver ativado para o fluxo de trabalho CDN [ativar a CDN do Azure](cdn-create-new-endpoint.md) antes de continuar.

1. No portal de Olá, navegue até demasiado**perfil da CDN**.
2. Selecione um perfil CDN, em seguida, selecione o ponto final de CDN Olá que pretende que o tooenable **registos de diagnóstico**.

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Aceda demasiado**registos de diagnóstico** painel em **monitorização** secção, em seguida, alterar o estado de Olá demasiado**no**.

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Ativar o registo com o Storage do Azure
    
Selecione toouse Storage do Azure toostore Olá registos **arquivar a conta de armazenamento tooa**, selecione os dias de retenção e, em **CoreAnalytics** em **registo**.

![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Figura 2 - registo com o Storage do Azure*

### <a name="logging-with-oms-log-analytics"></a>Registo de análise de registos do OMS

toouse OMS registo toostore Olá pelos registos de análise, siga estes passos:

1. De Olá **registos de diagnóstico** painel em **monitorização**, selecione **enviar tooLog análise** do 

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Configure o registo de análise de registos de Olá ao clicar em configurar. Isto leva-o diálogo tooa onde pode selecionar uma área de trabalho anterior ou crie um novo.

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Clique em **criar nova área de trabalho**.

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. Em seguida, tem de selecionar um novo nome de área de trabalho, a subscrição existente, a grupo de recursos (novo ou existente), a localização e o escalão de preço. Tem de opção de Olá de afixação este dashboard de tooyour de configuração. Clique em OK toocomplete Olá configuração.

    Em seguida, deverá ver a sua área de trabalho com os nomes de grupo do OMS área de trabalho e recursos. Os nomes têm de ser exclusivos e só podem utilizar letras, números e hífenes. Não são permitidos espaços e carateres de sublinhado. 

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Junto a obter uma mensagem curta indicar que a sua área de trabalho foi criada e são devolvidos tooyour ecrã de configuração de registo. Pode confirmar o nome de Olá da sua área de trabalho de análise de registos.

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Assim que tiver configurado a configuração de análise de registos de Olá, certifique-se de que Olá CoreAnalytics caixa para o registo de CDN também de verificação.

6. Se tudo está tooyour liking, clique em Olá **guardar** botão na Olá parte superior da caixa de diálogo de configuração de Olá.

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    Olá **guardar** botão já não está ativa e esse Olá no/DESATIVAR botão está ON, mas blue em vez de roxa.

7. Se quiser toosee a nova área de trabalho do OMS, aceda tooyour portal do Azure Dashboard, clique no nome de Olá da sua área de trabalho de análise de registos. Em seguida, verá a área de trabalho (Certifique-se de que a área de trabalho OMS é realçada Olá esquerda). Clique em toosee de mosaico do Portal do OMS Olá sua área de trabalho no repositório do Olá OMS. 

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    O repositório do OMS está agora pronto toolog dados. Na ordem tooconsume esses dados, tem de utilizar um [OMS solução](#consuming-oms-log-analytics-data), abrangidas neste artigo.

Para mais informações sobre os atrasos de dados de registo, visite [aqui](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Ativar o registo com o PowerShell

Segue-se um exemplo de como tooenable e obter os registos de diagnóstico através de Olá Cmdlets do PowerShell do Azure.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Ativar o diagnóstico inicia sessão numa conta do Storage

Primeiro início de sessão e selecionar uma subscrição:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable registos de diagnóstico numa conta do Storage, utilize este comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable registos de diagnóstico na área de trabalho do OMS, utilize este comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Consumir os registos de diagnóstico do armazenamento do Azure
Esta secção descreve o esquema de Olá da análise de núcleo CDN Olá, a forma como estas estão organizados dentro de uma conta de armazenamento do Azure e fornece Olá de toodownload de código de exemplo regista no ficheiro CSV de tooa.

### <a name="using-microsoft-azure-storage-explorer"></a>Utilizar o Explorador de armazenamento do Microsoft Azure
Antes de poder aceder a dados de análise de núcleo de Olá Olá conta do Storage do Azure, primeiro precisa de uma ferramenta tooaccess Olá do conteúdo numa conta do storage. Apesar de existirem várias ferramentas disponíveis no mercado Olá, Olá que recomendamos é Olá Explorador de armazenamento do Microsoft Azure. Pode transferir a ferramenta de Olá do [aqui](http://storageexplorer.com/). Depois de transferir e instalar software Olá, configurá-lo toouse Olá a mesma conta do Storage do Azure que foi configurado como um destino toohello registos de diagnóstico da CDN.

1.  Abra **Explorador de armazenamento do Microsoft Azure**
2.  Localize a conta de armazenamento Olá
3.  Aceda toohello **"Contentores de BLOBs"** nós sob este armazenamento conta e expanda o nó de Olá
4.  Com o nome de contentor de Olá selecione **"insights-registos-coreanalytics"** e faça duplo clique
5.  Resulta Mostrar cópias de segurança no Olá painel direita começadas Olá primeiro nível, que se parece com **"resourceId ="**. Continuar a clicar em todas as forma de Olá até ver ficheiros de Olá **PT1H.json**. Consulte Olá nota para obter explicações caminho Olá a seguir.
6.  Cada blob **PT1H.json** representa hello registos de análise para uma hora para um ponto final de CDN específico ou o domínio personalizado.
7.  esquema de Olá do conteúdo Olá deste ficheiro JSON está descrita na secção Olá esquema Olá registos de análise de núcleo


> [!NOTE]
> **Formato de caminho do blob**
> 
> Registos de análise do Core são gerados a cada hora. Todos os dados para uma hora são recolhidos e armazenados no interior de um único Blob do Azure como um payload JSON. Olá caminho toothis Blob do Azure é apresentado como se houver uma estrutura hierárquica. Isto acontece porque a ferramenta de Explorador de armazenamento Olá interpreta '/' como um separador de diretório e mostra hierarquia Olá para sua comodidade. Na realidade, caminho todo Olá apenas representa o nome do blob Olá. Este nome de blob Olá segue Olá seguinte convenção de nomenclatura 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Descrição de campos:**

|valor|descrição|
|-------|---------|
|ID da subscrição    |ID do Olá subscrição do Azure. Trata-se no formato de Guid Olá.|
|Recurso |Nome do grupo de recursos CDN de Olá grupo toowhich Olá recurso pertence.|
|Nome do perfil |Nome do Olá perfil da CDN|
|Nome do ponto final |Nome do Olá ponto final de CDN|
|ano|  representação de 4 dígitos do ano Olá 2017 por exemplo,|
|Mês| representação de 2-dígitos do número de meses Olá. 01 = Janeiro... 12 = Dezembro|
|Dia|   representação de dígitos 2 do dia de Olá do mês de Olá|
|PT1H.JSON| Armazenar dados de análise Olá real do ficheiro JSON|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Exportar dados de análise de núcleo de Olá tooa ficheiro CSV

toomake it tooaccess fácil Olá análise de núcleo, iremos fornecer um código de exemplo para uma ferramenta que permite a transferência de ficheiros de JSON de Olá para um formato de ficheiro flat separados por vírgulas, que pode ser utilizado tooeasily criar gráficos ou outras agregações.

Eis como pode utilizar a ferramenta de Olá:

1.  Visite Olá github ligação: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Transferir o código de Olá
3.  Siga as instruções toocompile e configurar
4.  Execute a ferramenta de Olá
5.  Um ficheiro CSV resultante mostra os dados de análise de Olá numa hierarquia simples simple.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Consumir os registos de diagnóstico de um repositório de análise de registos do OMS
Análise de registos é um serviço no Operations Management Suite (OMS) que monitoriza o toomaintain de ambientes de nuvem e no local, disponibilidade e o desempenho. Recolhe dados gerados pelos recursos nos seus ambientes de nuvem e no local e de outro análise de tooprovide ferramentas monitorização em várias origens. 

Análise de registos toouse, tem de [ativar o registo](#enable-logging-with-azure-storage) repositório de análise de registos do Azure OMS toohello, que é abordado anteriores no artigo.

### <a name="using-hello-oms-repository"></a>Utilizar Olá repositório do OMS

 Olá diagrama a seguir mostra a arquitetura de Olá de entradas de Olá e saídas do repositório de Olá:

![Repositório de análise de registo do OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Figura 3 - repositório de análise do registo*

Pode apresentar dados Olá numa variedade de formas utilizando soluções de gestão. Pode obter as soluções de gestão de Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Pode instalar as soluções de gestão do Azure marketplace, clicando em Olá **obtê-lo agora** ligação na parte inferior de Olá de cada solução.

### <a name="adding-an-oms-cdn-management-solution"></a>Adicionar uma solução de gestão da CDN do OMS

Siga estes passos tooadd uma solução de gestão:

1.   Se ainda não o fez, inicie sessão toohello portal do Azure através da sua subscrição do Azure e aceda tooyour Dashboard.
    ![Dashboard do Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. No Olá **novo** painel em **Marketplace**, selecione **monitorização + gestão**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. No Olá **monitorização + gestão** painel, clique em **ver todos os**.

    ![Ver tudo](./media/cdn-diagnostics-log/15_See-all.png)

4.  Procure CDN na caixa de pesquisa de Olá.

    ![Ver tudo](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Selecione **análise de núcleo da CDN do Azure**. 

    ![Ver tudo](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Depois de clicar em **criar**, será pedido toocreate uma área de trabalho do OMS nova ou utilize uma já existente. 

    ![Ver tudo](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Selecione a área de trabalho Olá criado antes de. Em seguida, terá de tooadd uma conta de automatização.

    ![Ver tudo](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Olá ecrã seguinte mostra formulário de conta de automatização de Olá, terá de preencher enviados. 

    ![Ver tudo](./media/cdn-diagnostics-log/20_Automation.png)

9. Assim que tiver criado a conta de automatização Olá, está pronto tooadd sua solução. Clique em Olá **criar** botão.

    ![Ver tudo](./media/cdn-diagnostics-log/21_Ready.png)

10. A solução foi agora adicionada tooyour área de trabalho. Volte tooyour Dashboard de portal do Azure.

    ![Ver tudo](./media/cdn-diagnostics-log/22_Dashboard.png)

    Clique em área de trabalho do Log Analytics Olá criou toogo tooyour área. 

11. Clique em Olá **Portal do OMS** mosaico toosee solução nova no portal do OMS Olá.

    ![Ver tudo](./media/cdn-diagnostics-log/23_workspace.png)

12. O portal do OMS deve agora ter o seguinte aspeto Olá ecrã a seguir:

    ![Ver tudo](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Clique das Olá mosaicos toosee várias vistas sobre os seus dados.

    ![Ver tudo](./media/cdn-diagnostics-log/25_Interior-view.png)

    Pode se deslocar para a esquerda ou direita toosee ainda mais os mosaicos que representa vistas individuais em dados de Olá. 

    Clicar dos mosaicos Olá dá-lhe obter mais detalhes sobre os dados.

     ![Ver tudo](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Ofertas e escalões de preços

Pode ver ofertas e escalões de preços para soluções de gestão do OMS [aqui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Personalizar vistas

Pode personalizar vista Olá sobre os seus dados através da utilização de Olá **estruturador de vistas**. Aceda a área de trabalho do tooyour OMS e começar a estruturar clicando Olá **estruturador de vistas** mosaico.

![Estruturador de Vista](./media/cdn-diagnostics-log/27_Designer.png)

Pode arrastar e largar tipos de gráficos da esquerda Olá e preencha os detalhes de dados de Olá que pretende tooanalyze no Olá à esquerda.

![Estruturador de Vista](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Atrasos de dados de registo

Atrasos de dados de registo da Verizon | Atrasos de dados de registo Akamai
--- | ---
Dados de registo da Verizon estão atrasados 1 hora em demorar too2 horas toostart apresentação após a conclusão da propagação de ponto final. | Dados de registo da Akamai é de 24 horas atrasadas e ocupa too2 horas toostart apresentação se tiver sido criado há mais de 24 horas. Se tiver sido recentemente criado, pode demorar até too25 horas para Olá registos toostart volte a aparecer.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Tipos de registo de diagnóstico para análise de núcleo de CDN

Estamos atualmente oferecem apenas os registos de análise de núcleo, que contêm as métricas que mostra as estatísticas de resposta HTTP e estatísticas de saída, conforme visto a partir de Olá CDN POPs/contornos.

### <a name="core-analytics-metrics-details"></a>Detalhes de métricas de análise de núcleo
Olá, a tabela seguinte mostra uma lista das métricas disponíveis no Olá que os registos de análise de núcleo. Nem todas as métricas estão disponíveis de todos os fornecedores, apesar destas diferenças são mínimas. Olá, a tabela seguinte também mostra uma métrica de determinado estiver disponível a partir de um fornecedor. Tenha em atenção que as métricas de Olá estão disponíveis para apenas esses pontos finais da CDN que tenham tráfego nos mesmos.


|Métrica                     | Descrição   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Número total de pedidos de pedido durante este período| Sim  |Sim   |
| RequestCountHttpStatus2xx |Contagem de todos os pedidos que resultaram num código de HTTP 2xx (por exemplo, 200, 202)              | Sim  |Sim   |
| RequestCountHttpStatus3xx | Contagem de todos os pedidos que resultaram num código de HTTP 3xx (por exemplo, 300, 302)              | Sim  |Sim   |
| RequestCountHttpStatus4xx |Contagem de todos os pedidos que resultaram num código de HTTP 4xx (por exemplo, 400, 404)               | Sim   |Sim   |
| RequestCountHttpStatus5xx | Contagem de todos os pedidos que resultaram num código de HTTP 5xx (por exemplo, 500, 504)              | Sim  |Sim   |
| RequestCountHttpStatusOthers |  Contagem de todos os outros códigos HTTP (fora 2xx-5xx) | Sim  |Sim   |
| RequestCountHttpStatus200 | Contagem de todos os pedidos que resultaram numa resposta de código HTTP 200              |Não   |Sim   |
| RequestCountHttpStatus206 | Contagem de todos os pedidos que resultaram numa resposta código 206 HTTP              |Não   |Sim   |
| RequestCountHttpStatus302 | Contagem de todos os pedidos que resultaram numa resposta de código HTTP 302              |Não   |Sim   |
| RequestCountHttpStatus304 |  Contagem de todos os pedidos que resultaram numa resposta código 304 HTTP             |Não   |Sim   |
| RequestCountHttpStatus404 | Contagem de todos os pedidos que resultaram numa resposta de código HTTP 404              |Não   |Sim   |
| RequestCountCacheHit |Contagem de todos os pedidos que resultaram num de acertos na Cache. Isto significa que o recurso de Olá servido diretamente a partir de Olá POP toohello cliente.               | Sim  |Não   |
| RequestCountCacheMiss | Contagem de todos os pedidos que resultaram numa Cache de falha de acerto na. Isto significa que não foi encontrado no cliente de toohello mais próximo do Olá POP asset Olá e, por conseguinte, foi obtido do Olá origem.              |Sim   | Não  |
| RequestCountCacheNoCache | Contagem de todos os pedidos de recurso de tooan impedido de ser colocadas em cache devido a configuração do utilizador tooa no limite de Olá.              |Sim   | Não  |
| RequestCountCacheUncacheable | Contagem de todos os pedidos tooassets impedido de ser colocadas em cache por Cache-Control do elemento de Olá e expira cabeçalhos, o que indicam que este deve não ser colocadas em cache num POP ou pelo cliente de Olá HTTP                |Sim   |Não   |
| RequestCountCacheOthers | Contagem de todos os pedidos com o estado de cache não abrangido por acima.              |Sim   | Não  |
| EgressTotal | Transferência de dados de saída em GB              |Sim   |Sim   |
| EgressHttpStatus2xx | Dados de saída transferência * para respostas com códigos de estado HTTP 2xx em GB            |Sim   |Não   |
| EgressHttpStatus3xx | Transferência de dados de saída para as respostas com códigos de estado HTTP 3xx em GB              |Sim   |Não   |
| EgressHttpStatus4xx | Transferência de dados de saída para as respostas com códigos de estado HTTP 4xx em GB               |Sim   | Não  |
| EgressHttpStatus5xx | Transferência de dados de saída para as respostas com códigos de estado HTTP 5xx em GB               |Sim   |  Não |
| EgressHttpStatusOthers | Transferência de dados de saída para as respostas com outros códigos de estado HTTP em GB                |Sim   |Não   |
| EgressCacheHit |  Saída transferência de dados para as respostas que foram fornecidas diretamente a partir da cache CDN Olá no Olá POPs/contornos de CDN  |Sim   |  Não |
| EgressCacheMiss | Transferência de dados de saída para as respostas que não foram encontradas no Olá mais próximo do servidor POP e obtidas a partir do servidor de origem Olá              |Sim   |  Não |
| EgressCacheNoCache | Transferem de dados de saída para recursos que são impedidos de ser colocadas em cache devido a configuração do utilizador tooa no limite de Olá.                |Sim   |Não   |
| EgressCacheUncacheable | Transferência de dados de saída para recursos que são impedidos de ser colocadas em cache por Cache-Control e/ou Expires cabeçalhos, o que indicam que este deve não ser colocadas em cache num POP ou pelo cliente de Olá HTTP do elemento de Olá                    |Sim   | Não  |
| EgressCacheOthers |  Transferências de dados de saída para obter outros cenários de cache.             |Sim   | Não  |

* Transferência de dados saída refere-se tootraffic entregar do cliente de toohello de servidores POP do CDN.


### <a name="schema-of-hello-core-analytics-logs"></a>Esquema de Olá registos de análise de núcleo 

Todos os registos são armazenados no formato JSON e cada entrada tem campos de cadeia Olá abaixo esquema os seguintes:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Onde Olá 'time' representa a hora de início de Olá de limite de hora Olá para o qual é reportadas a estatísticas de Olá. Quando uma métrica não é suportada por um fornecedor CDN, em vez de um valor de duplo ou número inteiro, será um valor nulo. Este valor nulo indica ausência Olá uma métrica e isto é diferente do valor de 0. Note também que vai haver um conjunto destas métricas por domínio configurado no ponto final de Olá.

Propriedades de exemplo abaixo:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Recursos adicionais

* [Registos de diagnóstico do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Análise de núcleo através do portal suplementar CDN do Azure](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Análise de registos do OMS do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Análise de registos do Azure REST API](https://docs.microsoft.com/en-us/rest/api/loganalytics)







