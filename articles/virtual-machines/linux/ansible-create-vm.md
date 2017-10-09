---
title: "aaaUse Ansible toocreate uma VM com Linux básico no Azure | Microsoft Docs"
description: "Saiba como toouse Ansible toocreate e gerir uma máquina virtual de Linux básica no Azure"
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
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="eb1d8-103">Criar uma máquina virtual básica no Azure com Ansible</span><span class="sxs-lookup"><span data-stu-id="eb1d8-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="eb1d8-104">Ansible permite-lhe implementação de Olá tooautomate e a configuração de recursos no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="eb1d8-105">Pode utilizar Ansible toomanage as máquinas virtuais (VMs) no Azure, Olá mesmo, tal como faria com qualquer outro recurso.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="eb1d8-106">Este artigo mostra como toocreate uma VM com Ansible básica.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="eb1d8-107">Também pode aprender como demasiado[criar um ambiente de VM completado com Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eb1d8-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="eb1d8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb1d8-108">Prerequisites</span></span>
<span data-ttu-id="eb1d8-109">toomanage Azure recursos com Ansible, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="eb1d8-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="eb1d8-110">Ansible e Olá módulos de SDK Python do Azure instalados no sistema anfitrião.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="eb1d8-111">Instalar Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="eb1d8-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="eb1d8-112">Credenciais do Azure e toouse Ansible configurado-los.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="eb1d8-113">Criar as credenciais do Azure e configurar Ansible</span><span class="sxs-lookup"><span data-stu-id="eb1d8-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="eb1d8-114">CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eb1d8-115">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="eb1d8-116">Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb1d8-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="eb1d8-117">Também pode utilizar [nuvem Shell](/azure/cloud-shell/quickstart) partir do seu browser.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="eb1d8-118">Criar suporte de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="eb1d8-118">Create supporting Azure resources</span></span>
<span data-ttu-id="eb1d8-119">Neste exemplo, vamos criar um runbook que implementa uma VM para uma infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="eb1d8-120">Em primeiro lugar, crie o grupo de recursos com [criar grupo az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="eb1d8-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="eb1d8-121">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="eb1d8-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="eb1d8-122">Criar uma rede virtual para a VM com [az rede vnet criar](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="eb1d8-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="eb1d8-123">Olá exemplo seguinte cria uma rede virtual denominada *myVnet* e uma sub-rede designada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="eb1d8-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="eb1d8-124">Criar e executar o manual de comunicação social Ansible</span><span class="sxs-lookup"><span data-stu-id="eb1d8-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="eb1d8-125">Criar um manual de comunicação social Ansible denominado **azure_create_vm.yml** e colar Olá seguir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="eb1d8-126">Este exemplo cria uma única VM e configura as credenciais SSH.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="eb1d8-127">Introduza os seus próprios dados de chaves públicos no Olá *key_data* emparelhe da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="eb1d8-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="eb1d8-128">Olá toocreate VM com Ansible, execute o manual de comunicação social Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="eb1d8-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="eb1d8-129">saída de Olá procura toohello semelhante seguinte o exemplo que mostra Olá que VM foi criada com êxito:</span><span class="sxs-lookup"><span data-stu-id="eb1d8-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="eb1d8-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="eb1d8-130">Next steps</span></span>
<span data-ttu-id="eb1d8-131">Este exemplo cria uma VM, um grupo de recursos existente e uma rede virtual já implementada.</span><span class="sxs-lookup"><span data-stu-id="eb1d8-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="eb1d8-132">Para obter um exemplo mais detalhado sobre como toouse Ansible toocreate recursos de suporte, como uma rede virtual e as regras do grupo de segurança de rede, consulte [criar um ambiente de VM completado com Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eb1d8-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
