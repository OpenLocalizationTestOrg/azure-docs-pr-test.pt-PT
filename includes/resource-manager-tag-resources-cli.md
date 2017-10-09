<span data-ttu-id="0a6cf-101">utilizar tooadd um grupo de recursos de tooa etiquetas, **conjunto de grupos do azure**.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="0a6cf-102">Se o grupo de recursos de Olá não tem quaisquer etiquetas existentes, passe na tag de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="0a6cf-103">As etiquetas são atualizadas como um todo.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-103">Tags are updated as a whole.</span></span> <span data-ttu-id="0a6cf-104">Se quiser tooadd um grupo de recursos do tooa a etiqueta que tem as etiquetas existentes, transmita todas as etiquetas de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="0a6cf-105">As etiquetas não são herdadas pelo recursos num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="0a6cf-106">utilizar tooadd um recurso de tooa etiquetas, **conjunto de recursos do azure**.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="0a6cf-107">Passe Olá número de versão de API para o tipo de recurso de Olá que estiver a adicionar tag Olá.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="0a6cf-108">Se precisar de versão de API de Olá tooretrieve, utilize Olá comando com o fornecedor de recursos de Olá para o tipo de Olá que estiver a definir os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0a6cf-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="0a6cf-109">Nos resultados de Olá, procure o tipo de recurso Olá que quiser.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="0a6cf-110">Agora, forneça essa versão de API, nome do grupo de recursos, o nome do recurso, o tipo de recurso e o valor de etiqueta como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="0a6cf-111">Etiquetas existem diretamente no recursos e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="0a6cf-112">toosee Olá existente as etiquetas, obter um grupo de recursos e os respetivos recursos com **mostrar de grupo do azure**.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="0a6cf-113">Que devolve metadados sobre o grupo de recursos de Olá, incluindo quaisquer tooit etiquetas aplicadas.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="0a6cf-114">Ver as etiquetas de Olá para um recurso específico utilizando **mostrar de recursos do azure**.</span><span class="sxs-lookup"><span data-stu-id="0a6cf-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="0a6cf-115">tooretrieve todos os recursos de Olá com um valor de etiqueta, utilize:</span><span class="sxs-lookup"><span data-stu-id="0a6cf-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="0a6cf-116">tooretrieve todos os grupos de recursos de Olá com um valor de etiqueta, utilize:</span><span class="sxs-lookup"><span data-stu-id="0a6cf-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="0a6cf-117">Pode ver as etiquetas existentes de Olá na sua subscrição com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0a6cf-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
