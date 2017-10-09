---
title: aaaDownload um VHD de Linux a partir do Azure | Microsoft Docs
description: "Transfira um VHD de Linux utilizando Olá CLI do Azure e Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Transferir um VHD de Linux a partir do Azure

Neste artigo, saiba como toodownload um [Linux de disco rígido virtual (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ficheiro a partir do Azure com Olá CLI do Azure e o portal do Azure. 

Máquinas virtuais (VMs) em utilização do Azure [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como um toostore implementado um sistema operativo, aplicações e dados. Todas as VMs do Azure de ter, pelo menos, dois discos – um disco de sistema operativo Windows e um disco temporário. disco do sistema operativo Olá for criado inicialmente a partir de uma imagem e o disco do sistema operativo Olá e imagem Olá são VHDs armazenados na conta de armazenamento do Azure. Máquinas virtuais podem ter também um ou mais discos de dados, que também são armazenados como VHDs.

Se ainda não o fez, instale [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Parar Olá VM

Não é possível transferir um VHD a partir do Azure se está ligado tooa VM a executar. É necessário toodownload VM de Olá toostop um VHD. Se quiser toouse um VHD como um [imagem](tutorial-custom-images.md) toocreate outras VMs com novos discos, tem de toodeprovision e generalizar o sistema de operativo Olá contido no Olá de ficheiros e parar Olá VM. Olá toouse VHD como um disco para uma nova instância de uma VM existente ou o disco de dados, apenas terá toostop e desalocar Olá VM.

toouse Olá VHD como uma imagem toocreate outras VMs, conclua estes passos:

1. Utilizar o SSH, o nome da conta Olá e o endereço IP público de Olá do Olá VM tooconnect tooit e desaprovisioná-lo. Olá + utilizador parâmetro também remove a última conta de utilizador aprovisionado Olá. Se estiver baking as credenciais da conta na toohello VM, deixe terminar este + parâmetro de utilizador. Olá exemplo a seguir remove última conta de utilizador aprovisionado Olá:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Inicie sessão no tooyour a conta do Azure com [início de sessão az](https://docs.microsoft.com/cli/azure/#login).
3. Pare e desalocar Olá VM.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Generalize Olá VM. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

Olá toouse VHD como um disco para uma nova instância de uma VM existente ou o disco de dados, conclua estes passos:

1.  Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2.  No menu do Hub de Olá, clique em **máquinas virtuais**.
3.  Selecione Olá VM Olá lista.
4.  No painel Olá Olá VM, clique em **parar**.

    ![Parar VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Gerar SAS URL

ficheiro VHD de Olá toodownload, terá de toogenerate um [assinatura de acesso partilhado (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Quando é gerado, o URL de Olá uma hora de expiração é atribuída toohello URL.

1.  Olá menu do painel Olá Olá VM, clique em **discos**.
2.  Selecione o disco do sistema operativo Olá para Olá VM e, em seguida, clique em **exportar**.
3.  Clique em **gerar URL**.

    ![Gerar URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Transferir o VHD

1.  Em Olá URL que foi gerado, clique em ficheiro VHD de Olá de transferência.

    ![Transferir o VHD](./media/download-vhd/export-download.png)

2.  Poderá ser necessário tooclick **guardar** na transferência do Olá browser toostart Olá. nome do Olá predefinido para o ficheiro VHD Olá é *abcd*.

    ![Clique em Guardar no browser Olá](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Passos seguintes

- Saiba como demasiado[carregar e criar uma VM com Linux a partir do disco personalizado com Olá Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Gerir Olá de discos do Azure CLI do Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

