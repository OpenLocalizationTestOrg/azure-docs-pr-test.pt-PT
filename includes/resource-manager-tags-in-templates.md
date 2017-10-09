tootag um recurso durante a implementação, adicionar Olá `tags` recursos de toohello do elemento que está a implementar. Forneça o nome da etiqueta Olá e valor.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Aplicam-se um nome de etiqueta do valor literal toohello
Olá exemplo seguinte mostra uma conta de armazenamento com duas etiquetas (`Dept` e `Environment`) que estão definidos valores tooliteral:

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

### <a name="apply-an-object-toohello-tag-element"></a>Aplicam-se num elemento de etiqueta do objecto toohello
Pode definir um parâmetro de objeto que armazena várias etiquetas e aplicam-se de que objeto toohello tag o elemento. Cada propriedade do objeto de Olá torna-se uma etiqueta para o recurso de Olá separada. Olá seguinte exemplo tem um parâmetro com o nome `tagValues` que é um elemento tag toohello aplicados.

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

### <a name="apply-a-json-string-toohello-tag-name"></a>Aplicam-se um nome de tag JSON toohello de cadeia

toostore muitos valores numa única tag, aplicar uma cadeia JSON que representa valores Olá. cadeia JSON toda Olá é armazenada como uma tag não pode exceder os 256 carateres. Olá seguinte exemplo tem uma única tag com o nome `CostCenter` que contém vários valores de uma cadeia JSON:  

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