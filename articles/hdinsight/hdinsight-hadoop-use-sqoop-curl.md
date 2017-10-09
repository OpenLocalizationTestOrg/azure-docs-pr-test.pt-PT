---
title: aaaUse Hadoop Sqoop com Curl no HDInsight - Azure | Microsoft Docs
description: Saiba como tooremotely submeter Sqoop tarefas tooHDInsight utilizando Curl.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Executar tarefas de Sqoop com o Hadoop no HDInsight com o Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Saiba como cluster de Sqoop toorun toouse Curl tarefas um Hadoop no HDInsight.

Curl é toodemonstrate utilizado como pode interagir com o HDInsight utilizando toorun de pedidos HTTP não processado, monitorizar e obter Olá resultados de tarefas Sqoop. Isto funciona utilizando Olá API do REST de WebHCat (anteriormente conhecido como Templeton) fornecida pelo cluster do HDInsight.

> [!NOTE]
> Se já estiver familiarizado com a utilização de servidores de Hadoop baseado em Linux, mas são tooHDInsight novo, consulte [informações sobre como utilizar o HDInsight no Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toocomplete Olá passos descritos neste artigo, irá necessitar de seguinte Olá:

* Um Hadoop no HDInsight cluster (Linux ou baseadas no Windows)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Submeter tarefas de Sqoop utilizando Curl
> [!NOTE]
> Quando utilizar Curl ou quaisquer outras comunicações REST com WebHCat, tem de autenticar pedidos Olá ao fornecer o nome de utilizador Olá e a palavra-passe de administrador de cluster do HDInsight Olá. Também tem de utilizar o nome do cluster Olá como parte da Olá Uniform Resource Identifier (URI) utilizado o servidor de toohello toosend Olá pedidos.
> 
> Para comandos Olá nesta secção, substitua **USERNAME** com o cluster de toohello Olá utilizador tooauthenticate e substitua **palavra-passe** com Olá palavra-passe da conta de utilizador Olá. Substitua **CLUSTERNAME** com o nome de Olá do cluster.
> 
> Olá REST API está protegida por [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication). Deve sempre efetuar pedidos utilizando HTTP Secure (HTTPS) toohelp Certifique-se de que as suas credenciais são enviadas de uma forma segura toohello servidor.
> 
> 

1. A partir de uma linha de comandos, utilize Olá tooverify de comando que se pode ligar tooyour HDInsight cluster a seguir:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Deverá receber um resposta semelhante toohello seguinte procedimento:
   
        {"status":"ok","version":"v1"}
   
    os parâmetros de Olá utilizados neste comando são os seguintes:
   
   * **-u** -nome de utilizador Olá e a palavra-passe utilizada pedido de Olá tooauthenticate.
   * **-G** -indica que se trata de um pedido GET.
     
     Olá, a partir do URL de Olá, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será hello igual para todos os pedidos. caminho de Olá, **/status**, indica esse pedido Olá tooreturn um Estado de WebHCat (também conhecido como Templeton) para o servidor de Olá. 
2. Utilize Olá toosubmit uma tarefa de sqoop os seguintes:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    os parâmetros de Olá utilizados neste comando são os seguintes:

    * **-d** - desde `-G` não for utilizado, o pedido de Olá predefinições do método POST toohello. `-d`Especifica os valores de dados de Olá que são enviados com o pedido de Olá.

        * **User.name** -utilizador Olá que está a executar o comando de Olá.

        * **comando** -Olá Sqoop tooexecute de comando.

        * **statusdir** -diretório Olá Olá estado para esta tarefa será escrito.

    Este comando deverá devolver um ID de tarefa que pode ser utilizado toocheck Olá estado da tarefa de Olá.

        {"id":"job_1415651640909_0026"}

1. Estado de Olá toocheck da tarefa de Olá, Olá utilize os seguintes comandos. Substitua **JOBID** com o valor de Olá devolvida no passo anterior Olá. Por exemplo, se hello devolver o valor era `{"id":"job_1415651640909_0026"}`, em seguida, **JOBID** seria `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Se a tarefa de Olá estiver concluída, o estado de Olá será **com êxito**.
   
   > [!NOTE]
   > Este pedido Curl devolve um documento de JavaScript Object Notation (JSON) com informações sobre a tarefa de Olá; é utilizado jq tooretrieve Olá apenas o valor de estado.
   > 
   > 
2. Depois do Estado de Olá da tarefa de Olá mudou demasiado**com êxito**, pode obter resultados de Olá da tarefa de Olá do Blob storage do Azure. Olá `statusdir` parâmetro transmitido com consulta Olá contém localização Olá Olá ficheiro de saída; neste caso, **wasb: / / / exemplo/curl**. Este endereço armazena saída Olá da tarefa de Olá no Olá **exemplo/curl** diretório no contentor de armazenamento Olá predefinido utilizado pelo cluster do HDInsight.
   
    Pode listar e transferir estes ficheiros utilizando Olá [CLI do Azure](../cli-install-nodejs.md). Por exemplo, toolist ficheiros em **exemplo/curl**, utilize Olá os seguintes comandos:
   
        azure storage blob list <container-name> example/curl
   
    toodownload um ficheiro, utilize o seguinte Olá:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Tem de especificar ou nome de conta de armazenamento Olá que contém o blob de Olá utilizando Olá `-a` e `-k` parâmetros ou conjunto Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave** variáveis de ambiente. Consulte < uma href = "data.md de carregamento de hdinsight" target = blank"para obter mais informações.
   > 
   > 

## <a name="limitations"></a>Limitações
* Exportação em massa - baseado em Linux com o HDInsight, Olá Sqoop conetor utilizado tooexport dados tooMicrosoft do SQL Server ou SQL Database do Azure não suporta atualmente inserções em massa.
* Criação de batches - com o HDInsight baseado em Linux, ao utilizar Olá `-batch` comutador quando efetuar inserções, Sqoop irá efetuar várias inserções em vez de criação de batches de operações de inserção de Olá.

## <a name="summary"></a>Resumo
Como é demonstrado neste documento, pode utilizar um toorun de pedido HTTP não processado, monitorizar e ver Olá resultados de tarefas Sqoop no cluster do HDInsight.

Para obter mais informações sobre a interface REST de Olá utilizada neste artigo, consulte Olá <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guia da API de REST Sqoop</a>.

## <a name="next-steps"></a>Passos seguintes
Para obter informações gerais sobre o Hive com o HDInsight:

* [Utilizar o Sqoop com o Hadoop no HDInsight](hdinsight-use-sqoop.md)

Para obter informações sobre outras formas pode trabalhar com o Hadoop no HDInsight:

* [Utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md)
* [Utilizar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md)
* [Utilizar o MapReduce com o Hadoop no HDInsight](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


