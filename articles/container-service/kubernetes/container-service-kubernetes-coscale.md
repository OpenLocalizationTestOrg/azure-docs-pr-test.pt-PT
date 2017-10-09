---
title: aaaMonitor um Kubernetes Azure cluster com CoScale | Microsoft Docs
description: "Monitor de um cluster de Kubernetes no serviço de contentor Azure utilizando CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Monitor de um cluster de Kubernetes de serviço de contentor do Azure com CoScale

Neste artigo, vamos mostrar-lhe como toodeploy Olá [CoScale](https://www.coscale.com/) toomonitor agente todos os nós e contentores no seu Kubernetes cluster do serviço de contentor do Azure. Precisa de uma conta com CoScale para esta configuração. 


## <a name="about-coscale"></a>Sobre CoScale 

CoScale é uma plataforma de monitorização que recolhe métricas e eventos de todos os contentores em várias plataformas de orquestração. CoScale oferece monitorização completa pilha para ambientes de Kubernetes. Fornece visualizações e análise de todas as camadas na pilha de Olá: Olá SO, Kubernetes, Docker e aplicações em execução dentro os contentores. CoScale oferece várias dashboards de monitorização incorporadas e tem operadores de tooallow de deteção de anomalias incorporadas e problemas de infraestrutura e aplicação de toofind de programadores rápido.

![CoScale da IU](./media/container-service-kubernetes-coscale/coscale.png)

Como é mostrado neste artigo, pode instalar agentes num toorun de cluster Kubernetes CoScale como uma solução de SaaS. Se quiser tookeep os dados on-site, CoScale também está disponível para instalação no local.


## <a name="prerequisites"></a>Pré-requisitos

Terá primeiro demasiado[criar uma conta de CoScale](https://www.coscale.com/free-trial).

Esta instrução parte do princípio de que tem [criado um cluster de Kubernetes utilizando o serviço de contentor do Azure](container-service-kubernetes-walkthrough.md).

Também parte do princípio que tem Olá `az` CLI do Azure e `kubectl` as ferramentas instaladas.

Pode testar se tiver Olá `az` ferramenta instalada através da execução:

```azurecli
az --version
```

Se não tiver Olá `az` ferramenta instalada, existem instruções [aqui](/cli/azure/install-azure-cli).

Pode testar se tiver Olá `kubectl` ferramenta instalada através da execução:

```bash
kubectl version
```

Se não tiver `kubectl` instalado, pode executar:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>Instalar o agente de CoScale Olá com um DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) são utilizados pelo Kubernetes toorun uma única instância de um contentor em cada anfitrião no cluster de Olá.
Se estiver a perfeita para a execução de agentes de monitorização, tais como o agente de CoScale Olá.

Depois de iniciar sessão no tooCoScale, aceda toohello [página agente](https://app.coscale.com/) agentes de CoScale tooinstall no seu cluster utilizando um DaemonSet. Olá CoScale IU fornece toocreate de passos de configuração orientada um agente e o início da monitorização completa do seu cluster Kubernetes.

![Configuração do agente coScale](./media/container-service-kubernetes-coscale/installation.png)

agente de Olá toostart no cluster de Olá, execute o comando de Olá fornecido:

![Iniciar o agente de CoScale Olá](./media/container-service-kubernetes-coscale/agent_script.png)

Já está! Depois de agentes Olá estão em execução, deve ver os dados na consola de Olá dentro de alguns minutos. Visite Olá [página agente](https://app.coscale.com/) toosee um resumo do cluster, execute os passos de configuração adicionais e ver os dashboards, tais como Olá **descrição geral do cluster Kubernetes**.

![Descrição geral do cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

agente de CoScale Olá é implementada automaticamente em novos computadores no cluster de Olá. Olá as atualizações de agente automaticamente quando é lançada uma nova versão.


## <a name="next-steps"></a>Passos seguintes

Consulte Olá [CoScale documentação](http://docs.coscale.com/) e [blogue](https://www.coscale.com/blog) para obter informações sobre CoScale soluções de monitorização. 

