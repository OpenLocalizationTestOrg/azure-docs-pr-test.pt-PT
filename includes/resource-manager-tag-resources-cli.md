utilizar tooadd um grupo de recursos de tooa etiquetas, **conjunto de grupos do azure**. Se o grupo de recursos de Olá não tem quaisquer etiquetas existentes, passe na tag de Olá.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

As etiquetas são atualizadas como um todo. Se quiser tooadd um grupo de recursos do tooa a etiqueta que tem as etiquetas existentes, transmita todas as etiquetas de Olá. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

As etiquetas não são herdadas pelo recursos num grupo de recursos. utilizar tooadd um recurso de tooa etiquetas, **conjunto de recursos do azure**. Passe Olá número de versão de API para o tipo de recurso de Olá que estiver a adicionar tag Olá. Se precisar de versão de API de Olá tooretrieve, utilize Olá comando com o fornecedor de recursos de Olá para o tipo de Olá que estiver a definir os seguintes:

```azurecli
azure provider show -n Microsoft.Storage --json
```

Nos resultados de Olá, procure o tipo de recurso Olá que quiser.

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

Agora, forneça essa versão de API, nome do grupo de recursos, o nome do recurso, o tipo de recurso e o valor de etiqueta como parâmetros.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Etiquetas existem diretamente no recursos e os grupos de recursos. toosee Olá existente as etiquetas, obter um grupo de recursos e os respetivos recursos com **mostrar de grupo do azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Que devolve metadados sobre o grupo de recursos de Olá, incluindo quaisquer tooit etiquetas aplicadas.

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

Ver as etiquetas de Olá para um recurso específico utilizando **mostrar de recursos do azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve todos os recursos de Olá com um valor de etiqueta, utilize:

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve todos os grupos de recursos de Olá com um valor de etiqueta, utilize:

```azurecli
azure group list -t Dept=Finance
```

Pode ver as etiquetas existentes de Olá na sua subscrição com Olá os seguintes comandos:

```azurecli
azure tag list
```
