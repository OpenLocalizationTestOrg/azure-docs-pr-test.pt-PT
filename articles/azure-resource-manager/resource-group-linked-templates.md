---
title: "modelos de aaaLink para implementação do Azure | Microsoft Docs"
description: "Descreve como toouse ligado modelos num toocreate de modelo Azure Resource Manager uma solução de modelo modulares. Mostra como valores de parâmetros de toopass, especifique um ficheiro de parâmetros e criados dinamicamente URLs."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="977af-104">Utilizar modelos ligados ao implementar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="977af-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="977af-105">De dentro de um modelo Azure Resource Manager, pode ligar tooanother modelo, que lhe permite toodecompose a implementação para um conjunto de modelos direcionados e com uma finalidade específica.</span><span class="sxs-lookup"><span data-stu-id="977af-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="977af-106">Tal como acontece com decomposing uma aplicação em várias classes de código, decomposição proporciona vantagens em termos de teste, reutilização e facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="977af-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="977af-107">Pode passar os parâmetros a partir de um modelo de ligado tooa modelo principal e esses parâmetros diretamente podem mapear tooparameters ou variáveis expostas pelo Olá chamar o modelo.</span><span class="sxs-lookup"><span data-stu-id="977af-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="977af-108">modelo ligado Olá também pode passar de um modelo de origem da variável toohello back-saída, ativar uma troca de dados bidirecional entre os modelos.</span><span class="sxs-lookup"><span data-stu-id="977af-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="977af-109">Ligação tooa modelo</span><span class="sxs-lookup"><span data-stu-id="977af-109">Linking tooa template</span></span>
<span data-ttu-id="977af-110">Criar uma ligação entre dois modelos, adicionando um recurso de implementação no modelo principal Olá esse toohello de pontos ligado modelo.</span><span class="sxs-lookup"><span data-stu-id="977af-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="977af-111">Definir Olá **templateLink** propriedade toohello URI de modelo de Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="977af-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="977af-112">Pode fornecer valores de parâmetro de modelo ligado Olá diretamente no seu modelo ou um ficheiro de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="977af-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="977af-113">Olá exemplo seguinte utiliza Olá **parâmetros** propriedade toospecify diretamente um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="977af-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="977af-114">Como outros tipos de recursos, pode definir as dependências entre modelo ligado Olá e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="977af-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="977af-115">Por conseguinte, quando a outros recursos necessitam de um valor de saída do modelo ligado Olá, pode certificar-se modelo ligado Olá é implementado antes de lhes.</span><span class="sxs-lookup"><span data-stu-id="977af-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="977af-116">Em alternativa, quando o modelo ligado Olá depende de outros recursos, pode certificar-se a que outros recursos são implementados antes do modelo ligado Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="977af-117">Pode obter um valor de um modelo ligado com Olá sintaxe:</span><span class="sxs-lookup"><span data-stu-id="977af-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="977af-118">Olá serviço Gestor de recursos tem de ser modelo ligado do tooaccess capaz de Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="977af-119">Não é possível especificar um ficheiro local ou um ficheiro que só está disponível na sua rede local para o modelo de Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="977af-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="977af-120">Apenas pode fornecer um valor URI que inclui um **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="977af-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="977af-121">Uma das alternativas consiste tooplace seu modelo ligado numa conta de armazenamento e utilização hello URI para que o item, tal como mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="977af-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="977af-122">Embora o modelo ligado Olá tem de estar disponível externamente, não é necessário toobe toohello geralmente disponível público.</span><span class="sxs-lookup"><span data-stu-id="977af-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="977af-123">Pode adicionar a conta de armazenamento privada tooa de modelo que é proprietário da conta do storage Olá tooonly acessível.</span><span class="sxs-lookup"><span data-stu-id="977af-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="977af-124">Em seguida, crie um acesso de token tooenable de assinatura (SAS) de acesso partilhado durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="977af-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="977af-125">Adicionar esse toohello de token SAS URI para o modelo de Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="977af-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="977af-126">Para obter passos sobre como configurar um modelo de uma conta de armazenamento e de gerar um token SAS, consulte [implementar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md) ou [implementar recursos com modelos do Resource Manager e CLI do Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="977af-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="977af-127">Olá seguinte exemplo mostra um modelo de principal que o modelo tooanother ligações.</span><span class="sxs-lookup"><span data-stu-id="977af-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="977af-128">modelo ligado Olá é acedido com um token SAS, que é transmitido como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="977af-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="977af-129">Apesar do token de Olá seja transmitido como uma cadeia segura, hello URI do modelo ligado Olá, incluindo o token SAS de Olá, é registado em operações de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="977af-130">exposição toolimit, definir uma expiração do token de Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="977af-131">O Resource Manager processa cada modelo ligado como uma implementação separada.</span><span class="sxs-lookup"><span data-stu-id="977af-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="977af-132">No histórico de implementação de Olá Olá grupo de recursos, consulte implementações separadas para principal Olá e modelos aninhados.</span><span class="sxs-lookup"><span data-stu-id="977af-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![histórico de implementações](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="977af-134">Ligar o ficheiro de parâmetros tooa</span><span class="sxs-lookup"><span data-stu-id="977af-134">Linking tooa parameter file</span></span>
<span data-ttu-id="977af-135">utiliza o exemplo seguinte Olá Olá **parametersLink** ficheiro de parâmetros do propriedade toolink tooa.</span><span class="sxs-lookup"><span data-stu-id="977af-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="977af-136">Olá URI valor para o ficheiro de parâmetro ligado Olá não pode ser um ficheiro local e tem de incluir um **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="977af-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="977af-137">ficheiro de parâmetros de Olá também pode ser limitado tooaccess através de um token SAS.</span><span class="sxs-lookup"><span data-stu-id="977af-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="977af-138">Utilizar variáveis toolink modelos</span><span class="sxs-lookup"><span data-stu-id="977af-138">Using variables toolink templates</span></span>
<span data-ttu-id="977af-139">exemplos anteriores Olá mostrou valores codificados de URL para ligações de modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="977af-140">Esta abordagem poderá funcionar para um modelo simples, mas não funciona bem quando trabalhar com um grande conjunto de modelos modulares.</span><span class="sxs-lookup"><span data-stu-id="977af-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="977af-141">Em vez disso, pode criar uma variável estática que armazena um URL de base para o modelo de Olá principal e, em seguida, criar dinamicamente os URLs para os modelos de Olá ligado desse URL base.</span><span class="sxs-lookup"><span data-stu-id="977af-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="977af-142">benefício de Olá desta abordagem é que pode facilmente mover ou bifurcação modelo Olá porque precisa apenas de variável estática de Olá toochange no modelo principal Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="977af-143">modelo de principais de Olá transmite Olá URIs em toda a Olá decomposed modelo correto.</span><span class="sxs-lookup"><span data-stu-id="977af-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="977af-144">Olá exemplo seguinte mostra como toouse um toocreate URL base ligado dois URLs para modelos (**sharedTemplateUrl** e **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="977af-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="977af-145">Também pode utilizar [deployment()](resource-group-template-functions-deployment.md#deployment) tooget Olá URL base do modelo atual Olá e utilizar esse URL de Olá tooget para outros modelos de Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="977af-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="977af-146">Esta abordagem é útil se a localização do modelo for alterada (talvez devida tooversioning) ou se quiser tooavoid rígido codificação URLs no ficheiro de modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="977af-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="977af-147">Exemplo completo</span><span class="sxs-lookup"><span data-stu-id="977af-147">Complete example</span></span>
<span data-ttu-id="977af-148">Olá, modelos de exemplo a seguir mostra uma disposição simplificada de modelos ligados tooillustrate muitos outros dos conceitos de Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="977af-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="977af-149">Parte do princípio de modelos de Olá foram adicionados toohello desativado mesmo contentor numa conta do storage com o acesso público.</span><span class="sxs-lookup"><span data-stu-id="977af-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="977af-150">modelo ligado Olá transmite um modelo de principal do valor back toohello no Olá **produz** secção.</span><span class="sxs-lookup"><span data-stu-id="977af-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="977af-151">Olá **parent.json** ficheiro é composta por:</span><span class="sxs-lookup"><span data-stu-id="977af-151">hello **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="977af-152">Olá **helloworld.json** ficheiro é composta por:</span><span class="sxs-lookup"><span data-stu-id="977af-152">hello **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="977af-153">No PowerShell, obter um token para o contentor de Olá e implementem modelos Olá com:</span><span class="sxs-lookup"><span data-stu-id="977af-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="977af-154">No Azure CLI 2.0, obter um token para o contentor de Olá e implementar modelos de Olá com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="977af-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="977af-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="977af-155">Next steps</span></span>
* <span data-ttu-id="977af-156">toolearn sobre Olá definir Olá ordem de implementação para os seus recursos, consulte [definir dependências nos modelos Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="977af-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="977af-157">toolearn como toodefine um recurso, mas criar várias instâncias do mesmo, consulte [criar várias instâncias de recursos no Gestor de recursos do Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="977af-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

