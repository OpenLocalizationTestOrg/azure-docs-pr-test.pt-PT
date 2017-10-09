---
title: aaaHow toocreate as imagens de VM do Linux do Azure com Packer | Microsoft Docs
description: Saiba como imagens de toocreate Packer toouse de computadores virtuais Linux no Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Como imagens de máquina virtual do toouse Packer toocreate Linux no Azure
Cada máquina virtual (VM) no Azure é criada a partir de uma imagem que define Olá distribuição de Linux e versão do SO. Imagens podem incluir aplicações pré-instaladas e configurações. Olá, Azure Marketplace disponibiliza várias imagens primeira e de terceiros para distribuições mais comuns e ambientes de aplicação, ou pode criar as suas próprias necessidades de tooyour imagens personalizadas e adaptadas. Este artigo fornece detalhes sobre como toouse Olá abrir a ferramenta de origem [Packer](https://www.packer.io/) toodefine e compilação imagens personalizadas no Azure.


## <a name="create-azure-resource-group"></a>Criar grupo de recursos do Azure
Durante o processo de compilação de Olá, Packer cria temporários recursos do Azure como compilações Olá de VM de origem. toocapture VM de origem para utilização como uma imagem, tem de definir um grupo de recursos. Olá saída do processo de compilação do Olá Packer é armazenada neste grupo de recursos.

Crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Criar as credenciais do Azure
Packer autentica com o Azure utilizando um principal de serviço. Um principal de serviço do Azure é uma identidade de segurança que pode utilizar com aplicações, serviços e ferramentas de automatização como Packer. Controlar e definir permissões de Olá como principal de serviço do toowhat operações Olá pode efetuar no Azure.

Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de Olá de saída que Packer necessita:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Segue-se um exemplo de saída de Olá do Olá precedente comandos:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, terá também tooobtain a sua subscrição do Azure com o ID [mostrar de conta az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Utilize o resultado Olá estes dois comandos no passo seguinte Olá.


## <a name="define-packer-template"></a>Definir Packer modelo
imagens de toobuild, crie um modelo como um ficheiro JSON. No modelo de Olá, definir construtores e processo de compilação provisioners realizar Olá real. Packer tem um [provisioner para o Azure](https://www.packer.io/docs/builders/azure.html) que lhe permite toodefine Azure recursos, tais como credenciais de principal de serviço de Olá criados no Olá precedente passo.

Crie um ficheiro denominado *ubuntu.json* e colar Olá seguir o conteúdo. Introduza os seus próprios valores para seguinte Olá:

| Parâmetro                           | Onde tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Primeira linha do resultado de `az ad sp` criar comando - *appId* |
| *client_secret*                     | Segunda linha de saída de `az ad sp` criar comando - *palavra-passe* |
| *tenant_id*                         | Terceira linha de saída de `az ad sp` criar comando - *inquilino* |
| *SUBSCRIPTION_ID*                   | O resultado da `az account show` comando |
| *managed_image_resource_group_name* | Nome do grupo de recursos que criou no passo primeiro Olá |
| *managed_image_name*                | Nome para a imagem de disco gerido Olá que é criada |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

Este modelo cria uma imagem de Ubuntu 16.04 LTS, instala NGINX e deprovisions Olá VM.

> [!NOTE]
> Se expandir nas credenciais de utilizador de tooprovision modelo, ajuste o comando de provisioner Olá que deprovisions Olá tooread de agente do Azure `-deprovision` vez `deprovision+user`.
> Olá `+user` sinalizador remove todas as contas de utilizador Olá de VM de origem.


## <a name="build-packer-image"></a>Compilar Packer imagem
Se ainda não tiver Packer instalado no seu computador local, [siga as instruções de instalação do Olá Packer](https://www.packer.io/docs/install/index.html).

Crie imagem Olá, especificando o Packer ficheiro do modelo da seguinte forma:

```bash
./packer build ubuntu.json
```

Segue-se um exemplo de saída de Olá do Olá precedente comandos:

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Criar a VM da imagem do Azure
Agora pode criar uma VM a partir da imagem com [az vm criar](/cli/azure/vm#create). Especifique Olá imagem que criou com Olá `--image` parâmetro. Olá exemplo seguinte cria uma VM chamada *myVM* de *myPackerImage* e gera chaves SSH, caso ainda não existam:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Demora alguns minutos de Olá de toocreate VM. Quando tiver sido criada Olá VM, tome nota do Olá `publicIpAddress` apresentado pela Olá CLI do Azure. Este endereço é o site NGINX de Olá de tooaccess utilizadas através de um browser web.

tooallow web tráfego tooreach a VM, abrir porta 80 do Olá Internet com [az vm open-porta](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Testar a VM e NGINX
Agora pode abrir um browser e introduza `http://publicIpAddress` na barra de endereço Olá. Forneça o suas próprias público endereços IP a partir Olá VM criar o processo. página NGINX Olá predefinida é apresentada como no seguinte exemplo de Olá:

![Site predefinido do NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Passos seguintes
Neste exemplo, utilizou Packer toocreate uma imagem de VM com NGINX já instalado. Pode utilizar esta imagem de VM em conjunto com a implementação fluxos de trabalho existentes, tais como toodeploy tooVMs sua aplicação criada a partir de Olá imagem com Ansible, Chef ou Puppet.

Para modelos de Packer de exemplo adicionais para outros distros Linux, consulte [este repositório do GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).