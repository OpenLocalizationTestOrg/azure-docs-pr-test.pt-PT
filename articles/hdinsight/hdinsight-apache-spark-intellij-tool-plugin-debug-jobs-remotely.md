---
title: "aaaAzure Toolkit para o IntelliJ - aplicações de depuração remota no HDInsight Spark | Microsoft Docs"
description: "Saiba como utilizar as ferramentas do HDInsight na Azure Toolkit para IntelliJ tooremotely depuração aplicações em execução em clusters do HDInsight Spark através de vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="9b996-103">Utilize o Toolkit do Azure para aplicações de toodebug IntelliJ remotamente no Spark do HDInsight através de VPN</span><span class="sxs-lookup"><span data-stu-id="9b996-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="9b996-104">Recomendamos a forma de Olá de depuração applicaltion spark remotamente através de ssh.</span><span class="sxs-lookup"><span data-stu-id="9b996-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="9b996-105">Para obter instruções, consulte [remotamente depurar aplicações do Spark num cluster do HDInsight com o Toolkit do Azure para o IntelliJ através de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="9b996-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="9b996-106">Este artigo fornece orientação passo a passo sobre como toouse hello as ferramentas do HDInsight na Azure Toolkit para o IntelliJ toosubmit uma tarefa do Spark no cluster do HDInsight Spark e, em seguida, depurá-lo remotamente a partir do seu computador de secretária.</span><span class="sxs-lookup"><span data-stu-id="9b996-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="9b996-107">toodo por isso, tem de efetuar Olá seguindo os passos de alto nível:</span><span class="sxs-lookup"><span data-stu-id="9b996-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="9b996-108">Crie um site para site ou ponto a site Virtual Network do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b996-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="9b996-109">Olá passos neste documento partem do princípio de que utiliza uma rede de site para site.</span><span class="sxs-lookup"><span data-stu-id="9b996-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="9b996-110">Crie um cluster do Spark no Azure HDInsight que faz parte de Olá site a site Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b996-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="9b996-111">Verifique a conectividade de Olá entre Olá cluster headnode e ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9b996-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="9b996-112">Criar uma aplicação de Scala no IntelliJ IDEA e configurá-la para depuração remota.</span><span class="sxs-lookup"><span data-stu-id="9b996-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="9b996-113">Execute e depurar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b996-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9b996-114">Prerequisites</span></span>
* <span data-ttu-id="9b996-115">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b996-115">An Azure subscription.</span></span> <span data-ttu-id="9b996-116">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9b996-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9b996-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b996-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9b996-118">Para obter instruções, consulte [clusters do Apache Spark criar no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9b996-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="9b996-119">Kit de desenvolvimento Java Oracle.</span><span class="sxs-lookup"><span data-stu-id="9b996-119">Oracle Java Development kit.</span></span> <span data-ttu-id="9b996-120">Pode instalar a [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="9b996-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="9b996-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9b996-121">IntelliJ IDEA.</span></span> <span data-ttu-id="9b996-122">Este artigo utiliza a versão 2017.1.</span><span class="sxs-lookup"><span data-stu-id="9b996-122">This article uses version 2017.1.</span></span> <span data-ttu-id="9b996-123">Pode instalar a [aqui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="9b996-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="9b996-124">Ferramentas do HDInsight no Toolkit do Azure para o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="9b996-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="9b996-125">As ferramentas do HDInsight para o IntelliJ estão disponíveis como parte da Olá Toolkit do Azure para o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="9b996-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="9b996-126">Para obter instruções sobre como tooinstall Olá Toolkit do Azure, consulte [instalar Olá Toolkit do Azure para o IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="9b996-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="9b996-127">Registo para a sua subscrição do Azure de IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9b996-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="9b996-128">Siga as instruções de Olá [aqui](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="9b996-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="9b996-129">Ao executar a aplicação de Spark Scala para depuração remota num computador Windows, poderá obter uma exceção, conforme explicado no [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) que ocorre devido a falta de tooa WinUtils.exe no Windows.</span><span class="sxs-lookup"><span data-stu-id="9b996-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="9b996-130">toowork em torno este erro, tem de [transferir Olá executável a partir daqui](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) como localização de tooa **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="9b996-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="9b996-131">Em seguida, tem de adicionar uma variável de ambiente **HADOOP_HOME** e defina o valor de Olá da variável de Olá demasiado**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="9b996-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="9b996-132">Passo 1: Criar uma Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="9b996-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="9b996-133">Siga as instruções de Olá do Olá abaixo ligações toocreate uma Azure Virtual Network e, em seguida, verifique a conectividade de Olá entre o ambiente de trabalho Olá e a rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b996-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="9b996-134">Criar uma VNet com uma ligação de VPN de site a site através do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b996-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="9b996-135">Criar uma VNet com uma ligação de VPN de site para site com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b996-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="9b996-136">Configurar uma rede virtual de ligação de ponto a site tooa através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b996-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="9b996-137">Passo 2: Criar um cluster do Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="9b996-138">Também deve criar um cluster do Apache Spark no Azure HDInsight que faz parte de Olá Azure Virtual Network que criou.</span><span class="sxs-lookup"><span data-stu-id="9b996-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="9b996-139">Utilize as informações de Olá disponíveis em [baseado em Linux criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9b996-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="9b996-140">Como parte da configuração opcional, selecione Olá Azure Virtual Network que criou no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="9b996-141">Passo 3: Verificar a conectividade de Olá entre Olá cluster headnode e ambiente de trabalho</span><span class="sxs-lookup"><span data-stu-id="9b996-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="9b996-142">Obter o endereço IP Olá Olá headnode.</span><span class="sxs-lookup"><span data-stu-id="9b996-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="9b996-143">Abra a IU do Ambari para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="9b996-144">No painel do cluster de Olá, clique em **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="9b996-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="9b996-146">Olá IU do Ambari, a partir do canto superior direito de Olá, clique em **anfitriões**.</span><span class="sxs-lookup"><span data-stu-id="9b996-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="9b996-148">Deverá ver uma lista de nós de zookeeper, nós de trabalho e headnodes.</span><span class="sxs-lookup"><span data-stu-id="9b996-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="9b996-149">Olá headnodes ter Olá **hn*** prefixo.</span><span class="sxs-lookup"><span data-stu-id="9b996-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="9b996-150">Clique em headnode primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-150">Click hello first headnode.</span></span>

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="9b996-152">Em Olá parte inferior da página Olá que se abre, de Olá **resumo** caixa, endereço IP de Olá de cópia de Olá headnode e nome de anfitrião Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Localizar headnode IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="9b996-154">Incluem o endereço IP Olá e nome de anfitrião Olá do Olá headnode toohello **anfitriões** ficheiro no computador de Olá de onde pretende toorun e remotamente as tarefas de Spark Olá de depuração.</span><span class="sxs-lookup"><span data-stu-id="9b996-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="9b996-155">Isto permitirá toocommunicate com headnode Olá utilizando o endereço IP Olá, bem como Olá nome do anfitrião.</span><span class="sxs-lookup"><span data-stu-id="9b996-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="9b996-156">Abra um bloco de notas com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="9b996-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="9b996-157">No menu de ficheiro Olá, clique em **abra** e, em seguida, navegue até toohello localização do ficheiro de anfitriões de Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="9b996-158">Num computador Windows, é `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="9b996-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="9b996-159">Adicionar Olá seguir toohello **anfitriões** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="9b996-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="9b996-160">O computador de Olá que ligado toohello Azure Virtual Network é utilizado pelo cluster do HDInsight Olá, certifique-se de que consegue enviar pings para ambos os headnodes Olá utilizando o endereço IP Olá, bem como o hostname Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="9b996-161">SSH no Olá cluster headnode utilizar instruções Olá em [Connect tooan cluster do HDInsight utilizando SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9b996-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="9b996-162">De Olá cluster headnode, executar um ping endereço IP de Olá do computador de secretária Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="9b996-163">Deve testar a conectividade tooboth Olá IP endereços atribuídos toohello computador, um para ligação de rede Olá e Olá para Olá Azure Virtual Network Olá computador está ligado.</span><span class="sxs-lookup"><span data-stu-id="9b996-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="9b996-164">Repita os passos de Olá para Olá, bem como outra headnode.</span><span class="sxs-lookup"><span data-stu-id="9b996-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="9b996-165">Passo 4: Criar uma aplicação de Spark Scala utilizando as ferramentas do HDInsight Olá no Toolkit do Azure para o IntelliJ e configurá-la para depuração remota</span><span class="sxs-lookup"><span data-stu-id="9b996-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="9b996-166">Inicie o IntelliJ IDEA e criar um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="9b996-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="9b996-167">Na caixa de diálogo de projeto novo do Olá, certifique-Olá seguintes opções e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="9b996-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Criar aplicações do Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="9b996-169">No painel esquerdo Olá, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9b996-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="9b996-170">No painel direito Olá, selecione **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="9b996-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="9b996-171">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="9b996-171">Click **Next**.</span></span>
2. <span data-ttu-id="9b996-172">Na próxima janela de Olá, forneça Olá os detalhes do projeto e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="9b996-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="9b996-173">Forneça um nome de projeto e a localização do projeto.</span><span class="sxs-lookup"><span data-stu-id="9b996-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="9b996-174">Para **projeto SDK**, utilize Java 1.8 para o cluster do spark 2. x, Java 1.7 para um cluster do spark 1. x.</span><span class="sxs-lookup"><span data-stu-id="9b996-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="9b996-175">Para **Spark versão**, Assistente de criação do projeto Scala integra-se a versão correta para o SDK do Spark e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="9b996-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="9b996-176">Se a versão de cluster do spark Olá for inferior 2.0, escolha spark 1. x.</span><span class="sxs-lookup"><span data-stu-id="9b996-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="9b996-177">Caso contrário, deve selecionar spark2.x.</span><span class="sxs-lookup"><span data-stu-id="9b996-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="9b996-178">Este exemplo utiliza Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="9b996-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="9b996-179">![Criar aplicações do Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="9b996-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="9b996-180">projeto de Spark Olá criará automaticamente um artefacto para si.</span><span class="sxs-lookup"><span data-stu-id="9b996-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="9b996-181">artefactos de Olá toosee, siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="9b996-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="9b996-182">De Olá **ficheiro** menu, clique em **estrutura do projeto**.</span><span class="sxs-lookup"><span data-stu-id="9b996-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="9b996-183">No Olá **estrutura do projeto** caixa de diálogo, clique em **artefactos** toosee Olá predefinido artefacto que é criado.</span><span class="sxs-lookup"><span data-stu-id="9b996-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="9b996-184">![Criar JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="9b996-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="9b996-185">Também pode criar os seus artefactos bly clicando no Olá  **+**  ícone, realçado na imagem de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="9b996-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="9b996-186">Adicione bibliotecas tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="9b996-186">Add libraries tooyour project.</span></span> <span data-ttu-id="9b996-187">tooadd uma biblioteca, clique no nome do projeto Olá na árvore de projeto Olá e, em seguida, clique em **abra as definições do módulo**.</span><span class="sxs-lookup"><span data-stu-id="9b996-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="9b996-188">No Olá **estrutura do projeto** caixa de diálogo, a partir do painel esquerdo do Olá, clique em **bibliotecas**, clique o símbolo de Olá (+) e, em seguida, clique em **do Maven**.</span><span class="sxs-lookup"><span data-stu-id="9b996-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Adicionar a biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="9b996-190">No Olá **transferir biblioteca do repositório Maven** diálogo caixa, procurar e adicionar Olá seguintes bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="9b996-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="9b996-191">Cópia `yarn-site.xml` e `core-site.xml` de Olá headnode do cluster e adicione-toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="9b996-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="9b996-192">Utilize Olá os seguintes ficheiros de Olá toocopy de comandos.</span><span class="sxs-lookup"><span data-stu-id="9b996-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="9b996-193">Pode utilizar [Cygwin](https://cygwin.com/install.html) seguinte de Olá toorun `scp` comandos toocopy ficheiros Olá Olá headnodes de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b996-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="9b996-194">Porque já foi adicionado o Olá cluster headnode IP endereços e nomes de anfitrião fo Olá ficheiro hosts no ambiente de trabalho Olá, podemos utilizar Olá **scp** comandos no Olá seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="9b996-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="9b996-195">Adicione o projeto de tooyour estes ficheiros ao copiá-las em Olá **/src** pasta na sua árvore de projeto, por exemplo `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="9b996-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="9b996-196">Olá atualização `core-site.xml` Olá toomake seguir as alterações.</span><span class="sxs-lookup"><span data-stu-id="9b996-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="9b996-197">`core-site.xml`inclui uma conta de armazenamento de chaves toohello Olá encriptado associada ao cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="9b996-198">No Olá `core-site.xml` que adicionou toohello projeto, substituir Olá chave encriptada com a chave de armazenamento real Olá associado à conta do storage predefinida Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="9b996-199">Consulte [gerir as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9b996-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="9b996-200">Remover Olá seguintes entradas de Olá `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="9b996-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="9b996-201">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-201">Save hello file.</span></span>
7. <span data-ttu-id="9b996-202">Adicione classe de principal de Olá para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9b996-202">Add hello Main class for your application.</span></span> <span data-ttu-id="9b996-203">De Olá **Explorador de projeto**, faça duplo clique **src**, ponto demasiado**novo**e, em seguida, clique em **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="9b996-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Adicione o código de origem](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="9b996-205">No Olá **criar uma nova classe de Scala** diálogo caixa, forneça um nome para **tipo** selecione **objeto**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b996-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Adicione o código de origem](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="9b996-207">No Olá `MyClusterAppMain.scala` de ficheiros, cole Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="9b996-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="9b996-208">Este código cria o contexto de Spark Olá e inicia uma `executeJob` método Olá `SparkSample` objeto.</span><span class="sxs-lookup"><span data-stu-id="9b996-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="9b996-209">Repita os passos 8 e 9 acima tooadd chamado um novo objeto de Scala `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="9b996-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="9b996-210">classe de toothis adicionar Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="9b996-210">toothis class add hello following code.</span></span> <span data-ttu-id="9b996-211">Este código lê dados de Olá de Olá HVAC.csv (disponível em todos os clusters do HDInsight Spark), obtém linhas Olá que têm apenas um dígito na coluna seventh Olá Olá CSV e escreve saída Olá demasiado**/HVACOut** em predefinido Olá contentor de armazenamento Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="9b996-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="9b996-212">Repita os passos 8 e 9 acima tooadd uma nova classe denominada `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="9b996-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="9b996-213">Esta classe implementa Olá Spark teste arquitetura que é utilizada para depuração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="9b996-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="9b996-214">Adicionar Olá seguinte código toohello `RemoteClusterDebugging` classe.</span><span class="sxs-lookup"><span data-stu-id="9b996-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="9b996-215">Alguns pontos importantes toonote aqui:</span><span class="sxs-lookup"><span data-stu-id="9b996-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="9b996-216">Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, certifique-se Olá assemblagem Spark JAR no armazenamento de cluster Olá no caminho especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="9b996-217">Para `setJars`, especifique a localização olá onde será criada jar do artefacto de Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="9b996-218">Normalmente, é `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="9b996-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="9b996-219">No Olá `RemoteClusterDebugging` classe, faça duplo clique Olá `test` palavra-chave e selecione **criar configuração de RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="9b996-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="9b996-221">Na caixa de diálogo Olá, forneça um nome para a configuração de Olá e selecione Olá **testar tipo** como **nome para o teste**.</span><span class="sxs-lookup"><span data-stu-id="9b996-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="9b996-222">Deixe todos os outros valores como predefinição, clique em **aplicar**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b996-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="9b996-224">Deverá ver uma **remoto execute** configuração pendente na barra de menus Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="9b996-226">Passo 5: Executar a aplicação Olá no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="9b996-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="9b996-227">No projeto IntelliJ IDEA, abra `SparkSample.scala` e criar um rdd1 too'val seguinte do ponto de interrupção '.</span><span class="sxs-lookup"><span data-stu-id="9b996-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="9b996-228">No menu de pop-up de Olá para criar um ponto de interrupção, selecione **linha na função executeJob**.</span><span class="sxs-lookup"><span data-stu-id="9b996-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Adicionar um ponto de interrupção](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="9b996-230">Clique em Olá **depurar executar** toohello seguinte botão **remoto execute** configuração pendente toostart execução da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9b996-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="9b996-232">Quando a execução do programa Olá atinge o ponto de interrupção Olá, deverá ver uma **depurador** separador Olá inferior painel.</span><span class="sxs-lookup"><span data-stu-id="9b996-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="9b996-234">Clique em Olá (**+**) ícone tooadd uma veja conforme mostrado na imagem de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="9b996-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="9b996-236">Aqui, porque a aplicação Olá quebrou antes de variável de Olá `rdd1` foi criado, utilizando este veja é possível ver o que são Olá primeiro 5 linhas na variável Olá `rdd`.</span><span class="sxs-lookup"><span data-stu-id="9b996-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="9b996-237">Prima **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="9b996-237">Press **ENTER**.</span></span>

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="9b996-239">O que vê na imagem de Olá acima é no tempo de execução, pode consultar terrabytes de dados e de depuração como avança de ser a aplicação.</span><span class="sxs-lookup"><span data-stu-id="9b996-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="9b996-240">Por exemplo, no resultado de Olá mostrado na imagem de Olá acima, pode ver essa Olá primeira linha da saída de Olá é um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="9b996-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="9b996-241">Com base nisso, pode modificar a linha de cabeçalho do aplicação código tooskip Olá se necessário.</span><span class="sxs-lookup"><span data-stu-id="9b996-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="9b996-242">Agora pode clicar em Olá **retomar programa** tooproceed ícone com a sua aplicação em execução.</span><span class="sxs-lookup"><span data-stu-id="9b996-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="9b996-244">Se a aplicação Olá for concluída com êxito, deve ver um resultado semelhante Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="9b996-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Executar o programa de Olá no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="9b996-246"><a name="seealso"></a>Ver também</span><span class="sxs-lookup"><span data-stu-id="9b996-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9b996-247">Descrição geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="9b996-248">Demonstração</span><span class="sxs-lookup"><span data-stu-id="9b996-248">Demo</span></span>
* <span data-ttu-id="9b996-249">Criar projeto Scala (vídeo): [criar aplicações do Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="9b996-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="9b996-250">Depuração remota (vídeo): [Toolkit do Azure de utilização para o IntelliJ toodebug aplicações do Spark remotamente num Cluster do HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="9b996-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="9b996-251">Cenários</span><span class="sxs-lookup"><span data-stu-id="9b996-251">Scenarios</span></span>
* [<span data-ttu-id="9b996-252">Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI</span><span class="sxs-lookup"><span data-stu-id="9b996-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9b996-253">Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC</span><span class="sxs-lookup"><span data-stu-id="9b996-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9b996-254">Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares</span><span class="sxs-lookup"><span data-stu-id="9b996-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9b996-255">Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real</span><span class="sxs-lookup"><span data-stu-id="9b996-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9b996-256">Análise de registos de sites com o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9b996-257">Criar e executar aplicações</span><span class="sxs-lookup"><span data-stu-id="9b996-257">Create and run applications</span></span>
* [<span data-ttu-id="9b996-258">Criar uma aplicação autónoma com o Scala</span><span class="sxs-lookup"><span data-stu-id="9b996-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9b996-259">Executar tarefas remotamente num cluster do Spark com o Livy</span><span class="sxs-lookup"><span data-stu-id="9b996-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9b996-260">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="9b996-260">Tools and extensions</span></span>
* [<span data-ttu-id="9b996-261">Utilize as ferramentas do HDInsight no Toolkit do Azure para o IntelliJ toocreate e submeter aplicações do Spark scala</span><span class="sxs-lookup"><span data-stu-id="9b996-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9b996-262">Utilize o Toolkit do Azure para aplicações do Spark toodebug IntelliJ remotamente através de SSH</span><span class="sxs-lookup"><span data-stu-id="9b996-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="9b996-263">Utilize as ferramentas do HDInsight para o IntelliJ com Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="9b996-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="9b996-264">Utilize as ferramentas do HDInsight Toolkit do Azure para aplicações do Spark Eclipse toocreate</span><span class="sxs-lookup"><span data-stu-id="9b996-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="9b996-265">Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9b996-266">Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9b996-267">Utilizar pacotes externos com blocos de notas do Jupyter</span><span class="sxs-lookup"><span data-stu-id="9b996-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9b996-268">Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9b996-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9b996-269">Gerir recursos</span><span class="sxs-lookup"><span data-stu-id="9b996-269">Manage resources</span></span>
* [<span data-ttu-id="9b996-270">Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9b996-271">Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b996-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
