---
title: "aaaCreate autónoma do cluster com as VMs do Azure com o Windows | Microsoft Docs"
description: "Saiba como toocreate e gerir um cluster do Service Fabric do Azure em máquinas virtuais do Azure com o Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="a27e7-103">Criar um cluster do Service Fabric autónomo três nó máquinas virtuais do Azure com o Windows Server</span><span class="sxs-lookup"><span data-stu-id="a27e7-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="a27e7-104">Este artigo descreve como toocreate um cluster baseado no Windows Azure máquinas virtuais (VMs), utilizando Olá instalador autónomo do Service Fabric para Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a27e7-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="a27e7-105">cenário de Olá é num caso especial de [criar e gerir um cluster em execução no Windows Server](service-fabric-cluster-creation-for-windows-server.md) onde são Olá VMs [VMs do Azure com o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json); no entanto, não estiver a criar [do Azure cluster do Service Fabric baseado na nuvem](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a27e7-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="a27e7-106">distinção Olá nos seguintes este padrão é esse cluster do Service Fabric Olá autónomo criado pelo Olá os seguintes passos completamente gerido por si, enquanto Olá clusters do Azure Service Fabric baseado na nuvem são geridos e atualizado pela Olá Service Fabric fornecedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="a27e7-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="a27e7-107">Cluster do passos toocreate Olá autónomo</span><span class="sxs-lookup"><span data-stu-id="a27e7-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="a27e7-108">Inicie sessão toohello portal do Azure e criar um novo Datacenter do Windows Server 2012 R2 ou VM do Windows Server 2016 Centro de dados num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a27e7-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="a27e7-109">Artigo de Olá leitura [criar uma VM do Windows no portal do Azure de Olá](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a27e7-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="a27e7-110">Adicionar alguns toohello VMs mais mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a27e7-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="a27e7-111">Certifique-se de que cada um dos Olá VMs tem Olá mesmo nome de utilizador de administrador e palavra-passe quando o criou.</span><span class="sxs-lookup"><span data-stu-id="a27e7-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="a27e7-112">Depois de criada, deve ver todas as três VMs no Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a27e7-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="a27e7-113">Ligar tooeach de Olá VMs balanceado, desligando Olá Firewall do Windows utilizando Olá [Gestor de servidores, o dashboard do servidor Local](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="a27e7-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="a27e7-114">Isto garante que o tráfego de rede Olá pode comunicar entre máquinas Olá.</span><span class="sxs-lookup"><span data-stu-id="a27e7-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="a27e7-115">Enquanto máquina tooeach ligado, obter o endereço IP de Olá, abrir uma linha de comandos e digitar `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="a27e7-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="a27e7-116">Em alternativa, pode ver Olá IP endereço de cada máquina no portal de Olá, selecionando o recurso de rede virtual Olá Olá grupo de recursos e a verificação de interfaces de rede de Olá criadas para cada uma destas máquinas.</span><span class="sxs-lookup"><span data-stu-id="a27e7-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="a27e7-117">Ligue tooone de Olá VMs e teste que pode enviar ping Olá as outras duas VMs com êxito.</span><span class="sxs-lookup"><span data-stu-id="a27e7-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="a27e7-118">Ligar tooone de Olá VMs e [transferir pacotes de Service Fabric Olá autónomo para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) para uma nova pasta no Olá máquina e extrair Olá pacote.</span><span class="sxs-lookup"><span data-stu-id="a27e7-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="a27e7-119">Abra Olá *ClusterConfig.Unsecure.MultiMachine.json* ficheiro no bloco de notas e editar cada nó com Olá três endereços IP Olá.</span><span class="sxs-lookup"><span data-stu-id="a27e7-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="a27e7-120">Alterar o nome do cluster Olá na parte superior do Olá e guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="a27e7-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="a27e7-121">Um exemplo parcial Olá do manifesto do cluster é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a27e7-121">A partial example of hello cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="a27e7-122">Se tenciona este toobe um cluster seguro, decidir a medida de segurança de Olá teria como toouse e siga os passos de Olá em Olá associado à ligação: [certificados X509](service-fabric-windows-cluster-x509-security.md) ou [segurança do Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="a27e7-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="a27e7-123">Se configurar o cluster de Olá através de segurança do Windows, terá de tooset segurança um toomanage de controlador de domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a27e7-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="a27e7-124">Tenha em atenção que utilizar um computador de controlador de domínio como um recurso de infraestrutura do serviço de nó não é suportado.</span><span class="sxs-lookup"><span data-stu-id="a27e7-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="a27e7-125">Abra um [janela ISE do PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="a27e7-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="a27e7-126">Navegue toohello pasta onde extraiu o pacote de instalador do Olá autónomo transferido e guardado Olá ficheiro de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="a27e7-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="a27e7-127">Execute Olá seguir o cluster de Olá de toodeploy de comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a27e7-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="a27e7-128">script de Olá remotamente irá configurar o cluster do Service Fabric Olá e deve comunica o progresso como faz o através da implementação.</span><span class="sxs-lookup"><span data-stu-id="a27e7-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="a27e7-129">Após sobre um minuto, pode verificar se o cluster de Olá está operacional ligando toohello Service Fabric Explorer através de um IP da máquina de Olá endereços, por exemplo, utilizando `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="a27e7-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a27e7-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a27e7-130">Next steps</span></span>
* [<span data-ttu-id="a27e7-131">Create standalone Service Fabric clusters on Windows Server or Linux (Criar clusters autónomos do Service Fabric no Windows Server ou no Linux)</span><span class="sxs-lookup"><span data-stu-id="a27e7-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="a27e7-132">Adicionar ou remover cluster do Service Fabric nós tooa autónomo</span><span class="sxs-lookup"><span data-stu-id="a27e7-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="a27e7-133">Definições de configuração do cluster do Windows autónomo</span><span class="sxs-lookup"><span data-stu-id="a27e7-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="a27e7-134">Proteger um cluster autónomo no Windows com segurança do Windows</span><span class="sxs-lookup"><span data-stu-id="a27e7-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="a27e7-135">Proteger um cluster autónomo no Windows utilizando X509 certificados</span><span class="sxs-lookup"><span data-stu-id="a27e7-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

