---
title: "desempenho de Data Lake Store Storm aaaAzure otimização diretrizes | Microsoft Docs"
description: "Desempenho do Azure Data Lake Store Storm diretrizes de otimização"
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
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Orientações para Storm no HDInsight e o Azure Data Lake Store de otimização do desempenho

Compreenda os fatores de Olá que devem ser considerados ao otimizar o desempenho Olá de uma topologia do Storm do Azure. Por exemplo, é importante toounderstand características de Olá do trabalho Olá efetuado Olá spouts e bolts Olá (se trabalho Olá é exigente em termos de memória ou de e/s). Este artigo abrange uma série de diretrizes, incluindo a resolução de problemas comuns de otimização do desempenho.

## <a name="prerequisites"></a>Pré-requisitos

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do Azure Data Lake Store**. Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Um cluster do Azure HDInsight** com acesso tooa conta do Data Lake Store. Consulte [criar um cluster do HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Certifique-se de que ativar o ambiente de trabalho remoto para o cluster de Olá.
* **Executar um cluster do Storm no Data Lake Store**. Para obter mais informações, consulte [Storm no HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Desempenho de otimização diretrizes no Data Lake Store**.  Para os conceitos gerais de desempenho, consulte [guia de otimização de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Otimizar Olá paralelismo da topologia de Olá

Poderá ser tooimprove capaz de desempenho por crescente Olá simultaneidade de Olá tooand de e/s do Data Lake Store. Uma topologia do Storm tem um conjunto de configurações que determinam o paralelismo Olá:
* Número de processos de trabalho (trabalhadores Olá estão uniformemente distribuídos Olá VMs).
* Número de instâncias de executor de spout.
* Número de instâncias de executor bolt.
* Número de tarefas de spout.
* Número de tarefas bolt.

Por exemplo, num cluster com 4 VMs e 4 processos de trabalho, 32 spout executores e 32 spout tarefas e 256 executores de bolt e tarefas de 512 bolt, considere o seguinte Olá:

Cada supervisor, que é um nó de trabalho, tem uma função de trabalho único processo da máquina virtual (JVM) de Java. Este processo JVM gere 4 spout threads e 64 threads de bolt. Dentro de cada thread, são executadas sequencialmente. Com Olá anterior a configuração, cada thread spout tem 1 tarefas e 2 tarefas tem de cada thread bolt.

Storm, seguem-se Olá vários componentes envolvidos e como estas afetam nível Olá de paralelismo que tiver:
* nó principal do Olá (Nimbus chamado no Storm) é utilizado toosubmit e gerir tarefas. Estes nós tem nenhum impacto no grau de Olá de paralelismo.
* nós de supervisor Olá. No HDInsight, isto corresponde o nó de trabalho de tooa VM do Azure.
* tarefas de trabalho de Olá são processos de Storm em execução no Olá VMs. Cada tarefa de trabalho corresponde à instância JVM tooa. Storm distribui número Olá de processos de trabalho que especificar nós de trabalho toohello uniformemente quanto possível.
* Spout e instâncias de executor de bolt. Cada instância de executor corresponde ao thread tooa em execução numa trabalhadores Olá (JVMs).
* Tarefas do Storm. Estas são tarefas lógicas de cada um destes threads de execução. Isso não altera o nível de Olá de paralelismo, que deve avaliar se precisar de várias tarefas por executor ou não.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Obter o melhor desempenho possível Olá do Data Lake Store

Ao trabalhar com o Data Lake Store, obter o melhor desempenho possível Olá se Olá a seguir:
* Unir sua pequena acrescenta em tamanhos maiores (Idealmente 4 MB).
* Como muitas pedidos em simultâneo, pode fazê-lo. Porque cada thread bolt está a fazer o bloqueios de leituras, quer toohave algures no intervalo de Olá de 8 12 threads por núcleo. Este procedimento mantém Olá NIC e Olá da CPU também são utilizada. Uma VM maior permite mais pedidos simultâneos.  

### <a name="example-topology"></a>Topologia de exemplo

Vamos assumir que tem um cluster de nó de 8 trabalho com uma VM do Azure D13v2. Este VM tem 8 núcleos, por isso, entre Olá 8 nós de trabalho, terá de 64 núcleos totais.

Vamos supor que o fazemos 8 bolt threads por núcleo. Fornecido 64 núcleos, isto significa que queremos 512 instâncias de executor de total bolt (ou seja, threads). Neste caso, vamos supor que iremos começar com um JVM por VM e, principalmente utilizar simultaneidade de thread Olá dentro de simultaneidade de tooachieve Olá JVM. Isto significa que precisamos 8 tarefas de trabalho (uma por VM do Azure) e 512 executores de bolt. Tendo em conta esta configuração, Storm tenta trabalhadores de Olá toodistribute uniformemente em nós de trabalho (também conhecido como nós de supervisor), cada nó de trabalho 1 a dar JVM. Agora no supervisors Olá, Storm tenta executores de Olá toodistribute uniformemente entre supervisors, concedendo cada supervisor (ou seja, JVM) 8 threads cada.

## <a name="tune-additional-parameters"></a>Otimizar parâmetros adicionais
Depois de ter topologia básica Olá, pode considerar se pretende que tootweak qualquer um dos parâmetros Olá:
* **Número de JVMs por nó de trabalho.** Se tiver uma estrutura de dados de grandes dimensões (por exemplo, uma tabela de pesquisa) anfitrião na memória, cada JVM requer uma cópia separada. Em alternativa, pode utilizar a estrutura de dados de Olá através de vários threads se tiver menos JVMs. Para e/s do bolt Olá, número de Olá de JVMs não faz a maior quantidade de uma diferença como número de Olá de threads adicionados entre essas JVMs. Por razões de simplicidade, é toohave uma boa ideia um JVM por trabalho. Dependendo de que o bolt está a fazer ou as aplicações de processamento necessitam, embora, poderá ser necessário toochange este número.
* **Número de executor de spout.** Porque hello anterior exemplo utiliza bolts para escrever tooData Lake Store, número de Olá de spouts não se desempenho de bolt toohello diretamente relevantes. No entanto, dependendo da quantidade de Olá de processamento ou e/s a acontecer no spout Olá, é uma boa ideia tootune Olá spouts para um melhor desempenho. Certifique-se de que tem suficiente spouts toobe tookeep capaz de Olá bolts ocupado. Olá taxas de saída de Olá spouts devem corresponder ao débito Olá Olá bolts. depende da configuração real Olá em spout Olá.
* **Número de tarefas.** Cada bolt é executado como um único thread. Tarefas adicionais por bolt não fornecem qualquer simultaneidade adicional. Olá apenas são vantagem ocorre se o processo de confirmar a cadeia de identificação de Olá demora uma grande proporção do tempo de execução bolt. É um toogroup boa ideia que muitos cadeias de identificação para uma maior acrescentar antes de enviar uma confirmação de bolt Olá. Por isso, na maioria dos casos, várias tarefas não fornecem existir nenhuma vantagem adicional.
* **Local ou shuffle agrupamento.** Quando esta definição estiver ativada, cadeias de identificação são enviadas toobolts dentro Olá mesmo processo de trabalho. Isto reduz a chamadas de rede e de comunicação entre processos. Esta opção é recomendada para a maioria das topologias.

Este cenário básico é um ponto de partida. Testar com o seus próprios Olá tootweak de dados anterior um desempenho ideal tooachieve parâmetros.

## <a name="tune-hello-spout"></a>Otimizar spout Olá

Pode modificar Olá definições tootune Olá spout a seguir.

- **Tempo limite de cadeia de identificação: topology.message.timeout.secs**. Esta definição determina a quantidade de Olá de tempo uma mensagem demora toocomplete e receber a confirmação, antes de ser considerada falhou.

- **Memória máxima por processo de trabalho: worker.childopts**. Esta definição permite-lhe especificar trabalhadores de Java toohello de parâmetros da linha de comandos adicionais. Olá normalmente utilizada aqui a definição é XmX, que determina a pilha do JVM de Olá, máximo de memória alocado tooa.

- **Spout máximo pendentes: topology.max.spout.pending**. Esta definição determina o número de Olá de cadeias de identificação no pode ser voo (ainda não confirmado em todos os nós numa topologia de Olá) por thread de spout em qualquer altura.

 Uma boa cálculo toodo é o tamanho de Olá de tooestimate de cada uma das suas cadeias de identificação. Em seguida, descobrir tem de thread de spout uma quantidade de memória. Olá total de memória alocada tooa thread, dividido por este valor, deverá dar-lhe limite superior de Olá para spout máx. de Olá pendentes parâmetro.

## <a name="tune-hello-bolt"></a>Otimizar bolt Olá
Quando estiver a escrever tooData Lake Store, definir uma política de sincronização de tamanho (memória intermédia do lado do cliente de Olá) too4 MB. Um libertar ou hsync(), em seguida, é executada apenas quando o tamanho de memória intermédia de Olá Olá, este valor. controlador de Data Lake Store Olá no trabalho Olá VM automaticamente efetua Esta colocação em memória intermédia, a menos que efetua uma hsync() explicitamente.

bolt de Data Lake Store Storm Olá predefinido tem um parâmetro de política do sincronização tamanho (fileBufferSize) que pode ser utilizado tootune este parâmetro.

Topologias de I/O intensivo, é uma boa ideia toohave cada thread bolt escrever ficheiro próprio tooits e tooset uma política de rotação de ficheiro (fileRotationSize). Quando o ficheiro de Olá atinge um determinado tamanho, fluxo Olá automaticamente removida da cache e é escrito um novo ficheiro. Olá recomendado tamanho de ficheiro de rotação é de 1 GB.

### <a name="handle-tuple-data"></a>Processar os dados de cadeia de identificação

No Storm, um spout deter na cadeia de identificação tooa até explicitamente é confirmada pelo bolt Olá. Se uma cadeia de identificação foram lidos pelo bolt Olá, mas não tiver sido confirmada ainda, spout Olá poderá não ter continuada no back-end do Data Lake Store. Depois de uma cadeia de identificação é confirmada, spout Olá pode ser garantida persistência pelo bolt Olá e, em seguida, pode eliminar dados de origem Olá de qualquer origem que está a ler.  

Para melhor desempenho no Data Lake Store, ter bolt Olá a memória intermédia de 4 MB de dados de cadeia de identificação. Em seguida, escreva toohello novamente para o Data Lake Store terminar como uma escrita de 4 MB. Após dos dados Olá arquivo toohello escrito com êxito (por chamada hflush()), bolt Olá pode reconhecer Olá dados back-toohello spout. Este é o exemplo de Olá bolt fornecidos does aqui. Também é aceitável toohold um grande número de cadeias de identificação antes de chamada de hflush() Olá é efetuada e Olá cadeias de identificação confirmadas. No entanto, isto aumenta o número de Olá de cadeias de identificação em trânsito que necessita de spout Olá toohold e, por conseguinte, aumenta Olá a quantidade de memória necessária por JVM.

> [!NOTE]
As aplicações podem ter uma identificação de tooacknowledge requisito com mais frequência (em tamanhos de dados inferiores a 4 MB) por outros motivos de desempenho não. No entanto, o que poderá afetar o Olá e/s débito toohello armazenamento de back-end. Cuidadosamente pesar este compromisso contra o desempenho de e/s do bolt Olá.

Se a taxa de receção de Olá de cadeias de identificação é não elevada, pelo que a memória intermédia de 4 MB Olá demora um toofill muito tempo, considere a mitigar este por:
* Reduzir o número de Olá de bolts, pelo que existem menos toofill de memórias intermédias.
* Ter uma política com base em contagem ou baseados no tempo, em que um hflush() é acionada a cada x esvaziamentos ou cada milissegundos y e cadeias de identificação de Olá acumuladas até ao momento são confirmadas anterior.

Tenha em atenção que o débito de Olá neste caso é inferior, mas com uma velocidade de lenta de eventos, o débito máximo não é objetivo maior Olá mesmo assim. Estes mitigações ajudam a reduzir o tempo total de Olá que leva tooflow uma cadeia de identificação através de toohello loja. Isto poderá importa se pretender que um pipeline em tempo real, mesmo com uma taxa de eventos de baixa. Também tenha em atenção que se a taxa de receção na cadeia de identificação é baixa, deverá ajustar parâmetro de topology.message.timeout_secs Olá, pelo que as cadeias de identificação de Olá não o tempo limite enquanto está a obter colocado na memória intermédia ou processados.

## <a name="monitor-your-topology-in-storm"></a>Monitorizar a topologia de Storm  
Enquanto a topologia está em execução, pode monitorizá-lo na interface de utilizador do Storm Olá. Seguem-se Olá parâmetros principal toolook em:

* **Latência de execução do processo total.** Este é o tempo médio de Olá uma cadeia de identificação demora toobe emitidos pelo spout Olá, processados pelo bolt Olá e confirmada.

* **Latência de processo total bolt.** Este é Olá de tempo médio despendido por uma cadeia de identificação de Olá no bolt Olá até receber uma confirmação.

* **Total bolt executar latência.** Esta é a média de Olá tempo despendida pelos Olá bolt no Olá executar o método.

* **Número de falhas.** Isto refere-se toohello número de cadeias de identificação que falharam toobe totalmente processada antes que foi excedido.

* **Capacidade.** Esta é uma medida é como ocupado do seu sistema. Se este número for 1, a sua bolts estão a funcionar como rápido podem. Se for inferior a 1, aumente o paralelismo Olá. Se for superior a 1, reduza o paralelismo Olá.

## <a name="troubleshoot-common-problems"></a>Resolver problemas comuns
Seguem-se alguns cenários comuns de resolução de problemas.
* **Cadeias de identificação muitos são exceder o tempo limite.** Procure em cada nó no Olá topologia toodetermine onde é estrangulamento Olá. razão mais comum de Olá para este está que Olá bolts não estão tookeep capaz de cópia de segurança com Olá spouts. Esta situação origina tootuples clogging Olá interno das memórias intermédias ao toobe a aguardar processada. Considere aumentar o valor de tempo limite de Olá ou diminua spout máx. de Olá pendentes.

* **Há uma latência de execução do processo total elevada, mas a latência de processo bolt baixa.** Neste caso, é possível que cadeias de identificação de Olá não estão a ser confirmadas fast suficiente. Verifique se existem um número suficiente de acknowledgers. Possibilidade de outra é que estes estão a aguardar na fila de Olá há demasiado tempo antes de Olá bolts início processamento-los. Diminua spout máx. de Olá pendentes.

* **Não há um bolt elevado executar latência.** Isto significa que método de execute () Olá do seu bolt está a demorar demasiado tempo. Otimizar o código de Olá, ou observar os tamanhos de escrita e descarregar o comportamento.

### <a name="data-lake-store-throttling"></a>Limitação do Data Lake Store
Se clicar em limites de Olá de largura de banda fornecida pelo Data Lake Store, poderá ver falhas de tarefas. Verifique os registos da tarefa para erros de limitação. Pode diminuir o paralelismo Olá através do aumento do tamanho do contentor.    

toocheck se a introdução limitada, ativar a depuração de Olá início de sessão do lado do cliente de Olá:

1. No **Ambari** > **Storm** > **configuração** > **avançadas log4j de trabalho de storm**, alterar  **&lt;nível de raiz = "informações"&gt;**  demasiado**&lt;nível de raiz = "a depuração"&gt;**. Reinicie Olá todos os nós/serviço para o efeito de tootake Olá configuração.
2. Topologia do Storm monitor Olá os registos de nós de trabalho (em /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;porta&gt;/worker.log) do Data Lake Store exceções de limitação.

## <a name="next-steps"></a>Passos seguintes
Otimização de desempenho adicional para Storm pode ser referenciado na [este blogue](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Para um toorun exemplo adicionais, consulte [este um no GitHub](https://github.com/hdinsight/storm-performance-automation).
