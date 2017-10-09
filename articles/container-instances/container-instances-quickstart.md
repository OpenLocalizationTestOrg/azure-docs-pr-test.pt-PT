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
# <a name="create-your-first-container-in-azure-container-instances"></a>Criar o seu primeiro contentor no Azure Container Instances

Instâncias de contentor do Azure torna mais fácil toocreate e gerir contentores no Azure. Neste início rápido, irá criar um contentor no Azure e expô-la toohello internet com um endereço IP público. Esta operação é concluída com um único comando. Dentro de alguns segundos, verá isto no seu browser:

![Aplicação implementada com o Azure Container Instances vista no browser][aci-app-browser]

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este guia de introdução requer que está a executar versão CLI do Azure de Olá 2.0.12 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

As instâncias do Azure Container Instances são recursos do Azure e têm de ser colocadas num grupo de recursos do Azure, que é uma coleção lógica na qual estes recursos são implementados e geridos.

Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando. 

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Criar um contentor

Para criar um contentor, pode fornecer um nome, uma imagem do Docker e um grupo de recursos do Azure. Opcionalmente, pode expor Olá contentor toohello internet com um endereço IP público. Neste caso, vamos utilizar um contentor que aloja uma aplicação Web muito simples escrita em [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Dentro de alguns segundos, deve obter um pedido de tooyour de resposta. Inicialmente, o contentor de Olá estarão disponíveis num **criar** Estado, mas deve iniciar dentro de alguns segundos. Pode verificar o estado de Olá utilizando Olá `show` comando:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Na parte inferior de Olá de saída de Olá, irá ver o estado de aprovisionamento do contentor de Olá e o respetivo endereço IP:

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

Assim que o contentor de Olá move toohello **com êxito** Estado, pode chegá-la no browser Olá utilizando o endereço IP Olá fornecido. 

![Aplicação implementada com o Azure Container Instances vista no browser][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Extraia os registos do contentor de Olá

Pode obter registos de Olá do contentor de Olá criadas com Olá `logs` comando:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Saída:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Eliminar o contentor de Olá

Quando tiver terminado com o contentor de Olá, pode removê-la utilizando Olá `delete` comando:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Passos seguintes

Todos os Olá código para o contentor de Olá utilizado neste início rápido está disponível [no GitHub][app-github-repo], juntamente com o respetivo Dockerfile. Se quiser tootry criá-lo por si e implementar instâncias de contentor tooAzure utilizando Olá registo de contentor do Azure, continue toohello tutorial de instâncias de contentor do Azure.

> [!div class="nextstepaction"]
> [Azure Container Instances tutorials](./container-instances-tutorial-prepare-app.md) (Tutoriais do Azure Container Instances)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png