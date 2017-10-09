---
title: aaaQuickstart - cluster Kubernetes do Azure para Windows | Microsoft Docs
description: "Saiba rapidamente toocreate um cluster de Kubernetes para contentores do Windows no serviço de contentor do Azure com Olá CLI do Azure."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Implementar o cluster do Kubernetes para contentores do Windows

Olá CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts. Detalhes deste Guia utilizando Olá CLI do Azure toodeploy um [Kubernetes](https://kubernetes.io/docs/home/) cluster no [serviço de contentor Azure](../container-service-intro.md). Depois do cluster de Olá é implementado, ligar tooit com Olá Kubernetes `kubectl` ferramenta da linha de comandos e pretender implementa o primeiro contentor do Windows.

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este guia de introdução requer que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> O suporte para contentores do Windows com Kubernetes no Azure Container Service está em pré-visualização. 
>

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um grupo lógico, no qual os recursos do Azure são implementados e geridos. 

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Criar cluster do Kubernetes
Criar um cluster de Kubernetes no serviço de contentor do Azure com Olá [az acs criar](/cli/azure/acs#create) comando. 

Olá exemplo seguinte cria um cluster com o nome *myK8sCluster* com o um Linux principal de nós e dois nós de agente do Windows. Este exemplo cria SSH principal do Linux chaves tooconnect necessários toohello. Este exemplo utiliza *azureuser* para um nome de utilizador administrativo e *myPassword12* como palavra-passe de Olá em nós do Windows hello. Atualize o ambiente de tooyour adequada de toosomething estes valores. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Após vários minutos, o comando de Olá estiver concluída e mostra-lhe informações sobre a sua implementação.

## <a name="install-kubectl"></a>Instalar o kubectl

tooconnect toohello Kubernetes cluster do computador cliente, utilize [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), cliente da linha de comandos do Olá Kubernetes. 

Se estiver a utilizar o Azure CloudShell, `kubectl` já está instalado. Se quiser tooinstall-la localmente, pode utilizar Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Olá a CLI do Azure exemplo instala os seguintes `kubectl` tooyour sistema. No Windows, execute este comando como administrador.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Ligar-se com kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, execute Olá [az acs kubernetes get-credenciais](/cli/azure/acs/kubernetes#get-credentials) comando. Olá exemplo seguinte transfere para o seu cluster Kubernetes a configuração do cluster de Olá.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify Olá ligação tooyour cluster partir do seu computador, tente executar:

```azurecli-interactive
kubectl get nodes
```

`kubectl`Apresenta uma lista de nós de Olá mestre e o agente.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Implementar um contentor do IIS do Windows

Pode executar um contentor do Docker dentro de um *pod* do Kubernetes, que contém um ou mais contentores. 

Neste exemplo básico utiliza um toospecify de ficheiro JSON um contentor de servidor de informação Internet (IIS) da Microsoft e, em seguida, cria pod Olá utilizando Olá `kubctl apply` comando. 

Criar um ficheiro local com o nome `iis.json` e Olá cópia seguindo texto. Este ficheiro indica Kubernetes toorun IIS no servidor do Windows Server 2016 nano for apresentado, utilizando uma imagem de contentor público de [Docker Hub](https://hub.docker.com/r/nanoserver/iis/). contentor de Olá utiliza a porta 80, mas inicialmente só é acessível na rede de cluster Olá.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart pod de Olá, tipo:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

implementação de Olá tootrack, tipo:
  
```azurecli-interactive
kubectl get pods
```

Enquanto está a implementar pod Olá, o estado de Olá é `ContainerCreating`. Pode demorar alguns minutos para Olá do Olá contentor tooenter `Running` estado.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Olá vista página de boas-vindas do IIS

tooexpose Olá pod toohello mundo com um endereço IP público, Olá tipo os seguintes comandos:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Com este comando, Kubernetes cria um serviço e um [regra de Balanceador de carga do Azure](container-service-kubernetes-load-balancing.md) com um endereço IP público para o serviço de Olá. 

Execute Olá seguir o estado do comando toosee Olá do serviço de Olá.

```azurecli-interactive
kubectl get svc
```

Endereço IP Olá aparece inicialmente como `pending`. Após alguns minutos, Olá endereço IP externo de Olá `iis` pod está definido:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Pode utilizar um browser da sua choice toosee Olá predefinido IIS bem-vindo página no endereço IP externo de Olá:

![Imagem de navegação tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Eliminar o cluster
Quando o cluster de Olá já não é necessário, pode utilizar Olá [eliminação do grupo de az](/cli/azure/group#delete) comando o grupo de recursos do tooremove Olá, serviço de contentor e relacionados todos os recursos.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Passos seguintes

Neste guia de início rápido, implementou um cluster do Kubernetes, ligado a `kubectl`, e implementou um pod com um contentor IIS. toolearn mais informações sobre o serviço de contentor do Azure, continuar toohello Kubernetes tutorial.

> [!div class="nextstepaction"]
> [Gerir um cluster do ACS Kubernetes](container-service-tutorial-kubernetes-prepare-app.md)
