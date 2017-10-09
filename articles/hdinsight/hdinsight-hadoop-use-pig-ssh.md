---
title: aaaUse Hadoop o Pig com o SSH num cluster do HDInsight - Azure | Microsoft Docs
description: "Saiba como ligar o cluster de Hadoop baseado em Linux tooa com SSH e, em seguida, utilize Olá Pig comando toorun Pig Latin instruções interativamente, ou como um lote da tarefa."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Executar tarefas do Pig num cluster baseado em Linux com Olá comando Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Saiba como o toointeractively executar tarefas do Pig a partir de um cluster do HDInsight ligação SSH tooyour. Olá linguagem de programação do Pig Latin permite transformações de toodescribe que são aplicados toohello entrada dados tooproduce Olá pretendido saída.

> [!IMPORTANT]
> Olá passos neste documento exigem um cluster do HDInsight baseado em Linux. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a id="ssh"></a>Ligar com SSH

Utilize o SSH tooconnect tooyour HDInsight cluster. Olá exemplo seguinte estabelece ligação com o nome de cluster de tooa **myhdinsight** como com o nome de conta de Olá **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Se forneceu uma chave de certificado para autenticação SSH** quando criou o cluster do HDInsight Olá, poderá ser necessário localização de Olá toospecify da chave privada Olá no seu sistema de cliente.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Se forneceu uma palavra-passe para autenticação SSH** quando criou o cluster do HDInsight Olá, forneça a palavra-passe Olá quando lhe for pedido.

Para obter mais informações sobre como utilizar o SSH com o HDInsight, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Utilize o comando de Pig Olá

1. Assim que estiver ligado, inicie o interface de linha de comandos de Pig Olá (CLI) utilizando Olá os seguintes comandos:

        pig

    Depois de um momento, deve ver um `grunt>` linha.

2. Introduza Olá a seguinte instrução:

        LOGS = LOAD '/example/data/sample.log';

    Este comando carrega Olá conteúdo de Olá sample.log ficheiro para os registos. Pode ver o conteúdo de Olá do ficheiro de Olá utilizando Olá a seguinte instrução:

        DUMP LOGS;

3. Em seguida, transformar dados de Olá aplicando um nível de registo de Olá apenas tooextract de expressão regular de cada registo utilizando Olá a seguinte instrução:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Pode utilizar **informação do estado** dados de Olá tooview depois da transformação Olá. Neste caso, utilize `DUMP LEVELS;`.

4. Continue a aplicar as transformações utilizando as instruções de Olá Olá a tabela seguinte:

    | Declaração de PIg Latin | Instrução que Olá |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Remove linhas que contêm um valor nulo para o nível de registo Olá e armazena os resultados de Olá para `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Olá de grupos de linhas por nível de registo e armazena os resultados de Olá para `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Cria um conjunto de dados que contém cada registo exclusivo ocorre valor nível e quantas vezes-lo. conjunto de dados de Olá é armazenado no `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Ordena os níveis de registo de Olá por contagem (descendente) e armazena para `RESULT`. |

    > [!TIP]
    > Utilize `DUMP` resultado de Olá tooview da transformação Olá depois de cada passo.

5. Também pode guardar resultados de Olá de uma transformação utilizando Olá `STORE` instrução. Por exemplo, Olá seguinte declaração guarda Olá `RESULT` toohello `/example/data/pigout` diretório no armazenamento de predefinido Olá para o cluster:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > dados de Olá são armazenados no diretório especificado de Olá em ficheiros com o nome `part-nnnnn`. Se já existe um diretório de Olá, receberá um erro.

6. Olá tooexit grunt linha, introduza Olá a seguinte instrução:

        QUIT;

### <a name="pig-latin-batch-files"></a>Ficheiros de batch de PIg Latin

Também pode utilizar Olá Pig comando toorun Pig Latin contidos num ficheiro.

1. Depois de sair linha de grunt Olá, utilize seguinte de Olá comando toopipe STDIN num ficheiro denominado `pigbatch.pig`. Este ficheiro é criado no diretório raiz do Olá para Olá conta de utilizador SSH.

        cat > ~/pigbatch.pig

2. Escreva ou cole Olá seguintes linhas e, em seguida, utilize Ctrl + D quando terminar.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Seguinte de Olá utilize comando toorun Olá `pigbatch.pig` ficheiro utilizando o comando de Pig Olá.

        pig ~/pigbatch.pig

    Depois de concluída a tarefa de lote Olá, consulte Olá seguinte saída:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Passos seguintes

Para obter informações gerais sobre o Pig no HDInsight, consulte Olá seguintes documentos:

* [Utilizar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md)

Para obter mais informações sobre outra formas toowork com o Hadoop no HDInsight, consulte Olá seguintes documentos:

* [Utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md)
* [Utilizar o MapReduce com o Hadoop no HDInsight](hdinsight-use-mapreduce.md)
