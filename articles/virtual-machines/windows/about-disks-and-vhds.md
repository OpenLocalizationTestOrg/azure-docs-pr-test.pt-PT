---
title: aaaAbout discos e VHD para as VMs do Microsoft Azure Windows | Microsoft Docs
description: "Saiba mais sobre Olá Noções básicas sobre discos e as máquinas virtuais de VHDs para Windows no Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1b0d6bf05237bb3d1497b2c60f79a0159b730108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Sobre discos e VHDs para VMs do Windows Azure
Tal como qualquer outro computador, as máquinas virtuais no Azure utilizar discos como um toostore implementado um sistema operativo, aplicações e dados. Todas as máquinas virtuais do Azure de ter, pelo menos, dois discos – um disco de sistema operativo Windows e um disco temporário. disco do sistema operativo Olá é criado a partir de uma imagem e o disco do sistema operativo Olá e imagem Olá são discos rígidos virtuais (VHDs) armazenados numa conta de armazenamento do Azure. Máquinas virtuais podem ter também um ou mais discos de dados, que também são armazenados como VHDs. 

Neste artigo, iremos falar sobre utiliza diferentes de Olá para discos de Olá e, em seguida, aborda os diferentes tipos Olá de discos, pode criar e utilizar. Este artigo também está disponível para [máquinas virtuais do Linux](about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos utilizados por VMs

Vamos ver como discos de hello são utilizadas por Olá VMs.

### <a name="operating-system-disk"></a>Disco do sistema operativo
Cada máquina virtual possui um disco de sistema de operativo anexado. Tem registado como uma unidade SATA e identificados como unidade de c: Olá por predefinição. Este disco tem uma capacidade máxima de 2048 gigabytes (GB). 

### <a name="temporary-disk"></a>Disco temporário
Cada VM contém um disco temporário. disco temporário Olá fornece armazenamento de curta duração para aplicações e processos e tooonly pretendido arquivo de dados, tais como ficheiros de página ou a troca. Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando a [voltar a implementar uma VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Durante um reinício padrão do Olá VM, devem manter dados Olá na unidade temporária Olá.

disco temporário Olá assinalada como como Olá unidade d: por predefinição e utilizado para armazenar pagefile.sys. tooremap esta letra de unidade diferente do disco tooa, consulte [alteração Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md). o tamanho do disco temporário Olá Olá varia, com base no tamanho Olá da máquina virtual de Olá. Para obter mais informações, consulte [máquinas virtuais de tamanhos para Windows](sizes.md).

Para obter mais informações sobre como o Azure utiliza disco temporário Olá, consulte [compreender unidade temporária de Olá em do Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Disco de dados
Um disco de dados é uma imagem VHD que dados de aplicação de toostore de máquina virtual anexado tooa ou outros dados terá tookeep. Os discos de dados estão registados como unidades de SCSI e são etiquetados com uma letra que escolher. Cada disco de dados tem uma capacidade máxima de 4095 GB. Olá tamanho da máquina virtual de Olá determina quantos discos de dados, pode anexar tooit e Olá tipo de armazenamento pode utilizar discos de Olá toohost.

> [!NOTE]
> Para obter mais informações sobre as capacidades de máquinas virtuais, consulte [máquinas virtuais de tamanhos para Windows](sizes.md).
> 

Quando criar uma máquina virtual a partir de uma imagem, o Azure cria um disco de sistema operativo. Se utilizar uma imagem que inclui os discos de dados, o Azure também cria Olá discos de dados quando cria a máquina virtual de Olá. Caso contrário, adicione discos de dados depois de criar a máquina virtual de Olá.

Pode adicionar máquinas de virtuais de tooa de discos de dados em qualquer altura, pelo **anexar** Olá disco toohello máquina. Pode utilizar uma imagem VHD que tiver carregado ou copiados tooyour conta de armazenamento ou um que Azure cria por si. Anexar um disco de dados associa ficheiro VHD Olá Olá VM colocando uma concessão no Olá VHD, pelo que não pode ser eliminada do armazenamento enquanto ainda está ligado.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Uma recomendação última: Utilize cortar com discos padrão não geridos 

Se utilizar discos padrão não geridos (HDD), deverá ativar a limitação. Operações de COMPACTAÇÃO elimina os blocos no disco Olá, é-lhe faturado apenas para o armazenamento que está a utilizar, na verdade, de modo. Isto permite poupar nos custos se criar ficheiros grandes e, em seguida, elimine-os. 

Pode executar esta definição COMPACTAÇÃO do comando toocheck Olá. Abra uma linha de comandos na sua VM do Windows e o tipo:


```
fsutil behavior query DisableDeleteNotify
```

Se o comando de Olá devolve 0, cortar está ativada corretamente. Se devolver-1, execute Olá comando tooenable cortar os seguintes:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Nota: O suporte começa com o Windows Server 2012 / Windows 8 e superior, consulte ver [nova API permite que aplicações toosend "Compactar e Unmap" sugestões toostorage suporte de dados](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Passos seguintes
* [Anexar um disco](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd armazenamento adicional para a VM.
* [Alteração Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para a aplicação pode utilizar a unidade de d: Olá de dados.

