---
title: "cluster aaaMonitor um serviço de contentor do Azure com Sysdig | Microsoft Docs"
description: Monitorizar um cluster do Azure Container Service com o Sysdig.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contentores, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Monitorizar um cluster do Azure Container Service com o Sysdig
Neste artigo, iremos implementar Sysdig agentes tooall Olá agente nós do cluster do serviço de contentor do Azure. Para esta configuração, é necessária uma conta do Sysdig. 

## <a name="prerequisites"></a>Pré-requisitos
[Implemente](container-service-deployment.md) e [ligue](../container-service-connect.md) um cluster configurado pelo Azure Container Service. Explorar Olá [IU do Marathon](container-service-mesos-marathon-ui.md). Aceda demasiado[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset uma conta de nuvem Sysdig. 

## <a name="sysdig"></a>Sysdig
Sysdig é um serviço de monitorização que permite-lhe toomonitor os contentores no seu cluster. Sysdig é conhecido toohelp na resolução de problemas, mas também tem as métricas de monitorização básicas para a CPU, redes, memória e e/s. Sysdig torna mais fácil toosee os contentores estão a funcionar Olá hardest ou essencialmente utilizando hello mais memória e CPU. Esta vista está a ser Olá secção "Descrição geral", o que está atualmente na versão beta. 

![IU do Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Configurar uma implementação do Sysdig com o Marathon
Estes passos irão mostrar como tooconfigure e implementar Sysdig aplicações tooyour cluster com o Marathon. 

Aceder à IU do DC/OS, através de [http://localhost:80 /](http://localhost:80/) uma vez na IU do DC/SO de Olá navegue toohello "Universo", que se encontre na Olá inferior esquerda e, em seguida, procure "Sysdig."

![Sysdig no DC/OS Universe](./media/container-service-monitoring-sysdig/sysdig1.png)

Agora o configuração de Olá toocomplete terá um Sysdig nuvem conta ou uma conta de avaliação gratuita. Uma vez que tem sessão iniciada num Web site do toohello Sysdig na nuvem, clique em seu nome de utilizador e, na página Olá, deverá ver a "chave de acesso". 

![Chave de API do Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

Em seguida, introduza a chave de acesso na configuração de Sysdig Olá dentro Olá do DC/OS. 

![Configuração de Sysdig no Olá do DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

Agora defina Olá instâncias too10000000 para que sempre que é adicionado um novo nó de toohello cluster Sysdig irão implementar automaticamente um agente toothat novo nó. Este é um toomake solução provisória se que sysdig implementará tooall novos agentes num cluster de Olá. 

![Configuração de Sysdig no Olá DC/SO universo-instâncias](./media/container-service-monitoring-sysdig/sysdig4.png)

Assim que instalou o pacote de Olá navegue toohello back Sysdig IU e irá ser tooexplore capaz de métricas de utilização diferentes Olá para contentores de Olá dentro do seu cluster. 

Também pode instalar dasboards específicos do Mesos e do Marathon através do [assistente de dashboard novo](https://app.sysdigcloud.com/#/dashboards/new).
