---
title: "aaaCreate e publicar uma aplicação gerida do catálogo de serviço do Azure | Microsoft Docs"
description: "Mostra como toocreate do Azure gerida a aplicação que foi concebida para os membros da sua organização."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>Publicar uma aplicação gerida para consumo interno

Pode criar e publicar Azure [geridos aplicações](managed-application-overview.md) que se destinam a ser membros da sua organização. Por exemplo, um departamento de TI pode publicar aplicações geridas que garantir a conformidade com as normas organizacionais. Estas aplicações geridas estão disponíveis através do catálogo de serviços de Olá, Olá Azure Marketplace.

uma aplicação gerida para o catálogo de serviço Olá toopublish, tem de:

* Crie um pacote. zip que contém ficheiros de modelo necessários três Olá.
* Decida que utilizador, grupo ou aplicação precisa de aceder toohello o grupo de recursos na subscrição do utilizador Olá.
* Crie a definição da aplicação Olá gerido que pontos toohello. zip pacote e pedidos de acesso para a identidade de Olá.

## <a name="create-a-managed-application-package"></a>Criar um pacote de aplicações geridas

Step-by-Olá primeiro passo é toocreate Olá três modelo necessários ficheiros. Todos os três ficheiros de pacote para um ficheiro. zip e carregue a mesma localização acessível tooan, por exemplo, uma conta de armazenamento. Passar o ficheiro. zip toothis ligação quando criar Olá gerido definição da aplicação.

* **applianceMainTemplate.json**: este ficheiro define Olá Azure recursos aprovisionados como parte da Olá aplicações geridas. modelo de Olá é não diferente de um modelo do Resource Manager regular. Por exemplo, toocreate uma conta de armazenamento através de uma aplicação gerida, applianceMainTemplate.json contém:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**: os utilizadores implementar este modelo quando criar Olá aplicações geridas. Define recursos de aplicação Olá gerido, que é um tipo de recurso Microsoft.Solutions/appliances. Este ficheiro contém todos os parâmetros de Olá que precisa para recursos Olá applianceMainTemplate.json.

  Definir duas propriedades importantes neste modelo. Em primeiro lugar, Olá **applianceDefinitionId** propriedade é Olá ID de definição da aplicação Olá gerido. Criar definição Olá posterior deste tópico. Quando a definição deste valor, tem de decidir quais subscrição e toouse do grupo de recursos para armazenar Olá definições de aplicações geridas. Além disso, tem de decidir um nome para a definição de Olá. ID de Olá está num formato de Olá:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  Segundo, Olá **managedResourceGroupId** propriedade é o ID de Olá Olá do grupo de recursos onde hello recursos do Azure são criados. Pode atribuir um valor para este nome de grupo de recursos ou permitir que o utilizador Olá, forneça um nome. formato de Olá do ID de Olá é:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Olá seguinte exemplo mostra um ficheiro de mainTemplate.json. Especifica um grupo de recursos para recursos de Olá implementado. Olá ID da definição é toouse conjunto com o nome de uma definição **storageApp** num grupo de recursos denominado **managedApplicationGroup**. Pode alterar estes valores toouse diferentes nomes. Forneça a suas próprias ID de subscrição no ID de definição de Olá.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: Olá portal do Azure utiliza este ficheiro toogenerate Olá interface de utilizador para os utilizadores que criam Olá aplicações geridas. Definir a forma como os utilizadores forneçam entrada para cada parâmetro. Pode utilizar as opções, como uma lista pendente, caixa de texto, a caixa de palavra-passe e outras ferramentas de entrada. toolearn como toocreate um ficheiro de definição de IU para uma aplicação gerida, consulte [começar com CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Olá exemplo seguinte mostra um ficheiro de applianceCreateUiDefinition.json que permite que os utilizadores toospecify Olá armazenamento conta prefixo do nome através de uma caixa de texto.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

Depois de todos os ficheiros de Olá necessário estiverem prontos, empacotá-las como um ficheiro. zip. Step-by-Olá três ficheiros deverão estar no nível de raiz de Olá de ficheiro. zip de Olá. Se o put-los numa pasta, receberá um erro quando criar Olá gerido a definição da aplicação que indica a Olá necessários ficheiros não estão presentes. Carregar localização acessível do Olá pacote tooan onde podem ser consumidos. resto Olá deste artigo assume que o ficheiro. zip de Olá existe no contentor do blob storage acessível publicamente.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Criar um grupo de utilizadores do Azure Active Directory ou a aplicação

segundo passo de Olá é tooselect um grupo de utilizadores ou aplicações para gerir recursos de Olá em nome do cliente de Olá. Este grupo de utilizadores ou a aplicação não tem permissões no Olá gerido grupo de acordo com toohello função de recursos que está atribuída. função de Olá pode ser qualquer função de controlo de acesso baseado em funções (RBAC) incorporada, como o proprietário ou contribuinte. Também pode dar um utilizador individual recursos de Olá toomanage de permissão, mas normalmente atribuir o grupo de utilizadores de tooa esta permissão. toocreate um novo grupo de utilizadores do Active Directory, consulte [criar um grupo e adicionar membros no Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

Terá de ID de objeto Olá de Olá utilizador grupo toouse para gerir recursos de Olá. Olá seguinte exemplo mostra como tooget Olá ID de objeto de nome a apresentar do grupo de Olá:

```azurecli-interactive
az ad group show --group exampleGroupName
```

comando de exemplo de Olá devolve Olá seguinte saída:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

ID de objeto de Olá apenas tooretrieve, utilize:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Obter ID de definição de função Olá

Em seguida, terá de ID de definição de função Olá de Olá função incorporada RBAC pretende que o utilizador de toohello toogrant acesso, grupo de utilizadores ou aplicações. Normalmente, utiliza Olá proprietário ou função de contribuinte ou leitor. Olá comando a seguir mostra como tooget Olá ID de definição de função para a função de proprietário Olá:


```azurecli-interactive
az role definition list --name owner
```

Se o comando devolve Olá seguinte saída:

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

É necessário o valor de Olá da propriedade de "name" Olá de Olá anterior exemplo. Pode obter apenas essa propriedade com:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Criar a definição da aplicação Olá gerido

Se ainda não tiver um grupo de recursos para armazenar a definição da aplicação gerida, crie uma agora:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Agora, crie o recurso de definição de aplicação Olá gerido.

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

os parâmetros de Olá utilizados Olá anterior exemplo são:

* **grupo de recursos**: nome de Olá Olá do grupo de recursos onde Olá geridos a definição da aplicação é criado.
* **nível de bloqueio**: tipo de Olá de bloqueio colocadas num grupo de recursos geridos de Olá. Impede que o cliente de Olá efetuar operações indesejáveis neste grupo de recursos. Atualmente, só de leitura é Olá suportado apenas o nível de bloqueio. Quando é especificado só de leitura, o cliente Olá pode apenas ler recursos de Olá presentes no grupo de recursos geridos de Olá.
* **autorizações**: descreve Olá ID de principal e o ID de definição de função Olá são o grupo de recursos geridos de toohello de permissão de toogrant utilizados. Foi especificado no formato de Olá de `<principalId>:<roleDefinitionId>`. Vários valores também podem ser especificados para esta propriedade. Se forem necessárias vários valores, deve ser especificados no formato de Olá `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Vários valores separados por um espaço.
* **uri de ficheiro de pacote**: Olá localização Olá gerido do pacote de aplicação que contém ficheiros de modelo de Olá, que podem ser um blob de armazenamento do Azure.

## <a name="next-steps"></a>Passos seguintes

* Para aplicações de toomanaged uma introdução, consulte [descrição geral de aplicações gerido](managed-application-overview.md).
* Para obter exemplos de ficheiros de Olá, consulte [geridos amostras de aplicação](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Para obter informações sobre a consumir uma aplicação do catálogo de serviço geridas, consulte [consumir uma aplicação do catálogo de serviço geridas](managed-application-consumption.md).
* Para obter informações sobre a publicação de aplicações geridas de toohello Azure Marketplace, consulte [Azure geridos aplicações no mercado de Olá](managed-application-author-marketplace.md).
* Para obter informações sobre a consumir uma aplicação gerida Olá Marketplace, consulte [consuma Azure gerida aplicações no mercado de Olá](managed-application-consume-marketplace.md).
* toolearn como toocreate um ficheiro de definição de IU para uma aplicação gerida, consulte [começar com CreateUiDefinition](managed-application-createuidefinition-overview.md).
