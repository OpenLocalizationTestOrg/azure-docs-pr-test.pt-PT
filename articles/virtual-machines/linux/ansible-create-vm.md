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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Criar uma máquina virtual básica no Azure com Ansible
Ansible permite-lhe implementação de Olá tooautomate e a configuração de recursos no seu ambiente. Pode utilizar Ansible toomanage as máquinas virtuais (VMs) no Azure, Olá mesmo, tal como faria com qualquer outro recurso. Este artigo mostra como toocreate uma VM com Ansible básica. Também pode aprender como demasiado[criar um ambiente de VM completado com Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Pré-requisitos
toomanage Azure recursos com Ansible, terá de Olá seguintes:

- Ansible e Olá módulos de SDK Python do Azure instalados no sistema anfitrião.
    - Instalar Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Credenciais do Azure e toouse Ansible configurado-los.
    - [Criar as credenciais do Azure e configurar Ansible](ansible-install-configure.md#create-azure-credentials)
- CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. 
    - Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). Também pode utilizar [nuvem Shell](/azure/cloud-shell/quickstart) partir do seu browser.


## <a name="create-supporting-azure-resources"></a>Criar suporte de recursos do Azure
Neste exemplo, vamos criar um runbook que implementa uma VM para uma infraestrutura existente. Em primeiro lugar, crie o grupo de recursos com [criar grupo az](/cli/azure/vm#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroup --location eastus
```

Criar uma rede virtual para a VM com [az rede vnet criar](/cli/azure/network/vnet#create). Olá exemplo seguinte cria uma rede virtual denominada *myVnet* e uma sub-rede designada *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Criar e executar o manual de comunicação social Ansible
Criar um manual de comunicação social Ansible denominado **azure_create_vm.yml** e colar Olá seguir o conteúdo. Este exemplo cria uma única VM e configura as credenciais SSH. Introduza os seus próprios dados de chaves públicos no Olá *key_data* emparelhe da seguinte forma:

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

Olá toocreate VM com Ansible, execute o manual de comunicação social Olá da seguinte forma:

```bash
ansible-playbook azure_create_vm.yml
```

saída de Olá procura toohello semelhante seguinte o exemplo que mostra Olá que VM foi criada com êxito:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Passos seguintes
Este exemplo cria uma VM, um grupo de recursos existente e uma rede virtual já implementada. Para obter um exemplo mais detalhado sobre como toouse Ansible toocreate recursos de suporte, como uma rede virtual e as regras do grupo de segurança de rede, consulte [criar um ambiente de VM completado com Ansible](ansible-create-complete-vm.md).
