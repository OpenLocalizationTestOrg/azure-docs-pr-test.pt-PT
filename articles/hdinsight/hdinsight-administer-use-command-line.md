---
title: clusters do Hadoop de aaaManage utilizando a CLI do Azure - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá Interface de linha de comandos do Azure toomanage Hadoop clusters no Azure HDInsight. Olá CLI do Azure funciona no Windows, Mac e Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="b1a94-104">Gerir clusters do Hadoop no HDInsight com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b1a94-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="b1a94-105">Saiba como toouse Olá [Interface de linha de comandos do Azure](../cli-install-nodejs.md) toomanage Hadoop clusters no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1a94-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="b1a94-106">Olá CLI do Azure está implementada no Node.js.</span><span class="sxs-lookup"><span data-stu-id="b1a94-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="b1a94-107">Pode ser utilizado em qualquer plataforma que suporte Node.js, incluindo Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="b1a94-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="b1a94-108">Este artigo abrange apenas a utilização Olá CLI do Azure com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1a94-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="b1a94-109">Para obter um guia Geral sobre como toouse CLI do Azure, consulte [instalar e configurar a CLI do Azure][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="b1a94-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="b1a94-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b1a94-110">Prerequisites</span></span>
<span data-ttu-id="b1a94-111">Antes de começar este artigo, tem de ter o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="b1a94-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="b1a94-112">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b1a94-112">**An Azure subscription**.</span></span> <span data-ttu-id="b1a94-113">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b1a94-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b1a94-114">**CLI do Azure** -consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) para obter informações de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="b1a94-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="b1a94-115">**Ligar tooAzure**com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b1a94-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="b1a94-116">Para obter mais informações sobre a autenticação através de uma conta escolar ou profissional, consulte [ligar tooan subscrição do Azure a partir de Olá CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b1a94-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="b1a94-117">**Modo do comutador toohello Azure Resource Manager**com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b1a94-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="b1a94-118">tooget ajuda, utilize Olá **-h** mudar.</span><span class="sxs-lookup"><span data-stu-id="b1a94-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="b1a94-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1a94-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="b1a94-120">Criar clusters com Olá CLI</span><span class="sxs-lookup"><span data-stu-id="b1a94-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="b1a94-121">Consulte [criar clusters do HDInsight utilizando Olá CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b1a94-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="b1a94-122">Listar e mostrar os detalhes do cluster</span><span class="sxs-lookup"><span data-stu-id="b1a94-122">List and show cluster details</span></span>
<span data-ttu-id="b1a94-123">Utilize Olá toolist de comandos a seguir e mostrar os detalhes do cluster:</span><span class="sxs-lookup"><span data-stu-id="b1a94-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="b1a94-124">![Vista da linha de comandos da lista de cluster][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="b1a94-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="b1a94-125">Eliminar clusters</span><span class="sxs-lookup"><span data-stu-id="b1a94-125">Delete clusters</span></span>
<span data-ttu-id="b1a94-126">Utilize Olá comando toodelete um cluster a seguir:</span><span class="sxs-lookup"><span data-stu-id="b1a94-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="b1a94-127">Também pode eliminar um cluster ao eliminar o grupo de recursos de Olá que contém o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1a94-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="b1a94-128">Tenha em atenção, esta ação irá eliminar todos os recursos de Olá no grupo de Olá, incluindo a conta do storage predefinida Olá.</span><span class="sxs-lookup"><span data-stu-id="b1a94-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="b1a94-129">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="b1a94-129">Scale clusters</span></span>
<span data-ttu-id="b1a94-130">Olá toochange tamanho de cluster do Hadoop:</span><span class="sxs-lookup"><span data-stu-id="b1a94-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="b1a94-131">Ativar/desativar o acesso HTTP para um cluster</span><span class="sxs-lookup"><span data-stu-id="b1a94-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="b1a94-132">Ativar/desativar acesso RDP para um cluster</span><span class="sxs-lookup"><span data-stu-id="b1a94-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="b1a94-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b1a94-133">Next steps</span></span>
<span data-ttu-id="b1a94-134">Neste artigo, aprendeu como tooperform diferentes HDInsight cluster tarefas administrativas.</span><span class="sxs-lookup"><span data-stu-id="b1a94-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="b1a94-135">toolearn mais, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b1a94-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="b1a94-136">[Administrar HDInsight utilizando Olá Portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="b1a94-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="b1a94-137">[Administrar HDInsight ao utilizar o Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="b1a94-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="b1a94-138">[Get started with Azure HDInsight (Introdução ao Azure HDInsight)][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b1a94-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="b1a94-139">[Como toouse Olá CLI do Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="b1a94-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Listar e Mostrar clusters"
