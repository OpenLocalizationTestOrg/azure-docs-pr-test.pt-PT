---
title: "aaaUse ação de Script tooinstall Solr no cluster de Hadoop - Azure | Microsoft Docs"
description: "Saiba como toocustomize HDInsight cluster com Solr através da ação de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="5b8e5-103">Instalar e utilizar Solr nos clusters do HDInsight baseados em Windows</span><span class="sxs-lookup"><span data-stu-id="5b8e5-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="5b8e5-104">Saiba como toocustomize HDInsight baseado em Windows cluster com Solr através da ação de Script e como toouse Solr toosearch dados.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b8e5-105">passos seguintes Olá em projetos de apenas este documento com clusters do HDInsight baseados em Windows.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5b8e5-106">HDInsight só está disponível no Windows para as versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="5b8e5-107">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5b8e5-108">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="5b8e5-109">Para obter informações sobre a utilização Solr com um cluster baseado em Linux, consulte [instalar e utilizar Solr nos clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="5b8e5-110">Pode instalar Solr em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight utilizando *ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="5b8e5-111">Um tooinstall de script de exemplo Solr num cluster do HDInsight está disponível a partir de um blob de armazenamento do Azure só de leitura em [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="5b8e5-112">script de exemplo de Olá funciona apenas com clusters do HDInsight versão 3.1.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="5b8e5-113">Para obter mais informações sobre as versões de cluster do HDInsight, consulte [as versões de cluster do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="5b8e5-114">script de exemplo de Olá utilizado neste tópico cria um cluster de Solr baseado no Windows com uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="5b8e5-115">Se pretender que o cluster de Solr Olá tooconfigure com diferentes coleções, shards, esquemas, as réplicas, etc., tem de modificar o script de Olá e binários Solr em conformidade.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="5b8e5-116">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="5b8e5-116">**Related articles**</span></span>

* [<span data-ttu-id="5b8e5-117">Instalar e utilizar Solr em clusters do HDinsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="5b8e5-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="5b8e5-118">[Criar clusters do Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre a criação de clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="5b8e5-119">[Personalizar clusters do HDInsight através da ação de Script][hdinsight-cluster-customize]: informações gerais sobre a personalização clusters do HDInsight através da ação de Script.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="5b8e5-120">[Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="5b8e5-121">O que é Solr?</span><span class="sxs-lookup"><span data-stu-id="5b8e5-121">What is Solr?</span></span>
<span data-ttu-id="5b8e5-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> é uma plataforma de pesquisa de empresa que lhe permite poderosa pesquisa em texto completo em dados.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="5b8e5-123">Enquanto Hadoop permite armazenar e gerir grandes quantidades de dados, Apache Solr fornece capacidades de pesquisa de Olá dados de Olá tooquickly obter.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="5b8e5-124">Instalar Solr através do portal</span><span class="sxs-lookup"><span data-stu-id="5b8e5-124">Install Solr using portal</span></span>
1. <span data-ttu-id="5b8e5-125">Iniciar criação de um cluster utilizando Olá **criação personalizada** opção, conforme descrito em [clusters do Hadoop criar no HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="5b8e5-126">No Olá **ações de Script** página do Assistente de Olá, clique em **adicionar ação de script** tooprovide detalhes sobre a ação de script de Olá, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="5b8e5-127">![Utilize a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize de ação de Script de utilizar um cluster")</span><span class="sxs-lookup"><span data-stu-id="5b8e5-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="5b8e5-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5b8e5-128">Property</span></span></th><th><span data-ttu-id="5b8e5-129">Valor</span><span class="sxs-lookup"><span data-stu-id="5b8e5-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="5b8e5-130">Nome</span><span class="sxs-lookup"><span data-stu-id="5b8e5-130">Name</span></span></td>
            <td><span data-ttu-id="5b8e5-131">Especifique um nome para a ação de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-131">Specify a name for hello script action.</span></span> <span data-ttu-id="5b8e5-132">Por exemplo, <b>instalar Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="5b8e5-133">URI de script</span><span class="sxs-lookup"><span data-stu-id="5b8e5-133">Script URI</span></span></td>
            <td><span data-ttu-id="5b8e5-134">Especifique Olá Uniform Resource Identifier (URI) toohello script que é invocada toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="5b8e5-135">Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="5b8e5-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="5b8e5-136">Tipo de Nó</span><span class="sxs-lookup"><span data-stu-id="5b8e5-136">Node Type</span></span></td>
            <td><span data-ttu-id="5b8e5-137">Especifique nós de Olá no qual o script de personalização de Olá é executado.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="5b8e5-138">Pode escolher <b>todos os nós</b>, <b>apenas nós principais</b>, ou <b>apenas nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="5b8e5-139">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="5b8e5-139">Parameters</span></span></td>
            <td><span data-ttu-id="5b8e5-140">Especifique parâmetros de Olá, se necessário pelo script de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="5b8e5-141">Olá script tooinstall Solr não requer quaisquer parâmetros, pelo que pode deixar isto em branco.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="5b8e5-142">Pode adicionar mais do que um tooinstall de ação de script vários componentes no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="5b8e5-143">Depois de ter adicionado scripts Olá, clique em Olá marca de verificação toostart Criar cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="5b8e5-144">Utilizar Solr</span><span class="sxs-lookup"><span data-stu-id="5b8e5-144">Use Solr</span></span>
<span data-ttu-id="5b8e5-145">Tem de começar com indexação Solr com alguns ficheiros de dados.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="5b8e5-146">Em seguida, pode utilizar consultas de pesquisa de toorun Solr nos dados de Olá indexada.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="5b8e5-147">Execute Olá os seguintes passos toouse Solr de um cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="5b8e5-148">**Utilizar tooremote do protocolo RDP (Remote Desktop Protocol) no cluster do HDInsight Olá com Solr instalado**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="5b8e5-149">Do portal do Azure Olá, ative o ambiente de trabalho remoto para o cluster de Olá que criou com o cluster de Olá instalado e, em seguida, remotamente Solr.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="5b8e5-150">Para obter instruções, consulte [ligar a clusters tooHDInsight através de RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="5b8e5-151">**Solr índice através do carregamento de ficheiros de dados**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="5b8e5-152">Quando o índice Solr, coloque documentos no mesmo que poderá ser necessário toosearch no.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="5b8e5-153">tooindex Solr, utilize RDP tooremote num cluster de Olá, navegue até toohello ambiente de trabalho, abra a linha de comandos do Hadoop Olá e navegue demasiado**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="5b8e5-154">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="5b8e5-155">Verá Olá seguinte resultado na consola de Olá:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="5b8e5-156">utilitário de post.jar Olá indexa Solr com dois documentos de exemplo, **solr.xml** e **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="5b8e5-157">utilitário de post.jar Olá e os documentos de exemplo de Olá estão disponíveis com a instalação de Solr.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="5b8e5-158">**Utilize Olá Solr dashboard toosearch dentro Olá indexar documentos**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="5b8e5-159">No Olá RDP sessão toohello HDInsight cluster, abra o Internet Explorer e iniciar o dashboard de Solr Olá em **http://headnodehost:8983/solr / #/**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="5b8e5-160">No painel esquerdo Olá, de Olá **Core Seletor** pendente, selecione **collection1**e em que, clique em **consulta**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="5b8e5-161">Como exemplo, tooselect e devolver todos os documentos de Olá no Solr, fornecer Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="5b8e5-162">No Olá **q** texto, introduza  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="5b8e5-163">Esta ação irá devolver todos os documentos de Olá que são indexados no Solr.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="5b8e5-164">Se pretender toosearch para uma cadeia específica dentro de documentos Olá, pode introduzir essa cadeia aqui.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="5b8e5-165">No Olá **wt** caixa de texto, selecione Olá formato de saída.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="5b8e5-166">Predefinição é **json**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-166">Default is **json**.</span></span> <span data-ttu-id="5b8e5-167">Clique em **executar a consulta**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="5b8e5-168">![Utilize a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "executar uma consulta num Solr dashboard")</span><span class="sxs-lookup"><span data-stu-id="5b8e5-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="5b8e5-169">saída de Olá devolve Olá dois documentos que utilizámos para Solr indexação.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="5b8e5-170">saída de Olá é semelhante a seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="5b8e5-171">**Recomendado: Cópia de segurança Olá indexada dados a partir de Solr tooAzure armazenamento de BLOBs associado ao cluster de HDInsight Olá**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="5b8e5-172">Como uma boa prática, deve copiar em segurança dados Olá indexada de nós de cluster Solr Olá no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="5b8e5-173">Execute Olá, por isso, os seguintes passos toodo:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="5b8e5-174">A partir de sessão do RDP Olá, abra o Internet Explorer e toohello ponto seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="5b8e5-175">Deverá ver uma resposta como esta:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="5b8e5-176">Na sessão remota Olá, navegue demasiado {SOLR_HOME}\{coleção} \data.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="5b8e5-177">Para o cluster de Olá criado através do script de exemplo de Olá, este deve ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="5b8e5-178">Nesta localização, deverá ver uma pasta de instantâneos criada com um nome semelhante demasiado**instantâneo.* Timestamp** *.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="5b8e5-179">Zip pasta de instantâneos de Olá e carregue-o armazenamento de BLOBs de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="5b8e5-180">Olá Hadoop linha de comandos, navegue toohello localização da pasta de instantâneos de Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b8e5-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="5b8e5-181">Este comando cópias instantâneo demasiado / / dados de exemplo de Olá/no contentor de Olá dentro da predefinição de Olá armazenamento conta associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="5b8e5-182">Instalar Solr com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b8e5-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="5b8e5-183">Consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="5b8e5-184">exemplo de Olá demonstra como tooinstall Spark com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="5b8e5-185">Terá de toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="5b8e5-186">Instalar Solr com o .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5b8e5-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="5b8e5-187">Consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="5b8e5-188">exemplo de Olá demonstra como tooinstall Spark utilizando Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="5b8e5-189">Terá de toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="5b8e5-190">Consultar também</span><span class="sxs-lookup"><span data-stu-id="5b8e5-190">See also</span></span>
* [<span data-ttu-id="5b8e5-191">Instalar e utilizar Solr em clusters do HDinsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="5b8e5-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="5b8e5-192">[Criar clusters do Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre a criação de clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="5b8e5-193">[Personalizar clusters do HDInsight através da ação de Script][hdinsight-cluster-customize]: informações gerais sobre a personalização clusters do HDInsight através da ação de Script.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="5b8e5-194">[Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="5b8e5-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="5b8e5-195">[Instalar e utilizar o Spark nos clusters do HDInsight][hdinsight-install-spark]: exemplo de ação de Script sobre a instalação do Spark.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="5b8e5-196">[Instalar o R nos clusters do HDInsight][hdinsight-install-r]: exemplo de ação de Script sobre a instalação do R.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="5b8e5-197">[Instalar Giraph nos clusters do HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de ação de Script sobre como instalar Giraph.</span><span class="sxs-lookup"><span data-stu-id="5b8e5-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
