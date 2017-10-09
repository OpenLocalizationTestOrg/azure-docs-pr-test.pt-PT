---
title: cluster de Azure Kubernetes aaaManage com IU da web | Microsoft Docs
description: "Utilizar Olá Kubernetes IU da web do serviço de contentor do Azure"
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Utilizar Olá Kubernetes IU da web do serviço de contentor do Azure

## <a name="prerequisites"></a>Pré-requisitos
Esta instrução parte do princípio de que tem [criado um cluster de Kubernetes utilizando o serviço de contentor do Azure](container-service-kubernetes-walkthrough.md).


Também parte do princípio que tem Olá Azure CLI 2.0 e `kubectl` as ferramentas instaladas.

Pode testar se tiver Olá `az` ferramenta instalada através da execução:

```console
$ az --version
```

Se não tiver Olá `az` ferramenta instalada, existem instruções [aqui](https://github.com/azure/azure-cli#installation).

Pode testar se tiver Olá `kubectl` ferramenta instalada através da execução:

```console
$ kubectl version
```

Se não tiver `kubectl` instalado, pode executar:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Descrição geral

### <a name="connect-toohello-web-ui"></a>Ligar a IU da web do toohello
Pode iniciar a IU da web do Olá Kubernetes executando:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Isto deve abrir um browser configurado tootalk tooa segura proxy web ligar o seu computador local toohello Kubernetes IU da web do.

### <a name="create-and-expose-a-service"></a>Criar e expor um serviço
1. Na IU da web de Kubernetes a Olá, clique em **criar** botão na janela do Olá superior direito.

    ![Kubernetes criar a IU](./media/container-service-kubernetes-ui/create.png)

    Abre de caixa de diálogo onde podem iniciar a criação da sua aplicação.

2. Atribua o nome de Olá `hello-nginx`. Olá utilize [ `nginx` contentor do Docker](https://hub.docker.com/_/nginx/) e implementar três réplicas deste serviço web.

    ![Caixa de diálogo de criar Kubernetes Pod](./media/container-service-kubernetes-ui/nginx.png)

3. Em **serviço**, selecione **externo** e introduza a porta 80.

    Esta definição carga balanceia três réplicas toohello de tráfego.

    ![Caixa de diálogo Criar do serviço de Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. Clique em **implementar** toodeploy desses contentores e serviços.

    ![Implementar Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Ver os contentores
Depois de clicar em **implementar**, Olá IU mostra uma vista do seu serviço, como implementa:

![Estado de Kubernetes](./media/container-service-kubernetes-ui/status.png)

Pode ver o estado de Olá de cada objeto Kubernetes no círculo Olá no lado esquerdo do Olá da IU, em **Pods**. Se for um círculo parcialmente completo, em seguida, objeto Olá ainda está em implementação. Quando um objeto é totalmente implementado, apresenta uma marca de verificação verde:

![Kubernetes implementado](./media/container-service-kubernetes-ui/deployed.png)

Assim que tudo está a ser executado, clique das suas pods toosee detalhes Olá com o serviço web.

![Kubernetes Pods](./media/container-service-kubernetes-ui/pods.png)

No Olá **Pods** vista, pode ver informações sobre contentores de Olá no pod Olá, bem como os recursos de CPU e memória do Olá utilizados por esses contentores:

![Kubernetes recursos](./media/container-service-kubernetes-ui/resources.png)

Se não vir recursos Olá, que poderá necessitar toowait alguns minutos para Olá toopropagate de dados de monitorização.

toosee Olá registos para o contentor, clique em **ver registos**.

![Registos de Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Visualizar o seu serviço
Na adição toorunning os contentores Olá Kubernetes IU criou um externo `Service` que Aprovisiona a contentores de tráfego toohello com uma carga balanceador toobring no seu cluster.

No painel de navegação esquerdo Olá, clique em **serviços** tooview todos os serviços (deve haver apenas um).

![Serviços de Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

Nessa vista, deverá ver um ponto final externo (endereço IP) que foi alocado tooyour serviço.
Se clicar nesse endereço IP, deverá ver o contentor Nginx em execução por detrás do Balanceador de carga.

![Vista de nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Redimensionar o seu serviço
Na adição tooviewing os seus objetos no Olá IU, pode editar e atualizar Olá Kubernetes API objetos.

Em primeiro lugar, clique em **implementações** no Olá deixado navegação painel toosee Olá implementação do serviço.

Assim que estiver nessa vista, clique no conjunto de réplicas Olá e, em seguida, clique em **editar** na barra de navegação superior Olá:

![Editar Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Editar Olá `spec.replicas` campo toobe `2`e clique em **atualização**.

Isto faz com que número de Olá de réplicas toodrop tootwo, eliminando um dos seus pods.

 

