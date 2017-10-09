<span data-ttu-id="9f935-101">tootag um recurso durante a implementação, adicionar Olá `tags` recursos de toohello do elemento que está a implementar.</span><span class="sxs-lookup"><span data-stu-id="9f935-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="9f935-102">Forneça o nome da etiqueta Olá e valor.</span><span class="sxs-lookup"><span data-stu-id="9f935-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="9f935-103">Aplicam-se um nome de etiqueta do valor literal toohello</span><span class="sxs-lookup"><span data-stu-id="9f935-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="9f935-104">Olá exemplo seguinte mostra uma conta de armazenamento com duas etiquetas (`Dept` e `Environment`) que estão definidos valores tooliteral:</span><span class="sxs-lookup"><span data-stu-id="9f935-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="9f935-105">Aplicam-se num elemento de etiqueta do objecto toohello</span><span class="sxs-lookup"><span data-stu-id="9f935-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="9f935-106">Pode definir um parâmetro de objeto que armazena várias etiquetas e aplicam-se de que objeto toohello tag o elemento.</span><span class="sxs-lookup"><span data-stu-id="9f935-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="9f935-107">Cada propriedade do objeto de Olá torna-se uma etiqueta para o recurso de Olá separada.</span><span class="sxs-lookup"><span data-stu-id="9f935-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="9f935-108">Olá seguinte exemplo tem um parâmetro com o nome `tagValues` que é um elemento tag toohello aplicados.</span><span class="sxs-lookup"><span data-stu-id="9f935-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="9f935-109">Aplicam-se um nome de tag JSON toohello de cadeia</span><span class="sxs-lookup"><span data-stu-id="9f935-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="9f935-110">toostore muitos valores numa única tag, aplicar uma cadeia JSON que representa valores Olá.</span><span class="sxs-lookup"><span data-stu-id="9f935-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="9f935-111">cadeia JSON toda Olá é armazenada como uma tag não pode exceder os 256 carateres.</span><span class="sxs-lookup"><span data-stu-id="9f935-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="9f935-112">Olá seguinte exemplo tem uma única tag com o nome `CostCenter` que contém vários valores de uma cadeia JSON:</span><span class="sxs-lookup"><span data-stu-id="9f935-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```