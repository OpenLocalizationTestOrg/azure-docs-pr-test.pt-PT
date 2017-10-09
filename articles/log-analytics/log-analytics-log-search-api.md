---
title: "pesquisa de registo de análise aaaLog REST API | Microsoft Docs"
description: "Este guia fornece um tutorial básico que descreve como pode utilizar Olá Log Analytics procurar REST API Olá Operations Management Suite (OMS) e fornece exemplos mostram como comandos de Olá toouse."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>Análise de registos de pesquisa REST API de registo
Este guia fornece um tutorial básico, incluindo exemplos, de como pode utilizar Olá API de REST de pesquisa de análise de registo. Análise de registos faz parte de Olá Operations Management Suite (OMS).

> [!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, deve continuar a linguagem de consulta legado Olá toouse com pesquisa de registo Olá API, tal como descrito neste artigo.  Para áreas de trabalho atualizadas é lançada uma nova API e documentação de Olá será atualizada nessa altura. 

> [!NOTE]
> Análise de registos foi anteriormente denominada das informações operacionais, que é a razão pela qual é o nome de Olá utilizado no fornecedor de recursos de Olá.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Descrição geral da API de REST do registo de pesquisa de Olá
Olá API de REST de pesquisa de análise de registo é RESTful e pode ser acedido através de Olá API do Azure Resource Manager. Este artigo fornece exemplos de aceder a API de Olá através de [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comandos de código aberto que simplifica a invocar Olá API do Azure Resource Manager. utilização Olá ARMClient encontra-se uma das muitas opções de Olá de tooaccess API de pesquisa de análise do registo. Outra opção é o módulo do PowerShell do Azure de Olá toouse para OperationalInsights, que inclui cmdlets para aceder a pesquisa. Com estas ferramentas, pode utilizar Olá API do Azure Resource Manager toomake chamadas tooOMS áreas de trabalho e executar comandos de pesquisa dentro delas. Olá API produz resultados de pesquisa no formato JSON, permitindo-lhe os resultados da pesquisa Olá toouse de várias maneiras diferentes através de programação.

Hello do Azure Resource Manager pode ser utilizado através de um [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) e Olá [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn mais, consulte as páginas web de Olá ligado.

> [!NOTE]
> Se utilizar um comando de agregação, como `|measure count()` ou `distinct`, cada chamada toosearch pode devolver até 500 000 registos. Procura não incluem um comando de agregação devolve até 5 000 registos.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Tutorial de API de REST de pesquisa de análise do registo básico
### <a name="toouse-armclient"></a>toouse ARMClient
1. Instalar [Chocolatey](https://chocolatey.org/), que é um Gestor de pacotes de origem aberta para o Windows. Abra uma janela da linha de comandos como administrador e, em seguida, execute Olá os seguintes comandos:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Instale ARMClient executando Olá os seguintes comandos:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform uma pesquisa utilizando ARMClient
1. Inicie sessão com a sua conta Microsoft ou a sua conta escolar ou profissional:

    ```
    armclient login
    ```

    Um início de sessão com êxito apresenta uma lista de todas as subscrições associadas toohello, dada conta:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Obter áreas de trabalho do Olá Operations Management Suite:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Uma chamada Get com êxito seria saída que todas as áreas de trabalho associada toohello subscrição:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Crie a variável de pesquisa:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Procure utilizando a nova variável de pesquisa:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Exemplos de referência da API de REST de pesquisa de análise de registo
Olá seguintes exemplos mostra como pode utilizar Olá API de pesquisa.

### <a name="search---actionread"></a>Procura - ação/leitura
**Url de exemplo:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Pedido:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Olá, a tabela seguinte descreve as propriedades de Olá que estão disponíveis.

| **Propriedade** | **Descrição** |
| --- | --- |
| Parte superior |número máximo de Olá de tooreturn de resultados. |
| Realce |Contém parâmetros de pré e post, normalmente, utilizados para campos de correspondência de realce |
| Pre |Prefixos Olá fornecido campos de tooyour correspondida de cadeia. |
| Post |Acrescenta Olá fornecido campos de tooyour correspondida de cadeia. |
| consulta |consulta de pesquisa de Olá utilizado toocollect e devolver resultados. |
| start |início de Olá Olá de janela de tempo que pretende toobe resultados foi encontrado. |
| Fim |fim de Olá Olá de janela de tempo que pretende toobe resultados foi encontrado. |

**Resposta:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Procurar / {ID} - ação/leitura
**Pedido Olá conteúdo de uma procura guardada:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Se a pesquisa de Olá devolve com um Estado 'Pendente', resultados de Olá atualizado de consulta podem ser feitos através desta API. Depois de 6 Mín, resultado Olá da pesquisa de Olá será removido da cache de Olá e HTTP removido vai ser devolvido. Se o pedido de pesquisa inicial Olá devolve um Estado 'Bem sucedido' imediatamente, resultados de Olá não foram adicionados cache toohello causar este tooreturn API HTTP removido se consultado. é conteúdo Olá um resultado de HTTP 200 na Olá mesmo formato como pedidos de pesquisa inicial Olá apenas com valores atualizados.
>
>

### <a name="saved-searches"></a>Pesquisas guardadas
**Pedido de lista de pesquisas guardadas:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Suportado métodos: GET colocar eliminar

Suportado métodos de coleção: introdução

Olá, a tabela seguinte descreve as propriedades de Olá que estão disponíveis.

| Propriedade | Descrição |
| --- | --- |
| Id |Identificador exclusivo de Olá. |
| ETag |**Necessário para Patch**. Atualizada pelo servidor de cada operação de escrita. O valor deve ser igual toohello atual armazenados ou ' *' tooupdate. 409 devolvido para valores antigo/inválido. |
| Properties.Query |**Necessário**. consulta de pesquisa de Olá. |
| properties.displayName |**Necessário**. nome a apresentar definidos pelo utilizador Olá da consulta de Olá. |
| Properties.Category |**Necessário**. Olá definido pelo utilizador categoria da consulta de Olá. |

> [!NOTE]
> API de pesquisa de análise de registos de Olá atualmente devolve criados pelo utilizador guardar pesquisas quando consultados para pesquisas guardadas numa área de trabalho. Olá API não devolver pesquisas guardadas fornecidas por soluções.
>
>

### <a name="create-saved-searches"></a>Criar procuras guardadas
**Pedido:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> nome de Olá para pesquisas guardadas todos os, agendas e criadas com Olá API de análise do registo de ações, tem de ser em minúsculas.

### <a name="delete-saved-searches"></a>Apagar as pesquisas gravadas
**Pedido:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Atualizar procuras guardadas
 **Pedido:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Metadados - apenas JSON
Eis um campos de Olá toosee de forma para todos os tipos de registo de dados de Olá recolhidos na sua área de trabalho. Por exemplo, se quiser que saber se Olá tipo de evento tem um campo com o nome de computador, esta consulta é toocheck unidirecional.

**Pedido para campos:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Resposta:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Olá, a tabela seguinte descreve as propriedades de Olá que estão disponíveis.

| **Propriedade** | **Descrição** |
| --- | --- |
| nome |Nome do campo. |
| displayName |nome do campo Olá a apresentar Olá. |
| tipo |Tipo de valor de campo Olá Olá. |
| facetável |Combinação de atual, 'indexada', ' armazenados ' e 'aspeto' Propriedades. |
| apresentar |Propriedade de 'Mostrar' atual. TRUE se o campo está visível na pesquisa. |
| ownerType |Tipos de tooonly reduzida pertencente tooonboarded IPs. |

## <a name="optional-parameters"></a>Parâmetros opcionais
Olá informações a seguir descreve os parâmetros opcionais disponíveis.

### <a name="highlighting"></a>Realce
parâmetro de "Highlight" Olá é um parâmetro opcional que pode utilizar o subsistema de pesquisa de Olá toorequest inclui um conjunto de marcadores na respetiva resposta.

Estes marcadores indicam início Olá e de fim texto realçado que corresponda a termos de Olá fornecidos na sua consulta de pesquisa.
Pode especificar o início de Olá e terminar com visuais que são utilizadas pelo termo de Olá realçado de toowrap de pesquisa.

**Consulta de pesquisa de exemplo**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Resultado de exemplo:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Tenha em atenção que Olá resultado anterior contém uma mensagem de erro que foi adicionado como prefixo e anexada.

## <a name="computer-groups"></a>Grupos de computadores
Grupos de computadores são pesquisas guardadas especiais que devolvem um conjunto de computadores.  Pode utilizar um grupo de computadores em outras consultas toolimit Olá resultados toohello computadores Olá grupo.  Um grupo de computadores é implementado como uma pesquisa guardada com uma etiqueta de grupo com um valor de computador.

Segue-se uma resposta de exemplo para um grupo de computadores.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>A obter grupos de computadores
ID de um grupo de computadores, utilize Olá método Get com grupo Olá tooretrieve.

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Criar ou atualizar um grupo de computadores
toocreate um grupo de computadores, utilize Olá método Put com um ID exclusivo de pesquisa guardada. Se utilizar um ID de grupo de computador existente, em seguida, de um modificada. Quando cria um grupo de computadores no portal de análise de registos de Olá, é criado Olá ID do grupo de Olá e o nome.

consulta de Olá utilizada para a definição de grupo Olá tem de devolver um conjunto de computadores para Olá grupo toofunction corretamente.  É recomendado que termina a consulta com `| Distinct Computer` tooensure Olá correta são devolvidos dados.

definição de Olá de Olá guardada pesquisa tem de incluir uma etiqueta com o nome grupo com um valor de computador para Olá pesquisa toobe classificado como um grupo de computadores.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Eliminar grupos de computadores
ID de um grupo de computadores, utilize Olá método Delete com grupo Olá toodelete.

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) consultas de toobuild com campos personalizados para os critérios.
