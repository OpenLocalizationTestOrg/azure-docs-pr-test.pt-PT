---
title: "clusters do HDInsight de aaaCustomize com ações de script - Azure | Microsoft Docs"
description: "Adicione componentes personalizados que clusters do HDInsight baseado em tooLinux com ações de Script. Ações de script são scripts de Bash que podem ser utilizado toocustomize Olá cluster configuração ou adicione serviços adicionais e utilitários como Hue, Solr ou R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="61624-104">Personalizar clusters do HDInsight baseado em Linux através da ação de Script</span><span class="sxs-lookup"><span data-stu-id="61624-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="61624-105">O HDInsight fornece uma opção de configuração denominada **ação de Script** que invoca scripts personalizados que personalizar cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="61624-106">Estes scripts são utilizado tooinstall componentes adicionais e alterar as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="61624-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="61624-107">Ações de script podem ser utilizadas durante ou após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61624-108">ações de script do Olá capacidade toouse num cluster já em execução só está disponível para clusters do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="61624-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="61624-109">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="61624-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="61624-110">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="61624-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="61624-111">Ações de script também podem ser publicada toohello Azure Marketplace como uma aplicação do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61624-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="61624-112">Alguns exemplos de Olá neste documento mostram como instalar uma aplicação do HDInsight utilizando os comandos de ação de script do PowerShell e Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="61624-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="61624-113">Para obter mais informações sobre as aplicações do HDInsight, consulte [aplicações HDInsight publicar para Olá Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="61624-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="61624-114">Permissões</span><span class="sxs-lookup"><span data-stu-id="61624-114">Permissions</span></span>

<span data-ttu-id="61624-115">Se estiver a utilizar um cluster do HDInsight associados a um domínio, existem dois Ambari as permissões necessárias ao utilizar as ações de script com o cluster Olá:</span><span class="sxs-lookup"><span data-stu-id="61624-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="61624-116">**AMBARI. EXECUTAR\_personalizada\_comando**: função de administrador do Ambari Olá tenha esta permissão, por predefinição.</span><span class="sxs-lookup"><span data-stu-id="61624-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="61624-117">**CLUSTER. EXECUTAR\_personalizada\_comando**: ambos Olá administrador de Cluster do HDInsight e administrador de Ambari tem esta permissão, por predefinição.</span><span class="sxs-lookup"><span data-stu-id="61624-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="61624-118">Para obter mais informações sobre como trabalhar com permissões com o HDInsight associados a um domínio, consulte [gerir clusters do HDInsight associados a um domínio](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="61624-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="61624-119">Controlo de acesso</span><span class="sxs-lookup"><span data-stu-id="61624-119">Access control</span></span>

<span data-ttu-id="61624-120">Se não tiver Olá administrador/proprietário da sua subscrição do Azure, a conta tem de ter, pelo menos, **contribuinte** acesso toohello recursos grupo que contém o cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="61624-121">Além disso, se estiver a criar, pelo menos, um cluster do HDInsight, alguém com **contribuinte** acesso toohello subscrição do Azure tem tiver registado anteriormente fornecedor Olá para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61624-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="61624-122">Registo de fornecedor ocorre quando um utilizador com a subscrição do Contribuidor acesso toohello cria um recurso para Olá pela primeira vez no subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="61624-123">Também pode ser feito sem a criação de um recurso, ao [registar o fornecedor com REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="61624-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="61624-124">Para obter mais informações sobre como trabalhar com a gestão de acesso, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="61624-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="61624-125">Introdução à gestão de acesso no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="61624-126">Utilização de recursos de subscrição do Azure de tooyour toomanage acesso função atribuições</span><span class="sxs-lookup"><span data-stu-id="61624-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="61624-127">Noções sobre ações de Script</span><span class="sxs-lookup"><span data-stu-id="61624-127">Understanding Script Actions</span></span>

<span data-ttu-id="61624-128">Uma ação de Script é simplesmente um script de deteção que fornece um URI para e os parâmetros para.</span><span class="sxs-lookup"><span data-stu-id="61624-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="61624-129">script de Olá é executado em nós de cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="61624-130">Olá seguem-se as características e as funcionalidades de ações de script.</span><span class="sxs-lookup"><span data-stu-id="61624-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="61624-131">Deve ser armazenado no URI que é acessível a partir do cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="61624-132">Olá, são as localizações de armazenamento possíveis:</span><span class="sxs-lookup"><span data-stu-id="61624-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="61624-133">Um **Azure Data Lake Store** conta que seja acessível ao cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="61624-134">Para obter informações sobre como utilizar o Azure Data Lake Store com o HDInsight, consulte [criar um cluster do HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61624-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="61624-135">Quando utilizar um script armazenado no Data Lake Store, o formato de URI Olá é `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="61624-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="61624-136">Olá serviço principal HDInsight utiliza tooaccess Data Lake Store tem de ter acesso de leitura toohello script.</span><span class="sxs-lookup"><span data-stu-id="61624-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="61624-137">Um blob num **conta de armazenamento do Azure** é que as contas de armazenamento primário ou adicionais Olá para o cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="61624-138">HDInsight é concedido acesso tooboth um destes tipos de contas de armazenamento durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="61624-139">Um ficheiro pública partilha serviço como o Blob do Azure, o GitHub, OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="61624-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="61624-140">Por exemplo URIs, consulte Olá [scripts de ação de script de exemplo](#example-script-action-scripts) secção.</span><span class="sxs-lookup"><span data-stu-id="61624-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="61624-141">HDInsight suporta apenas __para fins gerais__ contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="61624-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="61624-142">Não suporta atualmente Olá __armazenamento de BLOBs__ tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="61624-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="61624-143">Pode ser restringida demasiado**em apenas determinados tipos de nó**para nós principais de exemplo ou nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="61624-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="61624-144">Quando utilizado com o HDInsight Premium, pode especificar que o script de Olá deve ser utilizado no nó de extremidade Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="61624-145">Pode ser **persistente** ou **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="61624-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="61624-146">**Persistente** scripts são cluster do tooworker aplicados nós adicionados toohello depois Olá script é executado.</span><span class="sxs-lookup"><span data-stu-id="61624-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="61624-147">Por exemplo, quando o cluster de Olá de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="61624-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="61624-148">Um script persistente também podem ser aplicadas alterações tipo de nó de tooanother, tais como um nó principal.</span><span class="sxs-lookup"><span data-stu-id="61624-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="61624-149">Ações de script persistentes tem de ter um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="61624-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="61624-150">**Ad hoc** scripts não são mantidos.</span><span class="sxs-lookup"><span data-stu-id="61624-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="61624-151">Não são cluster do tooworker aplicados nós adicionados toohello depois de script de Olá tem foi executada.</span><span class="sxs-lookup"><span data-stu-id="61624-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="61624-152">Pode promover subsequentemente um tooa scripts ad hoc persistente script ou despromover um script de ad hoc de tooan de script persistentes.</span><span class="sxs-lookup"><span data-stu-id="61624-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="61624-153">Ações de script utilizadas durante a criação do cluster automaticamente são mantidas.</span><span class="sxs-lookup"><span data-stu-id="61624-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="61624-154">Scripts que não são falhar persistem, mesmo se especificamente a indicar que devem ser.</span><span class="sxs-lookup"><span data-stu-id="61624-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="61624-155">Pode aceitar **parâmetros** que são utilizados pelo script de Olá durante a execução.</span><span class="sxs-lookup"><span data-stu-id="61624-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="61624-156">Executar com **privilégios de nível de raiz** em nós de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="61624-157">Pode ser utilizada através de Olá **portal do Azure**, **Azure PowerShell**, **CLI do Azure**, ou **SDK .NET do HDInsight**</span><span class="sxs-lookup"><span data-stu-id="61624-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="61624-158">cluster de Olá mantém um histórico de todos os scripts que tenha sido executado.</span><span class="sxs-lookup"><span data-stu-id="61624-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="61624-159">histórico de Olá é útil quando for necessário toofind Olá ID de um script para operações de promoção ou despromoção.</span><span class="sxs-lookup"><span data-stu-id="61624-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61624-160">Não há nenhum tooundo de forma automática Olá as alterações efetuadas por uma ação de script.</span><span class="sxs-lookup"><span data-stu-id="61624-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="61624-161">Inverter manualmente as alterações de Olá ou fornecer um script que inverte-los.</span><span class="sxs-lookup"><span data-stu-id="61624-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="61624-162">Ação de script no processo de criação do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="61624-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="61624-163">Ações de script utilizadas durante a criação do cluster são ligeiramente diferentes do script foi executadas ações num cluster existente:</span><span class="sxs-lookup"><span data-stu-id="61624-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="61624-164">script de Olá é **automaticamente persistente**.</span><span class="sxs-lookup"><span data-stu-id="61624-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="61624-165">A **falha** em Olá script pode originar toofail de processo de criação de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="61624-166">Olá diagrama seguinte ilustra quando a ação de Script é executada durante o processo de criação de Olá:</span><span class="sxs-lookup"><span data-stu-id="61624-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="61624-167">![Personalização de cluster do HDInsight e fases durante a criação do cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="61624-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="61624-168">executar script de Olá enquanto HDInsight está a ser configurado.</span><span class="sxs-lookup"><span data-stu-id="61624-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="61624-169">Nesta fase, Olá script é executado em paralelo em todos os Olá especificados de nós no cluster Olá e é executado com privilégios de raiz em nós de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="61624-170">Uma vez script Olá é executado com privilégios de nível de raiz em nós de cluster Olá, pode efetuar operações como parar e iniciar serviços, incluindo os serviços relacionados com o Hadoop.</span><span class="sxs-lookup"><span data-stu-id="61624-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="61624-171">Se parar os serviços, certifique-se de que serviço de Ambari Olá e outros serviços relacionados com o Hadoop estão em execução antes da execução do script Olá é concluída.</span><span class="sxs-lookup"><span data-stu-id="61624-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="61624-172">Estes serviços são necessários toosuccessfully determinar o estado de funcionamento de Olá e estado do cluster de Olá enquanto está a ser criada.</span><span class="sxs-lookup"><span data-stu-id="61624-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="61624-173">Durante a criação do cluster, pode utilizar várias ações de script em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="61624-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="61624-174">Estes scripts são invocados por ordem de Olá em que foram especificadas.</span><span class="sxs-lookup"><span data-stu-id="61624-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61624-175">Ações de script tem de concluir dentro de 60 minutos ou tempo limite.</span><span class="sxs-lookup"><span data-stu-id="61624-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="61624-176">Durante o aprovisionamento de cluster, o script de Olá é executada simultaneamente com outros processos de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="61624-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="61624-177">Disputa pelos recursos, tais como a largura de banda de CPU, tempo ou de rede pode fazer com que Olá script tootake mais toofinish que-lo no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="61624-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="61624-178">Olá toominimize tempo demora toorun Olá script, evite tarefas, tais como transferir e compilar aplicações a partir da origem.</span><span class="sxs-lookup"><span data-stu-id="61624-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="61624-179">Pré-compilar aplicações e armazenar os binários de Olá no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="61624-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="61624-180">Ação de script num cluster em execução</span><span class="sxs-lookup"><span data-stu-id="61624-180">Script action on a running cluster</span></span>

<span data-ttu-id="61624-181">Ao contrário das ações utilizadas durante a criação do cluster, uma falha num script são executadas num cluster já em execução do script não automaticamente causa Olá cluster toochange tooa falhada estado.</span><span class="sxs-lookup"><span data-stu-id="61624-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="61624-182">Depois de um script estiver concluído, o cluster Olá deverá devolver tooa "a executar o" Estado.</span><span class="sxs-lookup"><span data-stu-id="61624-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61624-183">Mesmo que o cluster de Olá tem um Estado 'em execução', hello script falhada pode quebraram coisas.</span><span class="sxs-lookup"><span data-stu-id="61624-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="61624-184">Por exemplo, um script foi possível eliminar ficheiros necessários pelo cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="61624-185">Ações de scripts executam com privilégios de raiz, pelo que deve certificar-se de que compreende o que faz um script antes de aplicá-la tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="61624-186">Ao aplicar um cluster de tooa de script, o estado do cluster Olá alterações toofrom **executar** demasiado**aceites**, em seguida, **HDInsight configuração**e, finalmente, faça uma cópia demasiado**Executar** para scripts com êxito.</span><span class="sxs-lookup"><span data-stu-id="61624-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="61624-187">Estado de script de Olá é registado no histórico de ações de script de Olá e pode utilizar este toodetermine informações se o script de Olá foi concluída com êxito ou falha.</span><span class="sxs-lookup"><span data-stu-id="61624-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="61624-188">Por exemplo, Olá `Get-AzureRmHDInsightScriptActionHistory` cmdlet do PowerShell pode ser utilizados tooview Olá estado de um script.</span><span class="sxs-lookup"><span data-stu-id="61624-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="61624-189">Devolve informações toohello semelhante seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="61624-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="61624-190">Se tiver alterado a palavra-passe de utilizador (administrador) do Olá cluster após a criação do cluster de Olá, script ações executaram este cluster poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="61624-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="61624-191">Se tiver quaisquer ações de script persistentes que nós de trabalho de destino, estes scripts podem falhar ao dimensionar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="61624-192">Scripts de ação de Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="61624-192">Example Script Action scripts</span></span>

<span data-ttu-id="61624-193">Scripts de ação de script podem ser utilizadas através de Olá utilitários os seguintes:</span><span class="sxs-lookup"><span data-stu-id="61624-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="61624-194">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-194">Azure portal</span></span>
* <span data-ttu-id="61624-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61624-195">Azure PowerShell</span></span>
* <span data-ttu-id="61624-196">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-196">Azure CLI</span></span>
* <span data-ttu-id="61624-197">SDK de .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="61624-198">O HDInsight fornece Olá de tooinstall scripts os seguintes componentes nos clusters do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61624-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="61624-199">Nome</span><span class="sxs-lookup"><span data-stu-id="61624-199">Name</span></span> | <span data-ttu-id="61624-200">Script</span><span class="sxs-lookup"><span data-stu-id="61624-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="61624-201">**Adicionar uma conta de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="61624-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="61624-202">https://hdiconfigactions.blob.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.SH. Consulte [cluster do HDInsight adicionar armazenamento adicional tooan](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="61624-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="61624-203">**Instalar a Hue**</span><span class="sxs-lookup"><span data-stu-id="61624-203">**Install Hue**</span></span> |<span data-ttu-id="61624-204">https://hdiconfigactions.blob.Core.Windows.NET/linuxhueconfigactionv02/Install-hue-uber-v02.SH. Consulte [instalar e utilizar Hue no HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="61624-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="61624-205">**Instalar Presto**</span><span class="sxs-lookup"><span data-stu-id="61624-205">**Install Presto**</span></span> |<span data-ttu-id="61624-206">https://RAW.githubusercontent.com/hdinsight/presto-hdinsight/Master/installpresto.SH. Consulte [instalar e utilizar Presto no HDInsight clusters](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="61624-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="61624-207">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="61624-207">**Install Solr**</span></span> |<span data-ttu-id="61624-208">https://hdiconfigactions.blob.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.SH. Consulte [instalar e utilizar Solr no HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="61624-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="61624-209">**Instalar Giraph**</span><span class="sxs-lookup"><span data-stu-id="61624-209">**Install Giraph**</span></span> |<span data-ttu-id="61624-210">https://hdiconfigactions.blob.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.SH. Consulte [instalar e utilizar Giraph no HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="61624-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="61624-211">**Pré-carregar as bibliotecas Hive**</span><span class="sxs-lookup"><span data-stu-id="61624-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="61624-212">https://hdiconfigactions.blob.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.SH. Consulte [bibliotecas adicionar Hive nos clusters do HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="61624-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="61624-213">**Instalar ou atualizar o Mono**</span><span class="sxs-lookup"><span data-stu-id="61624-213">**Install or update Mono**</span></span> | <span data-ttu-id="61624-214">https://hdiconfigactions.blob.Core.Windows.NET/Install-mono/Install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="61624-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="61624-215">Consulte [instalação ou atualização Mono no HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="61624-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="61624-216">Utilizar uma ação de Script durante a criação do cluster</span><span class="sxs-lookup"><span data-stu-id="61624-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="61624-217">Esta secção fornece exemplos sobre diferentes formas de Olá que pode utilizar ações de script ao criar um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61624-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="61624-218">Utilizar uma ação de Script durante a criação do cluster de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="61624-219">Começar a criar um cluster, conforme descrito em [clusters do Hadoop criar no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="61624-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="61624-220">Pare quando chegar Olá __resumo do Cluster__ secção.</span><span class="sxs-lookup"><span data-stu-id="61624-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="61624-221">De Olá __resumo do Cluster__ secção, selecione de Olá __editar__ hiperligação para __definições avançadas__.</span><span class="sxs-lookup"><span data-stu-id="61624-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Definições avançadas de ligação](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="61624-223">De Olá __definições avançadas__ secção, selecione __ações de Script__.</span><span class="sxs-lookup"><span data-stu-id="61624-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="61624-224">De Olá __ações de Script__ secção, selecione __+ submeter novos__</span><span class="sxs-lookup"><span data-stu-id="61624-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Submeter uma nova ação de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="61624-226">Olá utilize __selecionar um script__ entrada tooselect um script pré-cópia efetuado.</span><span class="sxs-lookup"><span data-stu-id="61624-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="61624-227">toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o script.</span><span class="sxs-lookup"><span data-stu-id="61624-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Adicionar um script no formulário de script selecione Olá](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="61624-229">Olá, a tabela seguinte descreve os elementos de Olá no formulário de Olá:</span><span class="sxs-lookup"><span data-stu-id="61624-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="61624-230">Propriedade</span><span class="sxs-lookup"><span data-stu-id="61624-230">Property</span></span> | <span data-ttu-id="61624-231">Valor</span><span class="sxs-lookup"><span data-stu-id="61624-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="61624-232">Selecione um script</span><span class="sxs-lookup"><span data-stu-id="61624-232">Select a script</span></span> | <span data-ttu-id="61624-233">toouse seu próprio script, selecione __personalizada__.</span><span class="sxs-lookup"><span data-stu-id="61624-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="61624-234">Caso contrário, selecione um dos scripts de Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="61624-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="61624-235">Nome</span><span class="sxs-lookup"><span data-stu-id="61624-235">Name</span></span> |<span data-ttu-id="61624-236">Especifique um nome para a ação de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="61624-237">Scripts de bash URI</span><span class="sxs-lookup"><span data-stu-id="61624-237">Bash script URI</span></span> |<span data-ttu-id="61624-238">Especifique Olá URI toohello script que é invocada toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="61624-239">Trabalho/HEAD/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="61624-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="61624-240">Especificar Olá nós (**Head**, **trabalho**, ou **ZooKeeper**) que personalização Olá script é executado.</span><span class="sxs-lookup"><span data-stu-id="61624-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="61624-241">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="61624-241">Parameters</span></span> |<span data-ttu-id="61624-242">Especifique parâmetros de Olá, se necessário pelo script de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="61624-243">Olá utilize __manter esta ação de script__ tooensure de entrada que Olá script é aplicada durante operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="61624-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="61624-244">Selecione __criar__ script de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="61624-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="61624-245">Em seguida, pode utilizar __+ submeter novo__ tooadd outro script.</span><span class="sxs-lookup"><span data-stu-id="61624-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Várias ações de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="61624-247">Quando tiver concluído a adição de scripts, utilize Olá __selecione__ botão e, em seguida, Olá __seguinte__ botão tooreturn toohello __resumo do Cluster__ secção.</span><span class="sxs-lookup"><span data-stu-id="61624-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="61624-248">cluster de Olá toocreate, selecione __criar__ de Olá __resumo do Cluster__ seleção.</span><span class="sxs-lookup"><span data-stu-id="61624-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="61624-249">Utilizar uma ação de Script a partir de modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61624-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="61624-250">Exemplos de Olá desta secção demonstram como toouse script ações com modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61624-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="61624-251">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="61624-251">Before you begin</span></span>

* <span data-ttu-id="61624-252">Para obter informações sobre como configurar uma estação de trabalho toorun cmdlets do Powershell do HDInsight, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61624-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="61624-253">Para obter instruções sobre como toocreate modelos, consulte [modelos Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="61624-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="61624-254">Se tiver não utilizado anteriormente Azure PowerShell com o Resource Manager, consulte o artigo [utilizar o Azure PowerShell com o Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="61624-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="61624-255">Criar clusters através da ação de Script</span><span class="sxs-lookup"><span data-stu-id="61624-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="61624-256">Copie Olá seguinte localização do modelo tooa no seu computador.</span><span class="sxs-lookup"><span data-stu-id="61624-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="61624-257">Este modelo instala Giraph em Olá headnodes e de trabalho nós Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="61624-258">Também pode verificar se o modelo JSON Olá é válido.</span><span class="sxs-lookup"><span data-stu-id="61624-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="61624-259">Cole o conteúdo do modelo [JSONLint](http://jsonlint.com/), uma ferramenta de validação JSON online.</span><span class="sxs-lookup"><span data-stu-id="61624-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="61624-260">Inicie o Azure PowerShell e inicie sessão tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="61624-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="61624-261">Depois de fornecer as suas credenciais, o comando de Olá devolve informações sobre a sua conta.</span><span class="sxs-lookup"><span data-stu-id="61624-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="61624-262">Se tiver várias subscrições, forneça o ID de subscrição de Olá desejar toouse para implementação.</span><span class="sxs-lookup"><span data-stu-id="61624-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="61624-263">Pode utilizar `Get-AzureRmSubscription` tooget uma lista de todas as subscrições associadas à sua conta, que inclui o ID de subscrição de Olá para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="61624-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="61624-264">Se não tiver um grupo de recursos existente, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="61624-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="61624-265">Forneça o nome de Olá do grupo de recursos de Olá e a localização que precisa para a sua solução.</span><span class="sxs-lookup"><span data-stu-id="61624-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="61624-266">Um resumo do grupo de recursos novo Olá é devolvido.</span><span class="sxs-lookup"><span data-stu-id="61624-266">A summary of hello new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="61624-267">toocreate uma implementação para o grupo de recursos, executar Olá **New-AzureRmResourceGroupDeployment** de comandos e fornecer os parâmetros necessários Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="61624-268">parâmetros de Olá incluem Olá dados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="61624-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="61624-269">Um nome para a implementação</span><span class="sxs-lookup"><span data-stu-id="61624-269">A name for your deployment</span></span>
    * <span data-ttu-id="61624-270">nome de Olá do seu grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="61624-270">hello name of your resource group</span></span>
    * <span data-ttu-id="61624-271">caminho de Olá ou modelo de toohello de URL que criou.</span><span class="sxs-lookup"><span data-stu-id="61624-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="61624-272">Se o seu modelo necessita de quaisquer parâmetros, tem de passar esses parâmetros bem.</span><span class="sxs-lookup"><span data-stu-id="61624-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="61624-273">Neste caso, ação de script Olá tooinstall R no cluster de Olá não requer quaisquer parâmetros.</span><span class="sxs-lookup"><span data-stu-id="61624-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="61624-274">São tooprovide pedido valores para parâmetros de Olá definidos no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="61624-275">Quando o grupo de recursos de Olá tiver sido implementado, é apresentado um resumo da implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="61624-276">Se a implementação falhar, pode utilizar Olá os seguintes cmdlets tooget informações sobre falhas de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="61624-277">Utilizar uma ação de Script durante a criação do cluster a partir do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61624-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="61624-278">Nesta secção, vamos utilizar Olá [adicionar AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts, utilizando a ação de Script toocustomize um cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="61624-279">Antes de continuar, certifique-se de que tem instalado e configurado o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61624-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="61624-280">Para obter informações sobre como configurar uma estação de trabalho toorun cmdlets do PowerShell do HDInsight, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61624-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="61624-281">Olá script seguinte demonstra como tooapply uma ação de script ao criar um cluster com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="61624-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="61624-282">Pode demorar vários minutos antes de Olá cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="61624-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="61624-283">Utilizar uma ação de Script durante a criação do cluster de Olá SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="61624-284">Olá SDK .NET do HDInsight fornece bibliotecas de cliente que torna mais fácil toowork com o HDInsight a partir de uma aplicação .NET.</span><span class="sxs-lookup"><span data-stu-id="61624-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="61624-285">Para um exemplo de código, consulte [baseado em Linux criar clusters do HDInsight utilizando Olá .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="61624-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="61624-286">Aplicar tooa uma ação de Script a executar o cluster</span><span class="sxs-lookup"><span data-stu-id="61624-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="61624-287">Nesta secção, saiba como tooapply script tooa ações a executar o cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="61624-288">Aplicar tooa uma ação de Script a executar o cluster de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="61624-289">De Olá [portal do Azure](https://portal.azure.com), selecione o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61624-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="61624-290">Na descrição geral do Olá HDInsight cluster, selecione Olá **ações de Script** mosaico.</span><span class="sxs-lookup"><span data-stu-id="61624-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Mosaico de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="61624-292">Também pode selecionar **todas as definições** e, em seguida, selecione **ações de Script** de Olá secção de definições.</span><span class="sxs-lookup"><span data-stu-id="61624-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="61624-293">Na parte superior de Olá de Olá secção ações de Script, selecione **submeter novo**.</span><span class="sxs-lookup"><span data-stu-id="61624-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Adicionar um tooa de script a executar o cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="61624-295">Olá utilize __selecionar um script__ entrada tooselect um script pré-cópia efetuado.</span><span class="sxs-lookup"><span data-stu-id="61624-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="61624-296">toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o script.</span><span class="sxs-lookup"><span data-stu-id="61624-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Adicionar um script no formulário de script selecione Olá](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="61624-298">Olá, a tabela seguinte descreve os elementos de Olá no formulário de Olá:</span><span class="sxs-lookup"><span data-stu-id="61624-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="61624-299">Propriedade</span><span class="sxs-lookup"><span data-stu-id="61624-299">Property</span></span> | <span data-ttu-id="61624-300">Valor</span><span class="sxs-lookup"><span data-stu-id="61624-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="61624-301">Selecione um script</span><span class="sxs-lookup"><span data-stu-id="61624-301">Select a script</span></span> | <span data-ttu-id="61624-302">toouse seu próprio script, selecione __personalizado__.</span><span class="sxs-lookup"><span data-stu-id="61624-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="61624-303">Caso contrário, selecione um script fornecidos.</span><span class="sxs-lookup"><span data-stu-id="61624-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="61624-304">Nome</span><span class="sxs-lookup"><span data-stu-id="61624-304">Name</span></span> |<span data-ttu-id="61624-305">Especifique um nome para a ação de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="61624-306">Scripts de bash URI</span><span class="sxs-lookup"><span data-stu-id="61624-306">Bash script URI</span></span> |<span data-ttu-id="61624-307">Especifique Olá URI toohello script que é invocada toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="61624-308">Trabalho/HEAD/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="61624-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="61624-309">Especificar Olá nós (**Head**, **trabalho**, ou **ZooKeeper**) que personalização Olá script é executado.</span><span class="sxs-lookup"><span data-stu-id="61624-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="61624-310">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="61624-310">Parameters</span></span> |<span data-ttu-id="61624-311">Especifique parâmetros de Olá, se necessário pelo script de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="61624-312">Olá utilize __manter esta ação de script__ script de Olá se toomake entrada é aplicada durante operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="61624-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="61624-313">Por último, utilize Olá **criar** o cluster de toohello do botão tooapply Olá script.</span><span class="sxs-lookup"><span data-stu-id="61624-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="61624-314">Aplicar tooa uma ação de Script a executar o cluster a partir do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61624-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="61624-315">Antes de continuar, certifique-se de que tem instalado e configurado o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61624-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="61624-316">Para obter informações sobre como configurar uma estação de trabalho toorun cmdlets do PowerShell do HDInsight, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61624-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="61624-317">Olá exemplo seguinte demonstra como tooapply um cluster em execução do script ação tooa:</span><span class="sxs-lookup"><span data-stu-id="61624-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="61624-318">Uma vez concluída a operação de Olá, receberá informações toohello semelhante, seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="61624-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="61624-319">Aplicar tooa uma ação de Script a executar o cluster de Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="61624-320">Antes de continuar, certifique-se de que instalou e configurou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="61624-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="61624-321">Para obter mais informações, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="61624-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="61624-322">tooswitch tooAzure modo Resource Manager, utilize Olá seguinte comando na linha de comandos Olá:</span><span class="sxs-lookup"><span data-stu-id="61624-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="61624-323">Utilize Olá seguir tooauthenticate tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="61624-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="61624-324">Utilize os seguintes comandos tooapply um tooa de ação de script a executar o cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="61624-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="61624-325">Se omitir parâmetros para este comando, é-lhe pedida-los.</span><span class="sxs-lookup"><span data-stu-id="61624-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="61624-326">Se Olá script especificar com `-u` aceite parâmetros, pode especificá-los utilizando Olá `-p` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="61624-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="61624-327">Os tipos de nó válido são `headnode`, `workernode`, e `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="61624-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="61624-328">Se o script de Olá deve ser aplicado toomultiple tipos de nó, especificar os tipos de Olá separados por um ';'.</span><span class="sxs-lookup"><span data-stu-id="61624-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="61624-329">Por exemplo, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="61624-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="61624-330">toopersist Olá script, adicione Olá `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="61624-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="61624-331">Pode também manter hello script mais tarde utilizando `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="61624-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="61624-332">Uma vez concluída a tarefa de Olá, receberá toohello semelhante de saída seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="61624-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="61624-333">Aplicar tooa uma ação de Script a executar o cluster utilizando a REST API</span><span class="sxs-lookup"><span data-stu-id="61624-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="61624-334">Consulte [executar ações de Script num cluster em execução](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="61624-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="61624-335">Aplicar tooa uma ação de Script a executar o cluster de Olá SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="61624-336">Para obter um exemplo de utilização Olá .NET SDK tooapply scripts tooa cluster, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="61624-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="61624-337">Ver histórico, promover e despromover ações de Script</span><span class="sxs-lookup"><span data-stu-id="61624-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="61624-338">Utilizar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="61624-339">De Olá [portal do Azure](https://portal.azure.com), selecione o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61624-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="61624-340">Na descrição geral do Olá HDInsight cluster, selecione Olá **ações de Script** mosaico.</span><span class="sxs-lookup"><span data-stu-id="61624-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Mosaico de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="61624-342">Também pode selecionar **todas as definições** e, em seguida, selecione **ações de Script** de Olá secção de definições.</span><span class="sxs-lookup"><span data-stu-id="61624-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="61624-343">Um histórico de scripts para este cluster é apresentado no Olá secção ações de Script.</span><span class="sxs-lookup"><span data-stu-id="61624-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="61624-344">Estas informações incluem uma lista de scripts persistentes.</span><span class="sxs-lookup"><span data-stu-id="61624-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="61624-345">Olá captura de ecrã abaixo, pode ver essa Olá Solr script foi executada neste cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="61624-346">Olá captura de ecrã mostra quaisquer scripts persistentes.</span><span class="sxs-lookup"><span data-stu-id="61624-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Secção de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="61624-348">A seleção de um script do histórico de Olá apresenta a secção de propriedades de Olá para este script.</span><span class="sxs-lookup"><span data-stu-id="61624-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="61624-349">De Olá parte superior do ecrã de Olá, pode voltar a executar o script de Olá ou promovê-lo.</span><span class="sxs-lookup"><span data-stu-id="61624-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Propriedades de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="61624-351">Também pode utilizar Olá **...**  toohello direito de entradas das ações do Olá ações de Script secção tooperform.</span><span class="sxs-lookup"><span data-stu-id="61624-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Ações de script... utilização](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="61624-353">Utilizar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61624-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="61624-354">Utilize o seguinte Olá...</span><span class="sxs-lookup"><span data-stu-id="61624-354">Use hello following...</span></span> | <span data-ttu-id="61624-355">demasiado...</span><span class="sxs-lookup"><span data-stu-id="61624-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="61624-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="61624-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="61624-357">Obter informações sobre ações de script persistentes</span><span class="sxs-lookup"><span data-stu-id="61624-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="61624-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="61624-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="61624-359">Obter um histórico de script ações aplicadas toohello cluster ou os detalhes para um script específico</span><span class="sxs-lookup"><span data-stu-id="61624-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="61624-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="61624-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="61624-361">Promove um ad hoc tooa de ação de script persistentes ação de script</span><span class="sxs-lookup"><span data-stu-id="61624-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="61624-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="61624-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="61624-363">Despromove uma ação do script persistentes ação tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="61624-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="61624-364">Utilizar `Remove-AzureRmHDInsightPersistedScriptAction` não anular ações Olá efetuadas por um script.</span><span class="sxs-lookup"><span data-stu-id="61624-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="61624-365">Este cmdlet apenas remove o sinalizador persistente Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="61624-366">Olá seguinte script de exemplo demonstra utilizando Olá cmdlets toopromote, em seguida, despromover um script.</span><span class="sxs-lookup"><span data-stu-id="61624-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="61624-367">Utilizar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="61624-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="61624-368">Utilize o seguinte Olá...</span><span class="sxs-lookup"><span data-stu-id="61624-368">Use hello following...</span></span> | <span data-ttu-id="61624-369">demasiado...</span><span class="sxs-lookup"><span data-stu-id="61624-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="61624-370">Obter uma lista de ações de script persistentes</span><span class="sxs-lookup"><span data-stu-id="61624-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="61624-371">Obter informações sobre uma ação de script persistentes específico</span><span class="sxs-lookup"><span data-stu-id="61624-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="61624-372">Obter um histórico de script ações aplicadas toohello cluster</span><span class="sxs-lookup"><span data-stu-id="61624-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="61624-373">Obter informações sobre uma ação de script específico</span><span class="sxs-lookup"><span data-stu-id="61624-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="61624-374">Promove um ad hoc tooa de ação de script persistentes ação de script</span><span class="sxs-lookup"><span data-stu-id="61624-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="61624-375">Despromove uma ação do script persistentes ação tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="61624-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="61624-376">Utilizar `azure hdinsight script-action persisted delete` não anular ações Olá efetuadas por um script.</span><span class="sxs-lookup"><span data-stu-id="61624-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="61624-377">Este cmdlet apenas remove o sinalizador persistente Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="61624-378">Utilizar Olá SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="61624-379">Para obter um exemplo de utilização Olá .NET SDK tooretrieve histórico de script de um cluster, promover ou despromover scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="61624-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="61624-380">Este exemplo mostra também como tooinstall uma aplicação do HDInsight utilizando Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="61624-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="61624-381">Suporte para o software de open source utilizados nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="61624-382">Olá serviço Microsoft Azure HDInsight utiliza um ecossistema de tecnologias de open source formado em torno do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="61624-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="61624-383">Microsoft Azure fornece um nível geral de suporte para tecnologias de open source.</span><span class="sxs-lookup"><span data-stu-id="61624-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="61624-384">Para obter mais informações, consulte Olá **suporte âmbito** secção Olá [site FAQ de suporte do Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="61624-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="61624-385">Olá serviço HDInsight fornece um nível adicional de suporte para componentes incorporados.</span><span class="sxs-lookup"><span data-stu-id="61624-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="61624-386">Existem dois tipos de componentes de open source que estão disponíveis no Olá serviço HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61624-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="61624-387">**Componentes incorporados** -estes componentes são previamente instalados nos clusters do HDInsight e fornecer a funcionalidade principal do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="61624-388">Por exemplo, YARN ResourceManager, idioma de consulta do Hive Olá (HiveQL) e biblioteca de Mahout Olá pertencem toothis categoria.</span><span class="sxs-lookup"><span data-stu-id="61624-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="61624-389">Uma lista completa dos componentes de cluster está disponível no [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="61624-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="61624-390">**Componentes personalizados** -, como um utilizador do cluster de Olá, pode instalar ou utilizar na sua carga de trabalho qualquer componente disponível na Comunidade Olá ou criado por si.</span><span class="sxs-lookup"><span data-stu-id="61624-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="61624-391">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados.</span><span class="sxs-lookup"><span data-stu-id="61624-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="61624-392">Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="61624-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="61624-393">Componentes personalizados recebem suporte comercialmente razoáveis toohelp toofurther poderá resolver o problema de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="61624-394">Suporte da Microsoft pode ser capaz de tooresolve problema de Olá ou poderão pedir-lhe canais disponíveis tooengage para tecnologias de código aberto olá onde se encontra profundo conhecimentos para que a tecnologia.</span><span class="sxs-lookup"><span data-stu-id="61624-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="61624-395">Por exemplo, existem vários sites de Comunidade que podem ser utilizadas, como: [fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Também projetos do Apache tem sites de projeto no [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="61624-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="61624-396">Olá serviço HDInsight fornece várias formas componentes personalizados toouse.</span><span class="sxs-lookup"><span data-stu-id="61624-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="61624-397">Olá mesmo nível de suporte aplica-se, independentemente da forma como um componente utilizado ou não está instalado no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="61624-398">Olá lista seguinte descreve formas mais comuns Olá que componentes personalizados podem ser utilizados nos clusters do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61624-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="61624-399">Submissão de tarefa - Hadoop ou outros tipos de tarefas que executarem ou utilizam componentes personalizados pode ser submetidos toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="61624-400">Personalização de cluster - durante a criação do cluster, pode especificar definições adicionais e componentes personalizados que estão instalados em nós de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="61624-401">Fornecem exemplos de como estes componentes podem ser utilizados nos clusters do HDInsight Olá amostras - para componentes personalizados populares, a Microsoft e outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="61624-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="61624-402">Estes exemplos são fornecidos sem suporte.</span><span class="sxs-lookup"><span data-stu-id="61624-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="61624-403">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="61624-403">Troubleshooting</span></span>

<span data-ttu-id="61624-404">Pode utilizar Ambari web IU tooview informações registadas pelas ações de script.</span><span class="sxs-lookup"><span data-stu-id="61624-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="61624-405">Se o script de Olá falhar durante a criação do cluster, os registos de Olá também estão disponíveis na conta do storage predefinida Olá associada ao cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="61624-406">Esta secção fornece informações sobre como tooretrieve Olá registos utilizando ambas estas opções.</span><span class="sxs-lookup"><span data-stu-id="61624-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="61624-407">Utilizar Olá IU da Web do Ambari</span><span class="sxs-lookup"><span data-stu-id="61624-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="61624-408">No seu browser, navegue até toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="61624-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="61624-409">Substitua CLUSTERNAME pelo nome de Olá do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61624-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="61624-410">Quando lhe for pedido, introduza o nome da conta de administrador Olá (administrador) e palavra-passe para o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="61624-411">Poderá ter credenciais de administrador de Olá tooreenter num formulário web.</span><span class="sxs-lookup"><span data-stu-id="61624-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="61624-412">Na barra de Olá na Olá parte superior da página Olá, selecione Olá **ops** entrada.</span><span class="sxs-lookup"><span data-stu-id="61624-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="61624-413">É apresentada uma lista de atuais e anteriores operações executadas no cluster de Olá através do Ambari.</span><span class="sxs-lookup"><span data-stu-id="61624-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Barra de IU do Ambari web com ops selecionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="61624-415">Localizar as entradas de Olá que tenham **executar\_customscriptaction** no Olá **operações** coluna.</span><span class="sxs-lookup"><span data-stu-id="61624-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="61624-416">Estas entradas são criadas quando executar ações de Script de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-416">These entries are created when hello Script Actions run.</span></span>

    ![Captura de ecrã de operações](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="61624-418">Olá tooview STDOUT e STDERR resultado. o, selecione a entrada de run\customscriptaction Olá e desagregar através de ligações de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="61624-419">Este resultado é gerado quando executa o script de Olá e pode conter informações úteis.</span><span class="sxs-lookup"><span data-stu-id="61624-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="61624-420">Registos de acesso da conta do storage predefinida Olá</span><span class="sxs-lookup"><span data-stu-id="61624-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="61624-421">Se a criação do cluster Olá falhar devido a erro de ação de script tooa, Olá registos podem ser acedidos da conta de armazenamento de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="61624-422">Olá os registos de armazenamento estão disponíveis em `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="61624-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Captura de ecrã de operações](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="61624-424">Neste diretório, Olá registos são organizados em separado para headnode, workernode e nós de zookeeper.</span><span class="sxs-lookup"><span data-stu-id="61624-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="61624-425">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="61624-425">Some examples are:</span></span>

    * <span data-ttu-id="61624-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="61624-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="61624-427">**Nó de trabalho** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="61624-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="61624-428">**Nós de zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="61624-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="61624-429">Todos os stdout e stderr do anfitrião correspondente Olá é carregado toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="61624-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="61624-430">Há um **resultado -\*. txt** e **erros -\*. txt** para cada ação de script.</span><span class="sxs-lookup"><span data-stu-id="61624-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="61624-431">ficheiro de saída *.txt Olá contém informações sobre Olá URI de script de Olá que recebeu a ser executado no anfitrião de Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="61624-432">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="61624-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="61624-433">É possível criar repetidamente um cluster de ação de script com Olá mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="61624-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="61624-434">Esse caso, poder diferenciar os registos relevantes Olá com base no nome da pasta data Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="61624-435">Por exemplo, a estrutura da pasta de Olá para um cluster (mycluster) criado em datas diferentes aparece toohello semelhante seguintes entradas de registo:</span><span class="sxs-lookup"><span data-stu-id="61624-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="61624-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="61624-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="61624-437">Se criar um cluster de ação de script com Olá mesmo nome no Olá mesmo dia, pode utilizar ficheiros de registo relevantes do Olá prefixo exclusivo tooidentify Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="61624-438">Se criar um cluster quase 12:00:00 (meia-noite), é possível que os ficheiros de registo Olá span em dois dias.</span><span class="sxs-lookup"><span data-stu-id="61624-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="61624-439">Nestes casos, verá duas pastas data diferente para Olá mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="61624-440">Carregamento contentor de predefinido do toohello de ficheiros de registo pode demorar até too5 minutos, especialmente para grandes clusters.</span><span class="sxs-lookup"><span data-stu-id="61624-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="61624-441">Por isso, se pretender que os registos de Olá tooaccess, não deverá imediatamente Eliminar cluster Olá se falhar de uma ação de script.</span><span class="sxs-lookup"><span data-stu-id="61624-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="61624-442">Watchdog do Ambari</span><span class="sxs-lookup"><span data-stu-id="61624-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="61624-443">Não altere Olá palavra-passe para Olá Ambari watchdog do (hdinsightwatchdog) no cluster do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="61624-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="61624-444">A alteração Olá palavra-passe para esta conta de quebras de ações de script Olá capacidade toorun novo num cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="61624-445">Não é possível importar o nome BlobService</span><span class="sxs-lookup"><span data-stu-id="61624-445">Can't import name BlobService</span></span>

<span data-ttu-id="61624-446">__Sintomas__: Olá falha de ação de script.</span><span class="sxs-lookup"><span data-stu-id="61624-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="61624-447">Toohello semelhante de texto seguinte erro é apresentado quando visualizar operação Olá no Ambari:</span><span class="sxs-lookup"><span data-stu-id="61624-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="61624-448">__Causa__: Este erro ocorre se atualizar o cliente de armazenamento do Azure de Python Olá que está incluída no cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="61624-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="61624-449">HDInsight espera que o cliente de armazenamento do Azure 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="61624-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="61624-450">__Resolução__: tooresolve este erro, manualmente estabeleçam ligação através do nó de cluster da tooeach `ssh` e versão de cliente de armazenamento correta do comando tooreinstall Olá Olá utilize os seguintes:</span><span class="sxs-lookup"><span data-stu-id="61624-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="61624-451">Para obter informações sobre a ligação toohello cluster com SSH, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="61624-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="61624-452">Histórico não mostra scripts utilizados durante a criação do cluster</span><span class="sxs-lookup"><span data-stu-id="61624-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="61624-453">Se o cluster foi criado antes de 15 de Março de 2016, não poderá ver uma entrada no histórico de ação de Script.</span><span class="sxs-lookup"><span data-stu-id="61624-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="61624-454">Se redimensionar cluster Olá após 15 de Março de 2016, os scripts de Olá com durante a criação do cluster são apresentados no histórico de como estas são aplicadas toonew nós no cluster de Olá como parte da Olá redimensionar a operação.</span><span class="sxs-lookup"><span data-stu-id="61624-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="61624-455">Existem duas exceções:</span><span class="sxs-lookup"><span data-stu-id="61624-455">There are two exceptions:</span></span>

* <span data-ttu-id="61624-456">Se o cluster foi criado antes de 1 de Setembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="61624-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="61624-457">Esta data é quando foram introduzidas ações de Script.</span><span class="sxs-lookup"><span data-stu-id="61624-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="61624-458">Qualquer cluster criado antes desta data não foi ter utilizar ações de Script para a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="61624-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="61624-459">Se utilizar várias ações de Script durante a criação do cluster e utilizado Olá mesmo nome para vários scripts ou Olá mesmo nome, mesmo URI, mas parâmetros diferentes de vários scripts.</span><span class="sxs-lookup"><span data-stu-id="61624-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="61624-460">Nestes casos, receberá Olá seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="61624-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="61624-461">Não existe nenhum script de nova ações podem ser executadas neste cluster devido a nomes do script tooconflicting em scripts existentes.</span><span class="sxs-lookup"><span data-stu-id="61624-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="61624-462">Nomes do script fornecidos no cluster criar tem de ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="61624-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="61624-463">Os scripts existentes são executadas no redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="61624-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61624-464">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="61624-464">Next steps</span></span>

* [<span data-ttu-id="61624-465">Desenvolver scripts de ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="61624-466">Instalar e utilizar Solr nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="61624-467">Instalar e utilizar Giraph nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61624-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="61624-468">Adicionar o cluster de HDInsight tooan armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="61624-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fases durante a criação do cluster"
