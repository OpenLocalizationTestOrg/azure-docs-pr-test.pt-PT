---
title: "aaaCreate a sua primeira função do Olá CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate a sua primeira Azure funcionar para a utilização de execução sem servidor Olá CLI do Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="76f7f-103">Criar a sua primeira função com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="76f7f-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="76f7f-104">Este tutorial de início rápido explica como toouse das funções do Azure toocreate sua primeira função.</span><span class="sxs-lookup"><span data-stu-id="76f7f-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="76f7f-105">Utilize Olá CLI do Azure toocreate uma aplicação de função, o que é Olá infraestrutura sem servidor que aloja a função.</span><span class="sxs-lookup"><span data-stu-id="76f7f-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="76f7f-106">código de função Olá em si é implementado um repositório de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="76f7f-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="76f7f-107">Pode seguir os passos seguintes Olá num computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="76f7f-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76f7f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76f7f-108">Prerequisites</span></span> 

<span data-ttu-id="76f7f-109">Antes de executar este exemplo, tem de ter o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="76f7f-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="76f7f-110">Uma conta do [GitHub](https://github.com) ativa.</span><span class="sxs-lookup"><span data-stu-id="76f7f-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="76f7f-111">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="76f7f-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="76f7f-112">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="76f7f-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="76f7f-113">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="76f7f-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="76f7f-114">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="76f7f-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="76f7f-115">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="76f7f-115">Create a resource group</span></span>

<span data-ttu-id="76f7f-116">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="76f7f-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="76f7f-117">Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure, como aplicações Function App, bases de dados e contas de armazenamento, são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="76f7f-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="76f7f-118">Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="76f7f-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="76f7f-119">Se não estiver a utilizar o Cloud Shell, tem primeiro de iniciar sessão com o `az login`.</span><span class="sxs-lookup"><span data-stu-id="76f7f-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="76f7f-120">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="76f7f-120">Create an Azure Storage account</span></span>

<span data-ttu-id="76f7f-121">As funções utiliza um Estado de toomaintain de conta do Storage do Azure e outras informações sobre as suas funções.</span><span class="sxs-lookup"><span data-stu-id="76f7f-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="76f7f-122">Crie uma conta de armazenamento no grupo de recursos de Olá que criou utilizando Olá [criar conta de armazenamento az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="76f7f-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="76f7f-123">No Olá seguinte comando, substitua o seu próprio nome de conta de armazenamento globalmente exclusivo onde vir Olá `<storage_name>` marcador de posição.</span><span class="sxs-lookup"><span data-stu-id="76f7f-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="76f7f-124">Os nomes das contas do Storage devem ter entre 3 e 24 carateres de comprimento e apenas podem conter números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="76f7f-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="76f7f-125">Depois de ter sido criada a conta de armazenamento Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="76f7f-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a><span data-ttu-id="76f7f-126">Criar uma aplicação de função</span><span class="sxs-lookup"><span data-stu-id="76f7f-126">Create a function app</span></span>

<span data-ttu-id="76f7f-127">Tem de ter uma execução de Olá do função aplicação toohost das suas funções.</span><span class="sxs-lookup"><span data-stu-id="76f7f-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="76f7f-128">aplicação de função Olá fornece um ambiente de execução sem servidor do seu código de função.</span><span class="sxs-lookup"><span data-stu-id="76f7f-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="76f7f-129">Permite-lhe agrupar funções como unidades lógicas para uma gestão, implementação e partilha de recursos mais fácil.</span><span class="sxs-lookup"><span data-stu-id="76f7f-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="76f7f-130">Criar uma aplicação de função utilizando Olá [az functionapp criar](/cli/azure/functionapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="76f7f-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="76f7f-131">No Olá seguinte comando, substitua o seu próprio nome de aplicação de função exclusivo onde vir Olá `<app_name>` marcador de posição e Olá nome de conta de armazenamento para `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="76f7f-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="76f7f-132">Olá `<app_name>` é utilizado como o domínio DNS Olá predefinido para a aplicação de função Olá e por isso, nome de Olá tem toobe exclusivo em todas as aplicações no Azure.</span><span class="sxs-lookup"><span data-stu-id="76f7f-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="76f7f-133">Por predefinição, é criada uma aplicação de função com Olá consumo alojamento plano, que significa que os recursos são adicionados dinamicamente conforme exigido pelas suas funções e paga apenas quando as funções em execução.</span><span class="sxs-lookup"><span data-stu-id="76f7f-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="76f7f-134">Para obter mais informações, consulte [plano de alojamento correto escolha Olá](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="76f7f-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="76f7f-135">Depois de ter sido criada a aplicação de função Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="76f7f-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="76f7f-136">Agora que tem uma aplicação de função, pode implementar o código de função real Olá do repositório de exemplo Olá GitHub.</span><span class="sxs-lookup"><span data-stu-id="76f7f-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="76f7f-137">Implementar o código de função</span><span class="sxs-lookup"><span data-stu-id="76f7f-137">Deploy your function code</span></span>  

<span data-ttu-id="76f7f-138">Existem várias formas toocreate o código de função na sua nova aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="76f7f-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="76f7f-139">Este tópico liga tooa repositório de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="76f7f-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="76f7f-140">Como anteriormente, no Olá seguinte código substitua Olá `<app_name>` marcador de posição com o nome de Olá da aplicação de função Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="76f7f-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="76f7f-141">Após a implementação de Olá origem foi definido, Olá CLI do Azure mostra informações toohello semelhante seguinte o exemplo (valores nulos removidos para legibilidade):</span><span class="sxs-lookup"><span data-stu-id="76f7f-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a><span data-ttu-id="76f7f-142">Testar a função de Olá</span><span class="sxs-lookup"><span data-stu-id="76f7f-142">Test hello function</span></span>

<span data-ttu-id="76f7f-143">Utilize cURL tootest Olá implementado função num computador Mac ou Linux ou utilizar Bash no Windows.</span><span class="sxs-lookup"><span data-stu-id="76f7f-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="76f7f-144">Executar o seguinte comando cURL, substituindo Olá de Olá `<app_name>` marcador de posição com o nome de Olá da sua aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="76f7f-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="76f7f-145">Acrescentar a cadeia de consulta Olá `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="76f7f-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Resposta da função mostrada num browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="76f7f-147">Se não tiver cURL disponível na sua linha de comandos, introduza Olá mesmo URL no endereço de Olá do seu browser.</span><span class="sxs-lookup"><span data-stu-id="76f7f-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="76f7f-148">Novamente, substitua Olá `<app_name>` marcador de posição com o nome de Olá da sua aplicação de função e acrescentar a cadeia de consulta Olá `&name=<yourname>` toohello URL e executar o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="76f7f-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Resposta da função mostrada num browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="76f7f-150">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="76f7f-150">Clean up resources</span></span>

<span data-ttu-id="76f7f-151">Outros guias de introdução desta coleção têm por base este guia de introdução.</span><span class="sxs-lookup"><span data-stu-id="76f7f-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="76f7f-152">Se pretender toocontinue toowork inícios rápidos subsequentes ou com tutoriais Olá, fazê-lo não limpar os recursos de Olá criados neste guia de introdução.</span><span class="sxs-lookup"><span data-stu-id="76f7f-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="76f7f-153">Se não planear toocontinue, utilize Olá toodelete de comando a seguir todos os recursos criados por este guia de introdução:</span><span class="sxs-lookup"><span data-stu-id="76f7f-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="76f7f-154">Escreva `y` quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="76f7f-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76f7f-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="76f7f-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
