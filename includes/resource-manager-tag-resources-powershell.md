<span data-ttu-id="fa86f-101">Versão 3.0 do módulo de AzureRm.Resources Olá incluídos alterações significativas na forma como trabalhar com etiquetas.</span><span class="sxs-lookup"><span data-stu-id="fa86f-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="fa86f-102">Antes de continuar, verifique a sua versão:</span><span class="sxs-lookup"><span data-stu-id="fa86f-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="fa86f-103">Se os seus resultados mostram versão 3.0 ou posterior, exemplos de Olá neste tópico trabalham com o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="fa86f-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="fa86f-104">Se a sua versão não for a 3.0 ou posterior, utilize a Galeria do PowerShell ou o Instalador de Plataforma Web para [atualizar a versão](/powershell/azureps-cmdlets-docs/), antes de continuar o tópico.</span><span class="sxs-lookup"><span data-stu-id="fa86f-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="fa86f-105">Olá, toosee etiquetas existentes para um *grupo de recursos*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="fa86f-106">Se o script devolve Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fa86f-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="fa86f-107">Olá, toosee etiquetas existentes para um *recursos que tem um ID de recurso especificado*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="fa86f-108">Ou, toosee Olá etiquetas existentes para um *recursos que tem um grupo de recursos e o nome especificado*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="fa86f-109">tooget *grupos de recursos que tenham uma tag específica*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="fa86f-110">tooget *recursos que têm uma tag específica*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="fa86f-111">Sempre que aplicar etiquetas tooa recursos ou um grupo de recursos, substituir etiquetas existente do Olá nesse recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fa86f-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="fa86f-112">Por conseguinte, tem de utilizar uma abordagem diferente com base se os recursos de Olá ou grupo de recursos tem etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="fa86f-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="fa86f-113">tooadd etiquetas tooa *grupo de recursos sem etiquetas existentes*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="fa86f-114">tooadd etiquetas tooa *grupo de recursos que tem as etiquetas existentes*, obter etiquetas existente Olá, adicionar a nova tag de Olá e volte a aplicar etiquetas Olá:</span><span class="sxs-lookup"><span data-stu-id="fa86f-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="fa86f-115">tooadd etiquetas tooa *recursos sem etiquetas existentes*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="fa86f-116">tooadd etiquetas tooa *recurso com etiquetas existentes*, utilize:</span><span class="sxs-lookup"><span data-stu-id="fa86f-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="fa86f-117">tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *mantém as etiquetas existentes nos recursos de Olá*, utilize Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="fa86f-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="fa86f-118">tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *manter as etiquetas existentes em recursos que não são duplicados*, utilize Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="fa86f-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="fa86f-119">tooremove todas as etiquetas, passa uma tabela hash vazio:</span><span class="sxs-lookup"><span data-stu-id="fa86f-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



