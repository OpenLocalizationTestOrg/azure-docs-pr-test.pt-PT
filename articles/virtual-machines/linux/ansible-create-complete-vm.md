---
title: aaaUse Ansible toocreate uma VM com Linux completa no Azure | Microsoft Docs
description: "Saiba como toouse Ansible toocreate e gerir um ambiente de máquina virtual completado do Linux no Azure"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Criar um ambiente de máquina virtual completado do Linux no Azure com Ansible
Ansible permite-lhe implementação de Olá tooautomate e a configuração de recursos no seu ambiente. Pode utilizar Ansible toomanage as máquinas virtuais (VMs) no Azure, Olá mesmo, tal como faria com qualquer outro recurso. Este artigo mostra como toocreate num ambiente de Linux completado e de recursos com Ansible de suporte. Também pode aprender como demasiado[criar uma VM básica com Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Pré-requisitos
toomanage Azure recursos com Ansible, terá de Olá seguintes:

- Ansible e Olá módulos de SDK Python do Azure instalados no sistema anfitrião.
    - Instalar Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Credenciais do Azure e toouse Ansible configurado-los.
    - [Criar as credenciais do Azure e configurar Ansible](ansible-install-configure.md#create-azure-credentials)
- CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. 
    - Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). Também pode utilizar [nuvem Shell](/azure/cloud-shell/quickstart) partir do seu browser.


## <a name="create-virtual-network"></a>Criar a rede virtual
Olá seguinte secção um manual de comunicação social Ansible cria uma rede virtual denominada *myVnet* no Olá *10.0.0.0/16* espaço de endereços:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd uma sub-rede, Olá secção a seguir cria uma sub-rede designada *mySubnet* no Olá *myVnet* rede virtual:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Criar endereço IP público
recursos de tooaccess em Olá Internet, criar e atribuir um tooyour de endereço IP público VM. Olá seguinte secção um manual de comunicação social Ansible cria um endereço IP público com o nome *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Criar o grupo de segurança de rede
Rede grupos de segurança Olá fluxo de controlo de tráfego de rede que entra e sai da VM. Olá seguinte secção um manual de comunicação social Ansible cria um grupo de segurança de rede com o nome *myNetworkSecurityGroup* e define o tráfego SSH tooallow uma regra na porta TCP 22:

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a>Criar o cartão de interface de rede virtual
Uma placa de interface de rede virtual (NIC) liga-se a sua tooa VM fornecido a rede virtual, o endereço IP público e o grupo de segurança de rede. Olá seguinte secção um manual de comunicação social Ansible cria uma NIC virtual com o nome *myNIC* ligado toohello virtual recursos de rede que criou:

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a>Criar a máquina virtual
passo final Olá é toocreate uma VM e utilize todos os recursos de Olá criados. Olá seguinte secção um manual de comunicação social Ansible cria uma VM chamada *myVM* e anexa Olá NIC virtual com o nome *myNIC*. Introduza os seus próprios dados de chaves públicos no Olá *key_data* emparelhe da seguinte forma:

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a>Concluir o manual de comunicação social Ansible
toobring todas estas secções em conjunto, crie um manual de comunicação social Ansible denominado *azure_create_complete_vm.yml* e colar Olá seguinte conteúdo:

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

Ansible tem um toodeploy do grupo de recursos de todos os recursos em. Crie um grupo de recursos com [az group create](/cli/azure/vm#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate Olá concluída VM ambiente com Ansible, execute o manual de comunicação social Olá da seguinte forma:

```bash
ansible-playbook azure_create_complete_vm.yml
```

saída de Olá procura toohello semelhante seguinte o exemplo que mostra Olá que VM foi criada com êxito:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a>Passos seguintes
Este exemplo cria um ambiente de VM completado, incluindo Olá necessário recursos de rede virtuais. Para um exemplo mais direto toocreate uma VM para recursos de rede existentes com opções predefinidas, consulte [criar uma VM](ansible-create-vm.md).
