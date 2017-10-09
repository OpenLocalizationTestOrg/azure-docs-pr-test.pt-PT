---
title: "aaaCreate imagens VM personalizadas com Olá CLI do Azure | Microsoft Docs"
description: "Tutorial - criar uma imagem VM personalizada utilizando Olá CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Criar uma imagem personalizada da VM do Azure utilizando Olá CLI

São imagens personalizadas, como imagens do marketplace, mas que são criados por si. Imagens personalizadas podem ser utilizados toobootstrap configurações, tais como o pré-carregamento de aplicações, configurações de aplicação e outras configurações de SO. Neste tutorial, vai criar sua imagem personalizada de uma máquina virtual do Azure. Saiba como:

> [!div class="checklist"]
> * Desaprovisionar e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM a partir de uma imagem personalizada
> * Lista todas as imagens de Olá na sua subscrição
> * Eliminar uma imagem


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de começar

passos de Olá abaixo de detalhe como tootake uma VM existente e ative a imagem para um reutilizável personalizado que podem utilizar toocreate novas instâncias de VM.

exemplo de Olá toocomplete neste tutorial, tem de ter uma máquina virtual existente. Se for necessário, isto [script de exemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) pode criar uma por si. Quando trabalhar com tutorial de Olá, substitua o grupo de recursos de Olá e VM nomes sempre que necessário.

## <a name="create-a-custom-image"></a>Criar uma imagem personalizada

toocreate uma imagem de uma máquina virtual, terá de tooprepare Olá VM ao desaprovisionamento, Desalocação e, em seguida, marcar Olá de VM de origem como generalizado. Uma vez Olá que VM tenha sido preparada, pode criar uma imagem.

### <a name="deprovision-hello-vm"></a>Desaprovisionar Olá VM 

Desaprovisionamento generaliza Olá VM ao remover informações específicas do computador. Este generalização torna possível toodeploy várias VMs a partir de uma única imagem. Durante o desaprovisionamento, nome de anfitrião Olá é reposto demasiado*localhost.localdomain*. Chaves de anfitrião do SSH, configurações de nameserver, palavra-passe raiz e concessões DHCP em cache também são eliminados.

Olá toodeprovision VM, utilize o agente de VM do Azure de Olá (waagent). agente de VM do Azure Olá Olá VM está instalado e gere de aprovisionamento e interagir com Olá controlador de recursos do Azure. Para obter mais informações, consulte Olá [guia de utilizador do agente Linux do Azure](agent-user-guide.md).

Ligar tooyour VM através de SSH e Olá de toodeprovision Olá executar comandos VM. Com Olá `+user` argumento, a última conta de utilizador aprovisionado Olá e quaisquer dados associados também são eliminados. Substitua o endereço IP do exemplo Olá pelo endereço IP público Olá da sua VM.

SSH toohello VM.
```bash
ssh azureuser@52.174.34.95
```
Desaprovisionar Olá VM.

```bash
sudo waagent -deprovision+user -force
```
Fechar a sessão SSH Olá.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Desalocar e marcar Olá VM como generalizado

toocreate uma imagem, tem de Olá VM toobe desalocada. Desalocar Olá VM utilizando [az vm desalocar](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Por fim, definir o estado de Olá de Olá VM como generalizado com [az vm Generalizar](/cli//azure/vm#generalize) para Olá plataforma Azure confie Olá VM tenha sido generalizada. Só pode criar uma imagem de uma VM generalizada.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Criar imagem Olá

Agora pode criar uma imagem de VM de Olá utilizando [criar imagem az](/cli//azure/image#create). Olá exemplo seguinte cria uma imagem com o nome *myImage* de uma VM chamada *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Criar as VMs da imagem de Olá

Agora que tem uma imagem, pode criar uma ou mais VMs novas da utilização de imagem Olá [az vm criar](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada *myVMfromImage* imagem Olá com o nome do *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Gestão de imagens 

Seguem-se alguns exemplos de tarefas comuns de gestão de imagem e como toocomplete-los utilizando Olá CLI do Azure.

Liste todas as imagens de por nome de um formato de tabela.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Elimine uma imagem. Neste exemplo eliminações Olá imagem com o nome *myOldImage* de Olá *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, vai criar uma imagem VM personalizada. Aprendeu a:

> [!div class="checklist"]
> * Desaprovisionar e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM a partir de uma imagem personalizada
> * Lista todas as imagens de Olá na sua subscrição
> * Eliminar uma imagem

Produzir toohello seguinte toolearn tutorial sobre máquinas virtuais altamente disponíveis.

> [!div class="nextstepaction"]
> [Criar VMs de elevada](tutorial-availability-sets.md).

