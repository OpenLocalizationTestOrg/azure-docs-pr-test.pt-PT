---
title: "aaaCreate Docker aloja no Azure com o Docker máquina | Microsoft Docs"
description: "Descreve a utilização de anfitriões de docker toocreate Docker máquina no Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Criar Anfitriões do Docker no Azure com Máquina do Docker
Executar [Docker](https://www.docker.com/) contentores requer o daemon de docker de Olá em execução para um anfitrião VM.
Este tópico descreve como toouse Olá [docker máquina](https://docs.docker.com/machine/) comando toocreate novas VMs do Linux, configurados com Olá daemon de Docker, em execução no Azure. 

**Nota:** 

* *Este artigo depende 0.9.0-rc2 de versão da máquina de docker ou superior*
* *Contentores do Windows serão suportados através do docker-máquina no Olá quase futuro*

## <a name="create-vms-with-docker-machine"></a>Criar as VMs com a máquina do Docker
Criar docker anfitrião VMs no Azure com Olá `docker-machine create` comando utilizando Olá `azure` controlador. 

Olá controlador do Azure requer o ID de subscrição. Pode utilizar Olá [CLI do Azure](cli-install-nodejs.md) ou Olá [Portal do Azure](https://portal.azure.com) tooretrieve sua subscrição do Azure. 

**Utilizar Olá Portal do Azure**

* Selecione **subscrições** Olá navegação à esquerda página e copie Olá do id de subscrição.

**Utilizar Olá CLI do Azure**

* Tipo ```azure account list``` e id de subscrição de Olá de cópia.

Tipo `docker-machine create --driver azure` toosee Olá opções e os respetivos valores predefinidos.
Também pode ver Olá [documentação do controlador de Azure do Docker](https://docs.docker.com/machine/drivers/azure/) para obter mais informações. 

Olá exemplo a seguir depende Olá [valores predefinidos](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mas, opcionalmente, defina estes valores: 

* dns do Azure para o nome de Olá associado ao IP público Olá e certificados gerados. Este é o nome DNS Olá da sua máquina virtual. Olá VM pode, em seguida, em segurança parar, Olá IP dinâmico de versão e fornecer Olá capacidade tooreconnect após a vm Olá novamente começa com um IP de novo. prefixo de nome de Olá tem de ser exclusivo para essa região UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* Abra a porta 80 no Olá VM para acesso de internet de saída
* tamanho de Olá armazenamento mais rápido de premium do VM tooutilize
* armazenamento Premium utilizado para o disco da vm Olá

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Escolha um anfitrião de docker com máquina docker
Assim que tiver uma entrada na máquina de docker para o anfitrião, é possível definir o anfitrião predefinido de Olá ao executar comandos de docker.

## <a name="using-powershell"></a>Com o PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Utilizar Bash
```bash
eval $(docker-machine env MyDockerHost)
```

Agora, pode executar comandos de docker contra anfitriões especificados Olá

```
docker ps
docker info
```

## <a name="run-a-container"></a>Executar um contentor
Com um anfitrião configurado, pode agora executar um tootest de servidor web simples se o anfitrião foi configurado corretamente.
Aqui vamos utilizar uma imagem de padrão nginx, especifique se deve escutar na porta 80 e que, se o anfitrião de Olá VM reiniciar, contentor Olá irá reiniciar bem (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

saída de Olá deve ter um aspeto semelhante Olá seguinte:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Contentor de Olá de teste
Examine os contentores em execução com `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

E, Olá toosee com o contentor, tipo `docker-machine ip <VM name>` toofind Olá IP endereço tooenter no browser Olá:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Contentor de ngnix em execução](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Resumo
Com o docker-máquina, pode aprovisionar facilmente os anfitriões de docker no Azure para as validações de anfitriões de docker individuais.
Para produção de alojamento de contentores, consulte o artigo Olá [serviço de contentor do Azure](http://aka.ms/AzureContainerService)

toodevelop .NET Core aplicações com o Visual Studio, consulte [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)

