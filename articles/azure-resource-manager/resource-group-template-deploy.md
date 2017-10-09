---
title: aaaDeploy recursos com o PowerShell e o modelo | Microsoft Docs
description: "Utilize o Azure Resource Manager e o Azure PowerShell toodeploy um tooAzure de recursos. recursos de Olá são definidos num modelo do Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="9a1ce-104">Implementar recursos com modelos do Resource Manager e do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a1ce-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="9a1ce-105">Este tópico explica como toouse Azure PowerShell com toodeploy de modelos do Resource Manager a tooAzure de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="9a1ce-106">Se não estiver familiarizado com conceitos de Olá implementar e gerir as suas soluções do Azure, consulte [descrição geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="9a1ce-107">modelo do Resource Manager Olá implementar possível ser um ficheiro no seu computador local ou um ficheiro externo que está localizado num repositório como GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="9a1ce-108">modelo de Olá implementar neste artigo está disponível no Olá [modelo de exemplo](#sample-template) secção, ou como [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="9a1ce-109">Implementar um modelo a partir do seu computador local</span><span class="sxs-lookup"><span data-stu-id="9a1ce-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="9a1ce-110">Quando implementar tooAzure de recursos, pode:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="9a1ce-111">Inicie sessão no tooyour a conta do Azure</span><span class="sxs-lookup"><span data-stu-id="9a1ce-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="9a1ce-112">Crie um grupo de recursos que funciona como contentor Olá recursos Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="9a1ce-113">nome de Olá Olá do grupo de recursos só pode incluir carateres alfanuméricos, pontos, carateres de sublinhado, hífenes e parênteses.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="9a1ce-114">Pode ser a cópia de segurança too90 carateres.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-114">It can be up too90 characters.</span></span> <span data-ttu-id="9a1ce-115">Não pode terminar num período.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="9a1ce-116">Implementar a modelo Olá de grupo de recursos de toohello que define Olá recursos toocreate</span><span class="sxs-lookup"><span data-stu-id="9a1ce-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="9a1ce-117">Um modelo pode incluir os parâmetros que permitem a implementação de Olá toocustomize.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="9a1ce-118">Por exemplo, pode fornecer valores que são adaptados para um ambiente específico (por exemplo, o desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="9a1ce-119">modelo de exemplo de Olá define um parâmetro da conta de armazenamento Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="9a1ce-120">Olá seguinte exemplo cria um grupo de recursos e implementa um modelo a partir do seu computador local:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="9a1ce-121">implementação de Olá pode demorar alguns minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="9a1ce-122">Quando terminar, verá uma mensagem que inclui o resultado de Olá:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="9a1ce-123">Implementar um modelo a partir de uma origem externa</span><span class="sxs-lookup"><span data-stu-id="9a1ce-123">Deploy a template from an external source</span></span>

<span data-ttu-id="9a1ce-124">Em vez de armazenar modelos do Resource Manager no seu computador local, pode preferir toostore-las numa localização externa.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="9a1ce-125">Pode armazenar modelos num repositório de controlo de origem (por exemplo, o GitHub).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="9a1ce-126">Em alternativa, pode armazená-las numa conta de armazenamento do Azure para acesso partilhado na sua organização.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="9a1ce-127">toodeploy um modelo externo, utilize Olá **TemplateUri** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="9a1ce-128">Utilize Olá URI no modelo de exemplo do Olá exemplo toodeploy Olá a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="9a1ce-129">Olá anterior exemplo requer um URI acessível publicamente para modelo de Olá, que funciona para a maioria dos cenários, porque o modelo não deve incluir dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="9a1ce-130">Se precisar de toospecify dados confidenciais (por exemplo, uma palavra-passe de administrador), passe esse valor como um parâmetro seguro.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="9a1ce-131">No entanto, se não pretender que o modelo toobe acessível publicamente, pode protegê-lo armazenando-o num contentor de armazenamento privada.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="9a1ce-132">Para obter informações sobre a implementação de um modelo que necessita de um token de assinatura (SAS) de acesso partilhado, consulte [implementar a modelo privado com o SAS token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="9a1ce-133">Ficheiros de parâmetro</span><span class="sxs-lookup"><span data-stu-id="9a1ce-133">Parameter files</span></span>

<span data-ttu-id="9a1ce-134">Em vez de a transmitir parâmetros como valores de inline no script, pode encontrá-lo mais fácil toouse um ficheiro JSON que contém os valores de parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="9a1ce-135">ficheiro de parâmetros de Olá tem de constar Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-135">hello parameter file must be in hello following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="9a1ce-136">Tenha em atenção que a secção de parâmetros de Olá inclui um nome de parâmetro que corresponda ao parâmetro Olá definido no seu modelo (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="9a1ce-137">ficheiro de parâmetros de Olá contém um valor para parâmetro Olá.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="9a1ce-138">Este valor é automaticamente transmitido toohello modelo durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="9a1ce-139">Pode criar vários ficheiros de parâmetro para diferentes cenários de implementação e, então, passe no ficheiro de parâmetro adequado Olá.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="9a1ce-140">Copie Olá anterior exemplo e guarde-o como um ficheiro denominado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="9a1ce-141">toopass um ficheiro de parâmetros local, utilizar Olá **TemplateParameterFile** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="9a1ce-142">toopass um ficheiro de parâmetros externos, utilize Olá **TemplateParameterUri** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="9a1ce-143">Pode utilizar parâmetros inline e um parâmetro de local ficheiros Olá mesma operação de implementação.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="9a1ce-144">Por exemplo, pode especificar alguns valores no ficheiro de parâmetro de local de Olá e adicionar outro inline valores durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="9a1ce-145">Se fornecer valores para um parâmetro num ficheiro de parâmetro de local de Olá e inline, o valor de inline Olá tem precedência.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="9a1ce-146">No entanto, quando utiliza um ficheiro de parâmetros externos, não poder passar outros valores ou inline ou a partir de um ficheiro local.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="9a1ce-147">Quando especificar um ficheiro de parâmetros no Olá **TemplateParameterUri** parâmetro, inline todos os parâmetros são ignorados.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="9a1ce-148">Fornece todos os valores de parâmetros no ficheiro externo Olá.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="9a1ce-149">Se o seu modelo incluir um valor confidencial que não pode incluir no ficheiro de parâmetros de Olá, adicione o Cofre de chaves de tooa esse valor ou fornecer dinamicamente a todas as inline de valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="9a1ce-150">Se o seu modelo inclui um parâmetro com o mesmo nome como um dos parâmetros Olá Olá comando do PowerShell de Olá, PowerShell apresenta o parâmetro de Olá a partir do seu modelo com o sufixo de Olá **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="9a1ce-151">Por exemplo, um parâmetro com o nome **ResourceGroupName** no seu conflitos de modelo com Olá **ResourceGroupName** parâmetro Olá [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="9a1ce-152">São tooprovide pedido um valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="9a1ce-153">Em geral, deve evitar este confusão ao nomear não parâmetros com Olá mesmo nome como parâmetros utilizada para operações de implementação.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="9a1ce-154">Testar um modelo de implementação</span><span class="sxs-lookup"><span data-stu-id="9a1ce-154">Test a template deployment</span></span>

<span data-ttu-id="9a1ce-155">Utilize os valores de parâmetros de modelo e sem a implementar, na verdade, quaisquer recursos, de tootest [teste-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="9a1ce-156">Se forem detetados sem erros, o comando de Olá terminar sem uma resposta.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="9a1ce-157">Se for detetado um erro, o comando de Olá devolve uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="9a1ce-158">Por exemplo, se tentar toopass um valor incorreto para a conta de armazenamento Olá SKU, devolve Olá seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="9a1ce-159">Se o seu modelo tem um erro de sintaxe, o comando de Olá devolve um erro que indica que não foi possível analisar o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="9a1ce-160">mensagem de saudação indica o número de linha de Olá e posição de Olá erro de análise.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="9a1ce-161">modo de toouse concluída, utilize Olá `Mode` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="9a1ce-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="9a1ce-162">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="9a1ce-162">Sample template</span></span>

<span data-ttu-id="9a1ce-163">Olá seguinte modelo é utilizado para obter exemplos de Olá neste tópico.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="9a1ce-164">Copie e guarde-o como um ficheiro denominado storage.json.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="9a1ce-165">toounderstand como toocreate este modelo, consulte [criar o primeiro modelo Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="9a1ce-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a1ce-166">Next steps</span></span>
* <span data-ttu-id="9a1ce-167">Exemplos de Olá neste artigo implementar o grupo de recursos de tooa recursos na sua subscrição predefinida.</span><span class="sxs-lookup"><span data-stu-id="9a1ce-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="9a1ce-168">toouse uma subscrição diferente, consulte [gerir várias subscrições do Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="9a1ce-169">Para um script de exemplo completo que implementa um modelo, consulte [script de implementação de modelos do Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="9a1ce-170">toounderstand como toodefine parâmetros no modelo, consulte [compreender a sintaxe de modelos Azure Resource Manager e estrutura Olá](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9a1ce-171">Para sugestões sobre como resolver erros comuns de implementação, consulte [resolver erros comuns de implementação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="9a1ce-172">Para obter informações sobre a implementação de um modelo que necessita de um token SAS, consulte [implementar a modelo privado com o SAS token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="9a1ce-173">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9a1ce-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

