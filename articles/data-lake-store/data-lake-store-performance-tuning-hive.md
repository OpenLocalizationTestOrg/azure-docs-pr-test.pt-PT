---
title: "aaaAzure Data Lake arquivo Hive desempenho otimização diretrizes | Microsoft Docs"
description: "Desempenho de ramo de registo do Azure Data Lake Store diretrizes de otimização"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Orientações para do Hive no HDInsight e o Azure Data Lake Store de otimização do desempenho

foram definidas predefinições Olá tooprovide um bom desempenho em muitos casos de utilização diferentes.  Para consultas de e/s intensivas, o ramo de registo pode estar atento tooget um melhor desempenho com ADLS.  

## <a name="prerequisites"></a>Pré-requisitos

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do Azure Data Lake Store**. Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Cluster do HDInsight Azure** com acesso tooa conta do Data Lake Store. Consulte [criar um cluster do HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Certifique-se de que ativar o ambiente de trabalho remoto para o cluster de Olá.
* **Em execução do Hive no HDInsight**.  toolearn sobre como executar tarefas do Hive no HDInsight, consulte [utilizar o Hive no HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Diretrizes no ADLS de otimização do desempenho**.  Para os conceitos gerais de desempenho, consulte [guia de otimização de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>Parâmetros

Seguem-se Olá tootune de definições mais importante para um melhor desempenho ADLS:

* **Hive.tez.Container.size** – quantidade de Olá de memória utilizada por cada tarefas

* **tamanho tez.grouping.min** – mínimo tamanho de cada mapeador

* **tamanho tez.grouping.Max** – máximo tamanho de cada mapeador

* **Hive.exec.reducer.bytes.Per.reducer** – tamanho de cada reducer

**Hive.tez.Container.size** -tamanho do contentor de Olá determina a quantidade de memória está disponível para cada tarefa.  Esta é a entrada principal de Olá para controlar simultaneidade Olá no ramo de registo.  

**tamanho tez.grouping.min** – este parâmetro permite-lhe tooset tamanho mínimo de Olá do mapeador de cada.  Se o número de Olá de mappers Tez escolhe é inferior ao valor de Olá deste parâmetro, Tez irá utilizar valor Olá definido aqui.  

**tamanho tez.grouping.Max** – parâmetro Olá permite-lhe tooset Olá máximo de cada mapeador.  Se o número de Olá de mappers Tez escolhe é superior ao valor Olá deste parâmetro, Tez irá utilizar valor Olá definido aqui.  

**Hive.exec.reducer.bytes.Per.reducer** – este parâmetro define o tamanho de cada reducer Olá.  Por predefinição, cada reducer é de 256MB.  

## <a name="guidance"></a>Orientação

**Definir hive.exec.reducer.bytes.per.reducer** – valor predefinido de Olá funciona bem quando os dados de Olá são descomprimidos.  Para os dados são comprimidos, deve de reduzir o tamanho de Olá dos reducer Olá.  

**Definir hive.tez.container.size** – em cada nó, memória é especificada por yarn.nodemanager.resource.memory mb e deve ser definida corretamente no HDI cluster por predefinição.  Para obter informações adicionais sobre a definição de memória adequada Olá no YARN, consulte este [publique](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

Cargas de trabalho de e/s intensivas podem beneficiar do paralelismo mais ao diminuir o tamanho de contentor do Olá Tez. Isto dá-utilizador Olá mais contentores que aumenta de concorrência.  No entanto, algumas consultas do Hive requerem uma quantidade significativa de memória (por exemplo, MapJoin).  Se a tarefa de Olá não tem memória suficiente, receberá um fora de exceção de memória durante o tempo de execução.  Se receber fora de exceções de memória, em seguida, deve aumentar memória Olá.   

Olá simultâneas diversas tarefas em execução ou o paralelismo tem um vínculo pelo total de memória YARN Olá.  número de Olá de contentores YARN determinarão como muitas tarefas simultâneas podem ser executado.  toofind Olá YARN memória por nó podem aceder tooAmbari.  Navegue tooYARN e ver o separador de folhas de Olá.  Olá memória YARN é apresentado nesta janela.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
desempenho de chave tooimproving Olá utilizando ADLS é simultaneidade de Olá tooincrease quanto possível.  Tez calcula automaticamente o número de Olá de tarefas que deverá ser criado, pelo que não necessita de tooset-lo.   

## <a name="example-calculation"></a>Cálculo de exemplo

Imaginemos que tem um cluster do 8 nó D14.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Limitações
**ADLS limitação** 

UIf atingiu limites de Olá de largura de banda fornecida pelo ADLS, seria começar toosee falhas de tarefas. Isto pode ser identificado ao observar erros limitação nos registos de tarefas.  Pode diminuir o paralelismo Olá através do aumento do tamanho do contentor de Tez.  Se precisar de concorrência mais a tarefa, contacte-nos.   

toocheck se a introdução limitada, terá de depuração de Olá tooenable início de sessão do lado do cliente de Olá. Eis como, pode fazê-lo:

1. Colocar Olá seguinte propriedade nas propriedades de log4j Olá na configuração do ramo de registo. Isto pode ser feito a partir da vista Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG reiniciar Olá todos os nós/serviço para o efeito de tootake Olá config.

2. Se a introdução limitada, verá o código de erro HTTP 429 Olá no ficheiro de registo do ramo de registo Olá. ficheiro de registo do ramo de registo Olá consta /tmp/&lt;utilizador&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Mais informações sobre a otimização de ramo de registo

Seguem-se alguns blogues que o irão ajudar a otimizar as consultas do Hive:
* [Otimizar as consultas do Hive do Hadoop no HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Resolução de problemas de desempenho das consultas do Hive](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Ignite peça no otimizar do Hive no HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
