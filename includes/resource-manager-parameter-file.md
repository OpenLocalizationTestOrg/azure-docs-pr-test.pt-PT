Se utilizar um valores de parâmetro de toopass de ficheiro de parâmetros durante a implementação, terá de toocreate um ficheiro JSON com um formato toohello semelhante seguinte exemplo:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

o tamanho do ficheiro de parâmetros de Olá Olá não pode ser superior a 64 KB.

Se precisar de tooprovide um valor sensível para um parâmetro (por exemplo, uma palavra-passe), adicione o Cofre de chaves de tooa esse valor. Obter o Cofre de chaves Olá durante a implementação, conforme mostrado no exemplo anterior Olá. Para obter mais informações, consulte [passar valores seguros durante a implementação](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

