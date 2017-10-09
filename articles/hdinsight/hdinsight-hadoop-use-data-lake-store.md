---
title: aaaUse Data Lake Store com o Hadoop no Azure HDInsight | Microsoft Docs
description: "Saiba como tooquery dados do Azure Data Lake Store e toostore resulta da sua análise."
keywords: "armazenamento de blobs, hdfs, dados estruturados, dados não estruturados, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="dce67-104">Utilizar o Data Lake Store com clusters do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dce67-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="dce67-105">dados de tooanalyze no cluster do HDInsight, pode armazenar dados Olá está no [Storage do Azure](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), ou ambos.</span><span class="sxs-lookup"><span data-stu-id="dce67-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="dce67-106">Ambas as opções de armazenamento permitem-lhe eliminar toosafely clusters do HDInsight que são utilizados para o cálculo sem que haja perda de dados do utilizador.</span><span class="sxs-lookup"><span data-stu-id="dce67-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="dce67-107">Neste artigo, ficará a saber como o Data Lake Store funciona com clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dce67-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="dce67-108">toolearn como funciona o Storage do Azure com clusters do HDInsight, consulte [clusters de utilizar o Storage do Azure com o Azure HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dce67-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="dce67-109">Para obter mais informações sobre a criação de um cluster do HDInsight, veja [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Criar clusters do Hadoop no HDInsight).</span><span class="sxs-lookup"><span data-stu-id="dce67-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dce67-110">O Data Lake Store é sempre acedido através de um canal seguro, pelo que não existe nenhum nome de esquema de sistema de ficheiros `adls`.</span><span class="sxs-lookup"><span data-stu-id="dce67-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="dce67-111">Utiliza sempre `adl`.</span><span class="sxs-lookup"><span data-stu-id="dce67-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="dce67-112">Disponibilidades para clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="dce67-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="dce67-113">O Hadoop suporta uma noção do sistema de ficheiros Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="dce67-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="dce67-114">sistema de ficheiros Olá predefinido implica um esquema predefinido e à autoridade.</span><span class="sxs-lookup"><span data-stu-id="dce67-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="dce67-115">Também pode ser caminhos relativos tooresolve utilizados.</span><span class="sxs-lookup"><span data-stu-id="dce67-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="dce67-116">Durante o processo de criação de cluster de HDInsight Olá, pode especificar um contentor do blob no Storage do Azure como sistema de ficheiros Olá predefinido ou com o HDInsight 3.5 e versões mais recentes, pode selecionar o Storage do Azure ou do Azure Data Lake Store como sistema de ficheiros predefinido Olá com um algumas exceções.</span><span class="sxs-lookup"><span data-stu-id="dce67-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="dce67-117">Os clusters do HDInsight podem utilizar o Data Lake Store de duas formas:</span><span class="sxs-lookup"><span data-stu-id="dce67-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="dce67-118">Como armazenamento de predefinido Olá</span><span class="sxs-lookup"><span data-stu-id="dce67-118">As hello default storage</span></span>
* <span data-ttu-id="dce67-119">Como armazenamento adicional, com o Azure Storage Blob como armazenamento predefinido.</span><span class="sxs-lookup"><span data-stu-id="dce67-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="dce67-120">A partir de agora, apenas algumas das Olá HDInsight cluster utilizando o Data Lake Store como armazenamento de predefinido e contas de armazenamento adicional de suporte de tipos/versões:</span><span class="sxs-lookup"><span data-stu-id="dce67-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="dce67-121">Tipo de cluster do HDInsight</span><span class="sxs-lookup"><span data-stu-id="dce67-121">HDInsight cluster type</span></span> | <span data-ttu-id="dce67-122">Data Lake Store como armazenamento predefinido</span><span class="sxs-lookup"><span data-stu-id="dce67-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="dce67-123">Data Lake Store como armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="dce67-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="dce67-124">Notas</span><span class="sxs-lookup"><span data-stu-id="dce67-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="dce67-125">HDInsight versão 3.6</span><span class="sxs-lookup"><span data-stu-id="dce67-125">HDInsight version 3.6</span></span> | <span data-ttu-id="dce67-126">Sim</span><span class="sxs-lookup"><span data-stu-id="dce67-126">Yes</span></span> | <span data-ttu-id="dce67-127">Sim</span><span class="sxs-lookup"><span data-stu-id="dce67-127">Yes</span></span> | |
| <span data-ttu-id="dce67-128">HDInsight versão 3.5</span><span class="sxs-lookup"><span data-stu-id="dce67-128">HDInsight version 3.5</span></span> | <span data-ttu-id="dce67-129">Sim</span><span class="sxs-lookup"><span data-stu-id="dce67-129">Yes</span></span> | <span data-ttu-id="dce67-130">Sim</span><span class="sxs-lookup"><span data-stu-id="dce67-130">Yes</span></span> | <span data-ttu-id="dce67-131">Com exceção de Olá do HBase</span><span class="sxs-lookup"><span data-stu-id="dce67-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="dce67-132">HDInsight versão 3.4</span><span class="sxs-lookup"><span data-stu-id="dce67-132">HDInsight version 3.4</span></span> | <span data-ttu-id="dce67-133">Não</span><span class="sxs-lookup"><span data-stu-id="dce67-133">No</span></span> | <span data-ttu-id="dce67-134">Sim</span><span class="sxs-lookup"><span data-stu-id="dce67-134">Yes</span></span> | |
| <span data-ttu-id="dce67-135">HDInsight versão 3.3</span><span class="sxs-lookup"><span data-stu-id="dce67-135">HDInsight version 3.3</span></span> | <span data-ttu-id="dce67-136">Não</span><span class="sxs-lookup"><span data-stu-id="dce67-136">No</span></span> | <span data-ttu-id="dce67-137">Não</span><span class="sxs-lookup"><span data-stu-id="dce67-137">No</span></span> | |
| <span data-ttu-id="dce67-138">HDInsight versão 3.2</span><span class="sxs-lookup"><span data-stu-id="dce67-138">HDInsight version 3.2</span></span> | <span data-ttu-id="dce67-139">Não</span><span class="sxs-lookup"><span data-stu-id="dce67-139">No</span></span> | <span data-ttu-id="dce67-140">Sim</span><span class="sxs-lookup"><span data-stu-id="dce67-140">Yes</span></span> | |
| <span data-ttu-id="dce67-141">HDInsight Premium (escalão)</span><span class="sxs-lookup"><span data-stu-id="dce67-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="dce67-142">Não</span><span class="sxs-lookup"><span data-stu-id="dce67-142">No</span></span> | <span data-ttu-id="dce67-143">Não</span><span class="sxs-lookup"><span data-stu-id="dce67-143">No</span></span> | |
| <span data-ttu-id="dce67-144">Storm</span><span class="sxs-lookup"><span data-stu-id="dce67-144">Storm</span></span> | | |<span data-ttu-id="dce67-145">Pode utilizar dados do Data Lake Store toowrite de uma topologia do Storm.</span><span class="sxs-lookup"><span data-stu-id="dce67-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="dce67-146">Também pode utilizar o Data Lake Store para dados de referência que podem então ser lidos por uma topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="dce67-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="dce67-147">Utilizar o Data Lake Store como uma conta de armazenamento adicional não afetar o desempenho ou Olá capacidade tooread ou escrever tooAzure armazenamento do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="dce67-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="dce67-148">Utilizar o Data Lake Store como armazenamento predefinido</span><span class="sxs-lookup"><span data-stu-id="dce67-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="dce67-149">Quando o HDInsight é implementado com o Data Lake Store, como armazenamento de predefinido, os ficheiros relacionados com o cluster de Olá são armazenados no Data Lake Store no Olá seguinte localização:</span><span class="sxs-lookup"><span data-stu-id="dce67-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="dce67-150">onde `<cluster_root_path>` é Olá nome de uma pasta que cria no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dce67-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="dce67-151">Ao especificar um caminho de raiz para cada cluster, pode utilizar Olá a mesma conta de Data Lake Store para mais de um cluster.</span><span class="sxs-lookup"><span data-stu-id="dce67-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="dce67-152">Por isso, pode ter uma configuração em que:</span><span class="sxs-lookup"><span data-stu-id="dce67-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="dce67-153">Cluster1 pode utilizar o caminho de Olá`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="dce67-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="dce67-154">Cluster2 pode utilizar o caminho de Olá`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="dce67-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="dce67-155">Tenha em atenção que ambos Olá clusters utilize Olá mesma conta do Data Lake Store **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="dce67-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="dce67-156">Cada cluster tem tooits acesso possui sistema de ficheiros de raiz no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dce67-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="dce67-157">Olá experiência de implementação no portal do Azure em particular pede-lhe toouse um nome de pasta, tais como **/clusters/\<clustername >** para o caminho da raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="dce67-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="dce67-158">toobe toouse capaz de um arquivo Data Lake como armazenamento de predefinido, tem de conceder Olá serviço acesso principal toohello seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="dce67-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="dce67-159">raiz de conta de Data Lake Store Olá.</span><span class="sxs-lookup"><span data-stu-id="dce67-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="dce67-160">Por exemplo: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="dce67-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="dce67-161">pasta de Olá para todas as pastas de cluster.</span><span class="sxs-lookup"><span data-stu-id="dce67-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="dce67-162">Por exemplo: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="dce67-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="dce67-163">pasta de Olá para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="dce67-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="dce67-164">Por exemplo: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="dce67-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="dce67-165">Para obter mais informações sobre como criar o principal de serviço e conceder acesso, veja [Configurar o acesso ao arquivo do Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="dce67-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="dce67-166">Utilizar o Data Lake Store como armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="dce67-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="dce67-167">Pode utilizar o Data Lake Store como armazenamento adicional para o cluster de Olá bem.</span><span class="sxs-lookup"><span data-stu-id="dce67-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="dce67-168">Nestes casos, o armazenamento de cluster de Olá predefinido pode ser um Blob de armazenamento do Azure ou uma conta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dce67-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="dce67-169">Se estiver a executar tarefas do HDInsight em relação a dados de Olá armazenados no Data Lake Store, como armazenamento adicional, tem de utilizar ficheiros de toohello Olá caminho completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="dce67-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="dce67-170">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dce67-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="dce67-171">Tenha em atenção que não existe nenhum **cluster_root_path** no URL de Olá agora.</span><span class="sxs-lookup"><span data-stu-id="dce67-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="dce67-172">Isto acontece porque o Data Lake Store não é um armazenamento de predefinido neste caso, pelo que tudo o que precisa toodo é fornecer Olá caminho toohello ficheiros.</span><span class="sxs-lookup"><span data-stu-id="dce67-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="dce67-173">toobe toouse capaz de um arquivo Data Lake como armazenamento adicional, o pode precisa apenas de toogrant Olá serviço acesso principal toohello caminhos onde estão armazenados os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="dce67-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="dce67-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dce67-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="dce67-175">Para obter mais informações sobre como criar o principal de serviço e conceder acesso, veja [Configurar o acesso ao arquivo do Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="dce67-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="dce67-176">Utilizar mais de uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dce67-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="dce67-177">Adicionar uma conta de Data Lake Store como adicionais e adicionar mais do que um Data Lake Store contas são conseguidas ao dar permissão ao cluster HDInsight Olá nos dados de contas de Data Lake Store um orar mais.</span><span class="sxs-lookup"><span data-stu-id="dce67-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="dce67-178">Veja [Configurar o acesso ao Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="dce67-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="dce67-179">Configurar o acesso ao arquivo do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dce67-179">Configure Data Lake store access</span></span>

<span data-ttu-id="dce67-180">tooconfigure acesso de arquivo Data Lake do cluster do HDInsight, tem de ter um principal de serviço (Azure AD) de diretório Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce67-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="dce67-181">Apenas um administrador do Azure AD pode criar um principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="dce67-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="dce67-182">o principal de serviço Olá tem de ser criado com um certificado.</span><span class="sxs-lookup"><span data-stu-id="dce67-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="dce67-183">Para obter mais informações, veja [Configurar o acesso ao Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) e [Criar um principal de serviço com certificado autoassinado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="dce67-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="dce67-184">Se pretender toouse Azure Data Lake Store como armazenamento adicional para o cluster do HDInsight, recomendamos vivamente que fazê-lo ao criar o cluster Olá, tal como descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="dce67-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="dce67-185">A adição de Azure Data Lake Store como armazenamento adicional tooan o cluster do HDInsight existente é um processo mais complicado e tooerrors suscetíveis.</span><span class="sxs-lookup"><span data-stu-id="dce67-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="dce67-186">Acesso aos ficheiros do cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="dce67-186">Access files from hello cluster</span></span>

<span data-ttu-id="dce67-187">Existem várias formas de poder aceder a ficheiros de Olá no Data Lake Store de um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dce67-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="dce67-188">**Com o nome completamente qualificado Olá**.</span><span class="sxs-lookup"><span data-stu-id="dce67-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="dce67-189">Com esta abordagem, que fornece o ficheiro de toohello Olá caminho completo que pretende que o tooaccess.</span><span class="sxs-lookup"><span data-stu-id="dce67-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="dce67-190">**Utilizando o formato de caminho encurtado Olá**.</span><span class="sxs-lookup"><span data-stu-id="dce67-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="dce67-191">Com esta abordagem, substitua caminho Olá toohello raiz de cluster de cópia de segurança com adl: / / /.</span><span class="sxs-lookup"><span data-stu-id="dce67-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="dce67-192">Por isso, no exemplo de Olá acima, pode substituir `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` com `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="dce67-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="dce67-193">**Utilizar o caminho relativo Olá**.</span><span class="sxs-lookup"><span data-stu-id="dce67-193">**Using hello relative path**.</span></span> <span data-ttu-id="dce67-194">Com esta abordagem, fornecer apenas ficheiro de toohello Olá caminho relativo que pretende que o tooaccess.</span><span class="sxs-lookup"><span data-stu-id="dce67-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="dce67-195">Por exemplo, se o ficheiro de toohello Olá caminho completo é:</span><span class="sxs-lookup"><span data-stu-id="dce67-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="dce67-196">Pode aceder ao hello do mesmo ficheiro sample.log utilizando este caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="dce67-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="dce67-197">Criar clusters do HDInsight com acesso tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="dce67-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="dce67-198">Utilize Olá seguintes ligações para instruções detalhadas sobre como toocreate clusters do HDInsight com acesso tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dce67-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="dce67-199">Utilizar o Portal</span><span class="sxs-lookup"><span data-stu-id="dce67-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="dce67-200">Utilizar o PowerShell (com o Data Lake Store como armazenamento predefinido)</span><span class="sxs-lookup"><span data-stu-id="dce67-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="dce67-201">Utilizar o PowerShell (com o Data Lake Store como armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="dce67-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="dce67-202">Utilizar modelos do Azure</span><span class="sxs-lookup"><span data-stu-id="dce67-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="dce67-203">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dce67-203">Next steps</span></span>
<span data-ttu-id="dce67-204">Neste artigo, aprendeu como toouse compatível com HDFS Azure Data Lake Store com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dce67-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="dce67-205">Isto permite-lhe toobuild dimensionável e de longa duração, arquivar soluções de aquisição de dados e a utilização HDInsight toounlock Olá informações Olá armazenado estruturadas e os dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="dce67-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="dce67-206">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="dce67-206">For more information, see:</span></span>

* <span data-ttu-id="dce67-207">[Get started with Azure HDInsight (Introdução ao Azure HDInsight)][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="dce67-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="dce67-208">Introdução ao Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dce67-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="dce67-209">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="dce67-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="dce67-210">[Use Hive with HDInsight (Utilizar o Hive com o HDInsight)][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="dce67-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="dce67-211">[Use Pig with HDInsight (Utilizar o Pig com o HDInsight)][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="dce67-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="dce67-212">[Utilizar assinaturas de acesso partilhado do Azure armazenamento toorestrict acesso toodata com o HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="dce67-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
