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
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="d3bfe-104">Criar e implementar o seu primeiro modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3bfe-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="d3bfe-105">Este tópico explica os passos de Olá da criação do seu primeiro modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="d3bfe-106">Modelos do Resource Manager são ficheiros JSON que definem os recursos de Olá toodeploy é necessário para a sua solução.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="d3bfe-107">conceitos de Olá toounderstand associados a implementar e gerir as suas soluções do Azure, consulte [descrição geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="d3bfe-108">Se tiver recursos existentes e quiser tooget um modelo para esses recursos, consulte o artigo [exportar um modelo Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="d3bfe-109">modelos toocreate e rever, precisa de um editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="d3bfe-110">O [Visual Studio Code](https://code.visualstudio.com/) é um editor de código simples, open source para várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="d3bfe-111">Recomendamos vivamente que utilize o Visual Studio Code para criar modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="d3bfe-112">Este tópico parte do princípio de que está a utilizar o Código VS. No entanto, se tiver outro editor de JSON (por exemplo, o Visual Studio), pode utilizar esse editor.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3bfe-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d3bfe-113">Prerequisites</span></span>

* <span data-ttu-id="d3bfe-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-114">Visual Studio Code.</span></span> <span data-ttu-id="d3bfe-115">Se for preciso, instale-o a partir do site [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="d3bfe-116">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-116">An Azure subscription.</span></span> <span data-ttu-id="d3bfe-117">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="d3bfe-118">Criar o modelo</span><span class="sxs-lookup"><span data-stu-id="d3bfe-118">Create template</span></span>

<span data-ttu-id="d3bfe-119">Vamos começar com um modelo simple que implementa uma subscrição de tooyour de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="d3bfe-120">Selecione **Ficheiro** > **Novo Ficheiro**.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-120">Select **File** > **New File**.</span></span> 

   ![Novo ficheiro](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="d3bfe-122">Copie e cole Olá seguindo a sintaxe JSON para o ficheiro:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-122">Copy and paste hello following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="d3bfe-123">Os nomes das contas de armazenamento têm várias restrições tornam difícil tooset.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="d3bfe-124">nome de Olá tem de ter entre 3 e 24 carateres de comprimento, utilize apenas os números e letras minúsculas e de ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="d3bfe-125">Olá anterior o modelo utiliza a Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) funcionar toogenerate um valor de hash.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="d3bfe-126">toogive este hash valor mais significado, é adicionado o prefixo de Olá *armazenamento*.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="d3bfe-127">Guarde este ficheiro como **azuredeploy. JSON** tooa de pasta local.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Guardar o modelo](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="d3bfe-129">Implementar o modelo</span><span class="sxs-lookup"><span data-stu-id="d3bfe-129">Deploy template</span></span>

<span data-ttu-id="d3bfe-130">É toodeploy preparado neste modelo.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="d3bfe-131">Utilize o PowerShell ou a CLI do Azure toocreate um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="d3bfe-132">Em seguida, implemente um grupo de recursos de toothat de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="d3bfe-133">Para o PowerShell, utilize os seguintes comandos a partir da pasta de Olá que contém o modelo de Olá de Olá:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="d3bfe-134">Para uma instalação local da CLI do Azure, utilize os seguintes comandos a partir da pasta de Olá que contém o modelo de Olá de Olá:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="d3bfe-135">Quando a conclusão da implementação, a conta de armazenamento existe no grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="d3bfe-136">Implementar o modelo a partir do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d3bfe-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="d3bfe-137">Pode utilizar [nuvem Shell](../cloud-shell/overview.md) comandos toorun Olá CLI do Azure para implementar o modelo.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="d3bfe-138">No entanto, tem primeiro carregar o modelo para a partilha de ficheiros de Olá para a Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="d3bfe-139">Se não utilizou o Cloud Shell, consulte a [Descrição Geral do Azure Cloud Shell](../cloud-shell/overview.md) para obter informações sobre como o configurar.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="d3bfe-140">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="d3bfe-141">Selecione o grupo de recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="d3bfe-142">Olá padrão do nome é `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selecionar grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="d3bfe-144">Selecione a conta de armazenamento de Olá para a Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Selecionar a conta de armazenamento](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="d3bfe-146">Selecione **Ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-146">Select **Files**.</span></span>

   ![Selecionar ficheiros](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="d3bfe-148">Selecione a partilha de ficheiros de Olá para Shell da nuvem.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="d3bfe-149">Olá padrão do nome é `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selecionar a partilha de ficheiros](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="d3bfe-151">Selecione **Adicionar diretório**.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-151">Select **Add directory**.</span></span>

   ![Adicionar diretório](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="d3bfe-153">Atribua-lhe o nome **templates** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-153">Name it **templates**, and select **Okay**.</span></span>

   ![Atribuir um nome ao diretório](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="d3bfe-155">Selecione o novo diretório.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-155">Select your new directory.</span></span>

   ![Selecionar o diretório](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="d3bfe-157">Selecione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-157">Select **Upload**.</span></span>

   ![Selecionar a operação carregar](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="d3bfe-159">Localize e carregue o modelo.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-159">Find and upload your template.</span></span>

   ![Carregar o ficheiro](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="d3bfe-161">Linha Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-161">Open hello prompt.</span></span>

   ![Abrir o Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="d3bfe-163">Introduza Olá os seguintes comandos no Olá Shell de Cloud:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="d3bfe-164">Quando a conclusão da implementação, a conta de armazenamento existe no grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="d3bfe-165">Personalizar o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="d3bfe-165">Customize hello template</span></span>

<span data-ttu-id="d3bfe-166">modelo de Olá funciona bem, mas não é flexível.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="d3bfe-167">Implementa sempre um tooSouth armazenamento localmente redundante EUA Central.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="d3bfe-168">nome de Olá é sempre *armazenamento* seguido por um valor de hash.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="d3bfe-169">tooenable utilizando o modelo de Olá para diferentes cenários, adicionar parâmetros toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="d3bfe-170">Olá exemplo seguinte mostra secção de parâmetros de Olá com dois parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="d3bfe-171">Olá primeiro parâmetro `storageSKU` permite-lhe o tipo de Olá toospecify de redundância.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="d3bfe-172">Limita os valores de Olá que possa passar toovalues que são válidas para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="d3bfe-173">Também especifica um valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-173">It also specifies a default value.</span></span> <span data-ttu-id="d3bfe-174">Olá segundo parâmetro `storageNamePrefix` é conjunto tooallow um máximo de 11 carateres.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="d3bfe-175">Especifica um valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-175">It specifies a default value.</span></span>

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

<span data-ttu-id="d3bfe-176">Na secção de variáveis de Olá, adicione uma variável com o nome `storageName`.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="d3bfe-177">Combina o valor de prefixo Olá de parâmetros de Olá e um valor de hash de Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) função.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="d3bfe-178">Utiliza Olá [toLower](resource-group-template-functions-string.md#tolower) funcionar tooconvert todos os carateres toolowercase.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="d3bfe-179">toouse estes novos valores para a sua conta de armazenamento, altere a definição do recurso de Olá:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-179">toouse these new values for your storage account, change hello resource definition:</span></span>

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

<span data-ttu-id="d3bfe-180">Tenha em atenção que Olá nome da conta de armazenamento Olá está agora definida variável toohello que adicionou.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="d3bfe-181">o nome SKU de Olá está definido toohello valor do parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="d3bfe-182">Olá localização é definida Olá a mesma localização do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="d3bfe-183">Guarde o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-183">Save your file.</span></span> 

<span data-ttu-id="d3bfe-184">Depois de concluir os passos de Olá neste artigo, o modelo agora aspeto:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-184">After completing hello steps in this article, your template now looks like:</span></span>

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

## <a name="redeploy-template"></a><span data-ttu-id="d3bfe-185">Reimplementar o modelo</span><span class="sxs-lookup"><span data-stu-id="d3bfe-185">Redeploy template</span></span>

<span data-ttu-id="d3bfe-186">Volte a implementar o modelo de Olá com diferentes valores.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="d3bfe-187">Para o PowerShell, utilize:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="d3bfe-188">Para a CLI do Azure, utilize:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="d3bfe-189">Para Olá Shell de nuvem, carregue a partilha de ficheiros de toohello do modelo foi alterada.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="d3bfe-190">Substitua ficheiro existente Olá.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-190">Overwrite hello existing file.</span></span> <span data-ttu-id="d3bfe-191">Em seguida, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="d3bfe-192">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="d3bfe-192">Clean up resources</span></span>

<span data-ttu-id="d3bfe-193">Quando já não é necessário, limpe os recursos de Olá que implementou ao eliminar o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="d3bfe-194">Para o PowerShell, utilize:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="d3bfe-195">Para a CLI do Azure, utilize:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="d3bfe-196">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d3bfe-196">Next steps</span></span>
* <span data-ttu-id="d3bfe-197">toolearn mais informações sobre a estrutura de Olá de um modelo, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d3bfe-198">toolearn sobre as propriedades de Olá para uma conta de armazenamento, consulte [referência ao modelo de contas de armazenamento](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="d3bfe-199">modelos de conclusão de tooview para vários tipos de soluções, consulte Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
