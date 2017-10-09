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
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="c1f55-103">Análise de registos de pesquisa REST API de registo</span><span class="sxs-lookup"><span data-stu-id="c1f55-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="c1f55-104">Este guia fornece um tutorial básico, incluindo exemplos, de como pode utilizar Olá API de REST de pesquisa de análise de registo.</span><span class="sxs-lookup"><span data-stu-id="c1f55-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="c1f55-105">Análise de registos faz parte de Olá Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="c1f55-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="c1f55-106">Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, deve continuar a linguagem de consulta legado Olá toouse com pesquisa de registo Olá API, tal como descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c1f55-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="c1f55-107">Para áreas de trabalho atualizadas é lançada uma nova API e documentação de Olá será atualizada nessa altura.</span><span class="sxs-lookup"><span data-stu-id="c1f55-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="c1f55-108">Análise de registos foi anteriormente denominada das informações operacionais, que é a razão pela qual é o nome de Olá utilizado no fornecedor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="c1f55-109">Descrição geral da API de REST do registo de pesquisa de Olá</span><span class="sxs-lookup"><span data-stu-id="c1f55-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="c1f55-110">Olá API de REST de pesquisa de análise de registo é RESTful e pode ser acedido através de Olá API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1f55-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="c1f55-111">Este artigo fornece exemplos de aceder a API de Olá através de [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comandos de código aberto que simplifica a invocar Olá API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1f55-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="c1f55-112">utilização Olá ARMClient encontra-se uma das muitas opções de Olá de tooaccess API de pesquisa de análise do registo.</span><span class="sxs-lookup"><span data-stu-id="c1f55-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="c1f55-113">Outra opção é o módulo do PowerShell do Azure de Olá toouse para OperationalInsights, que inclui cmdlets para aceder a pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c1f55-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="c1f55-114">Com estas ferramentas, pode utilizar Olá API do Azure Resource Manager toomake chamadas tooOMS áreas de trabalho e executar comandos de pesquisa dentro delas.</span><span class="sxs-lookup"><span data-stu-id="c1f55-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="c1f55-115">Olá API produz resultados de pesquisa no formato JSON, permitindo-lhe os resultados da pesquisa Olá toouse de várias maneiras diferentes através de programação.</span><span class="sxs-lookup"><span data-stu-id="c1f55-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="c1f55-116">Hello do Azure Resource Manager pode ser utilizado através de um [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) e Olá [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1f55-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="c1f55-117">toolearn mais, consulte as páginas web de Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="c1f55-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="c1f55-118">Se utilizar um comando de agregação, como `|measure count()` ou `distinct`, cada chamada toosearch pode devolver até 500 000 registos.</span><span class="sxs-lookup"><span data-stu-id="c1f55-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="c1f55-119">Procura não incluem um comando de agregação devolve até 5 000 registos.</span><span class="sxs-lookup"><span data-stu-id="c1f55-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="c1f55-120">Tutorial de API de REST de pesquisa de análise do registo básico</span><span class="sxs-lookup"><span data-stu-id="c1f55-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="c1f55-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="c1f55-121">toouse ARMClient</span></span>
1. <span data-ttu-id="c1f55-122">Instalar [Chocolatey](https://chocolatey.org/), que é um Gestor de pacotes de origem aberta para o Windows.</span><span class="sxs-lookup"><span data-stu-id="c1f55-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="c1f55-123">Abra uma janela da linha de comandos como administrador e, em seguida, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c1f55-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="c1f55-124">Instale ARMClient executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c1f55-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="c1f55-125">tooperform uma pesquisa utilizando ARMClient</span><span class="sxs-lookup"><span data-stu-id="c1f55-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="c1f55-126">Inicie sessão com a sua conta Microsoft ou a sua conta escolar ou profissional:</span><span class="sxs-lookup"><span data-stu-id="c1f55-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="c1f55-127">Um início de sessão com êxito apresenta uma lista de todas as subscrições associadas toohello, dada conta:</span><span class="sxs-lookup"><span data-stu-id="c1f55-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="c1f55-128">Obter áreas de trabalho do Olá Operations Management Suite:</span><span class="sxs-lookup"><span data-stu-id="c1f55-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="c1f55-129">Uma chamada Get com êxito seria saída que todas as áreas de trabalho associada toohello subscrição:</span><span class="sxs-lookup"><span data-stu-id="c1f55-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="c1f55-130">Crie a variável de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="c1f55-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="c1f55-131">Procure utilizando a nova variável de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="c1f55-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="c1f55-132">Exemplos de referência da API de REST de pesquisa de análise de registo</span><span class="sxs-lookup"><span data-stu-id="c1f55-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="c1f55-133">Olá seguintes exemplos mostra como pode utilizar Olá API de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c1f55-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="c1f55-134">Procura - ação/leitura</span><span class="sxs-lookup"><span data-stu-id="c1f55-134">Search - Action/Read</span></span>
<span data-ttu-id="c1f55-135">**Url de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="c1f55-136">**Pedido:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-136">**Request:**</span></span>

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
<span data-ttu-id="c1f55-137">Olá, a tabela seguinte descreve as propriedades de Olá que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c1f55-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="c1f55-138">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="c1f55-138">**Property**</span></span> | <span data-ttu-id="c1f55-139">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="c1f55-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c1f55-140">Parte superior</span><span class="sxs-lookup"><span data-stu-id="c1f55-140">top</span></span> |<span data-ttu-id="c1f55-141">número máximo de Olá de tooreturn de resultados.</span><span class="sxs-lookup"><span data-stu-id="c1f55-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="c1f55-142">Realce</span><span class="sxs-lookup"><span data-stu-id="c1f55-142">highlight</span></span> |<span data-ttu-id="c1f55-143">Contém parâmetros de pré e post, normalmente, utilizados para campos de correspondência de realce</span><span class="sxs-lookup"><span data-stu-id="c1f55-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="c1f55-144">Pre</span><span class="sxs-lookup"><span data-stu-id="c1f55-144">pre</span></span> |<span data-ttu-id="c1f55-145">Prefixos Olá fornecido campos de tooyour correspondida de cadeia.</span><span class="sxs-lookup"><span data-stu-id="c1f55-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="c1f55-146">Post</span><span class="sxs-lookup"><span data-stu-id="c1f55-146">post</span></span> |<span data-ttu-id="c1f55-147">Acrescenta Olá fornecido campos de tooyour correspondida de cadeia.</span><span class="sxs-lookup"><span data-stu-id="c1f55-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="c1f55-148">consulta</span><span class="sxs-lookup"><span data-stu-id="c1f55-148">query</span></span> |<span data-ttu-id="c1f55-149">consulta de pesquisa de Olá utilizado toocollect e devolver resultados.</span><span class="sxs-lookup"><span data-stu-id="c1f55-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="c1f55-150">start</span><span class="sxs-lookup"><span data-stu-id="c1f55-150">start</span></span> |<span data-ttu-id="c1f55-151">início de Olá Olá de janela de tempo que pretende toobe resultados foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="c1f55-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="c1f55-152">Fim</span><span class="sxs-lookup"><span data-stu-id="c1f55-152">end</span></span> |<span data-ttu-id="c1f55-153">fim de Olá Olá de janela de tempo que pretende toobe resultados foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="c1f55-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="c1f55-154">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="c1f55-155">Procurar / {ID} - ação/leitura</span><span class="sxs-lookup"><span data-stu-id="c1f55-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="c1f55-156">**Pedido Olá conteúdo de uma procura guardada:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="c1f55-157">Se a pesquisa de Olá devolve com um Estado 'Pendente', resultados de Olá atualizado de consulta podem ser feitos através desta API.</span><span class="sxs-lookup"><span data-stu-id="c1f55-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="c1f55-158">Depois de 6 Mín, resultado Olá da pesquisa de Olá será removido da cache de Olá e HTTP removido vai ser devolvido.</span><span class="sxs-lookup"><span data-stu-id="c1f55-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="c1f55-159">Se o pedido de pesquisa inicial Olá devolve um Estado 'Bem sucedido' imediatamente, resultados de Olá não foram adicionados cache toohello causar este tooreturn API HTTP removido se consultado.</span><span class="sxs-lookup"><span data-stu-id="c1f55-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="c1f55-160">é conteúdo Olá um resultado de HTTP 200 na Olá mesmo formato como pedidos de pesquisa inicial Olá apenas com valores atualizados.</span><span class="sxs-lookup"><span data-stu-id="c1f55-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="c1f55-161">Pesquisas guardadas</span><span class="sxs-lookup"><span data-stu-id="c1f55-161">Saved searches</span></span>
<span data-ttu-id="c1f55-162">**Pedido de lista de pesquisas guardadas:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="c1f55-163">Suportado métodos: GET colocar eliminar</span><span class="sxs-lookup"><span data-stu-id="c1f55-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="c1f55-164">Suportado métodos de coleção: introdução</span><span class="sxs-lookup"><span data-stu-id="c1f55-164">Supported collection methods: GET</span></span>

<span data-ttu-id="c1f55-165">Olá, a tabela seguinte descreve as propriedades de Olá que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c1f55-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="c1f55-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c1f55-166">Property</span></span> | <span data-ttu-id="c1f55-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1f55-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1f55-168">Id</span><span class="sxs-lookup"><span data-stu-id="c1f55-168">Id</span></span> |<span data-ttu-id="c1f55-169">Identificador exclusivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-169">hello unique identifier.</span></span> |
| <span data-ttu-id="c1f55-170">ETag</span><span class="sxs-lookup"><span data-stu-id="c1f55-170">Etag</span></span> |<span data-ttu-id="c1f55-171">**Necessário para Patch**.</span><span class="sxs-lookup"><span data-stu-id="c1f55-171">**Required for Patch**.</span></span> <span data-ttu-id="c1f55-172">Atualizada pelo servidor de cada operação de escrita.</span><span class="sxs-lookup"><span data-stu-id="c1f55-172">Updated by server on each write.</span></span> <span data-ttu-id="c1f55-173">O valor deve ser igual toohello atual armazenados ou ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c1f55-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="c1f55-174">409 devolvido para valores antigo/inválido.</span><span class="sxs-lookup"><span data-stu-id="c1f55-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="c1f55-175">Properties.Query</span><span class="sxs-lookup"><span data-stu-id="c1f55-175">properties.query</span></span> |<span data-ttu-id="c1f55-176">**Necessário**.</span><span class="sxs-lookup"><span data-stu-id="c1f55-176">**Required**.</span></span> <span data-ttu-id="c1f55-177">consulta de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-177">hello search query.</span></span> |
| <span data-ttu-id="c1f55-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="c1f55-178">properties.displayName</span></span> |<span data-ttu-id="c1f55-179">**Necessário**.</span><span class="sxs-lookup"><span data-stu-id="c1f55-179">**Required**.</span></span> <span data-ttu-id="c1f55-180">nome a apresentar definidos pelo utilizador Olá da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="c1f55-181">Properties.Category</span><span class="sxs-lookup"><span data-stu-id="c1f55-181">properties.category</span></span> |<span data-ttu-id="c1f55-182">**Necessário**.</span><span class="sxs-lookup"><span data-stu-id="c1f55-182">**Required**.</span></span> <span data-ttu-id="c1f55-183">Olá definido pelo utilizador categoria da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="c1f55-184">API de pesquisa de análise de registos de Olá atualmente devolve criados pelo utilizador guardar pesquisas quando consultados para pesquisas guardadas numa área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c1f55-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="c1f55-185">Olá API não devolver pesquisas guardadas fornecidas por soluções.</span><span class="sxs-lookup"><span data-stu-id="c1f55-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="c1f55-186">Criar procuras guardadas</span><span class="sxs-lookup"><span data-stu-id="c1f55-186">Create saved searches</span></span>
<span data-ttu-id="c1f55-187">**Pedido:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="c1f55-188">nome de Olá para pesquisas guardadas todos os, agendas e criadas com Olá API de análise do registo de ações, tem de ser em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c1f55-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="c1f55-189">Apagar as pesquisas gravadas</span><span class="sxs-lookup"><span data-stu-id="c1f55-189">Delete saved searches</span></span>
<span data-ttu-id="c1f55-190">**Pedido:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="c1f55-191">Atualizar procuras guardadas</span><span class="sxs-lookup"><span data-stu-id="c1f55-191">Update saved searches</span></span>
 <span data-ttu-id="c1f55-192">**Pedido:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="c1f55-193">Metadados - apenas JSON</span><span class="sxs-lookup"><span data-stu-id="c1f55-193">Metadata - JSON only</span></span>
<span data-ttu-id="c1f55-194">Eis um campos de Olá toosee de forma para todos os tipos de registo de dados de Olá recolhidos na sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c1f55-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="c1f55-195">Por exemplo, se quiser que saber se Olá tipo de evento tem um campo com o nome de computador, esta consulta é toocheck unidirecional.</span><span class="sxs-lookup"><span data-stu-id="c1f55-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="c1f55-196">**Pedido para campos:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="c1f55-197">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-197">**Response:**</span></span>

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

<span data-ttu-id="c1f55-198">Olá, a tabela seguinte descreve as propriedades de Olá que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c1f55-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="c1f55-199">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="c1f55-199">**Property**</span></span> | <span data-ttu-id="c1f55-200">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="c1f55-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c1f55-201">nome</span><span class="sxs-lookup"><span data-stu-id="c1f55-201">name</span></span> |<span data-ttu-id="c1f55-202">Nome do campo.</span><span class="sxs-lookup"><span data-stu-id="c1f55-202">Field name.</span></span> |
| <span data-ttu-id="c1f55-203">displayName</span><span class="sxs-lookup"><span data-stu-id="c1f55-203">displayName</span></span> |<span data-ttu-id="c1f55-204">nome do campo Olá a apresentar Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="c1f55-205">tipo</span><span class="sxs-lookup"><span data-stu-id="c1f55-205">type</span></span> |<span data-ttu-id="c1f55-206">Tipo de valor de campo Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="c1f55-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="c1f55-207">facetável</span><span class="sxs-lookup"><span data-stu-id="c1f55-207">facetable</span></span> |<span data-ttu-id="c1f55-208">Combinação de atual, 'indexada', ' armazenados ' e 'aspeto' Propriedades.</span><span class="sxs-lookup"><span data-stu-id="c1f55-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="c1f55-209">apresentar</span><span class="sxs-lookup"><span data-stu-id="c1f55-209">display</span></span> |<span data-ttu-id="c1f55-210">Propriedade de 'Mostrar' atual.</span><span class="sxs-lookup"><span data-stu-id="c1f55-210">Current ‘display’ property.</span></span> <span data-ttu-id="c1f55-211">TRUE se o campo está visível na pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c1f55-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="c1f55-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="c1f55-212">ownerType</span></span> |<span data-ttu-id="c1f55-213">Tipos de tooonly reduzida pertencente tooonboarded IPs.</span><span class="sxs-lookup"><span data-stu-id="c1f55-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="c1f55-214">Parâmetros opcionais</span><span class="sxs-lookup"><span data-stu-id="c1f55-214">Optional parameters</span></span>
<span data-ttu-id="c1f55-215">Olá informações a seguir descreve os parâmetros opcionais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c1f55-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="c1f55-216">Realce</span><span class="sxs-lookup"><span data-stu-id="c1f55-216">Highlighting</span></span>
<span data-ttu-id="c1f55-217">parâmetro de "Highlight" Olá é um parâmetro opcional que pode utilizar o subsistema de pesquisa de Olá toorequest inclui um conjunto de marcadores na respetiva resposta.</span><span class="sxs-lookup"><span data-stu-id="c1f55-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="c1f55-218">Estes marcadores indicam início Olá e de fim texto realçado que corresponda a termos de Olá fornecidos na sua consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c1f55-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="c1f55-219">Pode especificar o início de Olá e terminar com visuais que são utilizadas pelo termo de Olá realçado de toowrap de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c1f55-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="c1f55-220">**Consulta de pesquisa de exemplo**</span><span class="sxs-lookup"><span data-stu-id="c1f55-220">**Example search query**</span></span>

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

<span data-ttu-id="c1f55-221">**Resultado de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="c1f55-221">**Sample result:**</span></span>

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

<span data-ttu-id="c1f55-222">Tenha em atenção que Olá resultado anterior contém uma mensagem de erro que foi adicionado como prefixo e anexada.</span><span class="sxs-lookup"><span data-stu-id="c1f55-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="c1f55-223">Grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="c1f55-223">Computer groups</span></span>
<span data-ttu-id="c1f55-224">Grupos de computadores são pesquisas guardadas especiais que devolvem um conjunto de computadores.</span><span class="sxs-lookup"><span data-stu-id="c1f55-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="c1f55-225">Pode utilizar um grupo de computadores em outras consultas toolimit Olá resultados toohello computadores Olá grupo.</span><span class="sxs-lookup"><span data-stu-id="c1f55-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="c1f55-226">Um grupo de computadores é implementado como uma pesquisa guardada com uma etiqueta de grupo com um valor de computador.</span><span class="sxs-lookup"><span data-stu-id="c1f55-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="c1f55-227">Segue-se uma resposta de exemplo para um grupo de computadores.</span><span class="sxs-lookup"><span data-stu-id="c1f55-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="c1f55-228">A obter grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="c1f55-228">Retrieving computer groups</span></span>
<span data-ttu-id="c1f55-229">ID de um grupo de computadores, utilize Olá método Get com grupo Olá tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="c1f55-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="c1f55-230">Criar ou atualizar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="c1f55-230">Creating or updating a computer group</span></span>
<span data-ttu-id="c1f55-231">toocreate um grupo de computadores, utilize Olá método Put com um ID exclusivo de pesquisa guardada.</span><span class="sxs-lookup"><span data-stu-id="c1f55-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="c1f55-232">Se utilizar um ID de grupo de computador existente, em seguida, de um modificada.</span><span class="sxs-lookup"><span data-stu-id="c1f55-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="c1f55-233">Quando cria um grupo de computadores no portal de análise de registos de Olá, é criado Olá ID do grupo de Olá e o nome.</span><span class="sxs-lookup"><span data-stu-id="c1f55-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="c1f55-234">consulta de Olá utilizada para a definição de grupo Olá tem de devolver um conjunto de computadores para Olá grupo toofunction corretamente.</span><span class="sxs-lookup"><span data-stu-id="c1f55-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="c1f55-235">É recomendado que termina a consulta com `| Distinct Computer` tooensure Olá correta são devolvidos dados.</span><span class="sxs-lookup"><span data-stu-id="c1f55-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="c1f55-236">definição de Olá de Olá guardada pesquisa tem de incluir uma etiqueta com o nome grupo com um valor de computador para Olá pesquisa toobe classificado como um grupo de computadores.</span><span class="sxs-lookup"><span data-stu-id="c1f55-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="c1f55-237">Eliminar grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="c1f55-237">Deleting computer groups</span></span>
<span data-ttu-id="c1f55-238">ID de um grupo de computadores, utilize Olá método Delete com grupo Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="c1f55-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="c1f55-239">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c1f55-239">Next steps</span></span>
* <span data-ttu-id="c1f55-240">Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) consultas de toobuild com campos personalizados para os critérios.</span><span class="sxs-lookup"><span data-stu-id="c1f55-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
