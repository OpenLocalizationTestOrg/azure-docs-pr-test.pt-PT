---
title: "O Apache Kafka aumenta a escala – Azure HDInsight | Microsoft Docs"
description: Saiba como configurar discos geridos para o cluster do Apache Kafka no Azure HDInsight para aumentar a escalabilidade.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/28/2017
ms.author: larryfr
ms.openlocfilehash: e0fef242810148938e62dab9f77ee77b543fbbc0
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Configurar o armazenamento e a escalabilidade para o Apache Kafka no HDInsight

Saiba como configurar o número de discos geridos utilizados pelo Apache Kafka no HDInsight.

O Kafka no HDInsight utiliza o disco local das máquinas virtuais no cluster do HDInsight. Uma vez que o Kafka recebe um fluxo bastante pesado de dados de E/S, os [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) são utilizados para permitir um débito de transferência mais elevado e oferecer mais capacidade de armazenamento por nó. Se forem utilizadas unidades de disco rígido virtuais (VHD) tradicionais para o Kafka, cada nó tem um limite de 1 TB. Com os discos geridos, pode utilizar vários discos até alcançar 16 TB para cada nó do cluster.

O diagrama seguinte estabelece uma comparação entre o Kafka no HDInsight antes dos discos geridos e o Kafka no HDInsight com os discos geridos:

![Diagrama que mostra o Kafka no HDInsight com um único VHD por VM vs. vários discos geridos por VM](./media/apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Configurar discos geridos: portal do Azure

1. Siga os passos em [Create an HDInsight cluster](../hdinsight-hadoop-create-linux-clusters-portal.md) (Criar um cluster no HDInsight) para compreender os passos comuns de criação de um cluster com o portal. Não conclua o processo de criação do portal.

2. Na secção __Tamanho do cluster__, utilize o campo __Discos por nó de trabalho__ para configurar o número de discos.

    > [!NOTE]
    > O tipo de disco gerido pode ser __Standard__ (HDD) ou __Premium__ (SSD). Os discos Premium são utilizados com as VMs das séries DS e GS. Todos os outros tipos de VM utilizam discos Standard.

    ![Imagem da secção do tamanho do cluster com os discos por nó de trabalho realçados](./media/apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Configurar discos geridos: modelo do Resource Manager

Para controlar o número de discos utilizados por nós de trabalho num cluster do Kafka, utilize a seguinte secção do modelo:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Em [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json), pode encontrar um modelo completo que demonstra como configurar discos geridos.

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre como trabalhar com o Kafka no HDInsight, consulte os documentos seguintes:

* [Utilizar MirrorMaker para criar uma réplica de Kafka no HDInsight](apache-kafka-mirroring.md)
* [Utilizar o Apache Storm com Kafka no HDInsight](../hdinsight-apache-storm-with-kafka.md)
* [Utilizar o Apache Spark com Kafka no HDInsight](../hdinsight-apache-spark-with-kafka.md)
* [Ligar ao Kafka através de uma Rede Virtual do Azure](apache-kafka-connect-vpn-gateway.md)

* [Blogue do HDInsight sobre discos geridos com Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)