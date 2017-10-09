---
title: aaaQuickstart - cluster Azure Docker CE para Linux | Microsoft Docs
description: "Saiba rapidamente toocreate um cluster Docker CE para contentores de Linux no serviço de contentor do Azure com Olá CLI do Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Implementar um cluster do Docker CE

Este guia de introdução, um cluster Docker CE é implementado utilizando Olá CLI do Azure. Uma aplicação de contentor multi constituída front-end web e uma instância de Redis, em seguida, é implementada e é executada no cluster de Olá. Depois de concluída, a aplicação Olá está acessível através de Olá internet.

O Docker CE no Azure Container Service encontra-se em pré-visualização e **não deve ser utilizado em cargas de trabalho de produção**.

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Se escolher tooinstall e utilizar Olá CLI localmente, este guia de introdução requer que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um grupo lógico, no qual os recursos do Azure são implementados e geridos.

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *ukwest* localização.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

Saída:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Criar um cluster do Docker Swarm

Criar um cluster Docker CE no serviço de contentor do Azure com Olá [az acs criar](/cli/azure/acs#create) comando. 

Olá exemplo seguinte cria um cluster com o nome *mySwarmCluster* com o um Linux principal de nós e três nós de agente do Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Após vários minutos, o comando de Olá concluir e devolve informações de formatação json sobre cluster Olá.

## <a name="connect-toohello-cluster"></a>Ligue o cluster de toohello

Ao longo deste guia de introdução, terá de Olá FQDN do mestre de Docker Swarm Olá e agrupamento de agentes do Olá Docker. Execute Olá tooreturn ambos Olá FQDNs mestre e o agente de comando a seguir.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Saída:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Crie um SSH mestre do túnel toohello Swarm. Substitua `MasterFQDN` com endereço FQDN Olá mestre do Olá Swarm.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Conjunto Olá `DOCKER_HOST` variável de ambiente. Isto permite-lhe comandos de docker toorun contra Olá Docker Swarm sem ter de nome de Olá toospecify do anfitrião de Olá.

```bash
export DOCKER_HOST=localhost:2374
```

Agora, está pronto toorun serviços Docker Olá Docker Swarm.


## <a name="run-hello-application"></a>Executar a aplicação Olá

Crie um ficheiro denominado `azure-vote.yaml` e Olá cópia seguir o conteúdo para a mesma.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Executar Olá [pilha docker implementar](https://docs.docker.com/engine/reference/commandline/stack_deploy/) serviço de Azure voto toocreate Olá de comandos.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Saída:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Olá utilize [docker pilha ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) estado da implementação Olá tooreturn da aplicação Olá de comandos.

```bash
docker stack ps azure-vote
```

Uma vez Olá `CURRENT STATE` de cada serviço é `Running`, Olá aplicação esteja pronta.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Testar a aplicação Olá

Procure toohello FQDN do Olá Swarm agente conjunto tootest saída Olá aplicação de voto do Azure.

![Imagem de navegação tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Eliminar o cluster
Quando o cluster de Olá já não é necessário, pode utilizar Olá [eliminação do grupo de az](/cli/azure/group#delete) comando o grupo de recursos do tooremove Olá, serviço de contentor e relacionados todos os recursos.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Obter o código de Olá

Neste início rápido, imagens de contentor previamente criadas tem sido utilizado toocreate um serviço de Docker. Olá relacionados com o código da aplicação, Dockerfile, e o ficheiro de Compose estão disponíveis no GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Passos seguintes

Este início rápido, implementar um cluster Docker Swarm e implementar uma aplicação de contentor multi tooit.

toolearn sobre a integração de Docker transfira com o Visual Studio Team Services, continuar toohello CI/CD com o Docker Swarm e VSTS.

> [!div class="nextstepaction"]
> [CI/CD com Docker Swarm e VSTS](./container-service-docker-swarm-setup-ci-cd.md)