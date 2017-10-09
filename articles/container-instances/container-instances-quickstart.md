---
title: "aaaCreate do primeiro contentor de instâncias de contentor do Azure | Documentos do Azure"
description: "Implementar e começar a utilizar o Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="50b1e-103">Criar o seu primeiro contentor no Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="50b1e-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="50b1e-104">Instâncias de contentor do Azure torna mais fácil toocreate e gerir contentores no Azure.</span><span class="sxs-lookup"><span data-stu-id="50b1e-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="50b1e-105">Neste início rápido, irá criar um contentor no Azure e expô-la toohello internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="50b1e-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="50b1e-106">Esta operação é concluída com um único comando.</span><span class="sxs-lookup"><span data-stu-id="50b1e-106">This operation is completed in a single command.</span></span> <span data-ttu-id="50b1e-107">Dentro de alguns segundos, verá isto no seu browser:</span><span class="sxs-lookup"><span data-stu-id="50b1e-107">Within just a few seconds, you will see this in your browser:</span></span>

![Aplicação implementada com o Azure Container Instances vista no browser][aci-app-browser]

<span data-ttu-id="50b1e-109">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="50b1e-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="50b1e-110">Se escolher tooinstall e utilizar Olá CLI localmente, este guia de introdução requer que está a executar versão CLI do Azure de Olá 2.0.12 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="50b1e-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="50b1e-111">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="50b1e-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="50b1e-112">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="50b1e-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="50b1e-113">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="50b1e-113">Create a resource group</span></span>

<span data-ttu-id="50b1e-114">As instâncias do Azure Container Instances são recursos do Azure e têm de ser colocadas num grupo de recursos do Azure, que é uma coleção lógica na qual estes recursos são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="50b1e-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="50b1e-115">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="50b1e-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="50b1e-116">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização.</span><span class="sxs-lookup"><span data-stu-id="50b1e-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="50b1e-117">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="50b1e-117">Create a container</span></span>

<span data-ttu-id="50b1e-118">Para criar um contentor, pode fornecer um nome, uma imagem do Docker e um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="50b1e-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="50b1e-119">Opcionalmente, pode expor Olá contentor toohello internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="50b1e-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="50b1e-120">Neste caso, vamos utilizar um contentor que aloja uma aplicação Web muito simples escrita em [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="50b1e-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="50b1e-121">Dentro de alguns segundos, deve obter um pedido de tooyour de resposta.</span><span class="sxs-lookup"><span data-stu-id="50b1e-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="50b1e-122">Inicialmente, o contentor de Olá estarão disponíveis num **criar** Estado, mas deve iniciar dentro de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="50b1e-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="50b1e-123">Pode verificar o estado de Olá utilizando Olá `show` comando:</span><span class="sxs-lookup"><span data-stu-id="50b1e-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="50b1e-124">Na parte inferior de Olá de saída de Olá, irá ver o estado de aprovisionamento do contentor de Olá e o respetivo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="50b1e-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="50b1e-125">Assim que o contentor de Olá move toohello **com êxito** Estado, pode chegá-la no browser Olá utilizando o endereço IP Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="50b1e-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Aplicação implementada com o Azure Container Instances vista no browser][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="50b1e-127">Extraia os registos do contentor de Olá</span><span class="sxs-lookup"><span data-stu-id="50b1e-127">Pull hello container logs</span></span>

<span data-ttu-id="50b1e-128">Pode obter registos de Olá do contentor de Olá criadas com Olá `logs` comando:</span><span class="sxs-lookup"><span data-stu-id="50b1e-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="50b1e-129">Saída:</span><span class="sxs-lookup"><span data-stu-id="50b1e-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="50b1e-130">Eliminar o contentor de Olá</span><span class="sxs-lookup"><span data-stu-id="50b1e-130">Delete hello container</span></span>

<span data-ttu-id="50b1e-131">Quando tiver terminado com o contentor de Olá, pode removê-la utilizando Olá `delete` comando:</span><span class="sxs-lookup"><span data-stu-id="50b1e-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="50b1e-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="50b1e-132">Next steps</span></span>

<span data-ttu-id="50b1e-133">Todos os Olá código para o contentor de Olá utilizado neste início rápido está disponível [no GitHub][app-github-repo], juntamente com o respetivo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="50b1e-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="50b1e-134">Se quiser tootry criá-lo por si e implementar instâncias de contentor tooAzure utilizando Olá registo de contentor do Azure, continue toohello tutorial de instâncias de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="50b1e-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="50b1e-135">[Azure Container Instances tutorials](./container-instances-tutorial-prepare-app.md) (Tutoriais do Azure Container Instances)</span><span class="sxs-lookup"><span data-stu-id="50b1e-135">[Azure Container Instances tutorials](./container-instances-tutorial-prepare-app.md)</span></span>


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png