---
title: "aloja aaaUse Docker máquina toocreate Linux no Azure | Microsoft Docs"
description: "Descreve como toouse Docker máquina toocreate Docker aloja no Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Como toouse Docker máquina toocreate aloja no Azure
Este artigo detalhes como toouse [Docker máquina](https://docs.docker.com/machine/) toocreate anfitriões no Azure. Olá `docker-machine` comando cria uma máquina virtual (VM) do Linux no Azure, em seguida, instala Docker. Em seguida, pode gerir os anfitriões de Docker no Azure com Olá mesmas ferramentas locais e fluxos de trabalho.

## <a name="create-vms-with-docker-machine"></a>Criar as VMs com a máquina do Docker
Em primeiro lugar, obter o ID de subscrição do Azure com [mostrar de conta az](/cli/azure/account#show) da seguinte forma:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Crie o Docker anfitrião VMs no Azure com `docker-machine create` especificando *azure* como controlador de Olá. Para obter mais informações, consulte Olá [documentação do controlador de Azure do Docker](https://docs.docker.com/machine/drivers/azure/)

Olá exemplo seguinte cria uma VM chamada *myVM*, cria uma conta de utilizador com o nome *azureuser*e abre-se a porta *80* no Olá anfitrião VM. Siga toolog quaisquer avisos no tooyour conta do Azure e conceder Docker máquina permissões toocreate e gerir os recursos.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

saída de Olá procura toohello semelhante seguinte exemplo:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Configurar a shell do Docker
anfitriões de Docker tooyour tooconnect no Azure, definir as definições de ligação adequado Olá. Conforme indicado no fim de Olá do resultado de Olá, veja as informações da ligação Olá para o anfitrião de Docker da seguinte forma: 

```bash
docker-machine env myvmdocker
```

Olá de saída é semelhante toohello seguinte exemplo:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

definições de ligação de Olá toodefine podem ambos Olá execução sugerida comandos de configuração (`eval $(docker-machine env myvmdocker)`), ou pode definir variáveis de ambiente de Olá manualmente. 

## <a name="run-a-container"></a>Executar um contentor
toosee um contentor em ação, permite executar um webserver NGINX básico. Criar um contentor com `docker run` e expor a porta 80 para o tráfego web da seguinte forma:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Olá de saída é semelhante toohello seguinte exemplo:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Vista de contentores com `docker ps`. Olá saídas de exemplo seguinte mostra contentor NGINX de Olá em execução com a porta 80 exposto:

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Contentor de Olá de teste
Obter o endereço IP público de Olá do anfitrião de Docker da seguinte forma:


```bash
docker-machine ip myvmdocker
```

contentor de Olá toosee em ação, abra um browser e introduza o endereço IP público Olá anotou na saída de Olá de Olá precedente comando:

![Contentor de ngnix em execução](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Passos seguintes
Também pode criar anfitriões com Olá [extensão da VM Docker](dockerextension.md). Para obter exemplos sobre como utilizar o Docker Compose, consulte [começar com o Docker e Compose no Azure](docker-compose-quickstart.md).
