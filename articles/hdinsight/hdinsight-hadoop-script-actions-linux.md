---
title: "desenvolvimento de ações de aaaScript com o HDInsight baseado em Linux - Azure | Microsoft Docs"
description: "Saiba como toouse Bash scripts toocustomize clusters do HDInsight baseado em Linux. funcionalidade de ação de script de Olá do HDInsight permite-lhe toorun scripts durante ou após a criação do cluster. Scripts podem ser utilizado toochange definições de configuração de cluster ou instalar software adicional."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="f4b0e-105">Desenvolvimento de ações de script com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-105">Script action development with HDInsight</span></span>

<span data-ttu-id="f4b0e-106">Saiba como utilizar o cluster do HDInsight Bash toocustomize scripts.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="f4b0e-107">Ações de script são uma forma toocustomize HDInsight durante ou após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4b0e-108">passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Linux.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="f4b0e-109">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f4b0e-110">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="f4b0e-111">Quais são as ações de script</span><span class="sxs-lookup"><span data-stu-id="f4b0e-111">What are script actions</span></span>

<span data-ttu-id="f4b0e-112">Ações de script são scripts de Bash Azure é executado na Olá cluster nós toomake as alterações de configuração ou instale o software.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="f4b0e-113">Uma ação de script é executada como raiz e fornece acesso total de nós de cluster toohello direitos.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="f4b0e-114">Ações de script podem ser aplicadas através de Olá seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="f4b0e-115">Utilize este método tooapply um script...</span><span class="sxs-lookup"><span data-stu-id="f4b0e-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="f4b0e-116">Durante a criação de cluster...</span><span class="sxs-lookup"><span data-stu-id="f4b0e-116">During cluster creation...</span></span> | <span data-ttu-id="f4b0e-117">Num cluster em execução...</span><span class="sxs-lookup"><span data-stu-id="f4b0e-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="f4b0e-118">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f4b0e-118">Azure portal</span></span> |<span data-ttu-id="f4b0e-119">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-119">✓</span></span> |<span data-ttu-id="f4b0e-120">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-120">✓</span></span> |
| <span data-ttu-id="f4b0e-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4b0e-121">Azure PowerShell</span></span> |<span data-ttu-id="f4b0e-122">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-122">✓</span></span> |<span data-ttu-id="f4b0e-123">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-123">✓</span></span> |
| <span data-ttu-id="f4b0e-124">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f4b0e-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="f4b0e-125">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-125">✓</span></span> |
| <span data-ttu-id="f4b0e-126">SDK de .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="f4b0e-127">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-127">✓</span></span> |<span data-ttu-id="f4b0e-128">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-128">✓</span></span> |
| <span data-ttu-id="f4b0e-129">Modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f4b0e-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="f4b0e-130">✓</span><span class="sxs-lookup"><span data-stu-id="f4b0e-130">✓</span></span> |&nbsp; |

<span data-ttu-id="f4b0e-131">Para obter mais informações sobre como utilizar estas ações de script de tooapply métodos, consulte [HDInsight personalizar clusters com ações de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="f4b0e-132"><a name="bestPracticeScripting"></a>Melhores práticas para o desenvolvimento do script</span><span class="sxs-lookup"><span data-stu-id="f4b0e-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="f4b0e-133">Quando desenvolver um script personalizado para um cluster do HDInsight, existem várias tookeep práticas melhor em mente:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="f4b0e-134">Versão do destino Olá Hadoop</span><span class="sxs-lookup"><span data-stu-id="f4b0e-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="f4b0e-135">Destino Olá versão do SO</span><span class="sxs-lookup"><span data-stu-id="f4b0e-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="f4b0e-136">Fornecer estável liga tooscript recursos</span><span class="sxs-lookup"><span data-stu-id="f4b0e-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="f4b0e-137">Utilizar recursos previamente compilados</span><span class="sxs-lookup"><span data-stu-id="f4b0e-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="f4b0e-138">Certifique-se de que o script de personalização do cluster Olá é idempotent</span><span class="sxs-lookup"><span data-stu-id="f4b0e-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="f4b0e-139">Certifique-se de elevada disponibilidade da arquitetura de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="f4b0e-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="f4b0e-140">Configurar Olá componentes personalizados toouse Blob storage do Azure</span><span class="sxs-lookup"><span data-stu-id="f4b0e-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="f4b0e-141">Escrever informações tooSTDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="f4b0e-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="f4b0e-142">Guardar ficheiros como ASCII com endings de linha de LF</span><span class="sxs-lookup"><span data-stu-id="f4b0e-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="f4b0e-143">Utilizar toorecover de lógica de repetição de erros transitórios</span><span class="sxs-lookup"><span data-stu-id="f4b0e-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="f4b0e-144">Ações de script tem de concluir dentro de 60 minutos ou processo Olá falha.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="f4b0e-145">Durante o aprovisionamento de nó, executar script de Olá simultaneamente com outros processos de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="f4b0e-146">Disputa pelos recursos, tais como a largura de banda de CPU, tempo ou de rede pode fazer com que Olá script tootake mais toofinish que-lo no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="f4b0e-147"><a name="bPS1"></a>Versão do destino Olá Hadoop</span><span class="sxs-lookup"><span data-stu-id="f4b0e-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="f4b0e-148">Versões diferentes do HDInsight têm versões diferentes dos serviços de Hadoop e componentes instalados.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="f4b0e-149">Se o script espera uma versão específica de um serviço ou componente, só deve utilizar o script de Olá com a versão de Olá do HDInsight que inclui os componentes de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="f4b0e-150">Pode encontrar informações sobre versões de componentes incluídos com o HDInsight utilizando Olá [controlo de versões do HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="f4b0e-151"><a name="bps10"></a>Versão de SO de Olá de destino</span><span class="sxs-lookup"><span data-stu-id="f4b0e-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="f4b0e-152">HDInsight baseado em Linux baseia Olá distribuição Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="f4b0e-153">Versões diferentes do HDInsight baseiam-se em diferentes versões do Ubuntu, que pode alterar a forma como se comporta seu script.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="f4b0e-154">Por exemplo, o HDInsight 3.4 e anterior baseiam-se em versões do Ubuntu que utilizam Upstart.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="f4b0e-155">Baseia-se no Ubuntu 16.04, que utiliza Systemd versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="f4b0e-156">Systemd e Upstart dependem comandos diferentes, pelo que o seu script deve ser escrito toowork com ambos.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="f4b0e-157">Outra diferença importante entre HDInsight 3.4 e 3.5 é que `JAVA_HOME` agora pontos tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="f4b0e-158">Pode verificar a versão de SO de Olá utilizando `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="f4b0e-159">Olá código seguinte demonstra como toodetermine se hello do script está em execução no Ubuntu 14 ou 16:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="f4b0e-160">Pode localizar o script de completo de Olá que contenha estes fragmentos em https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="f4b0e-161">Para a versão de Olá do Ubuntu que é utilizado pelo HDInsight, consulte Olá [versão do componente de HDInsight](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="f4b0e-162">toounderstand Olá diferenças Systemd e Upstart, consulte [Systemd para utilizadores Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="f4b0e-163"><a name="bPS2"></a>Fornecer estável liga tooscript recursos</span><span class="sxs-lookup"><span data-stu-id="f4b0e-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="f4b0e-164">Olá script e de recursos associados têm de permanecer disponíveis em toda a duração de Olá do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="f4b0e-165">Estes recursos são necessários se novos nós são adicionados toohello cluster durante operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="f4b0e-166">melhor prática de Olá é toodownload e arquivar tudo numa conta do Storage do Azure na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4b0e-167">conta de armazenamento de Olá utilizada tem de ser Olá conta do storage predefinida para o cluster de Olá ou um contentor público só de leitura em qualquer outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="f4b0e-168">Por exemplo, os exemplos de Olá fornecidos pela Microsoft são armazenados no Olá [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="f4b0e-169">Este é um contentor público só de leitura mantido pela equipa do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="f4b0e-170"><a name="bPS4"></a>Utilizar recursos previamente compilados</span><span class="sxs-lookup"><span data-stu-id="f4b0e-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="f4b0e-171">Olá tooreduce tempo demora toorun Olá script, evite operações compilam recursos a partir do código de origem.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="f4b0e-172">Por exemplo, a pré-compilar recursos e armazená-las num blob Storage do Azure de conta no Olá mesmo centro de dados como o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="f4b0e-173"><a name="bPS3"></a>Certifique-se de que o script de personalização do cluster Olá é idempotent</span><span class="sxs-lookup"><span data-stu-id="f4b0e-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="f4b0e-174">Scripts tem de ser idempotent.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-174">Scripts must be idempotent.</span></span> <span data-ttu-id="f4b0e-175">Se o script de Olá é executada várias vezes, deverá devolver Olá toohello cluster mesmo Estado de cada vez.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="f4b0e-176">Por exemplo, um script que modifica os ficheiros de configuração deve não adicionar as entradas duplicadas se executada várias vezes.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="f4b0e-177"><a name="bPS5"></a>Certifique-se de elevada disponibilidade da arquitetura de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="f4b0e-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="f4b0e-178">Clusters do HDInsight baseado em Linux fornecem dois nós principais que estão ativas num cluster de Olá e executam ações de script em ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="f4b0e-179">Se os componentes de Olá que instalar esperam apenas um nó principal, não instale componentes Olá em ambos os nós principais.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4b0e-180">Serviços fornecidos como parte do HDInsight são toofail concebida entre dois nós principais de Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="f4b0e-181">Esta funcionalidade não é prolongada componentes toocustom instalados através de ações de script.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="f4b0e-182">Se necessitar de elevada disponibilidade de componentes personalizados, tem de implementar o seus próprios mecanismo de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="f4b0e-183"><a name="bPS6"></a>Configurar Olá componentes personalizados toouse Blob storage do Azure</span><span class="sxs-lookup"><span data-stu-id="f4b0e-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="f4b0e-184">Os componentes que instalar num cluster de Olá poderão ter uma configuração predefinida, que utiliza armazenamento distribuído ficheiro sistema Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="f4b0e-185">O HDInsight utiliza o armazenamento do Azure ou para o Data Lake Store como armazenamento de predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="f4b0e-186">Ambos fornecem um sistema de ficheiros compatíveis do HDFS que mantém os dados, mesmo se o cluster de Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="f4b0e-187">Poderá ser necessário componentes tooconfigure instalar toouse WASB ou ADL em vez do HDFS.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="f4b0e-188">Na maioria das operações, não terá de sistema de ficheiros de Olá toospecify.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="f4b0e-189">Por exemplo, o seguinte Olá copia o ficheiro de giraph examples.jar de Olá do armazenamento de toocluster do sistema de ficheiros local Olá:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="f4b0e-190">Neste exemplo, Olá `hdfs` comando utiliza o armazenamento de cluster predefinido de Olá transparente.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="f4b0e-191">Para algumas operações, poderá ser necessário toospecify Olá URI.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="f4b0e-192">Por exemplo, `adl:///example/jars` para o Data Lake Store ou `wasb:///example/jars` para armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="f4b0e-193"><a name="bPS7"></a>Escrever informações tooSTDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="f4b0e-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="f4b0e-194">HDInsight regista a saída do script que é escrito tooSTDOUT e STDERR.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="f4b0e-195">Pode ver estas informações através da web do Ambari Olá IU.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="f4b0e-196">Ambari só está disponível se o cluster de Olá é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="f4b0e-197">Se utilizar uma ação de script durante a criação do cluster e a criação falhar, consulte Olá secção de resolução de problemas [clusters do HDInsight de personalizar através da ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para outras formas de aceder a informações com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="f4b0e-198">A maioria dos utilitários e pacotes de instalação já escrever informações tooSTDOUT e STDERR, no entanto, poderá pretender que o registo adicional tooadd.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="f4b0e-199">toosend texto tooSTDOUT, utilize `echo`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="f4b0e-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="f4b0e-201">Por predefinição, `echo` envia Olá tooSTDOUT de cadeia.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="f4b0e-202">toodirect-tooSTDERR, adicionar `>&2` antes `echo`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="f4b0e-203">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="f4b0e-204">Isto redireciona informações escritas em vez disso, tooSTDOUT tooSTDERR (2).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="f4b0e-205">Para obter mais informações sobre o redirecionamento de e/s, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="f4b0e-206">Para obter mais informações sobre a visualização de informações registadas pelas ações de script, consulte [clusters do HDInsight de personalizar através da ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="f4b0e-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="f4b0e-207"><a name="bps8"></a>Guardar ficheiros como ASCII com endings de linha de LF</span><span class="sxs-lookup"><span data-stu-id="f4b0e-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="f4b0e-208">Scripts de bash devem ser armazenados em formato ASCII, com linhas terminadas por LF.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="f4b0e-209">Os ficheiros que são armazenados como UTF-8 ou utilizam CRLF como o fim de linha de Olá poderão falhar com Olá seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="f4b0e-210"><a name="bps9"></a>Utilizar toorecover de lógica de repetição de erros transitórios</span><span class="sxs-lookup"><span data-stu-id="f4b0e-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="f4b0e-211">Quando a transferência de ficheiros, instalando pacotes com apt get ou outras ações que transmitem dados através de Olá internet, a ação de Olá poderão falhar devido a erros de rede tootransient.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="f4b0e-212">Por exemplo, recurso remoto Olá que estão a comunicar com poderá estar em processo Olá falha de ativação pós-falha de nó tooa de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="f4b0e-213">toomake os erros de script de tootransient resiliente, pode implementar a lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="f4b0e-214">Olá seguinte função demonstra como tooimplement repetir lógica.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="f4b0e-215">Repetir a operação de Olá três vezes antes de falhar.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="f4b0e-216">Olá exemplos seguintes demonstram como toouse esta função.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="f4b0e-217"><a name="helpermethods"></a>Métodos de programa auxiliar para scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="f4b0e-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="f4b0e-218">Métodos de programa auxiliar de ação de script são utilitários que pode utilizar ao escrever scripts personalizados.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="f4b0e-219">Estes métodos estão contidos no[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="f4b0e-220">Utilizar Olá seguir toodownload e utilizá-los como parte do seu script:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="f4b0e-221">Olá programas de ajuda disponíveis para utilização no seu script a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="f4b0e-222">Utilização de programa auxiliar</span><span class="sxs-lookup"><span data-stu-id="f4b0e-222">Helper usage</span></span> | <span data-ttu-id="f4b0e-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="f4b0e-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="f4b0e-224">Transfere um ficheiro a partir do caminho do ficheiro especificado toohello Olá origem URI.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="f4b0e-225">Por predefinição, este não substituir ficheiro existente.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="f4b0e-226">Extrai um ficheiro de tar (utilizando `-xf`) toohello diretório de destino.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="f4b0e-227">Se executou num nó principal do cluster, 1 retorno; caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="f4b0e-228">Se o nó atual Olá é um nó de dados (trabalho), devolver um 1; caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="f4b0e-229">Se o nó atual Olá é os dados de primeiro Olá (trabalho) nó (denominado workernode0) devolver um 1; caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="f4b0e-230">Devolva o nome de domínio completamente qualificado Olá de Olá headnodes num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="f4b0e-231">Os nomes são delimitados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-231">Names are comma delimited.</span></span> <span data-ttu-id="f4b0e-232">Uma cadeia vazia, é devolvida com o erro.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="f4b0e-233">Obtém o nome de domínio completamente qualificado Olá de headnode primário Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="f4b0e-234">Uma cadeia vazia, é devolvida com o erro.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="f4b0e-235">Obtém o nome de domínio completamente qualificado Olá de headnode secundário Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="f4b0e-236">Uma cadeia vazia, é devolvida com o erro.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="f4b0e-237">Obtém o sufixo numérico Olá headnode primário Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="f4b0e-238">Uma cadeia vazia, é devolvida com o erro.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="f4b0e-239">Obtém o sufixo numérico Olá headnode secundário Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="f4b0e-240">Uma cadeia vazia, é devolvida com o erro.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="f4b0e-241"><a name="commonusage"></a>Padrões de utilização comuns</span><span class="sxs-lookup"><span data-stu-id="f4b0e-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="f4b0e-242">Esta secção fornece orientação na implementação de algumas das Olá comuns padrões de utilização que possam ser executadas ao escrever o seu próprio script personalizado.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="f4b0e-243">Os parâmetros a transmitir tooa script</span><span class="sxs-lookup"><span data-stu-id="f4b0e-243">Passing parameters tooa script</span></span>

<span data-ttu-id="f4b0e-244">Em alguns casos, o script pode necessitar de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="f4b0e-245">Por exemplo, poderá ter palavra-passe de administrador de Olá para cluster Olá quando utilizar Olá API de REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="f4b0e-246">Os parâmetros transmitidos toohello script são conhecidos como *parâmetros posicionais*e são atribuídos demasiado`$1` para o primeiro parâmetro Olá, `$2` para Olá segundo e, de modo-no.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="f4b0e-247">`$0`contém o nome de Olá do script Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="f4b0e-248">Valores transmitidos toohello script como parâmetros devem estar entre símbolos por plicas (').</span><span class="sxs-lookup"><span data-stu-id="f4b0e-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="f4b0e-249">Se o fizer, assegura que Olá transmitido valor é tratado como um literal.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="f4b0e-250">Definir variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="f4b0e-250">Setting environment variables</span></span>

<span data-ttu-id="f4b0e-251">Definir uma variável de ambiente é realizado Olá a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="f4b0e-252">Onde VARIABLENAME é o nome de Olá da variável de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="f4b0e-253">utilização de variáveis, de Olá tooaccess `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="f4b0e-254">Por exemplo, tooassign um valor fornecido por um parâmetro posicional como uma variável de ambiente com o nome palavra-passe, teria de utilizar Olá a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="f4b0e-255">Depois, pode utilizar informações de toohello acesso subsequentes `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="f4b0e-256">Variáveis de ambiente definidas dentro do script Olá só existem no âmbito de Olá do script Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="f4b0e-257">Em alguns casos, poderá ter de variáveis de ambiente em todo o sistema de tooadd serão mantidas após terminar o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="f4b0e-258">as variáveis de ambiente em todo o sistema tooadd, adicione a variável de Olá demasiado`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="f4b0e-259">Por exemplo, Olá a seguinte instrução adiciona `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="f4b0e-260">Toolocations acesso onde estão armazenados os scripts personalizados Olá</span><span class="sxs-lookup"><span data-stu-id="f4b0e-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="f4b0e-261">Scripts utilizadas toocustomize um cluster precisa toobe armazenado dos Olá seguintes localizações:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="f4b0e-262">Um __conta de armazenamento do Azure__ que está associado ao cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="f4b0e-263">Um __conta de armazenamento adicional__ associados ao cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="f4b0e-264">A __URI legível publicamente__.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-264">A __publicly readable URI__.</span></span> <span data-ttu-id="f4b0e-265">Por exemplo, um toodata URL armazenado no OneDrive, Dropbox ou outros ficheiros que aloja o serviço.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="f4b0e-266">Um __conta do Azure Data Lake Store__ que está associado ao cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="f4b0e-267">Para obter mais informações sobre como utilizar o Azure Data Lake Store com o HDInsight, consulte [criar um cluster do HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f4b0e-268">Olá serviço principal HDInsight utiliza tooaccess Data Lake Store tem de ter acesso de leitura toohello script.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="f4b0e-269">Recursos utilizados pelo script de Olá também tem de ser publicamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="f4b0e-270">Armazenamento de ficheiros de Olá numa conta do Storage do Azure ou do Azure Data Lake Store fornece acesso rápido, como ambas no Olá rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="f4b0e-271">Olá URI formato utilizado tooreference Olá script difere dependendo do serviço de Olá que está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="f4b0e-272">Para contas de armazenamento associadas ao cluster de HDInsight Olá, utilize `wasb://` ou `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="f4b0e-273">Para os URIs legíveis publicamente, utilize `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="f4b0e-274">Para o Data Lake Store, utilize `adl://`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="f4b0e-275">A verificar a versão do sistema operativo Olá</span><span class="sxs-lookup"><span data-stu-id="f4b0e-275">Checking hello operating system version</span></span>

<span data-ttu-id="f4b0e-276">Versões diferentes do HDInsight dependem de versões específicas do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="f4b0e-277">Poderão existir diferenças entre versões de SO que tem de verificar no script.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="f4b0e-278">Por exemplo, poderá ter tooinstall um binário que é uma versão de Ubuntu toohello associada.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="f4b0e-279">versão de SO de Olá toocheck, utilize `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="f4b0e-280">Por exemplo, Olá seguinte script demonstra como tooreference um tar específica de ficheiros, dependendo da versão do SO de Olá:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="f4b0e-281"><a name="deployScript"></a>Lista de verificação para implementar uma ação de script</span><span class="sxs-lookup"><span data-stu-id="f4b0e-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="f4b0e-282">Eis os passos de Olá que pegámos quando preparar toodeploy estes scripts:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="f4b0e-283">Colocar os ficheiros de Olá que contêm os scripts personalizados do Olá num local que esteja acessível a nós de cluster Olá durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="f4b0e-284">Por exemplo, Olá predefinido armazenamento Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="f4b0e-285">Ficheiros também podem ser armazenados nos serviços de alojamento legíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="f4b0e-286">Certifique-se de que o script de Olá é impotent.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="f4b0e-287">Se o fizer, permite Olá script toobe executada várias vezes no Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="f4b0e-288">Utilize Olá de tookeep um ficheiro temporário diretório /tmp dos ficheiros utilizados pelos scripts de Olá transferidos e, em seguida, limpe-los depois de tem executado scripts.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="f4b0e-289">Se as definições de nível de SO ou ficheiros de configuração de serviço do Hadoop são alterados, pretende toorestart HDInsight serviços.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="f4b0e-290"><a name="runScriptAction"></a>Como toorun uma ação de script</span><span class="sxs-lookup"><span data-stu-id="f4b0e-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="f4b0e-291">Pode utilizar o script ações toocustomize clusters do HDInsight utilizando Olá seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="f4b0e-292">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f4b0e-292">Azure portal</span></span>
* <span data-ttu-id="f4b0e-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4b0e-293">Azure PowerShell</span></span>
* <span data-ttu-id="f4b0e-294">Modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f4b0e-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="f4b0e-295">Olá SDK .NET do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="f4b0e-296">Para obter mais informações sobre como utilizar cada método, consulte [como toouse script ação](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="f4b0e-297"><a name="sampleScripts"></a>Exemplos de script personalizado</span><span class="sxs-lookup"><span data-stu-id="f4b0e-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="f4b0e-298">A Microsoft fornece scripts de exemplo tooinstall componentes num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="f4b0e-299">Consulte as seguintes ligações para mais ações de script de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="f4b0e-300">Instalar e utilizar Hue nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="f4b0e-301">Instalar e utilizar Solr nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="f4b0e-302">Instalar e utilizar Giraph nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="f4b0e-303">Instalar ou atualizar Mono nos clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="f4b0e-304">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="f4b0e-304">Troubleshooting</span></span>

<span data-ttu-id="f4b0e-305">Olá, são erros que poderá encontrar ao utilizar scripts que criou:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="f4b0e-306">**Erro**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="f4b0e-307">Por vezes, seguido de `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="f4b0e-308">*Causa*: Este erro é causado quando terminar de linhas de Olá num script com CRLF.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="f4b0e-309">Sistemas UNIX esperam LF apenas como o fim de linha de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="f4b0e-310">Este problema ocorre frequentemente quando script Olá foi criado no ambiente do Windows, como CRLF é uma linha comuns final para muitos editores de texto no Windows.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="f4b0e-311">*Resolução*: se for uma opção no seu editor de texto, selecione o formato Unix ou LF para o fim de linha de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="f4b0e-312">Também pode utilizar os seguintes comandos no Unix sistema toochange Olá CRLF tooan LF de Olá:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="f4b0e-313">Olá comandos seguintes são quase equivalentes nessa Olá CRLF linha endings tooLF deve ser alterado.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="f4b0e-314">Selecione um com base no utilitários Olá disponíveis no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="f4b0e-315">Comando</span><span class="sxs-lookup"><span data-stu-id="f4b0e-315">Command</span></span> | <span data-ttu-id="f4b0e-316">Notas</span><span class="sxs-lookup"><span data-stu-id="f4b0e-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="f4b0e-317">ficheiro original Olá cópias de segurança com um. Extensão BAK</span><span class="sxs-lookup"><span data-stu-id="f4b0e-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="f4b0e-318">OUTFILE contém uma versão com apenas os endings LF</span><span class="sxs-lookup"><span data-stu-id="f4b0e-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="f4b0e-319">Modifica o ficheiro de Olá diretamente</span><span class="sxs-lookup"><span data-stu-id="f4b0e-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="f4b0e-320">OUTFILE contém uma versão com apenas os endings LF.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="f4b0e-321">**Erro**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="f4b0e-322">*Causa*: Este erro ocorre quando hello script foi guardado como UTF-8 com uma marca de ordem de bytes (LM).</span><span class="sxs-lookup"><span data-stu-id="f4b0e-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="f4b0e-323">*Resolução*: guardar o ficheiro de Olá ou como ASCII ou UTF-8 sem um LM.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="f4b0e-324">Também pode utilizar os seguintes comandos num toocreate de sistema Linux ou Unix um ficheiro sem Olá LM de Olá:</span><span class="sxs-lookup"><span data-stu-id="f4b0e-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="f4b0e-325">Substitua `INFILE` com o ficheiro de Olá contendo Olá LM.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="f4b0e-326">`OUTFILE`deve ser um novo nome de ficheiro, que contém o script de Olá sem Olá LM.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="f4b0e-327"><a name="seeAlso"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f4b0e-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="f4b0e-328">Saiba como demasiado[clusters do HDInsight de personalizar através da ação de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="f4b0e-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="f4b0e-329">Olá utilize [referência do SDK .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) toolearn mais sobre como criar aplicações de .NET que gerem o HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4b0e-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="f4b0e-330">Olá utilize [API de REST do HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn como clusters toouse REST tooperform as ações de gestão no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4b0e-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
