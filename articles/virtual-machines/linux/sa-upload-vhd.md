---
title: aaaUpload um disco do Linux personalizado com o Azure CLI 2.0 | Microsoft Docs
description: "Criar e carregar um tooAzure de disco rígido virtual (VHD) utilizando o modelo de implementação do Resource Manager Olá e Olá Azure CLI 2.0"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Carregar e criar uma VM com Linux a partir do disco personalizado com Olá Azure CLI 2.0
Este artigo mostra-lhe como tooupload tooan um disco rígido virtual (VHD) storage do Azure da conta com Olá 2.0 de CLI do Azure e criar VMs com Linux a partir deste disco personalizado. Também pode executar estes passos com Olá [CLI do Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Esta funcionalidade permite-lhe tooinstall e configurar um requisitos do Linux distro tooyour e, em seguida, utilizar essa VHD tooquickly criar máquinas de virtuais (VMs) do Azure.

Este tópico utiliza contas de armazenamento para hello VHDs finais, mas também pode fazer estes passos através de [discos geridos pelo](upload-vhd.md). 

## <a name="quick-commands"></a>Comandos rápidos
Se precisar de tooquickly realizar tarefas Olá, Olá Olá de detalhes de secção a seguir base tooupload comandos tooAzure um VHD. Mais informações e o contexto de cada passo pode ser encontrado rest Olá documento Olá, [Iniciar aqui](#requirements).

Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes de parâmetros de exemplo incluídos `myResourceGroup`, `mystorageaccount`, e `mydisks`.

Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `WestUs` localização:

```azurecli
az group create --name myResourceGroup --location westus
```

Criar um toohold de conta de armazenamento de discos virtuais com [criar conta de armazenamento az](/cli/azure/storage/account#create). Olá exemplo seguinte cria uma conta de armazenamento com o nome `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Listar chaves de acesso de Olá para a sua conta de armazenamento com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list). Tome nota do `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Criar um contentor na sua conta de armazenamento utilizando a chave de armazenamento Olá obtida com [criar contentor de armazenamento az](/cli/azure/storage/container#create). Olá exemplo seguinte cria um contentor com o nome `mydisks` utilizando o valor de chave de armazenamento de Olá de `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Por fim, carregue o contentor de toohello do VHD que criou com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload). Especifique o caminho local de Olá tooyour VHD em `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Especifique Olá URI tooyour disco (`--image`) com [az vm criar](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada `myVM` utilização de disco virtual Olá carregado anteriormente:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

conta de armazenamento de destino Olá tem toobe Olá mesmo como onde o seu disco virtual para que carregou. É também necessário toospecify ou responder a pedidos de, Olá todos os parâmetros adicionais necessários ao hello **az vm criar** comando tais como a rede virtual, o endereço IP público, o nome de utilizador e chaves SSH. Pode ler mais sobre Olá [parâmetros disponíveis de Gestor de recursos do CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisitos
Olá toocomplete os seguintes passos, tem de:

* **Sistema de operativo Linux instalado num ficheiro. vhd** -instalar um [distribuição Linux aprovadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual Olá VHD formato. Várias ferramentas existem toocreate uma VM e os VHD:
  * Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tendo cuidado toouse VHD como o formato de imagem. Se necessário, pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) utilizando `qemu-img convert`.
  * Também pode utilizar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> formato VHDX mais recente Olá não é suportado no Azure. Quando cria uma VM, especifique o VHD como formato Olá. Se for necessário, pode converter VHDX discos tooVHD utilizando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou Olá [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell. Além disso, Azure não suporta o carregamento de VHDs dinâmicos, por isso terá de tooconvert essa toostatic discos VHDs antes de carregar. Pode utilizar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinâmicos durante o processo de Olá de carregamento tooAzure.
> 
> 

* VMs criadas a partir do seu disco personalizado tem de residir na Olá mesma conta de armazenamento como disco de Olá próprio
  * Criar toohold de conta e contentor de armazenamento do disco personalizado e VMs criadas
  * Depois de criar as suas VMs, pode eliminar em segurança o disco

Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes de parâmetros de exemplo incluídos `myResourceGroup`, `mystorageaccount`, e `mydisks`.

<a id="prepimage"> </a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Preparar Olá disco toobe carregado
Azure suporta várias distribuições em Linux (consulte [distribuições aprovadas pelo](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Olá seguintes artigos orientá-lo através do como tooprepare Olá várias distribuições em Linux que são suportadas no Azure:

* **[Distribuições baseado em centOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Outras - distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Consulte também Olá  **[Linux instalação notas](create-upload-generic.md#general-linux-installation-notes)**  para dicas mais gerais sobre preparar imagens de Linux para o Azure.

> [!NOTE]
> Olá [plataforma Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs com o Linux apenas quando um dos Olá distribuições aprovadas pelo é utilizada com detalhes de configuração de Olá conforme especificado em versões suportadas em [Linux em aprovadas pelo Azure Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Grupos de recursos logicamente reunir toosupport de recursos do Azure Olá todas as suas máquinas virtuais, tais como redes virtuais Olá e armazenamento. Para grupos de recursos mais informações, consulte [descrição geral de grupos de recursos](../../azure-resource-manager/resource-group-overview.md). Antes de carregar o seu disco personalizado e a criação de VMs, terá primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).

Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `westus` localização:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Criar uma conta de armazenamento para o seu disco personalizado e VMs com [criar conta de armazenamento az](/cli/azure/storage/account#create). Quaisquer VMs com discos não geridos que cria a partir do seu toobe necessidade de disco personalizado no Olá a mesma conta de armazenamento como esse disco. 

Olá exemplo seguinte cria uma conta de armazenamento com o nome `mystorageaccount` no grupo de recursos de Olá que criou anteriormente:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Lista de chaves de conta de armazenamento
O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento. Estas chaves de acesso são utilizadas ao autenticar a conta do storage toohello, tais como toocarry operações de escrita. Leia mais sobre [gerir acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Visualizar chaves de acesso de Olá com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).

Ver as chaves de acesso Olá Olá conta de armazenamento que criou:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Tome nota do `key1` como pode utilizá-lo toointeract com a sua conta de armazenamento nos passos seguintes Olá.

## <a name="create-a-storage-container"></a>Criar um contentor de armazenamento
No Olá mesma forma que criar diretórios diferentes toologically organizar o sistema de ficheiros local, criar contentores dentro de um tooorganize de conta de armazenamento aos discos. Uma conta do storage pode conter qualquer número de contentores. Criar um contentor com [criar contentor de armazenamento az](/cli/azure/storage/container#create).

Olá exemplo seguinte cria um contentor com o nome `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Carregar o VHD
Agora carregue o seu disco personalizado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload). Carregar e armazenar o disco personalizado como um blob de página.

Especifique a chave de acesso, o contentor de Olá que criou no passo anterior Olá e, em seguida, Olá disco de personalizado toohello caminho no seu computador local:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Criar Olá VM
toocreate uma VM com os discos não geridos, especifique o disco do Olá URI tooyour (`--image`) com [az vm criar](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada `myVM` utilização de disco virtual Olá carregado anteriormente:

Especifique Olá `--image` parâmetro com [az vm criar](/cli/azure/vm#create) toopoint tooyour personalizado disco. Certifique-se de que `--storage-account` correspondências Olá conta do storage onde está armazenado o seu disco personalizado. Não dispõe de toouse Olá mesmo contentor como Olá disco personalizado toostore as suas VMs. Certifique-se de que toocreate quaisquer contentores adicionais Olá igual forma ao hello passos anteriores antes de carregar o seu disco personalizado.

Olá exemplo seguinte cria uma VM chamada `myVM` do seu disco personalizado:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Ainda necessário toospecify, ou responder a pedidos de, Olá todos os parâmetros adicionais necessários ao hello **az vm criar** comando como o nome de utilizador e as chaves SSH.


## <a name="resource-manager-template"></a>Modelo do Resource Manager
Modelos Azure Resource Manager são ficheiros JavaScript Object Notation (JSON) que definem o ambiente de Olá desejar toobuild. modelos de Olá são divididos em toodifferent fornecedores de recursos, tais como a computação ou rede. Pode utilizar os modelos existentes ou escrever os seus próprios. Leia mais sobre [utilizando o Gestor de recursos e modelos](../../azure-resource-manager/resource-group-overview.md).

Dentro do Olá `Microsoft.Compute/virtualMachines` fornecedor do seu modelo, tiver um `storageProfile` nó que contém os detalhes de configuração de Olá para a VM. Olá dois parâmetros principal tooedit são Olá `image` e `vhd` URIs ponto disco personalizado tooyour e disco virtual a nova VM. seguinte Olá mostra um exemplo de Olá JSON para utilizar um disco personalizado:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Pode utilizar [este toocreate modelo existente uma VM a partir de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou leia sobre [criar os seus próprios modelos Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Assim que tiver um modelo configurado, utilize [criar a implementação do grupo az](/cli/azure/group/deployment#create) toocreate as suas VMs. Especifique o URI do seu modelo JSON de Olá com Olá `--template-uri` parâmetro:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Se tiver um ficheiro JSON armazenado localmente no seu computador, pode utilizar Olá `--template-file` parâmetro em vez disso:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Passos seguintes
Depois de ter preparado e carregado o disco virtual personalizado, pode ler mais sobre [utilizando o Gestor de recursos e modelos](../../azure-resource-manager/resource-group-overview.md). Também poderá demasiado[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs. Se tiver aplicações em execução no seu VMs que precisa de tooaccess, lembre-se demasiado[abrir portas e os pontos finais](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

