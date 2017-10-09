---
title: "aaaInstall e configurar Ansible para utilização com máquinas virtuais do Azure | Microsoft Docs"
description: Saiba como tooinstall e configurar Ansible para gerir recursos do Azure no Ubuntu, CentOS e SLES
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Instalar e configurar toomanage Ansible máquinas virtuais no Azure
Este artigo descreve em detalhe como tooinstall Ansible e módulos de SDK Python do Azure necessários para algumas das Olá distros mais comuns do Linux. Pode instalar Ansible em outros distros ao ajustar Olá instalado pacotes toofit sua plataforma específica. toocreate Azure recursos de forma segura, que também aprender como toocreate e definir credenciais para Ansible toouse. 

Para mais opções de instalação e passos para plataformas adicionais, consulte Olá [Ansible instalar guia](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Instalar Ansible
Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupAnsible* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Agora criar uma VM e instalar Ansible para uma das Olá distros os seguintes:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM utilizando Olá `publicIpAddress` indicado no Olá operação de criação da saída de Olá VM:

```bash
ssh azureuser@<publicIpAddress>
```

Na sua VM, instale pacotes de Olá necessário de módulos de SDK Python do Azure de Olá e Ansible da seguinte forma:

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

Agora avançar demasiado[credenciais do Azure crie](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM utilizando Olá `publicIpAddress` indicado no Olá operação de criação da saída de Olá VM:

```bash
ssh azureuser@<publicIpAddress>
```

Na sua VM, instale pacotes de Olá necessário de módulos de SDK Python do Azure de Olá e Ansible da seguinte forma:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Agora avançar demasiado[credenciais do Azure crie](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM utilizando Olá `publicIpAddress` indicado no Olá operação de criação da saída de Olá VM:

```bash
ssh azureuser@<publicIpAddress>
```

Na sua VM, instale pacotes de Olá necessário de módulos de SDK Python do Azure de Olá e Ansible da seguinte forma:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Agora avançar demasiado[credenciais do Azure crie](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Criar as credenciais do Azure
Ansible comunica com o Azure com um nome de utilizador e palavra-passe ou um principal de serviço. Um principal de serviço do Azure é uma identidade de segurança que pode utilizar com aplicações, serviços e ferramentas de automatização como Ansible. Controlar e definir permissões de Olá como principal de serviço do toowhat operações Olá pode efetuar no Azure. segurança de tooimprove através de apenas a fornecer um nome de utilizador e palavra-passe, este exemplo cria um serviço básico principal.

Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de Olá de saída que Ansible necessita:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Segue-se um exemplo de saída de Olá do Olá precedente comandos:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure, terá também tooobtain a sua subscrição do Azure com o ID [mostrar de conta az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Utilize o resultado Olá estes dois comandos no passo seguinte Olá.


## <a name="create-ansible-credentials-file"></a>Criar ficheiro de credenciais Ansible
tooprovide credenciais tooAnsible, definir variáveis de ambiente ou criar um ficheiro de credenciais local. Para obter mais informações sobre como toodefine Ansible credenciais, consulte [tooAzure de fornecer credenciais módulos](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Para um ambiente de desenvolvimento, crie um *credenciais* de ficheiros para Ansible no seu anfitrião VM da seguinte forma:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Olá *credenciais* próprio ficheiro combina Olá ID de subscrição com a saída de Olá de criação de um principal de serviço. O resultado da Olá anterior [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) comando é Olá mesmo ordenar conforme necessário para *client_id*, *segredo*, e *inquilino* . Olá seguintes exemplo *credenciais* ficheiro mostra estes valores correspondente ao resultado anterior Olá. Introduza os seus próprios valores da seguinte forma:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Utilizar variáveis de ambiente de Ansible
Se pretender toouse ferramentas como Ansible Torre ou Jenkins, pode definir variáveis de ambiente da seguinte forma. Estas variáveis combinam o ID de subscrição de Olá com uma saída Olá da criação de um serviço principal. O resultado da Olá anterior [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) comando é Olá mesmo ordenar conforme necessário para *AZURE_CLIENT_ID*, *AZURE_SECRET*, e *AZURE_ INQUILINO*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Passos seguintes
Tem agora Ansible e Olá necessário módulos SDK Python do Azure instalados e as credenciais definidas para Ansible toouse. Saiba como demasiado[criar uma VM com Ansible](ansible-create-vm.md). Também pode aprender como demasiado[criar uma VM do Azure completa e que suporta a recursos com Ansible](ansible-create-complete-vm.md).
