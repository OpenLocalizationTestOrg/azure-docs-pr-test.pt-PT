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
# <a name="create-your-first-function-using-hello-azure-cli"></a>Criar a sua primeira função com Olá CLI do Azure

Este tutorial de início rápido explica como toouse das funções do Azure toocreate sua primeira função. Utilize Olá CLI do Azure toocreate uma aplicação de função, o que é Olá infraestrutura sem servidor que aloja a função. código de função Olá em si é implementado um repositório de exemplo do GitHub.    

Pode seguir os passos seguintes Olá num computador Mac, Windows ou Linux. 

## <a name="prerequisites"></a>Pré-requisitos 

Antes de executar este exemplo, tem de ter o seguinte Olá:

+ Uma conta do [GitHub](https://github.com) ativa. 
+ Uma subscrição ativa do Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create). Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure, como aplicações Function App, bases de dados e contas de armazenamento, são implementados e geridos.

Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup`.  
Se não estiver a utilizar o Cloud Shell, tem primeiro de iniciar sessão com o `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Criar uma conta de Armazenamento do Azure

As funções utiliza um Estado de toomaintain de conta do Storage do Azure e outras informações sobre as suas funções. Crie uma conta de armazenamento no grupo de recursos de Olá que criou utilizando Olá [criar conta de armazenamento az](/cli/azure/storage/account#create) comando.

No Olá seguinte comando, substitua o seu próprio nome de conta de armazenamento globalmente exclusivo onde vir Olá `<storage_name>` marcador de posição. Os nomes das contas do Storage devem ter entre 3 e 24 carateres de comprimento e apenas podem conter números e letras minúsculas.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Depois de ter sido criada a conta de armazenamento Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:

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

## <a name="create-a-function-app"></a>Criar uma aplicação de função

Tem de ter uma execução de Olá do função aplicação toohost das suas funções. aplicação de função Olá fornece um ambiente de execução sem servidor do seu código de função. Permite-lhe agrupar funções como unidades lógicas para uma gestão, implementação e partilha de recursos mais fácil. Criar uma aplicação de função utilizando Olá [az functionapp criar](/cli/azure/functionapp#create) comando. 

No Olá seguinte comando, substitua o seu próprio nome de aplicação de função exclusivo onde vir Olá `<app_name>` marcador de posição e Olá nome de conta de armazenamento para `<storage_name>`. Olá `<app_name>` é utilizado como o domínio DNS Olá predefinido para a aplicação de função Olá e por isso, nome de Olá tem toobe exclusivo em todas as aplicações no Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Por predefinição, é criada uma aplicação de função com Olá consumo alojamento plano, que significa que os recursos são adicionados dinamicamente conforme exigido pelas suas funções e paga apenas quando as funções em execução. Para obter mais informações, consulte [plano de alojamento correto escolha Olá](functions-scale.md). 

Depois de ter sido criada a aplicação de função Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:

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

Agora que tem uma aplicação de função, pode implementar o código de função real Olá do repositório de exemplo Olá GitHub.

## <a name="deploy-your-function-code"></a>Implementar o código de função  

Existem várias formas toocreate o código de função na sua nova aplicação de função. Este tópico liga tooa repositório de exemplo no GitHub. Como anteriormente, no Olá seguinte código substitua Olá `<app_name>` marcador de posição com o nome de Olá da aplicação de função Olá que criou. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Após a implementação de Olá origem foi definido, Olá CLI do Azure mostra informações toohello semelhante seguinte o exemplo (valores nulos removidos para legibilidade):

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

## <a name="test-hello-function"></a>Testar a função de Olá

Utilize cURL tootest Olá implementado função num computador Mac ou Linux ou utilizar Bash no Windows. Executar o seguinte comando cURL, substituindo Olá de Olá `<app_name>` marcador de posição com o nome de Olá da sua aplicação de função. Acrescentar a cadeia de consulta Olá `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Resposta da função mostrada num browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Se não tiver cURL disponível na sua linha de comandos, introduza Olá mesmo URL no endereço de Olá do seu browser. Novamente, substitua Olá `<app_name>` marcador de posição com o nome de Olá da sua aplicação de função e acrescentar a cadeia de consulta Olá `&name=<yourname>` toohello URL e executar o pedido de Olá. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Resposta da função mostrada num browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Limpar recursos

Outros guias de introdução desta coleção têm por base este guia de introdução. Se pretender toocontinue toowork inícios rápidos subsequentes ou com tutoriais Olá, fazê-lo não limpar os recursos de Olá criados neste guia de introdução. Se não planear toocontinue, utilize Olá toodelete de comando a seguir todos os recursos criados por este guia de introdução:

```azurecli-interactive
az group delete --name myResourceGroup
```
Escreva `y` quando lhe for pedido.

## <a name="next-steps"></a>Passos seguintes

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
