---
title: "funções de modelo do Resource Manager aaaAzure - recursos | Microsoft Docs"
description: "Descreve as funções de Olá toouse um valores de tooretrieve de modelo do Azure Resource Manager sobre os recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="f813a-103">Funções de recursos para os modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f813a-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="f813a-104">O Resource Manager fornece Olá funções para obter valores de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f813a-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="f813a-105">listKeys e lista {Value}</span><span class="sxs-lookup"><span data-stu-id="f813a-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="f813a-106">fornecedores</span><span class="sxs-lookup"><span data-stu-id="f813a-106">providers</span></span>](#providers)
* [<span data-ttu-id="f813a-107">referência</span><span class="sxs-lookup"><span data-stu-id="f813a-107">reference</span></span>](#reference)
* [<span data-ttu-id="f813a-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="f813a-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="f813a-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="f813a-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="f813a-110">subscrição</span><span class="sxs-lookup"><span data-stu-id="f813a-110">subscription</span></span>](#subscription)

<span data-ttu-id="f813a-111">tooget valores de parâmetros, variáveis ou implementação atual de Olá, consulte [das funções de valor de implementação](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f813a-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="f813a-112">listKeys e lista {Value}</span><span class="sxs-lookup"><span data-stu-id="f813a-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="f813a-113">Devolve Olá valores para qualquer tipo de recurso que suporta a operação de lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="f813a-114">utilização de mais comuns de Olá é `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="f813a-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="f813a-115">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f813a-115">Parameters</span></span>

| <span data-ttu-id="f813a-116">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f813a-116">Parameter</span></span> | <span data-ttu-id="f813a-117">Necessário</span><span class="sxs-lookup"><span data-stu-id="f813a-117">Required</span></span> | <span data-ttu-id="f813a-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="f813a-118">Type</span></span> | <span data-ttu-id="f813a-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="f813a-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f813a-120">resourceName ou resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="f813a-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="f813a-121">Sim</span><span class="sxs-lookup"><span data-stu-id="f813a-121">Yes</span></span> |<span data-ttu-id="f813a-122">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-122">string</span></span> |<span data-ttu-id="f813a-123">Identificador exclusivo para o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="f813a-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f813a-124">apiVersion</span></span> |<span data-ttu-id="f813a-125">Sim</span><span class="sxs-lookup"><span data-stu-id="f813a-125">Yes</span></span> |<span data-ttu-id="f813a-126">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-126">string</span></span> |<span data-ttu-id="f813a-127">Versão de API do Estado de runtime do recurso.</span><span class="sxs-lookup"><span data-stu-id="f813a-127">API version of resource runtime state.</span></span> <span data-ttu-id="f813a-128">Normalmente, no formato de Olá, **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="f813a-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f813a-129">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="f813a-129">Return value</span></span>

<span data-ttu-id="f813a-130">Olá devolveu o objeto de listKeys tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="f813a-131">Outras funções de lista têm formatos de retorno diferentes.</span><span class="sxs-lookup"><span data-stu-id="f813a-131">Other list functions have different return formats.</span></span> <span data-ttu-id="f813a-132">formato de Olá toosee de uma função, incluí-la na secção de saídas Olá conforme mostrado no modelo de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="f813a-133">Observações</span><span class="sxs-lookup"><span data-stu-id="f813a-133">Remarks</span></span>

<span data-ttu-id="f813a-134">Todas as operações que começa com **lista** pode ser utilizado como uma função no modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="f813a-135">Olá operações disponíveis incluem não só listKeys, mas também operações como `list`, `listAdminKeys`, e `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="f813a-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="f813a-136">No entanto, não é possível utilizar **lista** operações que requerem valores de Olá corpo do pedido.</span><span class="sxs-lookup"><span data-stu-id="f813a-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="f813a-137">Por exemplo, Olá [lista conta SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operação requer os parâmetros de corpo do pedido como *signedExpiry*, por isso, não é possível utilizá-lo dentro de um modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="f813a-138">toodetermine que tipos de recursos tem uma operação de lista, terá de Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="f813a-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="f813a-139">Olá vista [operações de REST API](/rest/api/) para um fornecedor de recursos e procure para operações de lista.</span><span class="sxs-lookup"><span data-stu-id="f813a-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="f813a-140">Por exemplo, contas de armazenamento tem Olá [listKeys operação](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="f813a-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="f813a-141">Olá utilize [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f813a-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="f813a-142">Olá exemplo seguinte obtém todas as operações de lista para contas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="f813a-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="f813a-143">Utilize Olá comando da CLI do Azure toofilter Olá apenas operações de lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="f813a-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="f813a-144">Especificar recursos Olá utilizando qualquer um dos Olá [resourceId função](#resourceid), ou o formato de Olá `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="f813a-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="f813a-145">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f813a-145">Example</span></span>

<span data-ttu-id="f813a-146">Olá exemplo seguinte mostra como tooreturn Olá chaves primária e secundária de uma conta de armazenamento no Olá produz secção.</span><span class="sxs-lookup"><span data-stu-id="f813a-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="f813a-147">fornecedores</span><span class="sxs-lookup"><span data-stu-id="f813a-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="f813a-148">Devolve informações sobre um fornecedor de recursos e os respetivos tipos de recurso suportados.</span><span class="sxs-lookup"><span data-stu-id="f813a-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="f813a-149">Se não fornecer um tipo de recurso, a função de Olá devolve todos os tipos de Olá suportado para o fornecedor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="f813a-150">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f813a-150">Parameters</span></span>

| <span data-ttu-id="f813a-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f813a-151">Parameter</span></span> | <span data-ttu-id="f813a-152">Necessário</span><span class="sxs-lookup"><span data-stu-id="f813a-152">Required</span></span> | <span data-ttu-id="f813a-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="f813a-153">Type</span></span> | <span data-ttu-id="f813a-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="f813a-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f813a-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="f813a-155">providerNamespace</span></span> |<span data-ttu-id="f813a-156">Sim</span><span class="sxs-lookup"><span data-stu-id="f813a-156">Yes</span></span> |<span data-ttu-id="f813a-157">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-157">string</span></span> |<span data-ttu-id="f813a-158">Espaço de nomes do fornecedor de Olá</span><span class="sxs-lookup"><span data-stu-id="f813a-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="f813a-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="f813a-159">resourceType</span></span> |<span data-ttu-id="f813a-160">Não</span><span class="sxs-lookup"><span data-stu-id="f813a-160">No</span></span> |<span data-ttu-id="f813a-161">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-161">string</span></span> |<span data-ttu-id="f813a-162">Olá o tipo de recurso dentro Olá especificado espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="f813a-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f813a-163">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="f813a-163">Return value</span></span>

<span data-ttu-id="f813a-164">Cada tipo suportado é devolvido em Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="f813a-165">Ordenação de matriz de Olá devolveu valores não é garantida.</span><span class="sxs-lookup"><span data-stu-id="f813a-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="f813a-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f813a-166">Example</span></span>

<span data-ttu-id="f813a-167">Olá seguinte exemplo mostra como toouse Olá a função de fornecedor:</span><span class="sxs-lookup"><span data-stu-id="f813a-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f813a-168">Olá anterior exemplo devolve um objeto numa Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="f813a-169">Referência</span><span class="sxs-lookup"><span data-stu-id="f813a-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="f813a-170">Devolve um objeto que representa o estado do tempo de execução de um recurso.</span><span class="sxs-lookup"><span data-stu-id="f813a-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="f813a-171">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f813a-171">Parameters</span></span>

| <span data-ttu-id="f813a-172">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f813a-172">Parameter</span></span> | <span data-ttu-id="f813a-173">Necessário</span><span class="sxs-lookup"><span data-stu-id="f813a-173">Required</span></span> | <span data-ttu-id="f813a-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="f813a-174">Type</span></span> | <span data-ttu-id="f813a-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="f813a-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f813a-176">resourceName ou resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="f813a-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="f813a-177">Sim</span><span class="sxs-lookup"><span data-stu-id="f813a-177">Yes</span></span> |<span data-ttu-id="f813a-178">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-178">string</span></span> |<span data-ttu-id="f813a-179">Nome ou o identificador exclusivo de um recurso.</span><span class="sxs-lookup"><span data-stu-id="f813a-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="f813a-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f813a-180">apiVersion</span></span> |<span data-ttu-id="f813a-181">Não</span><span class="sxs-lookup"><span data-stu-id="f813a-181">No</span></span> |<span data-ttu-id="f813a-182">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-182">string</span></span> |<span data-ttu-id="f813a-183">Versão de API do Olá recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="f813a-183">API version of hello specified resource.</span></span> <span data-ttu-id="f813a-184">Inclua este parâmetro quando o recurso de Olá não está aprovisionado dentro do mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="f813a-185">Normalmente, no formato de Olá, **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="f813a-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f813a-186">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="f813a-186">Return value</span></span>

<span data-ttu-id="f813a-187">Cada tipo de recurso devolve propriedades diferentes para a função de referência de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="f813a-188">função Olá não devolve um formato único e predefinido.</span><span class="sxs-lookup"><span data-stu-id="f813a-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="f813a-189">Propriedades de Olá toosee para um tipo de recurso, devolver objeto Olá Olá produz secção conforme mostrado no exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="f813a-190">Observações</span><span class="sxs-lookup"><span data-stu-id="f813a-190">Remarks</span></span>

<span data-ttu-id="f813a-191">função de referência de Olá deriva o respetivo valor a partir de um Estado de runtime e, por conseguinte, não pode ser utilizada na secção de variáveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="f813a-192">Pode ser utilizado na secção de saídas de um modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="f813a-193">Ao utilizar a função de referência de Olá, implicitamente declarar que um recurso depende outro recurso, se o recurso de Olá referenciado é aprovisionado dentro do mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="f813a-194">Não é necessário tooalso utilize Olá dependsOn a propriedade.</span><span class="sxs-lookup"><span data-stu-id="f813a-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="f813a-195">Olá função não é avaliada até hello recurso referenciado concluiu a implementação.</span><span class="sxs-lookup"><span data-stu-id="f813a-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="f813a-196">os nomes de propriedade de Olá toosee e valores para um tipo de recurso, crie um modelo que devolve o objeto de Olá Olá saídas secção.</span><span class="sxs-lookup"><span data-stu-id="f813a-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="f813a-197">Se tiver um recurso existente desse tipo, o seu modelo devolve o objeto de Olá sem a implementar quaisquer novos recursos.</span><span class="sxs-lookup"><span data-stu-id="f813a-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="f813a-198">Normalmente, utiliza Olá **referência** funcionar tooreturn um valor específico de um objeto, tal como o ponto final do blob Olá URI ou o nome de domínio completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="f813a-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="f813a-199">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f813a-199">Example</span></span>

<span data-ttu-id="f813a-200">referência e toodeploy recurso Olá Olá mesmo modelo, utilize:</span><span class="sxs-lookup"><span data-stu-id="f813a-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="f813a-201">Olá anterior exemplo devolve um objeto numa Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="f813a-202">Olá exemplo que se segue faz referência a uma conta de armazenamento que não seja implementada neste modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="f813a-203">Olá conta de armazenamento já existe num Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f813a-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="f813a-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="f813a-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="f813a-205">Devolve um objeto que representa o grupo de recursos atual Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="f813a-206">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="f813a-206">Return value</span></span>

<span data-ttu-id="f813a-207">Olá devolveu o objeto está no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="f813a-208">Observações</span><span class="sxs-lookup"><span data-stu-id="f813a-208">Remarks</span></span>

<span data-ttu-id="f813a-209">Uma utilização comum da função de resourceGroup Olá é recursos toocreate Olá mesma localização do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="f813a-210">Olá exemplo seguinte utiliza Olá recursos localização tooassign Olá localização do grupo de para um web site.</span><span class="sxs-lookup"><span data-stu-id="f813a-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="f813a-211">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f813a-211">Example</span></span>

<span data-ttu-id="f813a-212">Olá modelo seguinte devolve as propriedades de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f813a-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f813a-213">Olá anterior exemplo devolve um objeto numa Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="f813a-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="f813a-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="f813a-215">Devolve Olá Identificador exclusivo de um recurso.</span><span class="sxs-lookup"><span data-stu-id="f813a-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="f813a-216">Utilize esta função quando o nome de recurso Olá é ambíguo ou não aprovisionada no Olá mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="f813a-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="f813a-217">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f813a-217">Parameters</span></span>

| <span data-ttu-id="f813a-218">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f813a-218">Parameter</span></span> | <span data-ttu-id="f813a-219">Necessário</span><span class="sxs-lookup"><span data-stu-id="f813a-219">Required</span></span> | <span data-ttu-id="f813a-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="f813a-220">Type</span></span> | <span data-ttu-id="f813a-221">Descrição</span><span class="sxs-lookup"><span data-stu-id="f813a-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f813a-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="f813a-222">subscriptionId</span></span> |<span data-ttu-id="f813a-223">Não</span><span class="sxs-lookup"><span data-stu-id="f813a-223">No</span></span> |<span data-ttu-id="f813a-224">cadeia (formato de GUID no)</span><span class="sxs-lookup"><span data-stu-id="f813a-224">string (In GUID format)</span></span> |<span data-ttu-id="f813a-225">Valor predefinido é subscrição atual Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-225">Default value is hello current subscription.</span></span> <span data-ttu-id="f813a-226">Especificar este valor quando precisar de tooretrieve um recurso na outra subscrição.</span><span class="sxs-lookup"><span data-stu-id="f813a-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="f813a-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="f813a-227">resourceGroupName</span></span> |<span data-ttu-id="f813a-228">Não</span><span class="sxs-lookup"><span data-stu-id="f813a-228">No</span></span> |<span data-ttu-id="f813a-229">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-229">string</span></span> |<span data-ttu-id="f813a-230">Valor predefinido é o grupo de recursos atual.</span><span class="sxs-lookup"><span data-stu-id="f813a-230">Default value is current resource group.</span></span> <span data-ttu-id="f813a-231">Especificar este valor quando precisar de tooretrieve um recurso noutro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f813a-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="f813a-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="f813a-232">resourceType</span></span> |<span data-ttu-id="f813a-233">Sim</span><span class="sxs-lookup"><span data-stu-id="f813a-233">Yes</span></span> |<span data-ttu-id="f813a-234">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-234">string</span></span> |<span data-ttu-id="f813a-235">Tipo de recurso, incluindo o espaço de nomes de fornecedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f813a-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="f813a-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="f813a-236">resourceName1</span></span> |<span data-ttu-id="f813a-237">Sim</span><span class="sxs-lookup"><span data-stu-id="f813a-237">Yes</span></span> |<span data-ttu-id="f813a-238">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-238">string</span></span> |<span data-ttu-id="f813a-239">Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="f813a-239">Name of resource.</span></span> |
| <span data-ttu-id="f813a-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="f813a-240">resourceName2</span></span> |<span data-ttu-id="f813a-241">Não</span><span class="sxs-lookup"><span data-stu-id="f813a-241">No</span></span> |<span data-ttu-id="f813a-242">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-242">string</span></span> |<span data-ttu-id="f813a-243">Recursos nome segmento seguinte se o recurso está aninhado.</span><span class="sxs-lookup"><span data-stu-id="f813a-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f813a-244">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="f813a-244">Return value</span></span>

<span data-ttu-id="f813a-245">Identificador de Olá é devolvido em Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="f813a-246">Observações</span><span class="sxs-lookup"><span data-stu-id="f813a-246">Remarks</span></span>

<span data-ttu-id="f813a-247">Olá valores de parâmetros que especificou dependem se o recurso de Olá tem Olá mesmo grupo de recursos e subscrição implementação atual Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="f813a-248">ID de recurso de Olá tooget para uma conta de armazenamento no Olá mesma subscrição e grupo de recursos, utilize:</span><span class="sxs-lookup"><span data-stu-id="f813a-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="f813a-249">Olá tooget Olá ID de recurso para uma conta do storage na mesma subscrição, mas um grupo de recursos diferente, utilize:</span><span class="sxs-lookup"><span data-stu-id="f813a-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="f813a-250">ID de recurso de Olá tooget para uma conta de armazenamento numa subscrição diferente e o grupo de recursos, utilize:</span><span class="sxs-lookup"><span data-stu-id="f813a-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="f813a-251">ID de recurso de Olá tooget para uma base de dados de um grupo de recursos diferente, utilize:</span><span class="sxs-lookup"><span data-stu-id="f813a-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="f813a-252">Muitas vezes, precisa de toouse esta função quando utilizar uma conta de armazenamento ou de rede virtual num grupo de recursos alternativo.</span><span class="sxs-lookup"><span data-stu-id="f813a-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="f813a-253">Olá exemplo seguinte mostra como um recurso de um grupo de recursos externos pode facilmente ser utilizado:</span><span class="sxs-lookup"><span data-stu-id="f813a-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="f813a-254">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f813a-254">Example</span></span>

<span data-ttu-id="f813a-255">Olá exemplo seguinte devolve Olá ID de recurso para uma conta de armazenamento no grupo de recursos de Olá:</span><span class="sxs-lookup"><span data-stu-id="f813a-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="f813a-256">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="f813a-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f813a-257">Nome</span><span class="sxs-lookup"><span data-stu-id="f813a-257">Name</span></span> | <span data-ttu-id="f813a-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="f813a-258">Type</span></span> | <span data-ttu-id="f813a-259">Valor</span><span class="sxs-lookup"><span data-stu-id="f813a-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f813a-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="f813a-260">sameRGOutput</span></span> | <span data-ttu-id="f813a-261">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-261">String</span></span> | <span data-ttu-id="f813a-262">/subscriptions/{current-sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="f813a-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="f813a-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="f813a-263">differentRGOutput</span></span> | <span data-ttu-id="f813a-264">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-264">String</span></span> | <span data-ttu-id="f813a-265">/subscriptions/{current-sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="f813a-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="f813a-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="f813a-266">differentSubOutput</span></span> | <span data-ttu-id="f813a-267">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-267">String</span></span> | <span data-ttu-id="f813a-268">/subscriptions/{different-sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="f813a-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="f813a-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="f813a-269">nestedResourceOutput</span></span> | <span data-ttu-id="f813a-270">Cadeia</span><span class="sxs-lookup"><span data-stu-id="f813a-270">String</span></span> | <span data-ttu-id="f813a-271">/subscriptions/{current-sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.SQL/Servers/serverName/Databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="f813a-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="f813a-272">subscrição</span><span class="sxs-lookup"><span data-stu-id="f813a-272">subscription</span></span>
`subscription()`

<span data-ttu-id="f813a-273">Devolve detalhes sobre a subscrição de Olá para a implementação atual Olá.</span><span class="sxs-lookup"><span data-stu-id="f813a-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="f813a-274">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="f813a-274">Return value</span></span>

<span data-ttu-id="f813a-275">função de Olá devolve Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f813a-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="f813a-276">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f813a-276">Example</span></span>

<span data-ttu-id="f813a-277">Olá exemplo seguinte mostra a função de subscrição de Olá chamada Olá saídas secção.</span><span class="sxs-lookup"><span data-stu-id="f813a-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f813a-278">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f813a-278">Next steps</span></span>
* <span data-ttu-id="f813a-279">Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f813a-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f813a-280">toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f813a-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f813a-281">tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f813a-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="f813a-282">toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f813a-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

