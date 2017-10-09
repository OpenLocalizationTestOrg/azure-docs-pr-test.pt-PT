Versão 3.0 do módulo de AzureRm.Resources Olá incluídos alterações significativas na forma como trabalhar com etiquetas. Antes de continuar, verifique a sua versão:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Se os seus resultados mostram versão 3.0 ou posterior, exemplos de Olá neste tópico trabalham com o seu ambiente. Se a sua versão não for a 3.0 ou posterior, utilize a Galeria do PowerShell ou o Instalador de Plataforma Web para [atualizar a versão](/powershell/azureps-cmdlets-docs/), antes de continuar o tópico.

```powershell
Version
-------
3.5.0
```

Olá, toosee etiquetas existentes para um *grupo de recursos*, utilize:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Se o script devolve Olá seguinte formato:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

Olá, toosee etiquetas existentes para um *recursos que tem um ID de recurso especificado*, utilize:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Ou, toosee Olá etiquetas existentes para um *recursos que tem um grupo de recursos e o nome especificado*, utilize:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *grupos de recursos que tenham uma tag específica*, utilize:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *recursos que têm uma tag específica*, utilize:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Sempre que aplicar etiquetas tooa recursos ou um grupo de recursos, substituir etiquetas existente do Olá nesse recurso ou grupo de recursos. Por conseguinte, tem de utilizar uma abordagem diferente com base se os recursos de Olá ou grupo de recursos tem etiquetas existentes. 

tooadd etiquetas tooa *grupo de recursos sem etiquetas existentes*, utilize:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd etiquetas tooa *grupo de recursos que tem as etiquetas existentes*, obter etiquetas existente Olá, adicionar a nova tag de Olá e volte a aplicar etiquetas Olá:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd etiquetas tooa *recursos sem etiquetas existentes*, utilize:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd etiquetas tooa *recurso com etiquetas existentes*, utilize:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *mantém as etiquetas existentes nos recursos de Olá*, utilize Olá seguintes script:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *manter as etiquetas existentes em recursos que não são duplicados*, utilize Olá seguintes script:

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

tooremove todas as etiquetas, passa uma tabela hash vazio:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



