---
title: aaaCreate primeiro o modelo do Azure Resource Manager | Microsoft Docs
description: "Toocreating um guia passo a passo o primeiro modelo Azure Resource Manager. Mostra como toouse Olá referência de modelo para um modelo de Olá de toocreate de conta de armazenamento."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Criar e implementar o seu primeiro modelo do Azure Resource Manager
Este tópico explica os passos de Olá da criação do seu primeiro modelo Azure Resource Manager. Modelos do Resource Manager são ficheiros JSON que definem os recursos de Olá toodeploy é necessário para a sua solução. conceitos de Olá toounderstand associados a implementar e gerir as suas soluções do Azure, consulte [descrição geral do Azure Resource Manager](resource-group-overview.md). Se tiver recursos existentes e quiser tooget um modelo para esses recursos, consulte o artigo [exportar um modelo Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).

modelos toocreate e rever, precisa de um editor de JSON. O [Visual Studio Code](https://code.visualstudio.com/) é um editor de código simples, open source para várias plataformas. Recomendamos vivamente que utilize o Visual Studio Code para criar modelos do Resource Manager. Este tópico parte do princípio de que está a utilizar o Código VS. No entanto, se tiver outro editor de JSON (por exemplo, o Visual Studio), pode utilizar esse editor.

## <a name="prerequisites"></a>Pré-requisitos

* Visual Studio Code. Se for preciso, instale-o a partir do site [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Uma subscrição do Azure. Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="create-template"></a>Criar o modelo

Vamos começar com um modelo simple que implementa uma subscrição de tooyour de conta de armazenamento.

1. Selecione **Ficheiro** > **Novo Ficheiro**. 

   ![Novo ficheiro](./media/resource-manager-create-first-template/new-file.png)

2. Copie e cole Olá seguindo a sintaxe JSON para o ficheiro:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Os nomes das contas de armazenamento têm várias restrições tornam difícil tooset. nome de Olá tem de ter entre 3 e 24 carateres de comprimento, utilize apenas os números e letras minúsculas e de ser exclusivo. Olá anterior o modelo utiliza a Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) funcionar toogenerate um valor de hash. toogive este hash valor mais significado, é adicionado o prefixo de Olá *armazenamento*. 

3. Guarde este ficheiro como **azuredeploy. JSON** tooa de pasta local.

   ![Guardar o modelo](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Implementar o modelo

É toodeploy preparado neste modelo. Utilize o PowerShell ou a CLI do Azure toocreate um grupo de recursos. Em seguida, implemente um grupo de recursos de toothat de conta de armazenamento.

* Para o PowerShell, utilize os seguintes comandos a partir da pasta de Olá que contém o modelo de Olá de Olá:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Para uma instalação local da CLI do Azure, utilize os seguintes comandos a partir da pasta de Olá que contém o modelo de Olá de Olá:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Quando a conclusão da implementação, a conta de armazenamento existe no grupo de recursos de Olá.

## <a name="deploy-template-from-cloud-shell"></a>Implementar o modelo a partir do Cloud Shell

Pode utilizar [nuvem Shell](../cloud-shell/overview.md) comandos toorun Olá CLI do Azure para implementar o modelo. No entanto, tem primeiro carregar o modelo para a partilha de ficheiros de Olá para a Shell de nuvem. Se não utilizou o Cloud Shell, consulte a [Descrição Geral do Azure Cloud Shell](../cloud-shell/overview.md) para obter informações sobre como o configurar.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).   

2. Selecione o grupo de recursos do Cloud Shell. Olá padrão do nome é `cloud-shell-storage-<region>`.

   ![Selecionar grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Selecione a conta de armazenamento de Olá para a Shell de nuvem.

   ![Selecionar a conta de armazenamento](./media/resource-manager-create-first-template/select-storage.png)

4. Selecione **Ficheiros**.

   ![Selecionar ficheiros](./media/resource-manager-create-first-template/select-files.png)

5. Selecione a partilha de ficheiros de Olá para Shell da nuvem. Olá padrão do nome é `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selecionar a partilha de ficheiros](./media/resource-manager-create-first-template/select-file-share.png)

6. Selecione **Adicionar diretório**.

   ![Adicionar diretório](./media/resource-manager-create-first-template/select-add-directory.png)

7. Atribua-lhe o nome **templates** e selecione **OK**.

   ![Atribuir um nome ao diretório](./media/resource-manager-create-first-template/name-templates.png)

8. Selecione o novo diretório.

   ![Selecionar o diretório](./media/resource-manager-create-first-template/select-templates.png)

9. Selecione **Upload**.

   ![Selecionar a operação carregar](./media/resource-manager-create-first-template/select-upload.png)

10. Localize e carregue o modelo.

   ![Carregar o ficheiro](./media/resource-manager-create-first-template/upload-files.png)

11. Linha Olá aberta.

   ![Abrir o Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Introduza Olá os seguintes comandos no Olá Shell de Cloud:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Quando a conclusão da implementação, a conta de armazenamento existe no grupo de recursos de Olá.

## <a name="customize-hello-template"></a>Personalizar o modelo de Olá

modelo de Olá funciona bem, mas não é flexível. Implementa sempre um tooSouth armazenamento localmente redundante EUA Central. nome de Olá é sempre *armazenamento* seguido por um valor de hash. tooenable utilizando o modelo de Olá para diferentes cenários, adicionar parâmetros toohello modelo.

Olá exemplo seguinte mostra secção de parâmetros de Olá com dois parâmetros. Olá primeiro parâmetro `storageSKU` permite-lhe o tipo de Olá toospecify de redundância. Limita os valores de Olá que possa passar toovalues que são válidas para uma conta de armazenamento. Também especifica um valor predefinido. Olá segundo parâmetro `storageNamePrefix` é conjunto tooallow um máximo de 11 carateres. Especifica um valor predefinido.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

Na secção de variáveis de Olá, adicione uma variável com o nome `storageName`. Combina o valor de prefixo Olá de parâmetros de Olá e um valor de hash de Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) função. Utiliza Olá [toLower](resource-group-template-functions-string.md#tolower) funcionar tooconvert todos os carateres toolowercase.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse estes novos valores para a sua conta de armazenamento, altere a definição do recurso de Olá:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Tenha em atenção que Olá nome da conta de armazenamento Olá está agora definida variável toohello que adicionou. o nome SKU de Olá está definido toohello valor do parâmetro de Olá. Olá localização é definida Olá a mesma localização do grupo de recursos de Olá.

Guarde o ficheiro. 

Depois de concluir os passos de Olá neste artigo, o modelo agora aspeto:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Reimplementar o modelo

Volte a implementar o modelo de Olá com diferentes valores.

Para o PowerShell, utilize:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Para a CLI do Azure, utilize:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Para Olá Shell de nuvem, carregue a partilha de ficheiros de toohello do modelo foi alterada. Substitua ficheiro existente Olá. Em seguida, utilize Olá os seguintes comandos:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não é necessário, limpe os recursos de Olá que implementou ao eliminar o grupo de recursos de Olá.

Para o PowerShell, utilize:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Para a CLI do Azure, utilize:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre a estrutura de Olá de um modelo, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sobre as propriedades de Olá para uma conta de armazenamento, consulte [referência ao modelo de contas de armazenamento](/azure/templates/microsoft.storage/storageaccounts).
* modelos de conclusão de tooview para vários tipos de soluções, consulte Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).
