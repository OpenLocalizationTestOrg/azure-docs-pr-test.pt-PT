---
title: "agenda de aplicação de patches aaaConfigure SO para clusters do HDInsight baseado em Linux - Azure | Microsoft Docs"
description: "Saiba como clusters de agenda de aplicação de patches tooconfigure SO para o HDInsight baseado em Linux."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>Para o HDInsight a aplicação de patches de SO 
Como um serviço gerido do Hadoop, HDInsight encarrega-se de aplicação de patches Olá SO de Olá VMs subjacentes utilizadas pelo clusters do HDInsight. A partir de 1 de Agosto de 2016, vamos mudaram política aplicação de patches do SO de convidado de Olá para os clusters do HDInsight baseado em Linux (versão 3.4 ou superior). objetivo Olá nova política de Olá é toosignificantly reduzir o número de Olá de reinícios toopatching devida. nova política de Olá continuará toopatch as máquinas virtuais (VMs) no Linux clusters cada segunda-feira ou quinta começando UTC 12: 00, de forma escalonada em nós em qualquer cluster especificado. No entanto, qualquer VM especificada só será reiniciado no máximo uma vez a cada 30 dias que devem estar tooguest SO a aplicação de patches. Além disso, o primeiro reinício de Olá para um cluster recém-criado não acontecerá mais cedo do que 30 dias a partir da data de criação do cluster Olá. Correções de erros serão aplicadas depois de VMs de Olá são reiniciadas.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Como tooconfigure Olá agenda de aplicação de patches de SO para clusters do HDInsight baseado em Linux
Olá máquinas de virtuais num HDInsight cluster necessário toobe ocasionalmente reiniciado para que podem ser instaladas patches de segurança importantes. A partir de 1 de Agosto de 2016, os clusters do HDInsight baseado em Linux novo (versão 3.4 ou superior,) são reiniciados utilizando Olá seguinte agenda:

1. Uma máquina virtual no cluster de Olá pode apenas reiniciado para patches no máximo, uma vez num período de 30 dias.
2. reinício de Olá ocorre começando em 12: 00 UTC.
3. processo de reinício de Olá é escalonado em máquinas virtuais no cluster de Olá, pelo que o cluster de Olá ainda está disponível durante o processo de reinício de Olá o limite de tempo.
4. primeiro reinício de Olá para um cluster recém-criado não acontecerá mais cedo do que 30 dias após a data de criação do cluster Olá.

Através da ação de script de Olá descrita neste artigo, pode modificar agenda de aplicação de patches Olá SO da seguinte forma:
1. Ativar ou desativar reinícios automáticos
2. Frequência Olá conjunto é reiniciado (dias entre reinícios)
3. Definir Olá dia da semana de Olá quando ocorre uma reinicialização

> [!NOTE]
> Esta ação de script apenas irá trabalhar com clusters do HDInsight baseado em Linux criados após 1 de Agosto de 2016. Correções de erros serão aplicadas apenas quando são reiniciadas, VMs. 
>

## <a name="how-toouse-hello-script"></a>Como toouse Olá script 

Quando utilizar este script requer Olá seguintes informações:
1. Olá localização do script: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight utiliza este toofind URI e execute o script de Olá em todas as máquinas de virtuais Olá num cluster de Olá.
  
2. Olá tipos de nó de cluster que script Olá é aplicada: headnode, workernode, zookeeper. Este script tem de ser aplicados tooall tipos de nó no cluster de Olá. Se não for o tipo de nó tooa aplicados, em seguida, Olá virtual máquinas para esse tipo de nó irão continuar a agenda de aplicação de patches toouse Olá anterior.


3.  Parâmetro: Este script aceita três parâmetros numérico:

    | Parâmetro | Definição |
    | --- | --- |
    | Ativar/desativar reinícios automáticos |0 ou 1. Um valor de 0 desativa a reinícios automáticos enquanto 1 permite reinícios automáticos. |
    | Frequência |too90 7 (inclusive). Olá número toowait de dias antes de ser reiniciado Olá máquinas de virtuais para patches que necessitem de um reinício. |
    | Dia da semana |1 too7 (inclusive). Um valor de 1 indica o reinício de Olá deve ocorrer numa segunda-feira e 7 indica um exemplo de Sunday.For, utilizando os parâmetros de 1 60 2 resulta em automático é reiniciado a cada 60 dias (no máximo) na Terça-feira. |
    | Persistência |Ao aplicar um cluster existente do script ação tooan, é possível marcar o script Olá como persistente. Scripts persistentes são aplicadas quando workernodes novas são adicionadas toohello cluster através do dimensionamento operações. |

> [!NOTE]
> Tem de marcar este script como persistente ao aplicar tooan cluster existente. Caso contrário, quaisquer novos nós criados através do dimensionamento do operations utilizará a predefinição de Olá agenda de aplicação de patches.
Se aplicar o script de Olá como parte do processo de criação do cluster Olá, este é continuada automaticamente.
>

## <a name="next-steps"></a>Passos seguintes

Para obter passos específicos sobre como utilizar a ação de script de Olá, consulte Olá seguintes secções Olá [clusters do HDInsight baseado em Personalizar Linuz através da ação de script](hdinsight-hadoop-customize-cluster-linux.md):

* [Utilizar uma ação de script durante a criação do cluster](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Aplicar um tooa de ação de script a executar o cluster](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
