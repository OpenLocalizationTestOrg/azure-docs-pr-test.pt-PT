---
title: cluster aaaSubmit tarefas tooan pacote HPC no Azure | Microsoft Docs
description: "Saiba como tooset um toosubmit de computador no local de cópia de segurança das tarefas de cluster HPC Pack de tooan no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="89996-103">Submeter tarefas HPC de um cluster HPC Pack do local no computador tooan implementado no Azure</span><span class="sxs-lookup"><span data-stu-id="89996-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="89996-104">Configurar um local no cliente computador toosubmit tarefas tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster no Azure.</span><span class="sxs-lookup"><span data-stu-id="89996-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="89996-105">Este artigo mostra como tooset cópias de segurança num computador local com o cliente ferramentas toosubmit tarefa através de cluster toohello HTTPS no Azure.</span><span class="sxs-lookup"><span data-stu-id="89996-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="89996-106">Desta forma, vários utilizadores do cluster podem submeter tarefas tooa baseado na nuvem HPC Pack cluster, mas sem ligar diretamente o nó principal do toohello VM ou aceder a uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="89996-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Submeter um cluster de tooa tarefa no Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="89996-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89996-108">Prerequisites</span></span>
* <span data-ttu-id="89996-109">**Nó principal HPC Pack implementado na VM do Azure** -é recomendável que utilize ferramentas automatizadas, tais como um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) ou um [script do PowerShell do Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nó principal do toodeploy Olá e cluster.</span><span class="sxs-lookup"><span data-stu-id="89996-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="89996-110">Precisará de nome DNS de Olá do nó principal Olá e Olá as credenciais de um administrador de cluster para concluir os passos de Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="89996-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="89996-111">**Computador cliente** -necessita de um computador cliente Windows ou Windows Server que pode executar utilitários de cliente de HPC Pack (consulte [requisitos de sistema](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="89996-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="89996-112">Se pretender que apenas portal web do toouse Olá HPC Pack ou as tarefas de toosubmit de REST API, pode utilizar qualquer computador cliente à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="89996-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="89996-113">**Suporte de instalação do HPC Pack** -tooinstall Olá utilitários de cliente de HPC Pack, o pacote de instalação livre de Olá para a versão mais recente do HPC Pack (pacote HPC 2012 R2) está disponível a partir do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="89996-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="89996-114">Certifique-se de que transfira Olá mesma versão do pacote HPC que está instalado no nó principal do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="89996-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="89996-115">Passo 1: Instalar e configurar componentes do web Olá no nó principal Olá</span><span class="sxs-lookup"><span data-stu-id="89996-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="89996-116">tooenable REST interface toosubmit tarefas toohello cluster através de HTTPS, certifique-se de que os componentes da web HPC Pack Olá são configurados no nó principal do Olá HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="89996-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="89996-117">Se ainda não estiverem instalados, primeiro de instalar os componentes web do Olá executando o ficheiro de instalação de HpcWebComponents.msi Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="89996-118">Em seguida, configure os componentes de Olá executando o script de HPC PowerShell Olá **conjunto HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="89996-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="89996-119">Para obter procedimentos detalhados, consulte [instalar Olá Microsoft HPC Pack Web componentes](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="89996-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="89996-120">Determinados modelos de início rápido do Azure para HPC Pack instalar e configurar componentes do web Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="89996-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="89996-121">Se utilizar Olá [script de implementação de HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate cluster de Olá, opcionalmente, pode instalar e configurar componentes do web Olá como parte da implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="89996-122">**componentes do tooinstall Olá web**</span><span class="sxs-lookup"><span data-stu-id="89996-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="89996-123">Liga o nó principal do toohello VM utilizando Olá credenciais de um administrador de cluster.</span><span class="sxs-lookup"><span data-stu-id="89996-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="89996-124">A partir da pasta de configuração de pacote HPC Olá, execute HpcWebComponents.msi no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="89996-125">Siga os passos de Olá Olá assistente tooinstall Olá hospeda componentes da web</span><span class="sxs-lookup"><span data-stu-id="89996-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="89996-126">**componentes do tooconfigure Olá web**</span><span class="sxs-lookup"><span data-stu-id="89996-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="89996-127">No nó principal Olá, inicie o HPC PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="89996-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="89996-128">localização de toohello do diretório toochange de script de configuração de Olá, Olá tipo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89996-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="89996-129">tooconfigure Olá REST interface e iniciar Olá serviço Web de HPC, Olá tipo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89996-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="89996-130">Quando tooselect pedido um certificado, escolha o certificado de Olá que corresponde ao nome DNS público toohello de nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="89996-131">Por exemplo, se implementar nó principal Olá VM utilizando o modelo de implementação clássica Olá, nome do certificado Olá aspeto CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="89996-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="89996-132">Se utilizar o modelo de implementação do Resource Manager Olá, o nome do certificado Olá aspeto CN =&lt;*HeadNodeDnsName*&gt;.&lt; *região*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="89996-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="89996-133">Selecionar este certificado mais tarde ao submeter o nó principal do toohello de tarefas de um computador local.</span><span class="sxs-lookup"><span data-stu-id="89996-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="89996-134">Não selecione ou configurar um certificado que corresponde ao nome do computador toohello do nó principal do Olá num domínio do Active Directory Olá (por exemplo, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="89996-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="89996-135">portal de web de Olá tooconfigure para submissão da tarefa, Olá tipo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89996-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="89996-136">Após a conclusão do script Olá, pare e reinicie Olá, o serviço de agendador de tarefas HPC, escrevendo Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89996-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="89996-137">Passo 2: Instalar utilitários de cliente de HPC Pack Olá num computador local</span><span class="sxs-lookup"><span data-stu-id="89996-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="89996-138">Se quiser utilitários de cliente do tooinstall Olá HPC Pack no seu computador, transferir os ficheiros de configuração de HPC Pack (instalação completa) da Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="89996-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="89996-139">Quando iniciar a instalação de Olá, escolha a opção de configuração de Olá para Olá **utilitários de cliente de HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="89996-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="89996-140">nó principal do toosubmit tarefas toohello VM das ferramentas de cliente de HPC Pack toouse Olá, também tem de tooexport um certificado do nó principal Olá e instalá-lo no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="89996-141">certificado de Olá tem de estar no. Formato CER.</span><span class="sxs-lookup"><span data-stu-id="89996-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="89996-142">**certificado de Olá tooexport do nó principal Olá**</span><span class="sxs-lookup"><span data-stu-id="89996-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="89996-143">No nó principal Olá, adicione Olá certificados snap-in tooa consola de gestão da Microsoft para Olá conta de computador Local.</span><span class="sxs-lookup"><span data-stu-id="89996-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="89996-144">Para obter passos tooadd Olá snap-in, consulte [adicionar Olá Snap-in Certificados tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="89996-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="89996-145">Na árvore da consola de Olá, expanda **certificados-Computador Local** > **pessoais**e, em seguida, clique em **certificados**.</span><span class="sxs-lookup"><span data-stu-id="89996-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="89996-146">Localizar certificados Olá que configurou para Olá HPC Pack web componentes [passo 1: instalar e configurar componentes do web Olá no nó principal Olá](#step-1:-install-and-configure-the-web-components-on-the-head-node) (por exemplo, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="89996-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="89996-147">Faça duplo clique Olá certificado e clique em **todas as tarefas** > **exportar**.</span><span class="sxs-lookup"><span data-stu-id="89996-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="89996-148">No Assistente para exportar certificados Olá, clique em **seguinte**e certifique-se de que **não exportar chave privada Olá** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="89996-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="89996-149">Olá siga restantes passos Olá assistente tooexport Olá do certificado de no DER x. 509 binário de codificado (. Formato CER).</span><span class="sxs-lookup"><span data-stu-id="89996-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="89996-150">**certificado de Olá tooimport no computador de cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="89996-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="89996-151">Copie o certificado de Olá que exportou a partir da pasta de tooa Olá nó principal no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="89996-152">No computador de cliente Olá, execute certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="89996-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="89996-153">No Gestor de certificados, expanda **certificados-utilizador atual** > **autoridades de certificação de raiz fidedigna**, faça duplo clique **certificados**e, em seguida, Clique em **todas as tarefas** > **importação**.</span><span class="sxs-lookup"><span data-stu-id="89996-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="89996-154">No Assistente para importar certificados Olá, clique em **seguinte** e siga Olá passos tooimport Olá certificado que exportou do Olá nó principal toohello arquivo de autoridades de certificação de raiz fidedigna.</span><span class="sxs-lookup"><span data-stu-id="89996-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="89996-155">Poderá ver um aviso de segurança, porque a autoridade de certificação de Olá no nó principal Olá não é reconhecida pelo computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="89996-156">Para fins de teste, pode ignorar esta importação de certificados de Olá aviso e concluída.</span><span class="sxs-lookup"><span data-stu-id="89996-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="89996-157">Passo 3: Executar tarefas de teste no cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="89996-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="89996-158">tooverify a configuração, tente tarefas em execução no Olá cluster no Azure de Olá no local do computador.</span><span class="sxs-lookup"><span data-stu-id="89996-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="89996-159">Por exemplo, pode utilizar ferramentas de HPC Pack GUI ou cluster de toohello comandos da linha de comandos toosubmit tarefas.</span><span class="sxs-lookup"><span data-stu-id="89996-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="89996-160">Também pode utilizar um tarefas baseada na web toosubmit portal.</span><span class="sxs-lookup"><span data-stu-id="89996-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="89996-161">**comandos de submissão de tarefa toorun no computador de cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="89996-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="89996-162">Num computador cliente onde estão instalados os utilitários de cliente de HPC Pack Olá, inicie uma linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="89996-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="89996-163">Escreva um comando de exemplo.</span><span class="sxs-lookup"><span data-stu-id="89996-163">Type a sample command.</span></span> <span data-ttu-id="89996-164">Por exemplo, toolist todas as tarefas no cluster de Olá, escreva um tooone semelhante do comando de Olá seguintes, dependendo do nome DNS completo Olá de nó principal Olá:</span><span class="sxs-lookup"><span data-stu-id="89996-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="89996-165">ou</span><span class="sxs-lookup"><span data-stu-id="89996-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="89996-166">Utilize Olá nome DNS completo de nó principal do Olá, não Olá endereço IP, no URL de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="89996-167">Se especificar o endereço IP Olá, aparece um erro semelhante demasiado "necessita de certificado de servidor Olá tooeither tem uma cadeia válida de confiança ou toobe colocados no arquivo de raiz fidedigna Olá."</span><span class="sxs-lookup"><span data-stu-id="89996-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="89996-168">Quando lhe for pedido, escreva o nome de utilizador de Olá (formato Olá &lt;DomainName&gt;\\&lt;UserName&gt;) e palavra-passe de administrador de clusters HPC Olá ou outro utilizador de cluster que configurou.</span><span class="sxs-lookup"><span data-stu-id="89996-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="89996-169">Pode escolher toostore credenciais Olá localmente para mais operações de tarefa.</span><span class="sxs-lookup"><span data-stu-id="89996-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="89996-170">É apresentada uma lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="89996-170">A list of jobs appears.</span></span>

<span data-ttu-id="89996-171">**toouse Gestor de tarefas HPC no computador de cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="89996-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="89996-172">Se não armazenar as credenciais do domínio para um utilizador de cluster anteriormente quando submete uma tarefa, pode adicionar credenciais Olá no Gestor de credenciais.</span><span class="sxs-lookup"><span data-stu-id="89996-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="89996-173">a.</span><span class="sxs-lookup"><span data-stu-id="89996-173">a.</span></span> <span data-ttu-id="89996-174">No painel de controlo do computador de cliente Olá, inicie o Gestor de credenciais.</span><span class="sxs-lookup"><span data-stu-id="89996-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="89996-175">b.</span><span class="sxs-lookup"><span data-stu-id="89996-175">b.</span></span> <span data-ttu-id="89996-176">Clique em **credenciais do Windows** > **adicionar uma credencial genérica**.</span><span class="sxs-lookup"><span data-stu-id="89996-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="89996-177">c.</span><span class="sxs-lookup"><span data-stu-id="89996-177">c.</span></span> <span data-ttu-id="89996-178">Especifique o endereço do Internet Olá (por exemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler ou https://&lt;HeadNodeDnsName&gt;.&lt; região&gt;.cloudapp.azure.com/HpcScheduler) e o nome de utilizador Olá (&lt;DomainName&gt;\\&lt;UserName&gt;) e palavra-passe de administrador do cluster Olá ou outro utilizador de cluster que configurou.</span><span class="sxs-lookup"><span data-stu-id="89996-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="89996-179">No computador de cliente Olá, inicie o Gestor de tarefas HPC.</span><span class="sxs-lookup"><span data-stu-id="89996-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="89996-180">No Olá **selecionar nó Head** caixa de diálogo, tipo Olá URL toohello nó principal no Azure (por exemplo, https://&lt;HeadNodeDnsName&gt;. cloudapp.net ou https://&lt;HeadNodeDnsName&gt;. &lt;região&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="89996-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="89996-181">Gestor de tarefas HPC abre-se e mostra uma lista de tarefas no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="89996-182">**portal de web toouse Olá em execução no nó principal Olá**</span><span class="sxs-lookup"><span data-stu-id="89996-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="89996-183">Iniciar um browser no computador de cliente Olá e introduza um dos Olá endereços, dependendo do nome DNS completo Olá de nó principal Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="89996-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="89996-184">ou</span><span class="sxs-lookup"><span data-stu-id="89996-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="89996-185">Na Olá segurança caixa de diálogo que aparece, escreva as credenciais do domínio Olá de administrador de clusters HPC Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="89996-186">(Também pode adicionar outros utilizadores de cluster em diferentes funções.</span><span class="sxs-lookup"><span data-stu-id="89996-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="89996-187">Consulte [gestão de utilizadores de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="89996-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="89996-188">portal de web de Olá abre toohello vista de lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="89996-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="89996-189">Clique em toosubmit uma tarefa de exemplo que devolve a cadeia de Olá "Olá mundo" do cluster de Olá, **nova tarefa** na navegação esquerda Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="89996-190">No Olá **nova tarefa** página **de páginas de submissão**, clique em **Olámundo**.</span><span class="sxs-lookup"><span data-stu-id="89996-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="89996-191">é apresentada a página de submissão de tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="89996-192">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="89996-192">Click **Submit**.</span></span> <span data-ttu-id="89996-193">Se lhe for solicitado, forneça as credenciais do domínio Olá de administrador de clusters HPC Olá.</span><span class="sxs-lookup"><span data-stu-id="89996-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="89996-194">Olá trabalho é submetido e Olá ID da tarefa é apresentado no Olá **tarefas My** página.</span><span class="sxs-lookup"><span data-stu-id="89996-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="89996-195">resultados de Olá tooview da tarefa de Olá submetido, clique Olá ID da tarefa e, em seguida, clique em **tarefas vista** saída do comando de Olá tooview (em **saída**).</span><span class="sxs-lookup"><span data-stu-id="89996-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89996-196">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="89996-196">Next steps</span></span>
* <span data-ttu-id="89996-197">Também pode submeter tarefas toohello cluster do Azure com Olá [API de REST do HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="89996-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="89996-198">Se pretender que as tarefas do cluster toosubmit de um cliente Linux, consulte Olá Python exemplo no Olá [SDK do HPC Pack 2012 R2 e o código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="89996-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
