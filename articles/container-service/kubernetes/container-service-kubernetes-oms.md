---
title: "cluster de Azure Kubernetes aaaMonitor - operações de gestão | Microsoft Docs"
description: "Monitorização de Kubernetes cluster no serviço de contentor Azure utilizando o Microsoft Operations Management Suite"
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Monitor de um cluster do serviço de contentor do Azure com o Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Pré-requisitos
Esta instrução parte do princípio de que tem [criado um cluster de Kubernetes utilizando o serviço de contentor do Azure](container-service-kubernetes-walkthrough.md).

Também parte do princípio que tem Olá `az` cli do Azure e `kubectl` as ferramentas instaladas.

Pode testar se tiver Olá `az` ferramenta instalada através da execução:

```console
$ az --version
```

Se não tiver Olá `az` ferramenta instalada, existem instruções [aqui](https://github.com/azure/azure-cli#installation).  
Em alternativa, pode utilizar [Shell de nuvem do Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tem Olá `az` cli do Azure e `kubectl` ferramentas já instaladas por si.  

Pode testar se tiver Olá `kubectl` ferramenta instalada através da execução:

```console
$ kubectl version
```

Se não tiver `kubectl` instalado, pode executar:
```console
$ az acs kubernetes install-cli
```

tootest se tiver chaves kubernetes instaladas na sua ferramenta kubectl pode executar:
```console
$ kubectl get nodes
```

Se hello acima erros de comando terminar, terá das chaves de cluster do tooinstall kubernetes para a ferramenta de kubectl. Pode fazê-lo com Olá os seguintes comandos:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Contentores de monitorização no Operations Management Suite (OMS)

Gestão de operações do Microsoft (OMS) é baseado na nuvem IT solução de gestão que o ajuda a gerir e proteger no local e a infraestrutura de nuvem. da Microsoft Contentor é uma solução na análise de registos do OMS, que ajuda-o a ver Olá contentor o inventário, o desempenho e registos numa única localização. Pode de auditoria, resolver problemas de contentores através da visualização de registos de Olá numa localização centralizada e localizar inúteis consumir contentor em excesso num anfitrião.

![](media/container-service-monitoring-oms/image1.png)

Para obter mais informações sobre a solução de contentor, consulte toothe [análise de registos do contentor solução](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Instalar OMS Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Obter o ID da área de trabalho e a chave
Para Olá serviço toohello tootalk de agente do OMS tem toobe configurado com um id de área de trabalho e uma chave de área de trabalho. tooget Olá id e a chave tem de toocreate um OMS conta em <https://mms.microsoft.com>. Siga os passos de Olá toocreate uma conta. Quando tiver terminado a criar conta de Olá, terá de tooobtain o id e a chave clicando **definições**, em seguida, **origens ligadas**e, em seguida, **servidores Linux**, conforme mostrado abaixo.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Instalar o agente do OMS Olá utilizando um DaemonSet
DaemonSets são utilizadas pelo Kubernetes toorun uma única instância de um contentor em cada anfitrião no cluster de Olá.
Se estiver a perfeita para a execução de agentes de monitorização.

Eis Olá [ficheiro DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Guarde este ficheiro de tooa denominado `oms-daemonset.yaml` e substitua os valores de marcador de posição-Olá para `WSID` e `KEY` com o id da área de trabalho e a chave no ficheiro de Olá.

Depois de adicionar o seu ID de área de trabalho e a chave toohello DaemonSet configuração, pode instalar o agente do OMS Olá no seu cluster com Olá `kubectl` ferramenta de linha de comandos:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Instalar o agente do OMS Olá utilizando um segredo Kubernetes
tooprotect o ID da área de trabalho OMS e a chave, pode utilizar o segredo Kubernetes como parte do ficheiro de DaemonSet YAML.

 - Copie o script Olá, o ficheiro de modelo secreta e Olá ficheiro DaemonSet YAML (de [repositório](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) e certifique-se de que estão na Olá mesmo diretório. 
      - segredo gerar script - gen.sh segredo
      - modelo secreto - template.yaml segredo
   - Ficheiro DaemonSet YAML - omsagent-ds-secrets.yaml
 - Execute script de Olá. script de Olá pedirá para Olá ID da área de trabalho OMS e a chave primária. Insira o que e script Olá irá criar um ficheiro de yaml secreta, pelo que pode executá-lo.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Crie pod de segredos Olá, executando Olá seguinte:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, execute Olá seguinte: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Criar a sua omsagent daemon-set executando``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Conclusão
Já está! Após alguns minutos, deve ser dados toosee capaz de fluir tooyour dashboard do OMS.
