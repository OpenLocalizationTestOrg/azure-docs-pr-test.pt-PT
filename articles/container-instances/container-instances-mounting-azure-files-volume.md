---
title: "aaaMounting um volume de ficheiros do Azure em instâncias de contentor do Azure"
description: "Saiba como toomount um Azure ficheiros de estado de toopersist de volume com instâncias de contentor do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Montar uma partilha de ficheiros do Azure com instâncias de contentor do Azure

Por predefinição, as instâncias de contentor do Azure são sem monitorização de estado. Se contentor Olá falhas ou interrompe, todos os respetivo estado é perdida. toopersist de estado para além da duração de Olá do contentor de Olá, tem de montar um volume de um arquivo de externo. Este artigo mostra como toomount um Azure partilha de ficheiros para utilização com instâncias de contentor do Azure.

## <a name="create-an-azure-file-share"></a>Criar uma partilha de ficheiros do Azure

Antes de utilizar uma partilha de ficheiros do Azure com instâncias de contentor do Azure, tem de criá-la. Executar Olá toocreate de script a seguir uma partilha de ficheiros do armazenamento conta toohost Olá e Olá partilha de si próprio. Tenha em atenção de que nome da conta de armazenamento Olá deve ser globalmente exclusivo, para que o script de Olá adiciona uma cadeia de base do valor aleatório toohello.

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a>Adquirir detalhes de acesso da conta de armazenamento

toomount partilha de um ficheiro do Azure como um volume em instâncias de contentor do Azure, terá três valores: Olá nome da conta de armazenamento, nome da partilha Olá e chave de acesso de armazenamento Olá. 

Se utilizou o script de Olá acima, o nome de conta do storage Olá foi criado com um valor no fim de Olá aleatório. cadeia de final tooquery Olá (incluindo Olá aleatório parte), utilize Olá os seguintes comandos:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Olá nome da partilha já é conhecido (é *acishare* no script de Olá acima), pelo que tudo o que resta é Olá armazenamento chave da conta, que pode ser encontrado utilizando Olá os seguintes comandos:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Armazene os detalhes de acesso da conta de armazenamento com o Cofre de chaves do Azure

Chaves de conta de armazenamento protegem os dados de tooyour de acesso, pelo que recomendamos que armazene-os num cofre de chaves do Azure. 

Crie um cofre de chaves com Olá CLI do Azure:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Olá `enabled-for-template-deployment` comutador permite do Azure Resource Manager toopull segredos do seu Cofre de chaves no momento da implementação.

Armazenar a chave de conta do storage Olá como um novo segredo no Cofre de chaves Olá:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Montar o volume de Olá

Montar uma partilha de ficheiros do Azure como um volume num contentor é um processo de dois passos. Em primeiro lugar, forneça detalhes Olá da partilha de Olá como parte da definição de grupo do contentor de Olá, especificar como pretende que o volume de Olá montada num ou mais dos contentores Olá no grupo de Olá.

volumes de Olá toodefine pretende toomake disponível para a montagem, adicione um `volumes` matriz toohello definição de grupo contentor no modelo do Azure Resource Manager Olá, em seguida, referenciá-los na definição de Olá de contentores individuais Olá.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

modelo de Olá inclui o nome de conta do storage Olá e a chave como parâmetros, o que podem ser fornecidos num ficheiro separado de parâmetros. ficheiro de parâmetros de Olá toopopulate, precisa de três valores: Olá nome da conta de armazenamento, Olá ID de recurso do seu Cofre de chaves do Azure e Olá nome secreto do Cofre de chaves que utilizou a chave de armazenamento de Olá toostore. Se seguiu os passos anteriores, pode obter estes valores com Olá seguintes script:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Inserir valores Olá no ficheiro de parâmetros de Olá:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a>Implementar o contentor de Olá e gerir ficheiros

Com o modelo de Olá definido, pode criar o contentor de Olá e montar o volume utilizando Olá CLI do Azure. Partindo do princípio que hello ficheiro de modelo é denominado *azuredeploy. JSON* e o nome desse ficheiro de parâmetros de Olá *azuredeploy.parameters.json*, em seguida, é de linha de comandos Olá:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Assim que for iniciada contentor Olá cópias de segurança, pode utilizar a aplicação de web simples Olá implementada através de Olá **aci/seanmckenna-hellofiles** imagem, toohello gerir ficheiros numa partilha de ficheiros do Azure Olá no caminho de montagem de Olá que especificou. Obter o endereço de ip de Olá da aplicação web de Olá através do seguinte Olá:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Pode utilizar uma ferramenta como Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) tooretrieve e Inspecione a partilha de ficheiros do Olá ficheiro writen toohello.

>[!NOTE]
> toolearn mais informações sobre utilizar modelos Azure Resource Manager, os ficheiros de parâmetro e implementar com Olá CLI do Azure, consulte [implementar recursos com modelos do Resource Manager e a CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Passos seguintes

- Implementar para o seu primeiro contentor utilizando as instâncias de contentor do Azure Olá [início rápido](container-instances-quickstart.md)
- Saiba mais sobre Olá [relação entre instâncias de contentor do Azure e orchestrators de contentor](container-instances-orchestrator-relationship.md)
