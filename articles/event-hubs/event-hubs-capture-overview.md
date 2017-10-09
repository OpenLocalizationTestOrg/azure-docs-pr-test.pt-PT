---
title: aaaOverview de captura de Hubs de eventos do Azure | Microsoft Docs
description: Captura de dados de telemetria com capturar os Hubs de eventos
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Captura de Hubs de eventos do Azure

Captura de Hubs de eventos do Azure permite-lhe tooautomatically entregar Olá transmissão em fluxo de dados dos Event Hubs tooan [Blob storage do Azure](https://azure.microsoft.com/services/storage/blobs/) ou [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) conta à sua escolha, com Olá adicionada flexibilidade de especificar um intervalo de tempo ou tamanho. Configurar a captura é rápido, existem toorun sem os custos administrativos e se ajusta automaticamente com os Event Hubs [unidades de débito](event-hubs-features.md#capacity). Captura de Hubs de eventos é tooload forma mais fácil Olá transmissão em fluxo de dados no Azure e permite-lhe toofocus no processamento de dados em vez de na captura de dados.

Captura de Hubs de eventos permite-lhe tooprocess em tempo real e pipelines com base em lote em Olá mesma transmissão em fluxo. Isto significa que podem criar soluções que aumentam com necessidades ao longo do tempo. Se estiver a criar sistemas baseados em batch hoje com par para processamento futuro de em tempo real ou se quiser tooadd uma solução de em tempo real existente do caminho típico eficiente tooan, capturar os Hubs de eventos faz com que trabalhar com dados mais fácil de transmissão em fluxo.

## <a name="how-event-hubs-capture-works"></a>Como funciona a captura de Hubs de eventos

Os Event Hubs são uma tempo de retenção durável memória intermédia para a entrada de telemetria, registo de distribuída tooa semelhantes. Olá tooscaling chave no Event Hubs é Olá [modelo de consumidor particionado](event-hubs-features.md#partitions). Cada partição é um segmento de dados independente e é consumida de forma independente. Ao longo do tempo este sua idade aumenta desativado, com base no período de retenção configurável de Olá. Como resultado, um hub de eventos fornecido nunca obtém "demasiado completo".

Captura de Hubs de eventos permite toospecify a sua própria conta de armazenamento de Blobs do Azure e um contentor ou uma conta do Azure Data Lake Store, que são utilizados toostore Olá capturado dados. Estas contas podem ser Olá mesma região, como o hub de eventos ou noutra região, adicionar toohello flexibilidade da funcionalidade de captura de Hubs de eventos de Olá.

Dados capturados são escritos em [Apache Avro] [ Apache Avro] formato: um formato compacto, rápido, binário, que fornece as estruturas de dados formatado com o esquema inline. Este formato é amplamente utilizado ecossistema do Hadoop Olá, o Stream Analytics e o Azure Data Factory. Obter mais informações sobre como trabalhar com Avro estão disponíveis neste artigo.

### <a name="capture-windowing"></a>Capturar em modo de janela

Captura de Hubs de eventos permite tooset se uma captura de toocontrol de janela. Esta janela é um tamanho mínimo e a configuração de tempo com "primeira wins, uma política de", o que significa que Olá primeiro causas de Acionador encontrada uma operação de captura. Se tiver um introdução de quinze minutos, 100 MB capturar janela e a enviar de 1 MB por segundo, acionadores de janela de tamanho de Olá antes de janela de tempo de Olá. Cada partição capturas de forma independente e escreve um blob de blocos foi concluída no tempo de Olá de captura, com o nome para o tempo de Olá no qual Olá foi encontrado o intervalo de captura. Convenção de nomenclatura de armazenamento de Olá é o seguinte:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Dimensionamento toothroughput unidades

Tráfego de Hubs de eventos é controlado pelo [unidades de débito](event-hubs-features.md#capacity). Uma única unidade de débito permite 1 MB por segundo ou 1000 eventos por segundo de entrada e de duas vezes que quantidade de saída. Hubs de eventos Standard pode ser configurados com 1-20 unidades de débito e pode comprar mais com uma quota aumentar [pedido de suporte][support request]. Utilização para além das unidades de débito adquiridas é limitada. Hubs de eventos captura copia dados diretamente a partir do armazenamento de Event Hubs interno Olá, ignorando as quotas de saída de unidade de débito e guardar a saída para outros leitores de processamento, por exemplo, o Stream Analytics ou Spark.

Depois de configurar, capturar os Hubs de eventos é executado automaticamente quando enviar o primeiro evento e continua a ser executado. toomake mais fácil para o processamento a jusante tooknow que processo Olá está a funcionar, os Event Hubs escreve ficheiros vazios quando não existem dados. Este processo fornece uma cadência previsível e marcador que pode atribuir os processadores do batch.

## <a name="setting-up-event-hubs-capture"></a>Como configurar a captura de Hubs de eventos

Pode configurar a captura no Olá event hub momento da criação utilizando Olá [portal do Azure](https://portal.azure.com), ou utilizando os modelos Azure Resource Manager. Para obter mais informações, consulte Olá seguintes artigos:

- [Ativar a captura de Hubs de eventos utilizando Olá portal do Azure](event-hubs-capture-enable-through-portal.md)
- [Criar um espaço de nomes de Hubs de eventos com um hub de eventos e ativar a captura utilizando um modelo Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Explorar os ficheiros de Olá capturada e trabalhar com Avro

Hubs de eventos captura cria ficheiros no formato Avro, conforme especificado na janela de tempo de Olá configurado. Pode ver estes ficheiros em qualquer ferramenta tais como [Explorador de armazenamento do Azure][Azure Storage Explorer]. Pode transferir Olá localmente ficheiros toowork nos mesmos.

os ficheiros de Olá produzidos pela captura de Hubs de eventos têm Olá esquema Avro os seguintes:

![][3]

Uma forma fácil de Avro do tooexplore de ficheiros é utilizando Olá [Avro ferramentas] [ Avro Tools] jar do Apache. Depois de transferir este jar, pode ver o esquema de Olá de um ficheiro específico do Avro executando Olá os seguintes comandos:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Este comando devolve

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

Também pode utilizar ferramentas de Avro tooconvert Olá ficheiro tooJSON formato e efetuar outro processamento.

tooperform mais avançadas processar, transfira e instale o Avro para a escolha da plataforma. No momento de Olá desta redação, existem as implementações disponíveis para C, C++, C\#, Java, NodeJS, Perl, PHP, Python e Ruby.

Apache Avro tem concluídos guias de introdução para [Java] [ Java] e [Python][Python]. Também pode ler Olá [introdução ao Event Hubs capturar](event-hubs-capture-python.md) artigo.

## <a name="how-event-hubs-capture-is-charged"></a>Como capturar os Hubs de eventos é cobrada

Captura de Hubs de eventos é limitado da mesma forma toothroughput unidades: como um custo por hora. encargos de Olá é diretamente proporcional toohello número de unidades de débito adquiridas para Olá espaço de nomes. Unidades de débito são aumentar e diminuir, medidores capturar os Hubs de eventos aumentam e diminuir tooprovide correspondência de desempenho. Medidores Olá ocorrerem em conjunto. Para detalhes de preços, consulte [preços de Hubs de eventos](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Passos seguintes

Captura de Hubs de eventos é Olá mais fácil forma tooget dados no Azure. Utilizar o Azure Data Lake, o Azure Data Factory e o Azure HDInsight, pode realizar processamento em lote e outros analytics com ferramentas familiares e plataformas à sua escolha, em qualquer escala precisa.

Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:

* [Começar a enviar e receber eventos](event-hubs-dotnet-framework-getstarted-send.md)
* Uma [Aplicação de exemplo que utiliza os Hubs de Eventos][sample application that uses Event Hubs] completa
* [Descrição geral dos Hubs de Eventos][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
