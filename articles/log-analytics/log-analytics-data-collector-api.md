---
title: "aaaLog API do Recoletor de dados de HTTP de análise | Microsoft Docs"
description: "Pode utilizar Olá API de Recoletor de dados do registo análise HTTP tooadd POST JSON dados toohello Log Analytics repositório partir de qualquer cliente que pode chamar Olá REST API. Este artigo descreve como toouse Olá API e tem exemplos de como toopublish dados através da utilização de linguagens de programação diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="08514-104">Enviar dados tooLog análise com Olá API de Recoletor de dados de HTTP</span><span class="sxs-lookup"><span data-stu-id="08514-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="08514-105">Este artigo mostra como toouse Olá API de Recoletor de dados de HTTP toosend dados tooLog análise de um cliente de REST API.</span><span class="sxs-lookup"><span data-stu-id="08514-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="08514-106">Descreve como tooformat quaisquer dados recolhidos pelo seu script ou aplicação, inclua-o num pedido e tem esse pedido autorizado através da análise de registos.</span><span class="sxs-lookup"><span data-stu-id="08514-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="08514-107">São fornecidos exemplos do PowerShell, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="08514-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="08514-108">Conceitos</span><span class="sxs-lookup"><span data-stu-id="08514-108">Concepts</span></span>
<span data-ttu-id="08514-109">Pode utilizar Olá API de Recoletor de dados de HTTP toosend dados tooLog Analytics a partir de qualquer cliente que possa chamar uma API REST.</span><span class="sxs-lookup"><span data-stu-id="08514-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="08514-110">Esta situação pode ter um runbook na automatização do Azure que recolhe a gestão de dados do Azure ou outra nuvem ou poderão ser um sistema de gestão alternativo que utiliza a análise de registos tooconsolidate e analisar dados.</span><span class="sxs-lookup"><span data-stu-id="08514-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="08514-111">Todos os dados no repositório de análise de registos de Olá é armazenado como um registo com um tipo de registo específica.</span><span class="sxs-lookup"><span data-stu-id="08514-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="08514-112">Formatar o seu toohello de toosend dados API de Recoletor de dados de HTTP como vários registos em JSON.</span><span class="sxs-lookup"><span data-stu-id="08514-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="08514-113">Ao submeter dados Olá, será criado um registo individual no repositório de Olá para cada registo no payload de pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Descrição geral de Recoletores de dados HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="08514-115">Criar um pedido</span><span class="sxs-lookup"><span data-stu-id="08514-115">Create a request</span></span>
<span data-ttu-id="08514-116">API de Recoletores de dados do toouse Olá HTTP, criar um pedido POST inclui Olá dados toosend em JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="08514-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="08514-117">Olá três tabelas lista Olá atributos que são necessários para cada pedido.</span><span class="sxs-lookup"><span data-stu-id="08514-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="08514-118">Iremos descrevem cada atributo em mais detalhe posteriormente no artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="08514-119">URI do pedido</span><span class="sxs-lookup"><span data-stu-id="08514-119">Request URI</span></span>
| <span data-ttu-id="08514-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="08514-120">Attribute</span></span> | <span data-ttu-id="08514-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="08514-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="08514-122">Método</span><span class="sxs-lookup"><span data-stu-id="08514-122">Method</span></span> |<span data-ttu-id="08514-123">POST</span><span class="sxs-lookup"><span data-stu-id="08514-123">POST</span></span> |
| <span data-ttu-id="08514-124">URI</span><span class="sxs-lookup"><span data-stu-id="08514-124">URI</span></span> |<span data-ttu-id="08514-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="08514-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="08514-126">Tipo de conteúdo</span><span class="sxs-lookup"><span data-stu-id="08514-126">Content type</span></span> |<span data-ttu-id="08514-127">application/json</span><span class="sxs-lookup"><span data-stu-id="08514-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="08514-128">Parâmetros URI do pedido</span><span class="sxs-lookup"><span data-stu-id="08514-128">Request URI parameters</span></span>
| <span data-ttu-id="08514-129">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="08514-129">Parameter</span></span> | <span data-ttu-id="08514-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="08514-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08514-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="08514-131">CustomerID</span></span> |<span data-ttu-id="08514-132">Olá Identificador exclusivo para a área de trabalho do Olá Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="08514-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="08514-133">Recurso</span><span class="sxs-lookup"><span data-stu-id="08514-133">Resource</span></span> |<span data-ttu-id="08514-134">nome do recurso Olá API: / api/logs.</span><span class="sxs-lookup"><span data-stu-id="08514-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="08514-135">Versão de API</span><span class="sxs-lookup"><span data-stu-id="08514-135">API Version</span></span> |<span data-ttu-id="08514-136">versão de Olá do toouse Olá API com este pedido.</span><span class="sxs-lookup"><span data-stu-id="08514-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="08514-137">Atualmente, é 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="08514-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="08514-138">Cabeçalhos de pedido</span><span class="sxs-lookup"><span data-stu-id="08514-138">Request headers</span></span>
| <span data-ttu-id="08514-139">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="08514-139">Header</span></span> | <span data-ttu-id="08514-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="08514-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08514-141">Autorização</span><span class="sxs-lookup"><span data-stu-id="08514-141">Authorization</span></span> |<span data-ttu-id="08514-142">assinatura de autorização de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-142">hello authorization signature.</span></span> <span data-ttu-id="08514-143">Artigo de Olá, pode ler sobre como cabeçalho toocreate um SHA256 HMAC.</span><span class="sxs-lookup"><span data-stu-id="08514-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="08514-144">Tipo de registo</span><span class="sxs-lookup"><span data-stu-id="08514-144">Log-Type</span></span> |<span data-ttu-id="08514-145">Especifique o tipo de registo de Olá Olá de dados de que estão a ser submetidos.</span><span class="sxs-lookup"><span data-stu-id="08514-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="08514-146">Atualmente, o tipo de registo de Olá suporta apenas carateres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="08514-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="08514-147">Não suporta números ou carateres especiais.</span><span class="sxs-lookup"><span data-stu-id="08514-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="08514-148">x-ms-data</span><span class="sxs-lookup"><span data-stu-id="08514-148">x-ms-date</span></span> |<span data-ttu-id="08514-149">data de Olá esse pedido de Olá foi processado, no formato RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="08514-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="08514-150">campo Hora gerado</span><span class="sxs-lookup"><span data-stu-id="08514-150">time-generated-field</span></span> |<span data-ttu-id="08514-151">nome de Olá de um campo de dados de Olá que contém Olá timestamp Olá do item de dados.</span><span class="sxs-lookup"><span data-stu-id="08514-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="08514-152">Se especificar um campo, em seguida, o respetivo conteúdo é utilizado para **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="08514-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="08514-153">Se este campo não está especificado, Olá predefinido para **TimeGenerated** está na altura de Olá esse Olá é ingerida mensagem.</span><span class="sxs-lookup"><span data-stu-id="08514-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="08514-154">conteúdo de Olá do campo de mensagem de Olá deve seguir o formato de Olá ISO 8601 aaaa-MM-Aaaathh.</span><span class="sxs-lookup"><span data-stu-id="08514-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="08514-155">Autorização</span><span class="sxs-lookup"><span data-stu-id="08514-155">Authorization</span></span>
<span data-ttu-id="08514-156">Qualquer API de Recoletor de dados do registo de análise de HTTP de toohello do pedido tem de incluir um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="08514-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="08514-157">tooauthenticate um pedido, tem de iniciar sessão pedido Olá com Olá primário ou de chave secundária do Olá da área de trabalho de Olá que está a efetuar o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="08514-158">Em seguida, passe esse assinatura como parte do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="08514-159">Eis o formato de Olá para o cabeçalho de autorização de Olá:</span><span class="sxs-lookup"><span data-stu-id="08514-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="08514-160">*WorkspaceID* é Olá Identificador exclusivo para a área de trabalho do Olá Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="08514-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="08514-161">*Assinatura* é um [Message Authentication Code (HMAC) com base em Hash](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que é criada a partir do pedido de Olá e, em seguida, calculada utilizando Olá [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="08514-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="08514-162">Em seguida, codificá-lo utilizando a codificação Base64.</span><span class="sxs-lookup"><span data-stu-id="08514-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="08514-163">Utilize este Olá de tooencode formato **SharedKey** cadeia da assinatura:</span><span class="sxs-lookup"><span data-stu-id="08514-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="08514-164">Eis um exemplo de uma cadeia de assinatura:</span><span class="sxs-lookup"><span data-stu-id="08514-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="08514-165">Quando tiver a cadeia de assinatura de Olá, codificá-lo utilizando Olá Algoritmo HMAC SHA256 no Olá cadeia com codificação UTF-8 e, em seguida, codificar resultado Olá como Base64.</span><span class="sxs-lookup"><span data-stu-id="08514-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="08514-166">Utilize este formato:</span><span class="sxs-lookup"><span data-stu-id="08514-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="08514-167">Exemplos de Olá nas secções seguintes Olá tem toohelp de código de exemplo cria um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="08514-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="08514-168">Corpo do pedido</span><span class="sxs-lookup"><span data-stu-id="08514-168">Request body</span></span>
<span data-ttu-id="08514-169">Olá corpo de mensagem de saudação tem de ser no JSON.</span><span class="sxs-lookup"><span data-stu-id="08514-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="08514-170">Tem de incluir um ou mais registos com Olá propriedade pares nome / valor neste formato:</span><span class="sxs-lookup"><span data-stu-id="08514-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="08514-171">Pode batch vários registos num único pedido utilizando Olá seguir o formato.</span><span class="sxs-lookup"><span data-stu-id="08514-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="08514-172">Todos os registos de Olá tem de ser Olá mesmo tipo de registo.</span><span class="sxs-lookup"><span data-stu-id="08514-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="08514-173">Tipo de registo e as propriedades</span><span class="sxs-lookup"><span data-stu-id="08514-173">Record type and properties</span></span>
<span data-ttu-id="08514-174">Definir um tipo de registo personalizado ao submeter dados através de Olá API de Recoletor de dados do registo de análise de HTTP.</span><span class="sxs-lookup"><span data-stu-id="08514-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="08514-175">Atualmente, não é possível escrever dados tooexisting tipos de registo que foram criados por outros tipos de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="08514-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="08514-176">Análise de registos lê dados de entrada Olá e, em seguida, cria propriedades que correspondem aos tipos de dados de Olá dos valores de Olá que introduzir.</span><span class="sxs-lookup"><span data-stu-id="08514-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="08514-177">Cada toohello pedido API de análise do registo tem de incluir um **tipo de registo** cabeçalho com o nome de Olá para o tipo de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="08514-178">sufixo Olá **_CL** é nome toohello automaticamente anexado introduza toodistinguish-lo a partir do registo de outro tipos de como um registo personalizado.</span><span class="sxs-lookup"><span data-stu-id="08514-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="08514-179">Por exemplo, se introduzir o nome de Olá **MyNewRecordType**, análise de registos cria um registo com o tipo de Olá **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="08514-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="08514-180">Isto ajuda a garantir que não existem não existem conflitos entre os nomes de tipo criados pelo utilizador e os que são fornecidos na atuais ou futuras soluções da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="08514-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="08514-181">tipo de dados de uma propriedade de tooidentify, análise de registos adiciona um nome de propriedade de toohello sufixo.</span><span class="sxs-lookup"><span data-stu-id="08514-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="08514-182">Se uma propriedade contiver um valor nulo, a propriedade Olá não está incluída desse registo.</span><span class="sxs-lookup"><span data-stu-id="08514-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="08514-183">Esta tabela lista o tipo de dados de propriedade Olá e sufixo correspondente:</span><span class="sxs-lookup"><span data-stu-id="08514-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="08514-184">Tipo de dados de propriedade</span><span class="sxs-lookup"><span data-stu-id="08514-184">Property data type</span></span> | <span data-ttu-id="08514-185">Sufixo</span><span class="sxs-lookup"><span data-stu-id="08514-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="08514-186">Cadeia</span><span class="sxs-lookup"><span data-stu-id="08514-186">String</span></span> |<span data-ttu-id="08514-187">_s</span><span class="sxs-lookup"><span data-stu-id="08514-187">_s</span></span> |
| <span data-ttu-id="08514-188">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="08514-188">Boolean</span></span> |<span data-ttu-id="08514-189">_b</span><span class="sxs-lookup"><span data-stu-id="08514-189">_b</span></span> |
| <span data-ttu-id="08514-190">duplo</span><span class="sxs-lookup"><span data-stu-id="08514-190">Double</span></span> |<span data-ttu-id="08514-191">_d</span><span class="sxs-lookup"><span data-stu-id="08514-191">_d</span></span> |
| <span data-ttu-id="08514-192">Data/hora</span><span class="sxs-lookup"><span data-stu-id="08514-192">Date/time</span></span> |<span data-ttu-id="08514-193">_t</span><span class="sxs-lookup"><span data-stu-id="08514-193">_t</span></span> |
| <span data-ttu-id="08514-194">GUID</span><span class="sxs-lookup"><span data-stu-id="08514-194">GUID</span></span> |<span data-ttu-id="08514-195">_g</span><span class="sxs-lookup"><span data-stu-id="08514-195">_g</span></span> |

<span data-ttu-id="08514-196">tipo de dados de Olá que utiliza a análise de registos para cada propriedade depende se Olá o tipo de registo para o novo registo de Olá já existe.</span><span class="sxs-lookup"><span data-stu-id="08514-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="08514-197">Se o tipo de registo Olá não existir, a análise de registos cria um novo.</span><span class="sxs-lookup"><span data-stu-id="08514-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="08514-198">Análise de registos utiliza o tipo de dados ao hello do toodetermine de inferência Olá JSON tipo para cada propriedade para o novo registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="08514-199">Se existir o tipo de registo Olá, análise de registos tenta toocreate um novo registo com base nas propriedades existentes.</span><span class="sxs-lookup"><span data-stu-id="08514-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="08514-200">Se Olá tipo de dados para uma propriedade no registo novo Olá não corresponde ao e não pode ser convertida toohello existente tipo ou se hello registo inclui uma propriedade que não existe, análise de registos cria uma nova propriedade que tem o sufixo relevantes Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="08514-201">Por exemplo, esta entrada de submissão criaria um registo com três propriedades, **number_d**, **boolean_b**, e **string_s**:</span><span class="sxs-lookup"><span data-stu-id="08514-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Registo de exemplo 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="08514-203">Se tiver submetido, em seguida, esta entrada seguinte, com todos os valores a formatados como cadeias, propriedades Olá não ser alterado.</span><span class="sxs-lookup"><span data-stu-id="08514-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="08514-204">Estes valores podem ser convertida tooexisting tipos de dados:</span><span class="sxs-lookup"><span data-stu-id="08514-204">These values can be converted tooexisting data types:</span></span>

![Registo de exemplo 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="08514-206">No entanto, se tiver efetuado, em seguida, este submissão seguinte, análise de registos criaria Olá novas propriedades **boolean_d** e **string_d**.</span><span class="sxs-lookup"><span data-stu-id="08514-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="08514-207">Não não possível converter estes valores:</span><span class="sxs-lookup"><span data-stu-id="08514-207">These values can't be converted:</span></span>

![Registo de exemplo 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="08514-209">Se, em seguida, submetido Olá entrada, a seguir antes da criação do tipo de registo Olá, análise de registos criaria um registo com três propriedades, **number_s**, **boolean_s**, e **string_s**.</span><span class="sxs-lookup"><span data-stu-id="08514-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="08514-210">Esta entrada, cada um dos valores iniciais Olá está formatada como uma cadeia:</span><span class="sxs-lookup"><span data-stu-id="08514-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Registo de exemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="08514-212">Limites de dados</span><span class="sxs-lookup"><span data-stu-id="08514-212">Data limits</span></span>
<span data-ttu-id="08514-213">Existem algumas restrições à volta de dados de Olá publicados toohello recolha de dados do Log Analytics API.</span><span class="sxs-lookup"><span data-stu-id="08514-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="08514-214">Máximo de 30 MB por post tooLog API de Recoletor de dados de análise.</span><span class="sxs-lookup"><span data-stu-id="08514-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="08514-215">Este é um limite de tamanho para um único pedido de post.</span><span class="sxs-lookup"><span data-stu-id="08514-215">This is a size limit for a single post.</span></span> <span data-ttu-id="08514-216">Se os dados de um pedido de post único que exceda 30 MB Olá, deve dividir Olá dados de cópia de segurança toosmaller tamanho segmentos e enviá-las em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="08514-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="08514-217">Máximo de limite de 32 KB para os valores de campo.</span><span class="sxs-lookup"><span data-stu-id="08514-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="08514-218">Se o valor do campo Olá for superior a 32 KB, dados de Olá serão truncados.</span><span class="sxs-lookup"><span data-stu-id="08514-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="08514-219">Recomendada número máximo de campos para um determinado tipo é 50.</span><span class="sxs-lookup"><span data-stu-id="08514-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="08514-220">Este é um limite prático de uma perspetiva de experiência de pesquisa e facilidade de utilização.</span><span class="sxs-lookup"><span data-stu-id="08514-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="08514-221">Códigos de retorno</span><span class="sxs-lookup"><span data-stu-id="08514-221">Return codes</span></span>
<span data-ttu-id="08514-222">Olá, código de estado HTTP 200 significa que esse pedido Olá foi recebido para processamento.</span><span class="sxs-lookup"><span data-stu-id="08514-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="08514-223">Isto indica dessa operação Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="08514-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="08514-224">Esta tabela lista o conjunto completo de Olá de códigos de estado que poderá devolver serviço Olá:</span><span class="sxs-lookup"><span data-stu-id="08514-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="08514-225">Código</span><span class="sxs-lookup"><span data-stu-id="08514-225">Code</span></span> | <span data-ttu-id="08514-226">Estado</span><span class="sxs-lookup"><span data-stu-id="08514-226">Status</span></span> | <span data-ttu-id="08514-227">Código de erro</span><span class="sxs-lookup"><span data-stu-id="08514-227">Error code</span></span> | <span data-ttu-id="08514-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="08514-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08514-229">200</span><span class="sxs-lookup"><span data-stu-id="08514-229">200</span></span> |<span data-ttu-id="08514-230">OK</span><span class="sxs-lookup"><span data-stu-id="08514-230">OK</span></span> | |<span data-ttu-id="08514-231">pedido de Olá foi aceite com êxito.</span><span class="sxs-lookup"><span data-stu-id="08514-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="08514-232">400</span><span class="sxs-lookup"><span data-stu-id="08514-232">400</span></span> |<span data-ttu-id="08514-233">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-233">Bad request</span></span> |<span data-ttu-id="08514-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="08514-234">InactiveCustomer</span></span> |<span data-ttu-id="08514-235">área de trabalho Olá foi fechada.</span><span class="sxs-lookup"><span data-stu-id="08514-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="08514-236">400</span><span class="sxs-lookup"><span data-stu-id="08514-236">400</span></span> |<span data-ttu-id="08514-237">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-237">Bad request</span></span> |<span data-ttu-id="08514-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="08514-238">InvalidApiVersion</span></span> |<span data-ttu-id="08514-239">versão de API de Olá que especificou não foi reconhecido pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="08514-240">400</span><span class="sxs-lookup"><span data-stu-id="08514-240">400</span></span> |<span data-ttu-id="08514-241">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-241">Bad request</span></span> |<span data-ttu-id="08514-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="08514-242">InvalidCustomerId</span></span> |<span data-ttu-id="08514-243">ID da área de trabalho de Olá especificado é inválido.</span><span class="sxs-lookup"><span data-stu-id="08514-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="08514-244">400</span><span class="sxs-lookup"><span data-stu-id="08514-244">400</span></span> |<span data-ttu-id="08514-245">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-245">Bad request</span></span> |<span data-ttu-id="08514-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="08514-246">InvalidDataFormat</span></span> |<span data-ttu-id="08514-247">Foi submetida JSON inválido.</span><span class="sxs-lookup"><span data-stu-id="08514-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="08514-248">corpo da resposta Olá pode conter mais informações sobre como tooresolve Olá erro.</span><span class="sxs-lookup"><span data-stu-id="08514-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="08514-249">400</span><span class="sxs-lookup"><span data-stu-id="08514-249">400</span></span> |<span data-ttu-id="08514-250">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-250">Bad request</span></span> |<span data-ttu-id="08514-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="08514-251">InvalidLogType</span></span> |<span data-ttu-id="08514-252">o tipo de registo de Olá especificado continha carateres especiais ou números.</span><span class="sxs-lookup"><span data-stu-id="08514-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="08514-253">400</span><span class="sxs-lookup"><span data-stu-id="08514-253">400</span></span> |<span data-ttu-id="08514-254">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-254">Bad request</span></span> |<span data-ttu-id="08514-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="08514-255">MissingApiVersion</span></span> |<span data-ttu-id="08514-256">Não foi especificada a versão da API Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="08514-257">400</span><span class="sxs-lookup"><span data-stu-id="08514-257">400</span></span> |<span data-ttu-id="08514-258">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-258">Bad request</span></span> |<span data-ttu-id="08514-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="08514-259">MissingContentType</span></span> |<span data-ttu-id="08514-260">Não foi especificado o tipo de conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="08514-261">400</span><span class="sxs-lookup"><span data-stu-id="08514-261">400</span></span> |<span data-ttu-id="08514-262">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-262">Bad request</span></span> |<span data-ttu-id="08514-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="08514-263">MissingLogType</span></span> |<span data-ttu-id="08514-264">Olá necessário não foi especificado o tipo de valor de registo.</span><span class="sxs-lookup"><span data-stu-id="08514-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="08514-265">400</span><span class="sxs-lookup"><span data-stu-id="08514-265">400</span></span> |<span data-ttu-id="08514-266">Pedido incorreto</span><span class="sxs-lookup"><span data-stu-id="08514-266">Bad request</span></span> |<span data-ttu-id="08514-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="08514-267">UnsupportedContentType</span></span> |<span data-ttu-id="08514-268">tipo de conteúdo de Olá não foi definido demasiado**application/json**.</span><span class="sxs-lookup"><span data-stu-id="08514-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="08514-269">403</span><span class="sxs-lookup"><span data-stu-id="08514-269">403</span></span> |<span data-ttu-id="08514-270">Proibido</span><span class="sxs-lookup"><span data-stu-id="08514-270">Forbidden</span></span> |<span data-ttu-id="08514-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="08514-271">InvalidAuthorization</span></span> |<span data-ttu-id="08514-272">pedido de Olá tooauthenticate do serviço de Olá falhou.</span><span class="sxs-lookup"><span data-stu-id="08514-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="08514-273">Certifique-se de que essa chave de ID e a ligação de área de trabalho do Olá são válidos.</span><span class="sxs-lookup"><span data-stu-id="08514-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="08514-274">404</span><span class="sxs-lookup"><span data-stu-id="08514-274">404</span></span> |<span data-ttu-id="08514-275">Não foi encontrado</span><span class="sxs-lookup"><span data-stu-id="08514-275">Not Found</span></span> | | <span data-ttu-id="08514-276">O URL de Olá fornecido está incorreto ou Olá do pedido é demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="08514-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="08514-277">429</span><span class="sxs-lookup"><span data-stu-id="08514-277">429</span></span> |<span data-ttu-id="08514-278">Demasiados pedidos</span><span class="sxs-lookup"><span data-stu-id="08514-278">Too Many Requests</span></span> | | <span data-ttu-id="08514-279">serviço de Olá está com um elevado volume de dados da sua conta.</span><span class="sxs-lookup"><span data-stu-id="08514-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="08514-280">Repita o pedido de Olá mais tarde.</span><span class="sxs-lookup"><span data-stu-id="08514-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="08514-281">500</span><span class="sxs-lookup"><span data-stu-id="08514-281">500</span></span> |<span data-ttu-id="08514-282">Erro interno do servidor</span><span class="sxs-lookup"><span data-stu-id="08514-282">Internal Server Error</span></span> |<span data-ttu-id="08514-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="08514-283">UnspecifiedError</span></span> |<span data-ttu-id="08514-284">serviço de Olá encontrou um erro interno.</span><span class="sxs-lookup"><span data-stu-id="08514-284">hello service encountered an internal error.</span></span> <span data-ttu-id="08514-285">Repita o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-285">Please retry hello request.</span></span> |
| <span data-ttu-id="08514-286">503</span><span class="sxs-lookup"><span data-stu-id="08514-286">503</span></span> |<span data-ttu-id="08514-287">Serviço indisponível</span><span class="sxs-lookup"><span data-stu-id="08514-287">Service Unavailable</span></span> |<span data-ttu-id="08514-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="08514-288">ServiceUnavailable</span></span> |<span data-ttu-id="08514-289">o serviço de Olá está atualmente indisponível tooreceive pedidos.</span><span class="sxs-lookup"><span data-stu-id="08514-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="08514-290">Repita o pedido.</span><span class="sxs-lookup"><span data-stu-id="08514-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="08514-291">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="08514-291">Query data</span></span>
<span data-ttu-id="08514-292">dados de tooquery submetidos por Olá API de Recoletor de dados de HTTP de análise de registo, procure registos com **tipo** que seja igual toohello **LogType** valor que especificou, acrescentar **_CL**.</span><span class="sxs-lookup"><span data-stu-id="08514-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="08514-293">Por exemplo, se tiver utilizado **MyCustomLog**, em seguida, iria devolver todos os registos com **tipo = MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="08514-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="08514-294">Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consulta alteraria toohello seguinte.</span><span class="sxs-lookup"><span data-stu-id="08514-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="08514-295">Pedidos de exemplo</span><span class="sxs-lookup"><span data-stu-id="08514-295">Sample requests</span></span>
<span data-ttu-id="08514-296">Olá secções seguintes, irá encontrar exemplos de como toosubmit dados toohello API de Recoletor de dados do registo de análise de HTTP utilizando diferentes linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="08514-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="08514-297">Para cada amostra, execute estes passos variáveis de Olá tooset para o cabeçalho de autorização de Olá:</span><span class="sxs-lookup"><span data-stu-id="08514-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="08514-298">No portal do Operations Management Suite Olá, selecione Olá **definições** mosaico e, em seguida, selecione Olá **origens ligadas** separador.</span><span class="sxs-lookup"><span data-stu-id="08514-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="08514-299">toohello à direita dos **ID da área de trabalho**, selecione o ícone de cópia de Olá e, em seguida, cole Olá ID como valor Olá Olá **ID de cliente** variável.</span><span class="sxs-lookup"><span data-stu-id="08514-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="08514-300">toohello à direita dos **chave primária**, selecione o ícone de cópia de Olá e, em seguida, cole Olá ID como valor Olá Olá **chave partilhada** variável.</span><span class="sxs-lookup"><span data-stu-id="08514-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="08514-301">Em alternativa, pode alterar as variáveis de Olá para o tipo de registo de Olá e dados JSON.</span><span class="sxs-lookup"><span data-stu-id="08514-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="08514-302">Exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="08514-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="08514-303">Exemplo C#</span><span class="sxs-lookup"><span data-stu-id="08514-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="08514-304">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="08514-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="08514-305">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="08514-305">Next steps</span></span>
- <span data-ttu-id="08514-306">Olá utilize [API de pesquisa de registo](log-analytics-log-search-api.md) tooretrieve dados do repositório de análise de registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="08514-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
