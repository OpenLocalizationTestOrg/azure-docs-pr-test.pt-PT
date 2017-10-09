---
title: aaaAbout discos e VHD para as VMs de Linux do Microsoft Azure | Microsoft Docs
description: "Saiba mais sobre Olá Noções básicas sobre discos e VHDs para computadores virtuais Linux no Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Sobre discos e VHD para as VMs Linux do Azure
Tal como qualquer outro computador, as máquinas virtuais no Azure utilizar discos como um toostore implementado um sistema operativo, aplicações e dados. Todas as máquinas virtuais do Azure de ter, pelo menos, dois discos – um disco de sistema operativo Linux e um disco temporário. disco do sistema operativo Olá é criado a partir de uma imagem e o disco do sistema operativo Olá e imagem Olá são, na verdade, discos rígidos virtuais (VHDs) armazenados numa conta de armazenamento do Azure. Máquinas virtuais podem ter também um ou mais discos de dados, que também são armazenados como VHDs. 

Neste artigo, iremos falar sobre utiliza diferentes de Olá para discos de Olá e, em seguida, aborda os diferentes tipos Olá de discos, pode criar e utilizar. Este artigo também está disponível para [máquinas virtuais Windows](storage-about-disks-and-vhds-windows.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos utilizados por VMs

Vamos ver como discos de hello são utilizadas por Olá VMs.

## <a name="operating-system-disk"></a>Disco do sistema operativo
Cada máquina virtual possui um disco de sistema de operativo anexado. Este é registado como uma unidade SATA e assinalada como /dev/sda por predefinição. Este disco tem uma capacidade máxima de 2048 gigabytes (GB). 

## <a name="temporary-disk"></a>Disco temporário
Cada VM contém um disco temporário. disco temporário Olá fornece armazenamento de curta duração para aplicações e processos e tooonly pretendido arquivo de dados, tais como ficheiros de página ou a troca. Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando a [voltar a implementar uma VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante um reinício padrão do Olá VM, devem manter dados Olá na unidade temporária Olá.

Em máquinas virtuais do Linux, o disco Olá está normalmente **/dev/sdb** é formatado e montado demasiado**/mnt** por Olá agente Linux do Azure. o tamanho do disco temporário Olá Olá varia, com base no tamanho Olá da máquina virtual de Olá. Para obter mais informações, consulte [tamanhos de máquinas virtuais do Linux](../virtual-machines/linux/sizes.md).

Para obter mais informações sobre como o Azure utiliza disco temporário Olá, consulte [compreender unidade temporária de Olá em do Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Disco de dados
Um disco de dados é uma imagem VHD que dados de aplicação de toostore de máquina virtual anexado tooa ou outros dados terá tookeep. Os discos de dados estão registados como unidades de SCSI e são etiquetados com uma letra que escolher. Cada disco de dados tem uma capacidade máxima de 4095 GB. Olá tamanho da máquina virtual de Olá determina quantos discos de dados, pode anexar tooit e Olá tipo de armazenamento pode utilizar discos de Olá toohost.

> [!NOTE]
> Para obter mais detalhes sobre as capacidades de máquinas virtuais, consulte [tamanhos de máquinas virtuais do Linux](../virtual-machines/linux/sizes.md).
> 

Quando criar uma máquina virtual a partir de uma imagem, o Azure cria um disco de sistema operativo. Se utilizar uma imagem que inclui os discos de dados, o Azure também cria Olá discos de dados quando cria a máquina virtual de Olá. Caso contrário, adicione discos de dados depois de criar a máquina virtual de Olá.

Pode adicionar máquinas de virtuais de tooa de discos de dados em qualquer altura, pelo **anexar** Olá disco toohello máquina. Pode utilizar uma imagem VHD que tiver carregado ou copiados tooyour conta de armazenamento ou um que Azure cria por si. Anexar um disco de dados associa ficheiro VHD Olá Olá VM, colocando uma concessão no Olá VHD, pelo que não pode ser eliminada do armazenamento enquanto ainda está ligado.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Resolução de problemas
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Passos seguintes
* [Anexar um disco](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd armazenamento adicional para a VM.
* [Configurar software RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para redundância.
* [Capturar uma máquina virtual Linux](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) pelo que pode implementar rapidamente VMs adicionais.

