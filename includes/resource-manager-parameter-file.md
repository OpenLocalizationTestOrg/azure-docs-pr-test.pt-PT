<span data-ttu-id="8a133-101">Se utilizar um valores de parâmetro de toopass de ficheiro de parâmetros durante a implementação, terá de toocreate um ficheiro JSON com um formato toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="8a133-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="8a133-102">o tamanho do ficheiro de parâmetros de Olá Olá não pode ser superior a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="8a133-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="8a133-103">Se precisar de tooprovide um valor sensível para um parâmetro (por exemplo, uma palavra-passe), adicione o Cofre de chaves de tooa esse valor.</span><span class="sxs-lookup"><span data-stu-id="8a133-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="8a133-104">Obter o Cofre de chaves Olá durante a implementação, conforme mostrado no exemplo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="8a133-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="8a133-105">Para obter mais informações, consulte [passar valores seguros durante a implementação](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="8a133-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

