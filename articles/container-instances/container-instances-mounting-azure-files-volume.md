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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="9ed83-103">Montar uma partilha de ficheiros do Azure com instâncias de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="9ed83-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="9ed83-104">Por predefinição, as instâncias de contentor do Azure são sem monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="9ed83-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="9ed83-105">Se contentor Olá falhas ou interrompe, todos os respetivo estado é perdida.</span><span class="sxs-lookup"><span data-stu-id="9ed83-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="9ed83-106">toopersist de estado para além da duração de Olá do contentor de Olá, tem de montar um volume de um arquivo de externo.</span><span class="sxs-lookup"><span data-stu-id="9ed83-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="9ed83-107">Este artigo mostra como toomount um Azure partilha de ficheiros para utilização com instâncias de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed83-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="9ed83-108">Criar uma partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="9ed83-108">Create an Azure file share</span></span>

<span data-ttu-id="9ed83-109">Antes de utilizar uma partilha de ficheiros do Azure com instâncias de contentor do Azure, tem de criá-la.</span><span class="sxs-lookup"><span data-stu-id="9ed83-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="9ed83-110">Executar Olá toocreate de script a seguir uma partilha de ficheiros do armazenamento conta toohost Olá e Olá partilha de si próprio.</span><span class="sxs-lookup"><span data-stu-id="9ed83-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="9ed83-111">Tenha em atenção de que nome da conta de armazenamento Olá deve ser globalmente exclusivo, para que o script de Olá adiciona uma cadeia de base do valor aleatório toohello.</span><span class="sxs-lookup"><span data-stu-id="9ed83-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

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

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="9ed83-112">Adquirir detalhes de acesso da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9ed83-112">Acquire storage account access details</span></span>

<span data-ttu-id="9ed83-113">toomount partilha de um ficheiro do Azure como um volume em instâncias de contentor do Azure, terá três valores: Olá nome da conta de armazenamento, nome da partilha Olá e chave de acesso de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="9ed83-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="9ed83-114">Se utilizou o script de Olá acima, o nome de conta do storage Olá foi criado com um valor no fim de Olá aleatório.</span><span class="sxs-lookup"><span data-stu-id="9ed83-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="9ed83-115">cadeia de final tooquery Olá (incluindo Olá aleatório parte), utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9ed83-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="9ed83-116">Olá nome da partilha já é conhecido (é *acishare* no script de Olá acima), pelo que tudo o que resta é Olá armazenamento chave da conta, que pode ser encontrado utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9ed83-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="9ed83-117">Armazene os detalhes de acesso da conta de armazenamento com o Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="9ed83-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="9ed83-118">Chaves de conta de armazenamento protegem os dados de tooyour de acesso, pelo que recomendamos que armazene-os num cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed83-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="9ed83-119">Crie um cofre de chaves com Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="9ed83-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="9ed83-120">Olá `enabled-for-template-deployment` comutador permite do Azure Resource Manager toopull segredos do seu Cofre de chaves no momento da implementação.</span><span class="sxs-lookup"><span data-stu-id="9ed83-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="9ed83-121">Armazenar a chave de conta do storage Olá como um novo segredo no Cofre de chaves Olá:</span><span class="sxs-lookup"><span data-stu-id="9ed83-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="9ed83-122">Montar o volume de Olá</span><span class="sxs-lookup"><span data-stu-id="9ed83-122">Mount hello volume</span></span>

<span data-ttu-id="9ed83-123">Montar uma partilha de ficheiros do Azure como um volume num contentor é um processo de dois passos.</span><span class="sxs-lookup"><span data-stu-id="9ed83-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="9ed83-124">Em primeiro lugar, forneça detalhes Olá da partilha de Olá como parte da definição de grupo do contentor de Olá, especificar como pretende que o volume de Olá montada num ou mais dos contentores Olá no grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9ed83-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="9ed83-125">volumes de Olá toodefine pretende toomake disponível para a montagem, adicione um `volumes` matriz toohello definição de grupo contentor no modelo do Azure Resource Manager Olá, em seguida, referenciá-los na definição de Olá de contentores individuais Olá.</span><span class="sxs-lookup"><span data-stu-id="9ed83-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="9ed83-126">modelo de Olá inclui o nome de conta do storage Olá e a chave como parâmetros, o que podem ser fornecidos num ficheiro separado de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9ed83-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="9ed83-127">ficheiro de parâmetros de Olá toopopulate, precisa de três valores: Olá nome da conta de armazenamento, Olá ID de recurso do seu Cofre de chaves do Azure e Olá nome secreto do Cofre de chaves que utilizou a chave de armazenamento de Olá toostore.</span><span class="sxs-lookup"><span data-stu-id="9ed83-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="9ed83-128">Se seguiu os passos anteriores, pode obter estes valores com Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="9ed83-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="9ed83-129">Inserir valores Olá no ficheiro de parâmetros de Olá:</span><span class="sxs-lookup"><span data-stu-id="9ed83-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="9ed83-130">Implementar o contentor de Olá e gerir ficheiros</span><span class="sxs-lookup"><span data-stu-id="9ed83-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="9ed83-131">Com o modelo de Olá definido, pode criar o contentor de Olá e montar o volume utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed83-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="9ed83-132">Partindo do princípio que hello ficheiro de modelo é denominado *azuredeploy. JSON* e o nome desse ficheiro de parâmetros de Olá *azuredeploy.parameters.json*, em seguida, é de linha de comandos Olá:</span><span class="sxs-lookup"><span data-stu-id="9ed83-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="9ed83-133">Assim que for iniciada contentor Olá cópias de segurança, pode utilizar a aplicação de web simples Olá implementada através de Olá **aci/seanmckenna-hellofiles** imagem, toohello gerir ficheiros numa partilha de ficheiros do Azure Olá no caminho de montagem de Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="9ed83-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="9ed83-134">Obter o endereço de ip de Olá da aplicação web de Olá através do seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="9ed83-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="9ed83-135">Pode utilizar uma ferramenta como Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) tooretrieve e Inspecione a partilha de ficheiros do Olá ficheiro writen toohello.</span><span class="sxs-lookup"><span data-stu-id="9ed83-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="9ed83-136">toolearn mais informações sobre utilizar modelos Azure Resource Manager, os ficheiros de parâmetro e implementar com Olá CLI do Azure, consulte [implementar recursos com modelos do Resource Manager e a CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9ed83-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ed83-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9ed83-137">Next steps</span></span>

- <span data-ttu-id="9ed83-138">Implementar para o seu primeiro contentor utilizando as instâncias de contentor do Azure Olá [início rápido](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="9ed83-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="9ed83-139">Saiba mais sobre Olá [relação entre instâncias de contentor do Azure e orchestrators de contentor](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="9ed83-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
