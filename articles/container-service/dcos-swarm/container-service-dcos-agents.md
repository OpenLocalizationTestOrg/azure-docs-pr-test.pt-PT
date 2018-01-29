---
title: "Conjuntos de agente DC/OS para o serviço de contentor do Azure"
description: "Como funcionam os agrupamentos de agente públicas e privadas com um cluster do serviço de contentor do Azure DC/OS"
services: container-service
author: dlepow
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: e82a6c1ee2d45cd07f4e87c43ad4fb1149ef555c
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Conjuntos de agente DC/OS para o serviço de contentor do Azure
Clusters DC/SO no serviço de contentor do Azure contêm nós de agente em dois conjuntos, um conjunto público e um conjunto privado. Uma aplicação pode ser implementada para o agrupamento, que afeta a acessibilidade entre as máquinas no seu serviço de contentor. As máquinas podem ser expostas à internet (público) ou manter interno (privado). Este artigo fornece uma breve descrição geral do motivo que existem conjuntos de públicos e privados.


* **Agentes privados**: nós de agente privada executam através de uma rede não encaminháveis internos. Esta rede só é acessível da zona de administrador ou através de router de limite de zona público. Por predefinição, o DC/SO inicia as aplicações em nós de agente privada. 

* **Agentes públicos**: nós de agente público executam aplicações de DC/OS e serviços através de uma rede acessível publicamente. 

Para obter mais informações sobre a segurança de rede do DC/OS, consulte o [documentação de DC/SO](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Implementar os conjuntos de agente

Os agrupamentos do agente DC/SO no serviço de contentor do Azure são criados da seguinte forma:

* O **conjunto privado** contém o número de nós de agente que especificou quando [implementar o cluster DC/SO](container-service-deployment.md). 

* O **conjunto público** inicialmente contém um número predeterminado de nós de agente. Este agrupamento é adicionado automaticamente quando o cluster DC/OS é aprovisionado.

O conjunto privado e o conjunto público são conjuntos de dimensionamento de máquina virtual do Azure. Pode redimensionar estes conjuntos após a implementação.

## <a name="use-agent-pools"></a>Utilizar conjuntos de agente
Por predefinição, **Marathon** implementa qualquer aplicação nova para o *privada* nós de agente. Tem de ser explicitamente implementar a aplicação para o *pública* nós durante a criação da aplicação. Selecione o **opcional** separador e introduza **slave_public** para o **funções dos recursos aceites** valor. Este processo é documentado [aqui](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) e no [DC/SO](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentação.

## <a name="next-steps"></a>Passos seguintes
* Leia mais sobre [gerir os contentores de DC/SO](container-service-mesos-marathon-ui.md).

* Saiba como [abrir a firewall](container-service-enable-public-access.md) fornecida pelo Azure, para permitir o acesso público aos contentores de DC/OS.

