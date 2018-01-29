---
title: "Kubernetes no tutorial do Azure – cluster de atualização"
description: "Kubernetes no tutorial do Azure – cluster de atualização"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5fd9a1890c1940cdd4e79cc32e0b3984edd043e8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="upgrade-kubernetes-in-azure-container-service-aks"></a>Atualizar Kubernetes no serviço de contentor do Azure (AKS)

Um cluster do serviço de contentor do Azure (AKS) possa ser atualizado utilizando a CLI do Azure. Durante o processo de atualização, Kubernetes nós são cuidadosamente [cordoned e drained] [ kubernetes-drain] para minimizar perturbações para as aplicações em execução.

Neste tutorial, parte oito de oito, um cluster de Kubernetes é atualizado. As tarefas que concluir incluem:

> [!div class="checklist"]
> * Identificar as versões de Kubernetes atual e disponíveis
> * Atualize os nós de Kubernetes
> * Validar uma atualização com êxito

## <a name="before-you-begin"></a>Antes de começar

Tutoriais anteriores, uma aplicação foi compactada uma imagem de contentor, esta imagem carregada para o registo de contentor do Azure e um cluster de Kubernetes criada. A aplicação, em seguida, foi executada no Kubernetes cluster.

Se não o fez estes passos e gostaria de acompanhar, voltar para o [Tutorial 1 – criar imagens de contentor][aks-tutorial-prepare-app].


## <a name="get-cluster-versions"></a>Obter versões de cluster

Antes de atualizar um cluster, utilize o comando `az aks get-versions` para verificar que versões do Kubernetes estão disponíveis para atualização.

```azurecli-interactive
az aks get-versions --name myK8sCluster --resource-group myResourceGroup --output table
```

Aqui pode ver que a versão atual do nó é `1.7.7` e essa versão `1.7.9`, `1.8.1`, e `1.8.2` estão disponíveis.

```
Name     ResourceGroup    MasterVersion    MasterUpgrades       NodePoolVersion     NodePoolUpgrades
-------  ---------------  ---------------  -------------------  ------------------  -------------------
default  myAKSCluster     1.7.7            1.8.2, 1.7.9, 1.8.1  1.7.7               1.8.2, 1.7.9, 1.8.1
```

## <a name="upgrade-cluster"></a>Atualizar cluster

Utilize o `az aks upgrade` comando para atualizar os nós do cluster. Os exemplos seguintes atualiza o cluster para a versão `1.8.2`.

```azurecli-interactive
az aks upgrade --name myK8sCluster --resource-group myResourceGroup --kubernetes-version 1.8.2
```

Saída:

```json
{
  "id": "/subscriptions/4f48eeae-9347-40c5-897b-46af1b8811ec/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myK8sCluster",
  "location": "eastus",
  "name": "myK8sCluster",
  "properties": {
    "accessProfiles": {
      "clusterAdmin": {
        "kubeConfig": "..."
      },
      "clusterUser": {
        "kubeConfig": "..."
      }
    },
    "agentPoolProfiles": [
      {
        "count": 1,
        "dnsPrefix": null,
        "fqdn": null,
        "name": "myK8sCluster",
        "osDiskSizeGb": null,
        "osType": "Linux",
        "ports": null,
        "storageProfile": "ManagedDisks",
        "vmSize": "Standard_D2_v2",
        "vnetSubnetId": null
      }
    ],
    "dnsPrefix": "myK8sClust-myResourceGroup-4f48ee",
    "fqdn": "myk8sclust-myresourcegroup-4f48ee-406cc140.hcp.eastus.azmk8s.io",
    "kubernetesVersion": "1.8.2",
    "linuxProfile": {
      "adminUsername": "azureuser",
      "ssh": {
        "publicKeys": [
          {
            "keyData": "..."
          }
        ]
      }
    },
    "provisioningState": "Succeeded",
    "servicePrincipalProfile": {
      "clientId": "e70c1c1c-0ca4-4e0a-be5e-aea5225af017",
      "keyVaultSecretRef": null,
      "secret": null
    }
  },
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "type": "Microsoft.ContainerService/ManagedClusters"
}
```

## <a name="validate-upgrade"></a>Validar a atualização

Agora, pode confirmar se a atualização foi concluída com êxito com o comando `az aks show`.

```azurecli-interactive
az aks show --name myK8sCluster --resource-group myResourceGroup --output table
```

Saída:

```json
Name          Location    ResourceGroup    KubernetesVersion    ProvisioningState    Fqdn
------------  ----------  ---------------  -------------------  -------------------  ----------------------------------------------------------------
myK8sCluster  eastus     myResourceGroup  1.8.2                Succeeded            myk8sclust-myresourcegroup-3762d8-2f6ca801.hcp.eastus.azmk8s.io
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, atualizado Kubernetes num AKS cluster. As tarefas seguintes foram concluídas:

> [!div class="checklist"]
> * Identificar as versões de Kubernetes atual e disponíveis
> * Atualize os nós de Kubernetes
> * Validar uma atualização com êxito

Siga esta ligação para obter mais informações sobre AKS.

> [!div class="nextstepaction"]
> [Descrição geral AKS][aks-intro]

<!-- LINKS - external -->
[kubernetes-drain]: https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/

<!-- LINKS - internal -->
[aks-intro]: ./intro-kubernetes.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md