---
title: "as bibliotecas Hive de aaaAdd durante HDInsight cluster criação - Azure | Microsoft Docs"
description: "Saiba como bibliotecas de ramo de registo tooadd (ficheiros jar), tooan HDInsight cluster durante a criação do cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="fa186-103">Adicione as bibliotecas Hive personalizadas ao criar o cluster do HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa186-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="fa186-104">Se tiver de bibliotecas que utiliza com frequência, com o Hive no HDInsight, este documento contém informações sobre como utilizar as bibliotecas de Olá uma ação de Script toopre carga durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="fa186-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="fa186-105">Bibliotecas adicionadas utilizando os passos de Olá neste documento são globalmente disponíveis no ramo de registo - há toouse sem necessidade de [adicionar JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload-los.</span><span class="sxs-lookup"><span data-stu-id="fa186-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="fa186-106">Como funciona</span><span class="sxs-lookup"><span data-stu-id="fa186-106">How it works</span></span>

<span data-ttu-id="fa186-107">Quando criar um cluster, pode especificar opcionalmente uma ação de Script que executa um script em nós de cluster Olá, enquanto que estão a ser criadas.</span><span class="sxs-lookup"><span data-stu-id="fa186-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="fa186-108">script de Olá neste documento aceita um único parâmetro que é uma localização de WASB contém Olá bibliotecas (armazenadas como ficheiros jar) toobe previamente carregada.</span><span class="sxs-lookup"><span data-stu-id="fa186-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="fa186-109">Durante a criação do cluster, o script de Olá enumera ficheiros Olá, copia-as toohello `/usr/lib/customhivelibs/` diretório em nós head e de trabalho, em seguida, adiciona-toohello `hive.aux.jars.path` propriedade no Olá `core-site.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fa186-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="fa186-110">Em clusters baseados em Linux, também atualiza Olá `hive-env.sh` ficheiro com a localização Olá ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="fa186-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="fa186-111">Utilizando ações de script de Olá neste artigo disponibiliza bibliotecas Olá no Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="fa186-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="fa186-112">**HDInsight baseado em Linux** - quando utilizar Olá um cliente do Hive, **WebHCat**, e **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="fa186-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="fa186-113">**HDInsight baseado em Windows** - ao utilizar o cliente do ramo de registo de Olá e **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="fa186-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="fa186-114">script de Olá</span><span class="sxs-lookup"><span data-stu-id="fa186-114">hello script</span></span>

<span data-ttu-id="fa186-115">**Localização do script**</span><span class="sxs-lookup"><span data-stu-id="fa186-115">**Script location**</span></span>

<span data-ttu-id="fa186-116">Para **clusters baseados em Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="fa186-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="fa186-117">Para **clusters baseados em Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="fa186-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa186-118">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="fa186-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fa186-119">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="fa186-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="fa186-120">**Requisitos**</span><span class="sxs-lookup"><span data-stu-id="fa186-120">**Requirements**</span></span>

* <span data-ttu-id="fa186-121">scripts de Olá tem de ser aplicados tooboth Olá **nós principais** e **nós de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="fa186-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="fa186-122">Olá v7 desejar tooinstall deve ser armazenado no armazenamento de Blobs do Azure num **único contentor**.</span><span class="sxs-lookup"><span data-stu-id="fa186-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="fa186-123">conta de armazenamento de Olá que contém a biblioteca de Olá dos ficheiros jar **tem** ser o cluster do HDInsight toohello ligados durante a criação.</span><span class="sxs-lookup"><span data-stu-id="fa186-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="fa186-124">-Tem de estar conta do storage predefinida Olá ou uma conta adicionados através do __configuração opcional__.</span><span class="sxs-lookup"><span data-stu-id="fa186-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="fa186-125">contentor de toohello Olá WASB caminho tem de ser especificado como um parâmetro toohello ação de Script.</span><span class="sxs-lookup"><span data-stu-id="fa186-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="fa186-126">Por exemplo, se hello v7 é armazenados num contentor com o nome **libs** numa conta de armazenamento com o nome **mystorage**, parâmetro Olá seria  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="fa186-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fa186-127">Este documento assume que já tem criar uma conta de armazenamento, o contentor de blob e Olá carregado ficheiros tooit.</span><span class="sxs-lookup"><span data-stu-id="fa186-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="fa186-128">Se não tiver criado uma conta de armazenamento, pode fazê-através de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa186-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fa186-129">Em seguida, pode utilizar um utilitário como [Explorador de armazenamento do Azure](http://storageexplorer.com/) toocreate um contentor na conta de Olá e carregar ficheiros tooit.</span><span class="sxs-lookup"><span data-stu-id="fa186-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="fa186-130">Criar um cluster utilizando o script de Olá</span><span class="sxs-lookup"><span data-stu-id="fa186-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="fa186-131">os seguintes passos de Olá criar um cluster do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="fa186-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="fa186-132">Selecione toocreate um cluster baseado no Windows, **Windows** como Olá cluster SO ao criar o cluster de Olá e utilizar o script do Windows (PowerShell) de Olá em vez de scripts de bash Olá.</span><span class="sxs-lookup"><span data-stu-id="fa186-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="fa186-133">Também pode utilizar o Azure PowerShell ou Olá SDK .NET do HDInsight toocreate um cluster com este script.</span><span class="sxs-lookup"><span data-stu-id="fa186-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="fa186-134">Para obter mais informações sobre como utilizar estes métodos, consulte [HDInsight personalizar clusters com ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fa186-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="fa186-135">Começar a aprovisionar um cluster, utilizando os passos de Olá no [aprovisionar clusters do HDInsight no Linux](hdinsight-hadoop-provision-linux-clusters.md), mas não concluir o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="fa186-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="fa186-136">No Olá **configuração opcional** painel, selecione **ações de Script**e forneça Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="fa186-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="fa186-137">**NOME**: introduza um nome amigável para a ação de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa186-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="fa186-138">**URI de SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="fa186-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="fa186-139">**HEAD**: selecione esta opção.</span><span class="sxs-lookup"><span data-stu-id="fa186-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="fa186-140">**TRABALHO**: selecione esta opção.</span><span class="sxs-lookup"><span data-stu-id="fa186-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="fa186-141">**ZOOKEEPER**: deixar isto em branco.</span><span class="sxs-lookup"><span data-stu-id="fa186-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="fa186-142">**Os parâmetros**: introduza Olá WASB toohello contentor de armazenamento e de conta do endereço que contém Olá v7.</span><span class="sxs-lookup"><span data-stu-id="fa186-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="fa186-143">Por exemplo,  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="fa186-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="fa186-144">Na parte inferior de Olá de Olá **ações de Script**, utilize Olá **selecione** configuração de Olá toosave do botão.</span><span class="sxs-lookup"><span data-stu-id="fa186-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="fa186-145">No Olá **configuração opcional** painel, selecione **contas de armazenamento ligadas** e selecione Olá **adicionar uma chave de armazenamento** ligação.</span><span class="sxs-lookup"><span data-stu-id="fa186-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="fa186-146">Selecionar conta de armazenamento de Olá contém v7 Olá e, em seguida, utilizar Olá **selecione** definições de toosave botões e retorno Olá **configuração opcional** painel.</span><span class="sxs-lookup"><span data-stu-id="fa186-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="fa186-147">Olá utilize **selecione** botão na parte inferior de Olá de Olá **configuração opcional** painel toosave Olá opcional as informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="fa186-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="fa186-148">Continuar aprovisionamento cluster Olá, conforme descrito em [aprovisionar clusters do HDInsight no Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="fa186-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="fa186-149">Depois de concluída a criação do cluster, é capaz de toouse v7 de Olá adicionados através deste script de ramo de registo, sem ter toouse Olá `ADD JAR` instrução.</span><span class="sxs-lookup"><span data-stu-id="fa186-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa186-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fa186-150">Next steps</span></span>

<span data-ttu-id="fa186-151">Para obter mais informações sobre como trabalhar com o Hive, consulte [utilizar o Hive com o HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="fa186-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
