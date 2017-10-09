---
title: contentores de saldo aaaLoad no cluster DC/OS do Azure | Microsoft Docs
description: "O balanceamento de carga entre vários contentores num cluster DC/OS do serviço de contentor do Azure."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contentores, Microserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Contentores de balanceamento de carga de um cluster do serviço de contentor do Azure DC/OS
Neste artigo, vamos explorar como toocreate um balanceador de carga interno no DC/SO gerido o serviço de contentor Azure utilizando o Marathon-LB. Esta configuração permite tooscale as suas aplicações horizontalmente. Também permite-lhe tootake partido dos clusters de agente públicas e privadas Olá colocando os balanceadores de carga no cluster pública Olá e os contentores de aplicação no cluster privada Olá. Neste tutorial:

> [!div class="checklist"]
> * Configurar um balanceador de carga Marathon
> * Implementar uma aplicação utilizando Olá Balanceador de carga
> * Configurar e Balanceador de carga do Azure

Precisa de um DC/OS ACS Olá toocomplete de cluster, os passos neste tutorial. Se for necessário, [este script de exemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar uma por si.

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Descrição geral do balanceamento de carga

Existem duas camadas de balanceamento de carga num cluster DC/OS do serviço de contentor do Azure: 

**Balanceador de carga do Azure** fornece pontos de entrada públicos (Olá aqueles que os utilizadores finais acesso). Um Azure LB é fornecido automaticamente pelo serviço de contentor do Azure e está, por predefinição, configurado tooexpose porta 80, 443 e 8080.

**Olá Balanceador de carga Marathon (marathon-lb)** instâncias de toocontainer de pedidos que estes pedidos de serviço de entrada de rotas. À medida que dimensionamos os contentores de Olá que fornecem o nosso serviço web, Olá marathon-lb feita dinamicamente. Este Balanceador de carga não é fornecido por predefinição no seu serviço de contentor, mas é fácil tooinstall.

## <a name="configure-marathon-load-balancer"></a>Configurar o Balanceador de carga Marathon

Balanceador de carga Marathon reconfigura dinamicamente com base nos contentores Olá que tenha implementado. Também é resiliente toohello perda de um contentor ou um agente - se isto ocorrer, o Apache Mesos reinicia o contentor de Olá noutro local e marathon-lb feita.

Execute Olá seguindo o Balanceador de carga marathon do comando tooinstall Olá do cluster do agente Olá público.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Implementar aplicações com balanceamento de carga

Agora que temos o pacote do marathon-lb Olá, podemos implementar um contentor de aplicação que pretendemos saldo tooload. 

Em primeiro lugar, obter Olá FQDN dos agentes de Olá publicamente exposto.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Em seguida, crie um ficheiro denominado *Olá web.json* e de cópia no Olá seguir o conteúdo. Olá `HAPROXY_0_VHOST` toobe atualizado com Olá FQDN dos agentes DC/SO de Olá tem de etiqueta. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Utilize Olá CLI de DC/SO toorun Olá aplicação. Por predefinição o Marathon implementa cluster privada do Olá Olá applicaton toohello. Isto significa que Olá acima implementação só é acessível através do seu Balanceador de carga, que é normalmente o comportamento de Olá assim o desejar.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Quando tiver sido implementada a aplicação Olá, procure toohello FQDN Olá agente cluster tooview com balanceamento de carga aplicação.

![Imagem da aplicação com balanceamento de carga](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Configurar o Balanceador de carga do Azure

Por predefinição, o Balanceador de Carga do Azure expõe as portas 80, 8080 e 443. Se estiver a utilizar uma destas três portas (como no Olá acima exemplo), então, não há nada que terá toodo. Deve ser capaz de toohit FQDN do Balanceador de carga do agente e, sempre que atualizar, irá aceder a um dos seus três servidores web de uma maneira round-robin. 

Se utilizar uma porta diferente, terá de regra de tooadd round robin e uma sonda no balanceador de carga Olá para a porta de Olá que utilizou. Pode fazê-lo de Olá [CLI do Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), com os comandos de Olá `azure network lb rule create` e `azure network lb probe create`.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, aprendeu sobre balanceamento de carga no ACS com o Marathon Olá e carga do Azure balanceadores incluindo Olá seguintes ações:

> [!div class="checklist"]
> * Configurar um balanceador de carga Marathon
> * Implementar uma aplicação utilizando Olá Balanceador de carga
> * Configurar e Balanceador de carga do Azure

Produzir toohello seguinte toolearn tutorial sobre a integração de armazenamento do Azure com o DC/OS, no Azure.

> [!div class="nextstepaction"]
> [Azure de montar a partilha de ficheiros no cluster DC/OS](container-service-dcos-fileshare.md)