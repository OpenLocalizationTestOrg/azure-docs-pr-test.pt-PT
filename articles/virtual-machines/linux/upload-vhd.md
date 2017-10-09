---
title: aaaUpload ou copiar uma VM com Linux personalizada com o Azure CLI 2.0 | Microsoft Docs
description: "Carregar ou copiar uma máquina virtual personalizada utilizando o modelo de implementação do Resource Manager Olá e Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Criar uma VM com Linux a partir do disco personalizado com Olá Azure CLI 2.0

<!-- rename toocreate-vm-specialized -->

Este artigo mostra como tooupload um disco de rígido virtual (VHD) personalizado ou copie um um VHD existente no Azure e criar novas Linux de máquinas virtuais (VMs) do disco personalizado Olá. Pode instalar e configurar um requisitos do Linux distro tooyour e, em seguida, utilizar essa VHD tooquickly criar uma nova máquina virtual do Azure.

Se pretender toocreate várias VMs a partir do seu disco personalizado, deve criar uma imagem do seu VM ou o VHD. Para obter mais informações, consulte [criar uma imagem personalizada da VM do Azure utilizando Olá CLI](tutorial-custom-images.md).

Tem duas opções:
* [Carregar um VHD](#option-1-upload-a-specialized-vhd)
* [Copiar uma VM do Azure existente](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Comandos rápidos

Ao criar uma nova VM utilizando [az vm criar](/cli/azure/vm#create) partir de um disco personalizado ou especializado **anexar** disco Olá (– anexar--disco do SO) em vez de especificar uma imagem personalizada ou marketplace (– imagem). Olá exemplo seguinte cria uma VM chamada *myVM* através de Olá de gerido com o nome do disco *myManagedDisk* criadas a partir do seu VHD personalizado:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Requisitos
Olá toocomplete os seguintes passos, tem de:

* Uma máquina virtual de Linux que tenha sido preparada para utilização no Azure. Olá [preparar Olá VM](#prepare-the-vm) secção deste artigo abrange como toofind distro informações específicas sobre como instalar Olá agente Linux do Azure (waagent) que é necessária para Olá VM toowork corretamente no Azure e para toobe capaz de tooconnect tooit utilizando SSH.
* ficheiro VHD Olá existente de um [distribuição Linux aprovadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual no formato VHD Olá. Várias ferramentas existem toocreate uma VM e os VHD:
  * Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tendo cuidado toouse VHD como o formato de imagem. Se necessário, pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) utilizando **qemu img converter**.
  * Também pode utilizar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> formato VHDX mais recente Olá não é suportado no Azure. Quando cria uma VM, especifique o VHD como formato Olá. Se for necessário, pode converter VHDX discos tooVHD utilizando [qemu img converter](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou Olá [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell. Além disso, Azure não suporta o carregamento de VHDs dinâmicos, por isso terá de tooconvert essa toostatic discos VHDs antes de carregar. Pode utilizar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinâmicos durante o processo de Olá de carregamento tooAzure.
> 
> 


* Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes de parâmetros de exemplo incluídos *myResourceGroup*, *mystorageaccount*, e *mydisks*.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Preparar Olá VM

Azure suporta várias distribuições em Linux (consulte [distribuições aprovadas pelo](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Olá seguintes artigos orientá-lo através do como tooprepare Olá várias distribuições em Linux que são suportadas no Azure:

* [Distribuições baseado em centOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Outras - distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Consulte também Olá [Linux instalação notas](create-upload-generic.md#general-linux-installation-notes) para dicas mais gerais sobre preparar imagens de Linux para o Azure.

> [!NOTE]
> Olá [plataforma Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs com o Linux apenas quando um dos Olá distribuições aprovadas pelo é utilizada com detalhes de configuração de Olá conforme especificado em versões suportadas em [Linux em aprovadas pelo Azure Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Opção 1: Carregar um VHD

Pode carregar um VHD personalizado que tem de ser executado num computador local ou que tenha exportado a partir de outra nuvem. toouse Olá VHD toocreate uma nova VM do Azure, necessita de tooupload Olá VHD tooa armazenamento conta e criar um disco gerido a partir de Olá VHD. 

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Antes de carregar o seu disco personalizado e a criação de VMs, terá primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização: [descrição geral do Azure gerida discos](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Criar uma conta de armazenamento para o seu disco personalizado e VMs com [criar conta de armazenamento az](/cli/azure/storage/account#create). 

Olá exemplo seguinte cria uma conta de armazenamento com o nome *mystorageaccount* no grupo de recursos de Olá que criou anteriormente:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Lista de chaves de conta de armazenamento
O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento. Estas chaves de acesso são utilizadas ao autenticar a conta do storage toohello, como as devidas operações de escrita. Leia mais sobre [gerir acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Visualizar chaves de acesso de Olá com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).

Ver as chaves de acesso Olá Olá conta de armazenamento que criou:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

saída de Olá é semelhante a:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Tome nota do **chave1** como pode utilizá-lo toointeract com a sua conta de armazenamento nos passos seguintes Olá.

### <a name="create-a-storage-container"></a>Criar um contentor de armazenamento
No Olá mesma forma que criar diretórios diferentes toologically organizar o sistema de ficheiros local, criar contentores dentro de um tooorganize de conta de armazenamento aos discos. Uma conta do storage pode conter qualquer número de contentores. Criar um contentor com [criar contentor de armazenamento az](/cli/azure/storage/container#create).

Olá exemplo seguinte cria um contentor com o nome *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Carregar Olá VHD
Agora carregue o seu disco personalizado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload). Carregar e armazenar o disco personalizado como um blob de página.

Especifique a chave de acesso, o contentor de Olá que criou no passo anterior Olá e, em seguida, Olá disco de personalizado toohello caminho no seu computador local:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Carregamento Olá VHD poderá demorar algum tempo.

### <a name="create-a-managed-disk"></a>Criar um disco gerido


Criar um disco gerido da utilização de VHD Olá [criar disco de az](/cli/azure/disk#create). Olá exemplo seguinte cria um disco gerido com o nome *myManagedDisk* de Olá VHD que carregou tooyour com o nome de conta de armazenamento e um contentor:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Opção 2: Copiar uma VM existente

Também pode criar Olá VM personalizada no Azure e, em seguida, disco de SO de Olá de cópia e anexe-tooa nova VM toocreate outra cópia. Isto é adequado para fins de teste, mas se pretender toouse uma VM do Azure existente como modelo Olá para várias novas VMs, realmente deve criar um **imagem** em vez disso. Para obter mais informações sobre como criar uma imagem de VM do Azure existente, consulte [criar uma imagem personalizada da VM do Azure utilizando Olá CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Criar um instantâneo

Este exemplo cria um instantâneo de uma VM chamada *myVM* no grupo de recursos *myResourceGroup* e cria um instantâneo com o nome *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Criar disco Olá de gerido

Crie um novo disco gerido a partir do instantâneo Olá.

Obter ID de Olá de instantâneo Olá. Neste exemplo, é denominado instantâneo Olá *osDiskSnapshot* e está a ser Olá *myResourceGroup* grupo de recursos.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Crie disco Olá de gerido. Neste exemplo, vamos criar um disco gerido com o nome *myManagedDisk* do nosso instantâneo, que é 128 GB de tamanho no armazenamento standard.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Criar Olá VM

Agora, crie a VM com [az vm criar](/cli/azure/vm#create) e anexe (– anexar--disco do SO) Olá disco como disco de SO de Olá de gerido. Olá exemplo seguinte cria uma VM chamada *myNewVM* através de Olá de gerido criado a partir do seu carregado VHD do disco:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Deve ser capaz de tooSSH para Olá VM utilizando credenciais de Olá de Olá de VM de origem. 

## <a name="next-steps"></a>Passos seguintes
Depois de ter preparado e carregado o disco virtual personalizado, pode ler mais sobre [utilizando o Gestor de recursos e modelos](../../azure-resource-manager/resource-group-overview.md). Também poderá demasiado[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs. Se tiver aplicações em execução no seu VMs que precisa de tooaccess, lembre-se demasiado[abrir portas e os pontos finais](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

