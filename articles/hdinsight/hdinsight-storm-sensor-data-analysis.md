---
title: dados de sensores de aaaAnalyze com Apache Storm e HBase | Microsoft Docs
description: "Saiba como tooconnect tooApache Storm com uma rede virtual. Utilizar o Storm com dados de sensores do HBase tooprocess de um hub de eventos e visualizá-lo com D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="2a85d-104">Analisar dados de sensor com Apache Storm, o Hub de eventos e o HBase no HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="2a85d-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="2a85d-105">Saiba como toouse Apache Storm no HDInsight tooprocess dados de sensores do Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85d-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="2a85d-106">dados de Olá, em seguida, são armazenados no Apache HBase no HDInsight e visualizados utilizando D3.js.</span><span class="sxs-lookup"><span data-stu-id="2a85d-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="2a85d-107">modelo do Azure Resource Manager Olá utilizado neste documento demonstra como toocreate vários recursos do Azure num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2a85d-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="2a85d-108">modelo de Olá cria uma rede Virtual do Azure, dois clusters do HDInsight (Storm e HBase) e uma aplicação Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85d-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="2a85d-109">Uma implementação de node.js de um dashboard web em tempo real é automaticamente implementada toohello web app.</span><span class="sxs-lookup"><span data-stu-id="2a85d-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="2a85d-110">informações Olá este documento e o exemplo neste documento exigem HDInsight versão 3.6.</span><span class="sxs-lookup"><span data-stu-id="2a85d-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="2a85d-111">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="2a85d-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2a85d-112">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="2a85d-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a85d-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2a85d-113">Prerequisites</span></span>

* <span data-ttu-id="2a85d-114">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85d-114">An Azure subscription.</span></span>
* <span data-ttu-id="2a85d-115">[NODE.js](http://nodejs.org/): dashboard de web de Olá toopreview utilizados localmente no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2a85d-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="2a85d-116">[Java e Olá JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): utilizada topologia do Storm toodevelop Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="2a85d-117">[Maven](http://maven.apache.org/what-is-maven.html): projeto de Olá toobuild e compilação utilizados.</span><span class="sxs-lookup"><span data-stu-id="2a85d-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="2a85d-118">[Git](http://git-scm.com/): projeto de Olá toodownload utilizado a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a85d-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="2a85d-119">Um **SSH** cliente: utilizada tooconnect toohello HDInsight baseado em Linux clusters.</span><span class="sxs-lookup"><span data-stu-id="2a85d-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2a85d-120">Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2a85d-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="2a85d-121">Não precisa de um cluster do HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="2a85d-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="2a85d-122">passos de Olá neste documento criar Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="2a85d-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="2a85d-123">Uma rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="2a85d-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="2a85d-124">Um cluster Storm no HDInsight (baseado em Linux, dois nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="2a85d-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="2a85d-125">O HBase no HDInsight cluster (baseado em Linux, dois nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="2a85d-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="2a85d-126">Uma aplicação Web do Azure que aloja o dashboard de web de Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="2a85d-127">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="2a85d-127">Architecture</span></span>

![diagrama da arquitetura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="2a85d-129">Neste exemplo consiste em Olá os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="2a85d-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="2a85d-130">**Os Hubs de eventos do Azure**: contém dados que são recolhidos dos sensores.</span><span class="sxs-lookup"><span data-stu-id="2a85d-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="2a85d-131">**Storm no HDInsight**: fornece processamento em tempo real de dados a partir do Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2a85d-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="2a85d-132">**O HBase no HDInsight**: Fornece um arquivo de dados NoSQL persistente para os dados depois de ter sido processada pela Storm.</span><span class="sxs-lookup"><span data-stu-id="2a85d-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="2a85d-133">**Serviço de rede Virtual do Azure**: permite as comunicações seguras entre Olá Storm no HDInsight e HBase nos clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a85d-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2a85d-134">Uma rede virtual é necessária quando utilizar a API de cliente de Java HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="2a85d-135">Não está exposta através de gateway de público Olá para clusters de HBase.</span><span class="sxs-lookup"><span data-stu-id="2a85d-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="2a85d-136">Clusters de HBase instalar e Storm para Olá permite que a mesma rede virtual Olá cluster do Storm (ou qualquer outro sistema na rede virtual Olá) toodirectly aceder HBase através da API de cliente.</span><span class="sxs-lookup"><span data-stu-id="2a85d-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="2a85d-137">**Web site do dashboard**: um dashboard de exemplo que gráficos de dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="2a85d-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="2a85d-138">Web site de Olá está implementada no Node.js.</span><span class="sxs-lookup"><span data-stu-id="2a85d-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="2a85d-139">[Socket.IO](http://socket.io/) é utilizado para comunicação em tempo real entre topologia do Storm Olá e site Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2a85d-140">A utilização de Socket.io para comunicação é um detalhe de implementação.</span><span class="sxs-lookup"><span data-stu-id="2a85d-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="2a85d-141">Pode utilizar qualquer estrutura de comunicações, tais como WebSockets não processados ou SignalR.</span><span class="sxs-lookup"><span data-stu-id="2a85d-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="2a85d-142">[D3.js](http://d3js.org/) toograph utilizados Olá dados que é enviado toohello site.</span><span class="sxs-lookup"><span data-stu-id="2a85d-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a85d-143">Dois clusters são necessárias, conforme não é não existe nenhum método suportado toocreate um cluster do HDInsight para Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="2a85d-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="2a85d-144">Olá topologia lê dados de Hub de eventos utilizando Olá [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe e escreve dados no HBase utilizando Olá [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe.</span><span class="sxs-lookup"><span data-stu-id="2a85d-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="2a85d-145">Comunicação com o Web site de Olá é conseguida utilizando [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="2a85d-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="2a85d-146">Olá diagrama a seguir explica esquema Olá da topologia de Olá:</span><span class="sxs-lookup"><span data-stu-id="2a85d-146">hello following diagram explains hello layout of hello topology:</span></span>

![diagrama da topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="2a85d-148">Este diagrama é uma visão simplificada de topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="2a85d-149">Para cada partição no seu Hub de eventos, é criada uma instância de cada componente.</span><span class="sxs-lookup"><span data-stu-id="2a85d-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="2a85d-150">Estas instâncias são distribuídas entre os nós no cluster de Olá Olá e dados são encaminhados entre eles, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="2a85d-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="2a85d-151">Dados a partir do analisador de toohello Olá spout tem balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="2a85d-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="2a85d-152">Dados de Olá parser toohello Dashboard e o HBase são agrupados por ID de dispositivo, para que as mensagens de Olá mesmo dispositivo sempre fluxo toohello mesmo componente.</span><span class="sxs-lookup"><span data-stu-id="2a85d-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="2a85d-153">Componentes de topologia</span><span class="sxs-lookup"><span data-stu-id="2a85d-153">Topology components</span></span>

* <span data-ttu-id="2a85d-154">**Event Hub Spout**: spout Olá é fornecido como parte da versão do Apache Storm 0.10.0 e planos superiores.</span><span class="sxs-lookup"><span data-stu-id="2a85d-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2a85d-155">spout de Hub de eventos de Olá utilizado neste exemplo requer um Storm no clusters do HDInsight versão 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="2a85d-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="2a85d-156">**ParserBolt.java**: dados Olá que são emitidos por spout Olá for JSON não processado e, ocasionalmente mais do que um evento é emitido um momento.</span><span class="sxs-lookup"><span data-stu-id="2a85d-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="2a85d-157">Este bolt lê dados de Olá emitidos por Olá spout e analisa a mensagem de JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a85d-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="2a85d-158">bolt Olá, em seguida, emite dados Olá como uma cadeia de identificação contém vários campos.</span><span class="sxs-lookup"><span data-stu-id="2a85d-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="2a85d-159">**DashboardBolt.java**: este componente demonstra como toouse Olá Socket.io biblioteca de clientes para os dados de toosend Java no dashboard de web de toohello em tempo real.</span><span class="sxs-lookup"><span data-stu-id="2a85d-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="2a85d-160">**não hbase.yaml**: Olá utilizada quando executado no modo de local de definição de topologia.</span><span class="sxs-lookup"><span data-stu-id="2a85d-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="2a85d-161">Não utilize componentes de HBase.</span><span class="sxs-lookup"><span data-stu-id="2a85d-161">It does not use HBase components.</span></span>
* <span data-ttu-id="2a85d-162">**com hbase.yaml**: Olá utilizada ao executar a topologia de Olá no cluster de Olá de definição de topologia.</span><span class="sxs-lookup"><span data-stu-id="2a85d-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="2a85d-163">Utilizar o HBase componentes.</span><span class="sxs-lookup"><span data-stu-id="2a85d-163">It does use HBase components.</span></span>
* <span data-ttu-id="2a85d-164">**Dev.Properties**: Olá informações de configuração para spout de Hub de eventos de Olá, bolt de HBase e componentes de dashboard.</span><span class="sxs-lookup"><span data-stu-id="2a85d-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="2a85d-165">Preparar o ambiente</span><span class="sxs-lookup"><span data-stu-id="2a85d-165">Prepare your environment</span></span>

<span data-ttu-id="2a85d-166">Antes de utilizar este exemplo, tem de criar um Hub de eventos do Azure, que topologia do Storm Olá lê a partir do.</span><span class="sxs-lookup"><span data-stu-id="2a85d-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="2a85d-167">Configurar o Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="2a85d-167">Configure Event Hub</span></span>

<span data-ttu-id="2a85d-168">Hub de eventos é a origem de dados de Olá para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="2a85d-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="2a85d-169">Utilize os seguintes passos toocreate um Hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="2a85d-170">De Olá [portal do Azure](https://portal.azure.com), selecione **+ novo** -> **Internet das coisas** -> **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="2a85d-171">No Olá **criar espaço de nomes** secção, execute Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="2a85d-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="2a85d-172">Introduza um **nome** para Olá espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="2a85d-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="2a85d-173">Selecione um escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="2a85d-173">Select a pricing tier.</span></span> <span data-ttu-id="2a85d-174">**Básico** é suficiente para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="2a85d-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="2a85d-175">Selecione Olá Azure **subscrição** toouse.</span><span class="sxs-lookup"><span data-stu-id="2a85d-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="2a85d-176">Selecione um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="2a85d-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="2a85d-177">Selecione Olá **localização** para Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2a85d-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="2a85d-178">Selecione **Pin toodashboard**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="2a85d-179">Quando tiver concluído o processo de criação de Olá, é apresentada Olá informações de Hubs de eventos para o espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="2a85d-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="2a85d-180">Aqui, selecione **+ adicionar Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="2a85d-181">No Olá **criar o Hub de eventos** secção, introduza um nome de **sensordata**e, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="2a85d-182">Deixe Olá outros campos de valores predefinidos de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="2a85d-183">Hubs de eventos de Olá ver do seu espaço de nomes, selecione **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="2a85d-184">Selecione Olá **sensordata** entrada.</span><span class="sxs-lookup"><span data-stu-id="2a85d-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="2a85d-185">A partir da Olá sensordata Hub de eventos, selecione **políticas de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="2a85d-186">Olá utilize **+ adicionar** Olá tooadd de hiperligação seguinte políticas:</span><span class="sxs-lookup"><span data-stu-id="2a85d-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="2a85d-187">Nome da política</span><span class="sxs-lookup"><span data-stu-id="2a85d-187">Policy name</span></span> | <span data-ttu-id="2a85d-188">afirmações</span><span class="sxs-lookup"><span data-stu-id="2a85d-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="2a85d-189">dispositivos</span><span class="sxs-lookup"><span data-stu-id="2a85d-189">devices</span></span> | <span data-ttu-id="2a85d-190">Enviar</span><span class="sxs-lookup"><span data-stu-id="2a85d-190">Send</span></span> |
    | <span data-ttu-id="2a85d-191">Storm</span><span class="sxs-lookup"><span data-stu-id="2a85d-191">storm</span></span> | <span data-ttu-id="2a85d-192">Escutar</span><span class="sxs-lookup"><span data-stu-id="2a85d-192">Listen</span></span> |

1. <span data-ttu-id="2a85d-193">Selecione ambas as políticas e tome nota do Olá **chave primária** valor.</span><span class="sxs-lookup"><span data-stu-id="2a85d-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="2a85d-194">Precisa de valor de Olá para ambas as políticas nos passos futuras.</span><span class="sxs-lookup"><span data-stu-id="2a85d-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="2a85d-195">Transferir e configurar o projeto de Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-195">Download and configure hello project</span></span>

<span data-ttu-id="2a85d-196">Utilize Olá seguir o projeto de Olá toodownload a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a85d-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="2a85d-197">Após a conclusão do comando de Olá, tiver Olá seguir a estrutura de diretórios:</span><span class="sxs-lookup"><span data-stu-id="2a85d-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="2a85d-198">Este documento não passa nos detalhes de toofull de código Olá incluídos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="2a85d-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="2a85d-199">No entanto, o código de Olá totalmente é comentado.</span><span class="sxs-lookup"><span data-stu-id="2a85d-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="2a85d-200">tooconfigure Olá projeto tooread do Hub de eventos, abra Olá `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` de ficheiros e adicionar o seu toohello de informações de Hub de eventos seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="2a85d-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="2a85d-201">Compilar e testar localmente</span><span class="sxs-lookup"><span data-stu-id="2a85d-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a85d-202">Com a topologia de Olá localmente requer um ambiente de desenvolvimento do Storm de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2a85d-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="2a85d-203">Para obter mais informações, consulte [configurar um ambiente de desenvolvimento do Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="2a85d-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="2a85d-204">Se estiver a utilizar um ambiente de desenvolvimento do Windows, poderá receber um `java.io.IOException` ao executar localmente a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="2a85d-205">Se assim for, deslocar-se na topologia de Olá toorunning no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a85d-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="2a85d-206">Antes de testar, tem de começar Olá dashboard tooview Olá resultado topologia Olá e gerar dados toostore no Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2a85d-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a85d-207">componente de HBase Olá desta topologia não está ativo quando testar localmente.</span><span class="sxs-lookup"><span data-stu-id="2a85d-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="2a85d-208">Olá Java API para o cluster de HBase Olá não pode ser acedido a partir de fora Olá Azure Virtual Network contém Olá clusters.</span><span class="sxs-lookup"><span data-stu-id="2a85d-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="2a85d-209">Iniciar a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-209">Start hello web application</span></span>

1. <span data-ttu-id="2a85d-210">Abra uma linha de comandos e mude de diretório demasiado`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="2a85d-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="2a85d-211">Utilize Olá dependências Olá tooinstall de comando necessárias para a aplicação web de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2a85d-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="2a85d-212">Utilize Olá aplicação web do comando toostart Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2a85d-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="2a85d-213">Verá uma mensagem toohello semelhante seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="2a85d-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="2a85d-214">Abra um browser e introduza `http://localhost:3000/` como endereço Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="2a85d-215">É apresentada uma página de toohello semelhante seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="2a85d-215">A page similar toohello following image is displayed:</span></span>
   
    ![dashboard da Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="2a85d-217">Deixe esta linha de comandos aberta.</span><span class="sxs-lookup"><span data-stu-id="2a85d-217">Leave this command prompt open.</span></span> <span data-ttu-id="2a85d-218">Depois de testar, utilize o servidor de web de Olá de toostop Ctrl-C.</span><span class="sxs-lookup"><span data-stu-id="2a85d-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="2a85d-219">Gerar dados</span><span class="sxs-lookup"><span data-stu-id="2a85d-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="2a85d-220">Olá passos nesta secção utilizam o Node.js para que possa ser utilizados em qualquer plataforma.</span><span class="sxs-lookup"><span data-stu-id="2a85d-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="2a85d-221">Para outros exemplos de idioma, consulte Olá `SendEvents` diretório.</span><span class="sxs-lookup"><span data-stu-id="2a85d-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="2a85d-222">Abra uma nova linha de comandos, shell ou terminal e altere os diretórios demasiado`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="2a85d-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="2a85d-223">dependências de Olá tooinstall necessárias para a aplicação Olá, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2a85d-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="2a85d-224">Abra Olá `app.js` ficheiro num editor de texto e adicione Olá informações de Hub de eventos que obteve anteriormente:</span><span class="sxs-lookup"><span data-stu-id="2a85d-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="2a85d-225">Este exemplo assume que utilizou `sensordata` como nome de Olá do seu Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2a85d-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="2a85d-226">E que `devices` como nome de Olá da política de Olá que tenha um `Send` de afirmação.</span><span class="sxs-lookup"><span data-stu-id="2a85d-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="2a85d-227">Utilize os seguintes comandos tooinsert novo as entradas no Hub de eventos de Olá:</span><span class="sxs-lookup"><span data-stu-id="2a85d-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="2a85d-228">Pode ver várias linhas de saída que contenham dados Olá enviados tooEvent Hub:</span><span class="sxs-lookup"><span data-stu-id="2a85d-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="2a85d-229">Criar e iniciar a topologia de Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-229">Build and start hello topology</span></span>

1. <span data-ttu-id="2a85d-230">Abra uma nova linha de comandos e altere os diretórios demasiado`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="2a85d-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="2a85d-231">toobuild e pacote Olá topologia, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2a85d-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="2a85d-232">topologia de Olá toostart no modo local, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2a85d-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="2a85d-233">`--local`topologia de Olá é iniciado no modo local.</span><span class="sxs-lookup"><span data-stu-id="2a85d-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="2a85d-234">`--filter`utiliza Olá `dev.properties` ficheiro toopopulate parâmetros na definição de topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="2a85d-235">`resources/no-hbase.yaml`utiliza Olá `no-hbase.yaml` definição de topologia.</span><span class="sxs-lookup"><span data-stu-id="2a85d-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="2a85d-236">Depois de iniciada, a topologia de Olá lê entradas de Hub de eventos e envia-as dashboard toohello em execução no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="2a85d-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="2a85d-237">Deverá ver as linhas são apresentadas no dashboard de web de Olá, semelhante toohello seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="2a85d-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![dashboard com os dados](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="2a85d-239">Enquanto dashboard Olá está em execução, utilizar Olá `node app.js` toosend novos dados tooEvent Hubs os passos de comando a partir de Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="2a85d-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="2a85d-240">Porque os valores de temperatura Olá aleatoriamente são gerados, gráfico de Olá deve atualizar tooshow alterações grande temperatura.</span><span class="sxs-lookup"><span data-stu-id="2a85d-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2a85d-241">Tem de constar Olá **hdinsight-eventhub-exemplo/SendEvents/Nodejs** diretório quando utilizar Olá `node app.js` comando.</span><span class="sxs-lookup"><span data-stu-id="2a85d-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="2a85d-242">Depois de verificar que dashboard Olá atualizações, pare Olá topologia utilizando Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="2a85d-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="2a85d-243">Pode utilizar o servidor local web do Ctrl + C toostop Olá também.</span><span class="sxs-lookup"><span data-stu-id="2a85d-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="2a85d-244">Criar um cluster do Storm e HBase</span><span class="sxs-lookup"><span data-stu-id="2a85d-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="2a85d-245">Olá, os passos nesta utilização de secção um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate um cluster de rede Virtual do Azure e um Storm e HBase na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="2a85d-246">modelo de Olá também cria uma aplicação Web do Azure e implementa uma cópia do dashboard de Olá para a mesma.</span><span class="sxs-lookup"><span data-stu-id="2a85d-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="2a85d-247">Uma rede virtual é utilizada para que a topologia de Olá em execução no cluster do Storm Olá pode comunicar diretamente com o cluster de HBase Olá Olá HBase Java API a utilizar.</span><span class="sxs-lookup"><span data-stu-id="2a85d-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="2a85d-248">modelo do Resource Manager Olá utilizado neste documento está localizado num contentor de blob público em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="2a85d-249">Clique em Olá seguinte botão toosign no tooAzure e modelo do Resource Manager Olá aberta no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85d-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="2a85d-250">De Olá **implementação personalizada** secção, introduza Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="2a85d-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Parâmetros do HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="2a85d-252">**Nome do Cluster de base**: este valor é utilizado como nome de base de Olá para clusters de Storm e HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="2a85d-253">Por exemplo, introduzir **abc** cria um cluster do Storm com o nome **storm abc** e um cluster HBase com o nome **hbase abc**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="2a85d-254">**Nome de utilizador de início de sessão do cluster**: nome de utilizador de admin Olá para clusters de Storm e HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="2a85d-255">**Palavra-passe de início de sessão do cluster**: palavra-passe utilizador de administrador de Olá para clusters de Storm e HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="2a85d-256">**Nome de utilizador SSH**: Olá toocreate de utilizador do SSH para clusters de Storm e HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="2a85d-257">**Palavra-passe SSH**: Olá palavra-passe do utilizador do SSH Olá para clusters de Storm e HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="2a85d-258">**Localização**: região Olá clusters Olá criados no.</span><span class="sxs-lookup"><span data-stu-id="2a85d-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="2a85d-259">Clique em **OK** parâmetros de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="2a85d-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="2a85d-260">Olá utilize **Noções básicas** secção toocreate um grupo de recursos ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="2a85d-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="2a85d-261">No Olá **localização do grupo de recursos** menu pendente, selecione Olá mesma localização que selecionou para Olá **localização** parâmetro Olá **definições** secção.</span><span class="sxs-lookup"><span data-stu-id="2a85d-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="2a85d-262">Leia Olá termos e condições e, em seguida, selecione **concordo toohello termos e condições indicadas acima**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="2a85d-263">Por fim, verifique **Pin toodashboard** e, em seguida, selecione **Compra**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="2a85d-264">Demora cerca de 20 minutos toocreate clusters Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="2a85d-265">Depois de tem sido criados recursos Olá, são apresentadas informações sobre o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Grupo de recursos para vnet Olá e clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="2a85d-267">Tenha em atenção que os nomes de Olá dos clusters do HDInsight Olá são **storm BASENAME** e **hbase BASENAME**, onde BASENAME nome Olá fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="2a85d-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="2a85d-268">Utilize estes nomes num passo posterior ao ligar a toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="2a85d-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="2a85d-269">Também é tenha em atenção que Olá nome do site de dashboard Olá **basename dashboard**.</span><span class="sxs-lookup"><span data-stu-id="2a85d-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="2a85d-270">Este valor é utilizado mais tarde neste documento.</span><span class="sxs-lookup"><span data-stu-id="2a85d-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="2a85d-271">Configurar bolt de Dashboard Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="2a85d-272">toosend dashboard toohello dados implementado como uma aplicação web, tem de modificar Olá seguinte linha no Olá `dev.properties`ficheiro:</span><span class="sxs-lookup"><span data-stu-id="2a85d-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="2a85d-273">Alteração `http://localhost:3000` demasiado`http://BASENAME-dashboard.azurewebsites.net` e guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="2a85d-274">Substitua **BASENAME** com o nome de base Olá fornecido no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="2a85d-275">Também pode utilizar o grupo de recursos de Olá criado anteriormente tooselect Olá dashboard e vista Olá URL.</span><span class="sxs-lookup"><span data-stu-id="2a85d-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="2a85d-276">Criar a tabela de HBase Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-276">Create hello HBase table</span></span>

<span data-ttu-id="2a85d-277">toostore dados no HBase, iremos tem primeiro de criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2a85d-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="2a85d-278">Pré-criar recursos de que necessita de Storm toowrite para, como a tentar toocreate recursos a partir de dentro de uma topologia do Storm podem resultar em várias instâncias ao tentar toocreate Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="2a85d-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="2a85d-279">Criar Olá recursos fora da topologia de Olá e utilizar o Storm para leitura/escrita e de análise.</span><span class="sxs-lookup"><span data-stu-id="2a85d-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="2a85d-280">Utilize o SSH tooconnect toohello cluster de HBase utilizando SSH Olá e palavra-passe que forneceu toohello modelo durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="2a85d-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="2a85d-281">Por exemplo, se ligar utilizando Olá `ssh` comando, teria de utilizar Olá sintaxe:</span><span class="sxs-lookup"><span data-stu-id="2a85d-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="2a85d-282">Substitua `sshuser` com o nome de utilizador do SSH Olá que forneceu ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="2a85d-283">Substitua `clustername` com o nome de cluster de HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="2a85d-284">Sessão SSH Olá, inicie o shell de HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="2a85d-285">Assim que a shell de Olá foi carregadas, verá um `hbase(main):001:0>` linha.</span><span class="sxs-lookup"><span data-stu-id="2a85d-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="2a85d-286">No Olá shell de HBase, introduza Olá comando toocreate o dados do sensor toostore Olá uma tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a85d-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="2a85d-287">Certifique-se de que essa tabela Olá foi criada utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2a85d-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="2a85d-288">Esta ação devolve informações toohello semelhante seguinte o exemplo, indicando que existem 0 linhas na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="2a85d-289">Introduza `exit` tooexit Olá shell de HBase:</span><span class="sxs-lookup"><span data-stu-id="2a85d-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="2a85d-290">Configurar bolt de HBase Olá</span><span class="sxs-lookup"><span data-stu-id="2a85d-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="2a85d-291">toowrite tooHBase do cluster do Storm Olá, tem de fornecer bolt de HBase Olá com detalhes de configuração de Olá do HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="2a85d-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="2a85d-292">Utilize um dos Olá seguir o quórum do exemplos tooretrieve Olá Zookeeper para o cluster de HBase:</span><span class="sxs-lookup"><span data-stu-id="2a85d-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="2a85d-293">Substitua `your_HDInsight_cluster_name` com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a85d-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="2a85d-294">Para obter mais informações sobre como instalar Olá `jq` utilitário, consulte [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="2a85d-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="2a85d-295">Quando solicitado, introduza a palavra-passe de Olá para início de sessão do Olá HDInsight admin.</span><span class="sxs-lookup"><span data-stu-id="2a85d-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="2a85d-296">Substitua ' your_HDInsight_cluster_name com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a85d-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="2a85d-297">Quando solicitado, introduza a palavra-passe de Olá para início de sessão do Olá HDInsight admin.</span><span class="sxs-lookup"><span data-stu-id="2a85d-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="2a85d-298">Este exemplo requer o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a85d-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="2a85d-299">Para obter mais informações sobre como utilizar o Azure PowerShell, consulte [começar com o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="2a85d-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="2a85d-300">informações de Olá devolvidas por estes exemplos são semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="2a85d-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="2a85d-301">Estas informações são utilizadas por toocommunicate do Storm com o cluster de HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="2a85d-302">Modificar Olá `dev.properties` de ficheiros e adicionar Olá Zookeeper quórum informações toohello seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="2a85d-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="2a85d-303">Criar pacote e implementar Olá solução tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="2a85d-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="2a85d-304">No seu ambiente de desenvolvimento, utilize Olá os seguintes passos toodeploy Olá Storm topologia toohello cluster do storm.</span><span class="sxs-lookup"><span data-stu-id="2a85d-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="2a85d-305">De Olá `TemperatureMonitor` diretório seguinte de Olá utilize comandos tooperform uma nova compilação e cria um pacote JAR do seu projeto:</span><span class="sxs-lookup"><span data-stu-id="2a85d-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="2a85d-306">Este comando cria um ficheiro denominado `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `destino ' diretório do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="2a85d-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="2a85d-307">Olá do utilize scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` cluster do Storm de tooyour de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="2a85d-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="2a85d-308">No Olá seguinte o exemplo, substitua `sshuser` com o utilizador do SSH Olá que forneceu ao criar o cluster de Olá, e `clustername` com o nome de Olá do seu cluster do Storm.</span><span class="sxs-lookup"><span data-stu-id="2a85d-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="2a85d-309">Quando lhe for pedido, introduza a palavra-passe de Olá para utilizador do SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="2a85d-310">Poderá demorar vários minutos ficheiros de Olá tooupload.</span><span class="sxs-lookup"><span data-stu-id="2a85d-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="2a85d-311">Para obter mais informações sobre como utilizar Olá `scp` e `ssh` comandos com o HDInsight, consulte [utilizar o SSH com o HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="2a85d-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="2a85d-312">Depois de terem sido carregado ficheiro Olá, ligue o cluster do Storm toohello utilizando SSH.</span><span class="sxs-lookup"><span data-stu-id="2a85d-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2a85d-313">Substitua `sshuser` com o nome de utilizador do SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="2a85d-314">Substitua `clustername` com o nome de cluster do Storm Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="2a85d-315">toostart Olá topologia, utilize Olá comando da sessão SSH Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2a85d-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="2a85d-316">`--remote`submete Olá topologia toohello serviço Nimbus, nós de supervisor toohello no cluster de Olá, distribui-lo.</span><span class="sxs-lookup"><span data-stu-id="2a85d-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="2a85d-317">`--filter`utiliza Olá `dev.properties` ficheiro toopopulate parâmetros na definição de topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="2a85d-318">`-R /with-hbase.yaml`utiliza Olá `with-hbase.yaml` topologia incluída no pacote de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="2a85d-319">Depois de é iniciado a topologia de Olá, abra um Web site toohello do browser publicado no Azure, em seguida, utilize Olá `node app.js` comando toosend dados tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="2a85d-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="2a85d-320">Deverá ver Olá web dashboard toodisplay Olá as informações de atualização.</span><span class="sxs-lookup"><span data-stu-id="2a85d-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="2a85d-322">Ver os dados de HBase</span><span class="sxs-lookup"><span data-stu-id="2a85d-322">View HBase data</span></span>

<span data-ttu-id="2a85d-323">Utilize os seguintes passos tooconnect tooHBase de Olá e certifique-se de que foi escritos dados Olá toohello tabela:</span><span class="sxs-lookup"><span data-stu-id="2a85d-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="2a85d-324">Utilize o SSH tooconnect toohello HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="2a85d-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2a85d-325">Substitua `sshuser` com o nome de utilizador do SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="2a85d-326">Substitua `clustername` com o nome de cluster de HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="2a85d-327">Sessão SSH Olá, inicie o shell de HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="2a85d-328">Assim que a shell de Olá foi carregadas, verá um `hbase(main):001:0>` linha.</span><span class="sxs-lookup"><span data-stu-id="2a85d-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="2a85d-329">Ver as linhas da tabela de Olá:</span><span class="sxs-lookup"><span data-stu-id="2a85d-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="2a85d-330">Este comando devolve informações toohello semelhante seguir texto, com a indicação de que não há dados na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="2a85d-331">Esta operação de análise devolve um máximo de 10 linhas da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a85d-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="2a85d-332">Eliminar os clusters</span><span class="sxs-lookup"><span data-stu-id="2a85d-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="2a85d-333">clusters de Olá toodelete, de armazenamento e de aplicação web de uma só vez, elimine o grupo de recursos de Olá que contém-los.</span><span class="sxs-lookup"><span data-stu-id="2a85d-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a85d-334">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2a85d-334">Next steps</span></span>

<span data-ttu-id="2a85d-335">Para obter mais exemplos de topologias do Storm com o HDInsight, consulte [topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="2a85d-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="2a85d-336">Para mais informações sobre o Apache Storm, consulte Olá [Apache Storm](https://storm.incubator.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="2a85d-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="2a85d-337">Para obter mais informações sobre o HBase no HDInsight, consulte Olá [HBase com o HDInsight Overview](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a85d-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="2a85d-338">Para obter mais informações sobre Socket.io, consulte Olá [socket.io](http://socket.io/) site.</span><span class="sxs-lookup"><span data-stu-id="2a85d-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="2a85d-339">Para mais informações sobre D3.js, consulte [D3.js - documentos de orientada por dados](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="2a85d-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="2a85d-340">Para obter informações sobre como criar topologias em Java, consulte [topologias de Java desenvolver para o Apache Storm no HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2a85d-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="2a85d-341">Para obter informações sobre como criar topologias no .NET, consulte [desenvolver topologias c# para Apache Storm no HDInsight com o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2a85d-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
