---
title: "com base em aaaHD económica armazenamento padrão e discos da VM do Azure | Microsoft Docs"
description: "Aborda padrão de armazenamento económico e discos VM não geridos e geridos."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Padrão de armazenamento económico e discos de VM do Azure não geridos e geridos

Armazenamento padrão do Azure fornece suporte de disco fiável, de baixo custo para VMs executar cargas de trabalho insensível à latência. Também suporta blobs, tabelas, filas e os ficheiros. Com o armazenamento Standard, os dados de Olá são armazenados em unidades de disco rígido (HDDs). Ao trabalhar com as VMs, pode utilizar discos de armazenamento standard para cenários de desenvolvimento/teste e cargas de trabalho críticas inferior e discos de armazenamento premium para aplicações de produção fundamentais. Armazenamento Standard está disponível em todas as regiões do Azure. 

Este artigo foca-se na utilização de Olá de armazenamento standard para os discos de VM. Para obter mais informações sobre a utilização de Olá de armazenamento com blobs, tabelas, filas e ficheiros, consulte toohello [introdução tooStorage](storage-introduction.md).

## <a name="disk-types"></a>Tipos de disco

Existem duas formas toocreate discos padrão para VMs do Azure:

**Não gerido discos**: Este é método original olá onde irá gerir Olá armazenamento contas utilizadas toostore Olá ficheiros VHD que correspondem toohello discos VM. Ficheiros VHD são armazenados como blobs de páginas em contas de armazenamento. Os discos não geridos podem ser anexado tooany tamanho de VM do Azure, incluindo VMs Olá que utilizam o armazenamento Premium, principalmente como Olá série DSv2 e série GS. As VMs do Azure suportam anexar vários discos padrão, permitindo que a cópia de segurança too256 TB de armazenamento por VM.

[**Discos do Azure gerida**](storage-managed-disks-overview.md): esta funcionalidade gere contas de armazenamento de Olá utilizadas para discos VM Olá por si. Especifique o tipo de Olá (Premium ou Standard) e o tamanho do disco tem e o Azure cria e gere o disco de Olá por si. Não tem tooworry sobre colocação discos Olá em várias contas de armazenamento na ordem tooensure que permanecer dentro dos limites de escalabilidade Olá Olá contas do storage – Azure processa que por si.

Apesar de ambos os tipos de discos estão disponíveis, recomendamos que utilize partido tootake discos geridos as respetivas funcionalidades várias.

tooget começar a utilizar armazenamento padrão do Azure, visite [começar gratuitamente](https://azure.microsoft.com/pricing/free-trial/). 

Para obter informações sobre como toocreate uma VM com discos geridos, consulte um dos Olá os seguintes artigos.

* [Criar uma VM com o Resource Manager e o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)
* [Criar uma VM com Linux utilizando Olá Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>Funcionalidades de armazenamento Standard 

Vamos ver algumas das funcionalidades de Olá do armazenamento Standard. Para obter mais detalhes, consulte [introdução tooAzure armazenamento](storage-introduction.md).

**Armazenamento Standard**: armazenamento padrão do Azure suporta discos do Azure, Blobs do Azure, armazenamento ficheiros do Azure, Azure tabelas e filas do Azure. Serviços de armazenamento Standard toouse, começar a utilizar [criar uma conta de armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account).

**Discos de armazenamento Standard:** armazenamento Standard podem ser discos ligados tooall as VMs do Azure, incluindo VMs de tamanho da série utilizadas com o Premium Storage, tais como a série de série DSv2 e GS Olá. Um disco de armazenamento standard só pode ser anexado tooone VM. No entanto, poderá anexar um ou mais destes tooa de discos VM, se a contagem de disco máximo toohello definida para esse tamanho VM. Na secção a seguir no metas de desempenho e escalabilidade do Storage Standard de Olá, dita especificações de Olá mais detalhadamente. 

**Blob de páginas padrão**: blobs de páginas padrão são toohold utilizado discos persistentes para VMs e também pode ser acedidos diretamente através de REST como outros tipos de Blobs do Azure. [Blobs de páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) são uma coleção de páginas de 512 bytes otimizado para operações de escrita e leitura aleatória. 

**Replicação de armazenamento:** na maior parte das regiões, dados numa conta do standard storage podem ser replicadas localmente ou georreplicação em múltiplos centros de dados. tipos de Olá quatro de replicação disponível são armazenamento localmente redundante (LRS), o armazenamento com redundância de zona (ZRS), o armazenamento Georredundante (GRS) e o armazenamento Georredundante com acesso de leitura (RA-GRS). Gerido discos no armazenamento Standard suportam atualmente armazenamento localmente redundante (LRS) apenas. Para obter mais informações, consulte [replicação do Storage](storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Metas de Escalabilidade e Desempenho

Nesta secção, iremos descrevem metas de desempenho e escalabilidade do Olá precisa tooconsider quando utilizar o armazenamento standard.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Limites de contas – não se aplica toomanaged discos

| **Recurso** | **Limite Predefinido** |
|--------------|-------------------|
| TB por conta de armazenamento  | 500 TB |
| Entrada máximo<sup>1</sup> por conta de armazenamento (regiões EUA) | 10 Gbps, se estiver ativada GRS/ZRS, 20 Gbps para LRS |
| Saída máximo<sup>1</sup> por conta de armazenamento (regiões EUA) | 20 Gbps se estiver ativada RA-GRS/GRS/ZRS, 30 Gbps para LRS |
| Entrada máximo<sup>1</sup> por conta de armazenamento (Europeia e regiões Asian) | 5 Gbps, se estiver ativada GRS/ZRS, 10 Gbps para LRS |
| Saída máximo<sup>1</sup> por conta de armazenamento (Europeia e regiões Asian) | 10 Gbps, se estiver ativada RA-GRS/GRS/ZRS, 15 Gbps para LRS |
| Total de pedidos taxa (assumindo que o tamanho do objeto de 1 KB) por conta de armazenamento | Cópia de segurança too20, 000 IOPS, as entidades por segundo ou mensagens por segundo |

<sup>1</sup> entrada refere-se os dados de tooall (pedidos) que está a ser enviados tooa conta de armazenamento. Saída refere-se os dados de tooall (respostas) que está a ser recebidos de uma conta de armazenamento.

Para obter mais informações, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md).

Que excederem Olá precisa da sua aplicação metas de escalabilidade Olá de uma única conta de armazenamento, crie o toouse aplicação várias contas de armazenamento e os dados de partição entre essas contas de armazenamento. Em alternativa, pode discos gerida do Azure e Azure irá gerir Olá a criação de partições e o posicionamento dos seus dados para si.

### <a name="standard-disks-limits"></a>Limites de discos padrão

Ao contrário dos discos Premium, as operações de entrada/saída Olá por segundo (IOPS) e débito (largura de banda) de discos padrão não são aprovisionadas. Olá desempenho de discos padrão varia de acordo com Olá VM se encontra ligado tamanho toowhich Olá disco, não toohello tamanho do disco de Olá. Foi possível esperar tooachieve segurança toohello limite de desempenho listado na tabela de Olá abaixo.

**Limites de discos padrão (geridos e não gerido)**

| **Camada de VM**            | **Escalão básico VM** | **Escalão Standard VM** |
|------------------------|-------------------|----------------------|
| Tamanho máximo do disco          | 4095 GB           | 4095 GB              |
| Máx. 8 KB IOPS por disco | Cópia de segurança too300         | Cópia de segurança too500            |
| Largura de banda máximo por disco | Cópia de segurança too60 MB/s     | Cópia de segurança too60 MB/s        |

Se a carga de trabalho necessita de suporte de disco de elevado desempenho, baixa latência, deve considerar a utilizar o Premium Storage. tooknow mais benefícios do Premium Storage, visite [elevado desempenho Premium Storage e discos da VM do Azure](storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Instantâneos e BLOBs de cópia

toohello serviço de armazenamento, o ficheiro VHD Olá é um blob de página. Pode criar instantâneos de blobs de páginas e copie-os a localização de tooanother, tal como uma conta de armazenamento diferente.

### <a name="unmanaged-disks"></a>Discos não geridos

Pode criar [instantâneos incrementais](storage-incremental-snapshots.md) para discos de norma não gerida no Olá igual forma utilizar instantâneos de armazenamento Standard. Recomendamos que cria instantâneos e, em seguida, copiar esses conta de armazenamento standard georredundante tooa instantâneos se o disco de origem está a ser uma conta de armazenamento localmente redundante. Para obter mais informações, consulte [as opções de redundância do armazenamento do Azure](storage-redundancy.md).

Se um disco for anexado tooa VM, determinadas operações de API não são permitidas em discos de Olá. Por exemplo, não é possível efetuar um [copiar Blob](/rest/api/storageservices/Copy-Blob) operação nesse blob desde que o disco de Olá está ligado tooa VM. Em vez disso, primeiro de criar um instantâneo desse blob utilizando Olá [instantâneo Blob](/rest/api/storageservices/Snapshot-Blob) método API de REST e, em seguida, executar Olá [copiar Blob](/rest/api/storageservices/Copy-Blob) de Olá do Olá instantâneo toocopy o disco foi exposto. Em alternativa, pode desligar o disco de Olá e, em seguida, executar quaisquer operações necessárias.

toomaintain georredundante cópias da sua instantâneos, pode copiar instantâneos de uma conta de armazenamento standard georredundante tooa do armazenamento localmente redundante utilizando o AzCopy ou BLOBs de cópia. Para obter mais informações, consulte [transferir dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md) e [copiar Blob](/rest/api/storageservices/Copy-Blob).

Para obter informações detalhadas sobre efetuar as operações REST contra os blobs de páginas em contas do storage padrão, consulte [API de REST dos serviços de armazenamento do Azure](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Managed disks

Um instantâneo de um disco gerido é uma cópia só de leitura do disco de gerido Olá que é armazenado como um disco gerido standard. Instantâneos incrementais não são atualmente suportados para discos geridos, mas serão suportados em Olá futura.

Se um disco gerido está ligado ao tooa VM, determinadas operações de API não são permitidas em discos de Olá. Por exemplo, não é possível gerar um tooperform de assinatura (SAS) de acesso partilhado uma operação de cópia, enquanto o disco de Olá está anexado tooa VM. Em vez disso, primeiro criar um instantâneo do disco de Olá e, em seguida, efetuar cópia de Olá do instantâneo Olá. Em alternativa, pode desanexar o disco de Olá e, em seguida, gerar uma operação de cópia Olá tooperform do acesso partilhado (SAS) de assinatura.

## <a name="pricing-and-billing"></a>Preços e Faturação

Ao utilizar o armazenamento Standard, hello seguintes considerações de faturação aplicam-se:

* Tamanho de discos/dados de armazenamento Standard não gerido 
* Discos geridos padrão
* Instantâneos de armazenamento Standard
* Transferências de dados de saída
* Transações

**Não gerido tamanho de dados e o disco de armazenamento:** para discos não geridos e outros dados (blobs, tabelas, filas e ficheiros), são-lhe cobrados apenas para a quantidade de Olá de espaço está a utilizar. Por exemplo, se tiver uma VM cuja BLOBs de páginas é aprovisionado como 127 GB, mas hello VM é realmente utilizando 10 GB de espaço, apenas será faturado de 10 GB de espaço. Suportamos armazenamento Standard too8191 GB de cópia de segurança e os discos não geridos padrão segurança too4095 GB. 

**Discos geridos pelo:** discos geridos são faturados tamanho Olá aprovisionado. Se o disco é aprovisionado como um disco de 10 GB e estiver a utilizar apenas 5 GB, ainda será cobrada para o tamanho de aprovisionar Olá de 10 GB.

**Instantâneos**: os instantâneos de discos padrão são cobrados capacidade adicional Olá utilizada pelo instantâneos Olá. Para obter informações sobre instantâneos, consulte [criar um instantâneo de um Blob](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Transferências de dados de saída**: [transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) (dados ficar fora de centros de dados do Azure) cobrança para utilização de largura de banda.

**Transação**: Azure cobra 0.0036 $ 100 000 transações de armazenamento standard. Transações incluem ambos os leitura e escrita toostorage de operações.

Para obter informações detalhadas sobre os preços de armazenamento Standard, máquinas virtuais e discos geridos, consulte:

* [Preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Máquinas virtuais de preços](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Discos geridos de preços](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Suporte do serviço de cópia de segurança do Azure 

Máquinas virtuais com discos não geridos pode ser feitas através de cópia de segurança do Azure. [Obter mais detalhes](../backup/backup-azure-vms-first-look-arm.md).

Também pode utilizar Olá serviço cópia de segurança do Azure com discos geridos toocreate uma tarefa de cópia de segurança com políticas de retenção de cópias de segurança, fácil restauro de VM e cópias de segurança baseados no tempo. Pode ler mais sobre esta em [serviço utilizando a cópia de segurança do Azure para as VMs com discos geridos](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="next-steps"></a>Passos seguintes

* [Introdução tooAzure armazenamento](storage-introduction.md)

* [Criar uma conta de armazenamento](storage-create-storage-account.md)

* [Descrição Geral do Managed Disks](storage-managed-disks-overview.md)

* [Criar uma VM com o Resource Manager e o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Criar uma VM com Linux utilizando Olá Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md)
