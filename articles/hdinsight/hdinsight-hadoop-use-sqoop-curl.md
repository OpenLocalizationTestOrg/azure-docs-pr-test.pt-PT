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
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="26f0c-103">Executar tarefas de Sqoop com o Hadoop no HDInsight com o Curl</span><span class="sxs-lookup"><span data-stu-id="26f0c-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="26f0c-104">Saiba como cluster de Sqoop toorun toouse Curl tarefas um Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26f0c-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="26f0c-105">Curl é toodemonstrate utilizado como pode interagir com o HDInsight utilizando toorun de pedidos HTTP não processado, monitorizar e obter Olá resultados de tarefas Sqoop.</span><span class="sxs-lookup"><span data-stu-id="26f0c-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="26f0c-106">Isto funciona utilizando Olá API do REST de WebHCat (anteriormente conhecido como Templeton) fornecida pelo cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26f0c-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="26f0c-107">Se já estiver familiarizado com a utilização de servidores de Hadoop baseado em Linux, mas são tooHDInsight novo, consulte [informações sobre como utilizar o HDInsight no Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="26f0c-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="26f0c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26f0c-108">Prerequisites</span></span>
<span data-ttu-id="26f0c-109">toocomplete Olá passos descritos neste artigo, irá necessitar de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="26f0c-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="26f0c-110">Um Hadoop no HDInsight cluster (Linux ou baseadas no Windows)</span><span class="sxs-lookup"><span data-stu-id="26f0c-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="26f0c-111">Curl</span><span class="sxs-lookup"><span data-stu-id="26f0c-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="26f0c-112">jq</span><span class="sxs-lookup"><span data-stu-id="26f0c-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="26f0c-113">Submeter tarefas de Sqoop utilizando Curl</span><span class="sxs-lookup"><span data-stu-id="26f0c-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="26f0c-114">Quando utilizar Curl ou quaisquer outras comunicações REST com WebHCat, tem de autenticar pedidos Olá ao fornecer o nome de utilizador Olá e a palavra-passe de administrador de cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="26f0c-115">Também tem de utilizar o nome do cluster Olá como parte da Olá Uniform Resource Identifier (URI) utilizado o servidor de toohello toosend Olá pedidos.</span><span class="sxs-lookup"><span data-stu-id="26f0c-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="26f0c-116">Para comandos Olá nesta secção, substitua **USERNAME** com o cluster de toohello Olá utilizador tooauthenticate e substitua **palavra-passe** com Olá palavra-passe da conta de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="26f0c-117">Substitua **CLUSTERNAME** com o nome de Olá do cluster.</span><span class="sxs-lookup"><span data-stu-id="26f0c-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="26f0c-118">Olá REST API está protegida por [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="26f0c-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="26f0c-119">Deve sempre efetuar pedidos utilizando HTTP Secure (HTTPS) toohelp Certifique-se de que as suas credenciais são enviadas de uma forma segura toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="26f0c-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="26f0c-120">A partir de uma linha de comandos, utilize Olá tooverify de comando que se pode ligar tooyour HDInsight cluster a seguir:</span><span class="sxs-lookup"><span data-stu-id="26f0c-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="26f0c-121">Deverá receber um resposta semelhante toohello seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="26f0c-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="26f0c-122">os parâmetros de Olá utilizados neste comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="26f0c-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="26f0c-123">**-u** -nome de utilizador Olá e a palavra-passe utilizada pedido de Olá tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="26f0c-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="26f0c-124">**-G** -indica que se trata de um pedido GET.</span><span class="sxs-lookup"><span data-stu-id="26f0c-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="26f0c-125">Olá, a partir do URL de Olá, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será hello igual para todos os pedidos.</span><span class="sxs-lookup"><span data-stu-id="26f0c-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="26f0c-126">caminho de Olá, **/status**, indica esse pedido Olá tooreturn um Estado de WebHCat (também conhecido como Templeton) para o servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="26f0c-127">Utilize Olá toosubmit uma tarefa de sqoop os seguintes:</span><span class="sxs-lookup"><span data-stu-id="26f0c-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="26f0c-128">os parâmetros de Olá utilizados neste comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="26f0c-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="26f0c-129">**-d** - desde `-G` não for utilizado, o pedido de Olá predefinições do método POST toohello.</span><span class="sxs-lookup"><span data-stu-id="26f0c-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="26f0c-130">`-d`Especifica os valores de dados de Olá que são enviados com o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="26f0c-131">**User.name** -utilizador Olá que está a executar o comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="26f0c-132">**comando** -Olá Sqoop tooexecute de comando.</span><span class="sxs-lookup"><span data-stu-id="26f0c-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="26f0c-133">**statusdir** -diretório Olá Olá estado para esta tarefa será escrito.</span><span class="sxs-lookup"><span data-stu-id="26f0c-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="26f0c-134">Este comando deverá devolver um ID de tarefa que pode ser utilizado toocheck Olá estado da tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="26f0c-135">Estado de Olá toocheck da tarefa de Olá, Olá utilize os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="26f0c-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="26f0c-136">Substitua **JOBID** com o valor de Olá devolvida no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="26f0c-137">Por exemplo, se hello devolver o valor era `{"id":"job_1415651640909_0026"}`, em seguida, **JOBID** seria `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="26f0c-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="26f0c-138">Se a tarefa de Olá estiver concluída, o estado de Olá será **com êxito**.</span><span class="sxs-lookup"><span data-stu-id="26f0c-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26f0c-139">Este pedido Curl devolve um documento de JavaScript Object Notation (JSON) com informações sobre a tarefa de Olá; é utilizado jq tooretrieve Olá apenas o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="26f0c-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="26f0c-140">Depois do Estado de Olá da tarefa de Olá mudou demasiado**com êxito**, pode obter resultados de Olá da tarefa de Olá do Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="26f0c-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="26f0c-141">Olá `statusdir` parâmetro transmitido com consulta Olá contém localização Olá Olá ficheiro de saída; neste caso, **wasb: / / / exemplo/curl**.</span><span class="sxs-lookup"><span data-stu-id="26f0c-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="26f0c-142">Este endereço armazena saída Olá da tarefa de Olá no Olá **exemplo/curl** diretório no contentor de armazenamento Olá predefinido utilizado pelo cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26f0c-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="26f0c-143">Pode listar e transferir estes ficheiros utilizando Olá [CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="26f0c-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="26f0c-144">Por exemplo, toolist ficheiros em **exemplo/curl**, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="26f0c-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="26f0c-145">toodownload um ficheiro, utilize o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="26f0c-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="26f0c-146">Tem de especificar ou nome de conta de armazenamento Olá que contém o blob de Olá utilizando Olá `-a` e `-k` parâmetros ou conjunto Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave** variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="26f0c-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="26f0c-147">Consulte < uma href = "data.md de carregamento de hdinsight" target = blank"para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="26f0c-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="26f0c-148">Limitações</span><span class="sxs-lookup"><span data-stu-id="26f0c-148">Limitations</span></span>
* <span data-ttu-id="26f0c-149">Exportação em massa - baseado em Linux com o HDInsight, Olá Sqoop conetor utilizado tooexport dados tooMicrosoft do SQL Server ou SQL Database do Azure não suporta atualmente inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="26f0c-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="26f0c-150">Criação de batches - com o HDInsight baseado em Linux, ao utilizar Olá `-batch` comutador quando efetuar inserções, Sqoop irá efetuar várias inserções em vez de criação de batches de operações de inserção de Olá.</span><span class="sxs-lookup"><span data-stu-id="26f0c-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="26f0c-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="26f0c-151">Summary</span></span>
<span data-ttu-id="26f0c-152">Como é demonstrado neste documento, pode utilizar um toorun de pedido HTTP não processado, monitorizar e ver Olá resultados de tarefas Sqoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26f0c-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="26f0c-153">Para obter mais informações sobre a interface REST de Olá utilizada neste artigo, consulte Olá <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guia da API de REST Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="26f0c-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26f0c-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="26f0c-154">Next steps</span></span>
<span data-ttu-id="26f0c-155">Para obter informações gerais sobre o Hive com o HDInsight:</span><span class="sxs-lookup"><span data-stu-id="26f0c-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="26f0c-156">Utilizar o Sqoop com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f0c-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="26f0c-157">Para obter informações sobre outras formas pode trabalhar com o Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="26f0c-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="26f0c-158">Utilizar o Hive com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f0c-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="26f0c-159">Utilizar o Pig com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f0c-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="26f0c-160">Utilizar o MapReduce com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f0c-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


