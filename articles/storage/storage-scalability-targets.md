---
title: aaaAzure metas de desempenho e escalabilidade do Storage | Microsoft Docs
description: "Saiba mais sobre metas de desempenho e escalabilidade de Olá para o armazenamento do Azure, incluindo a capacidade, a taxa de pedidos e a largura de banda de entrada e saída para as contas do storage standard e premium. Compreenda metas de desempenho para partições dentro de cada um dos serviços de armazenamento do Azure Olá."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 98de116a01b64f3418808a5f626b6c70d8d432e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Alvos de Dimensionamento e Desempenho do Armazenamento do Azure
## <a name="overview"></a>Descrição geral
Este tópico descreve os tópicos de desempenho e escalabilidade Olá para armazenamento do Microsoft Azure. Para obter um resumo dos outros limites do Azure, consulte [subscrição do Azure e limites de serviço, Quotas e restrições](../azure-subscription-service-limits.md).

> [!NOTE]
> Todas as contas de armazenamento executam na topologia de rede simples novo Olá e suportam metas de desempenho e escalabilidade do Olá indicadas abaixo, independentemente de quando foram criados. Para obter mais informações na arquitetura de rede simples de armazenamento do Azure de Olá e na escalabilidade, consulte [armazenamento do Microsoft Azure: A nuvem armazenamento serviço de elevada disponibilidade com consistência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> metas de desempenho e escalabilidade do Olá aqui listadas são destinos de gama alta de classe, mas são alcançável. Em todos os casos, o pedido de Olá velocidade e largura de banda alcançada através da sua conta de armazenamento depende de tamanho de Olá de objetos armazenados, padrões de acesso de Olá utilizados e Olá o tipo de carga de trabalho que executa a sua aplicação. Ser tootest se o serviço toodetermine se o seu desempenho aos seus requisitos. Se for possível, evitar picos repentino na taxa de Olá de tráfego e certifique-se de que o tráfego é distribuído bem em partições.
> 
> Quando a aplicação atinge o limite de Olá do que uma partição pode processar a carga de trabalho, do armazenamento do Azure irá iniciar o código de erro de tooreturn 503 (servidor ocupado) ou o código de erro 500 respostas de (tempo limite da operação). Se isto ocorre, a aplicação Olá deve utilizar uma política de término exponencial de tentativas. término exponencial Olá permite Olá carga no Olá partição toodecrease e tooease saída picos na partição de toothat de tráfego.
> 
> 

Que excederem Olá precisa da sua aplicação metas de escalabilidade Olá de uma única conta de armazenamento, pode criar a aplicação toouse várias contas de armazenamento e os objetos de dados de partição entre essas contas de armazenamento. Consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre os preços de volume.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Objetivos de escalabilidade para ficheiros, tabelas, filas e blobs
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Objetivos de escalabilidade para discos de máquinas virtuais
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

Consulte [tamanhos de Windows VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tamanhos de VM com Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes adicionais.

## <a name="managed-virtual-machine-disks"></a>Discos de máquinas de virtuais gerido

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Discos de máquinas de virtuais não geridos
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Objetivos de escalabilidade para Gestor de recursos do Azure
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partições no armazenamento do Azure
Cada objeto que contém os dados armazenados no Storage do Azure (blobs, mensagens, as entidades e de ficheiros) pertence tooa partição e é identificado por uma chave de partição. partição de Olá determina como a carga de armazenamento do Azure equilibra e blobs, mensagens, as entidades e ficheiros em servidores toomeet Olá tráfego às necessidades desses objetos. chave de partição Olá é exclusivo e é utilizado toolocate um blob, mensagem ou entidade.

tabela de Olá mostrada acima na [metas de escalabilidade para contas de armazenamento padrão](#standard-storage-accounts) listas Olá metas de desempenho para uma partição individual para cada serviço.

As partições afetam o balanceamento de carga e escalabilidade para cada um dos serviços de armazenamento Olá no Olá seguintes formas:

* **Os BLOBs**: chave de partição de Olá para um blob é o nome da conta + nome do contentor + nome do blob. Isto significa que cada blob pode ter a sua própria partição se a carga no blob Olá imperativas-lo. Os BLOBs podem ser distribuídos em vários servidores num ordem tooscale saída toothem de acesso, mas um blob único só pode ser servido por um único servidor. Embora blobs podem ser logicamente agrupados em contentores de BLOBs, não há nenhum implicações de criação de partições deste agrupamento.
* **Ficheiros**: chave de partição de Olá para um ficheiro é o nome da partilha nome + ficheiro de conta. Isto significa que todos os ficheiros numa partilha de ficheiros também estão a ser uma única partição.
* **Mensagens**: chave de partição de Olá de uma mensagem é o nome de conta Olá + nome da fila, pelo que todas as mensagens numa fila são agrupadas numa única partição e que são servidas por um único servidor. Filas diferentes podem ser processadas por servidores diferentes toobalance Olá carregar para, no entanto, muitos filas uma conta de armazenamento pode ter.
* **Entidades**: chave de partição de Olá para uma entidade é o nome da conta + nome da tabela + chave de partição, em que a chave de partição Olá é valor Olá Olá necessário definidos pelo utilizador **PartitionKey** propriedade para a entidade de Olá. Todas as entidades com Olá mesmo valor de chave de partição estão agrupadas em Olá mesma partição e que é servida pelo Olá mesmo servidor de partição. Este é um toounderstand ponto importante conceber a sua aplicação. A aplicação deve equilibrar os benefícios de escalabilidade Olá de propagando-se de entidades em várias partições com Olá vantagens de acesso de dados de entidades numa partição única de agrupamento.  

Toogrouping das principais vantagens que é de um conjunto de entidades numa tabela numa única partição que é operações de atomic batch tooperform possível entre as entidades de Olá mesma partição, uma vez que existe uma partição num único servidor. Por conseguinte, se desejar tooperform operações de lote num grupo de entidades, considere agrupá-los com Olá mesma chave de partição. 

No Olá por outro lado, as entidades que estejam no Olá mesmo tabela mas ter chaves de partição diferentes podem ser balanceamento de carga em diferentes servidores, tornando toohave possíveis maior escalabilidade.

Recomendações para estruturar a estratégia de criação de partições para tabelas podem ser encontradas de detalhado [aqui](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Veja Também
* [Detalhes de preços de armazenamento](https://azure.microsoft.com/pricing/details/storage/)
* [Subscrição do Azure e limites de serviço, Quotas e restrições](../azure-subscription-service-limits.md)
* [Armazenamento Premium: Armazenamento de Elevado Desempenho para Cargas de Trabalho de Máquinas Virtuais do Azure](storage-premium-storage.md)
* [Replicação de armazenamento do Azure](storage-redundancy.md)
* [Desempenho de armazenamento do Microsoft Azure e a lista de verificação de escalabilidade](storage-performance-checklist.md)
* [Armazenamento do Microsoft Azure: Um elevada serviço em nuvem armazenamento com consistência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

