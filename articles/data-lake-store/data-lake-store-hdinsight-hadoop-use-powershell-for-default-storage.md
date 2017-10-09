---
title: aaaCreate HDInsight clusters, com o Data Lake Store, como armazenamento de predefinido utilizando o PowerShell | Microsoft Docs
description: Utilizar o Azure PowerShell toocreate e utilizar clusters do HDInsight com o Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="2f15a-103">Criar clusters do HDInsight com o Data Lake Store como armazenamento de predefinido utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f15a-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f15a-104">Utilizar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2f15a-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="2f15a-105">Utilize o PowerShell (para armazenamento de predefinido)</span><span class="sxs-lookup"><span data-stu-id="2f15a-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="2f15a-106">Utilize o PowerShell (para armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="2f15a-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="2f15a-107">Utilize o Gestor de recursos</span><span class="sxs-lookup"><span data-stu-id="2f15a-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="2f15a-108">Saiba como clusters de toouse Azure PowerShell tooconfigure Azure HDInsight com o Azure Data Lake Store, como armazenamento de predefinido.</span><span class="sxs-lookup"><span data-stu-id="2f15a-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="2f15a-109">Para obter instruções sobre como criar um cluster do HDInsight com o Data Lake Store, como armazenamento adicional, consulte [criar um cluster do HDInsight com o Data Lake Store, como armazenamento adicional](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2f15a-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="2f15a-110">Seguem-se algumas considerações importantes para utilizar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="2f15a-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="2f15a-111">Olá opção toocreate os clusters do HDInsight com acesso tooData Lake Store, como armazenamento de predefinição está disponível para o HDInsight versão 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="2f15a-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="2f15a-112">Olá opção toocreate clusters do HDInsight com aceder tooData Lake Store, como o armazenamento de predefinido é *não está disponível* para clusters do HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="2f15a-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="2f15a-113">tooconfigure toowork HDInsight com o Data Lake Store utilizando o PowerShell, siga instruções Olá secções junto cinco Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f15a-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f15a-114">Prerequisites</span></span>
<span data-ttu-id="2f15a-115">Antes de começar este tutorial, certifique-se de que cumpre os requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="2f15a-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="2f15a-116">**Uma subscrição do Azure**: aceda demasiado[avaliação gratuita do Azure obter](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f15a-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2f15a-117">**O Azure PowerShell 1.0 ou superior**: consulte [como tooinstall e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f15a-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2f15a-118">**Software Development Kit (SDK) do Windows**: tooinstall Windows SDK, aceda demasiado[transfere e ferramentas para Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="2f15a-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="2f15a-119">Olá SDK é toocreate utilizado um certificado de segurança.</span><span class="sxs-lookup"><span data-stu-id="2f15a-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="2f15a-120">**Principal de serviço do Azure Active Directory**: Este tutorial descreve como toocreate um principal de serviço no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f15a-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2f15a-121">No entanto, toocreate um principal de serviço, tem de ser um administrador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f15a-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="2f15a-122">Se for um administrador, pode ignorar este pré-requisito e continue com tutorial de Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="2f15a-123">Pode criar um serviço principal, apenas se for um administrador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f15a-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="2f15a-124">O administrador do Azure AD tem de criar um serviço principal antes de poder criar um cluster do HDInsight com o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2f15a-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="2f15a-125">Olá principal de serviço tem de ser criado com um certificado, conforme descrito em [criar um principal de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="2f15a-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="2f15a-126">Criar uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f15a-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="2f15a-127">toocreate uma conta de Data Lake Store, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="2f15a-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="2f15a-128">Do ambiente de trabalho, abra uma janela do PowerShell e, em seguida, introduza fragmentos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="2f15a-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="2f15a-129">Quando estiver toosign pedido no início de sessão como um dos administradores da subscrição de Olá ou proprietários.</span><span class="sxs-lookup"><span data-stu-id="2f15a-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="2f15a-130">Se registar o fornecedor de recursos do Data Lake Store Olá e receber um erro semelhante demasiado`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, a subscrição poderá não estar na lista de permissões para o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2f15a-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="2f15a-131">tooenable sua subscrição do Azure para pré-visualização pública do Data Lake Store Olá, siga as instruções de Olá em [introdução ao Azure Data Lake Store utilizando o portal do Azure de Olá](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2f15a-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="2f15a-132">Conta do Data Lake Store está associada um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f15a-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="2f15a-133">Comece por criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f15a-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="2f15a-134">Deverá ver um resultado como esta:</span><span class="sxs-lookup"><span data-stu-id="2f15a-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="2f15a-135">Crie uma conta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2f15a-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="2f15a-136">conta de Olá nome que especificar tem de conter apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="2f15a-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="2f15a-137">Deverá ver um resultado como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="2f15a-137">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. <span data-ttu-id="2f15a-138">Utilizar o Data Lake Store como armazenamento de predefinido requer toospecify que uma raiz caminho toowhich Olá cluster específicos os ficheiros são copiados durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="2f15a-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="2f15a-139">toocreate um caminho de raiz, o que é **/clusters/hdiadlcluster** no fragmento de Olá, utilize Olá os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="2f15a-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="2f15a-140">Configurar a autenticação para baseada em funções aceder tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f15a-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="2f15a-141">Cada subscrição do Azure está associada uma entidade do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f15a-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="2f15a-142">Utilizadores e serviços que aceder a recursos de subscrição utilizando Olá portal do Azure ou Olá API do Azure Resource Manager, devem primeiro autenticar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f15a-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="2f15a-143">É concedido acesso tooAzure subscrições e serviços ao lhes atribuir função adequada da Olá um recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f15a-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="2f15a-144">Para os serviços, um principal de serviço identifica o serviço de Olá no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f15a-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="2f15a-145">Esta secção ilustra como serviço toogrant uma aplicação, tais como o HDInsight, tooan de acesso a recursos do Azure (Olá conta do Data Lake Store que criou anteriormente).</span><span class="sxs-lookup"><span data-stu-id="2f15a-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="2f15a-146">Fazê-lo ao criar um serviço principal para a aplicação Olá e atribuir funções tooit através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f15a-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="2f15a-147">tooset configurar a autenticação do Active Directory para o Azure Data Lake, executar tarefas de Olá Olá duas secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="2f15a-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="2f15a-148">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="2f15a-148">Create a self-signed certificate</span></span>
<span data-ttu-id="2f15a-149">Certifique-se de que tem [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de prosseguir Olá passos nesta secção.</span><span class="sxs-lookup"><span data-stu-id="2f15a-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="2f15a-150">Tem de ter também criou um diretório, tais como *C:\mycertdir*, onde criar certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="2f15a-151">A partir da janela do PowerShell Olá, aceder localização toohello onde instalou o SDK do Windows (normalmente, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) e utilizar Olá [MakeCert] [ makecert] utilitário toocreate um certificado autoassinado e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="2f15a-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="2f15a-152">Utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2f15a-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="2f15a-153">Será pedido tooenter Olá chave palavra-passe privada.</span><span class="sxs-lookup"><span data-stu-id="2f15a-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="2f15a-154">Depois de comando Olá é executado com êxito, deverá ver **CertFile.cer** e **mykey.pvk** no diretório de certificado Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="2f15a-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="2f15a-155">Olá utilize [Pvk2Pfx] [ pvk2pfx] utilitário tooconvert Olá .pvk e. cer ficheiros se MakeCert tooa criado o ficheiro de. pfx.</span><span class="sxs-lookup"><span data-stu-id="2f15a-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="2f15a-156">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2f15a-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="2f15a-157">Quando lhe for pedido, introduza Olá chave palavra-passe privada que especificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2f15a-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="2f15a-158">Olá valor que especificar para Olá **-po** parâmetro é a palavra-passe de Olá associado ao arquivo. pfx Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="2f15a-159">Comando Olá tenha sido concluída com êxito, verá também uma **CertFile.pfx** no diretório de certificado Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="2f15a-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="2f15a-160">Criar um Azure AD e um principal de serviço</span><span class="sxs-lookup"><span data-stu-id="2f15a-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="2f15a-161">Nesta secção, criar um principal de serviço para uma aplicação do Azure AD, atribuir um principal de serviço de toohello de função e efetue a autenticação como principal de serviço Olá, fornecendo um certificado.</span><span class="sxs-lookup"><span data-stu-id="2f15a-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="2f15a-162">toocreate uma aplicação no Azure AD, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2f15a-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="2f15a-163">Colar Olá os seguintes cmdlets na janela de consola do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="2f15a-164">Certifique-se de que especificou para Olá o valor Olá **- DisplayName** propriedade é exclusiva.</span><span class="sxs-lookup"><span data-stu-id="2f15a-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="2f15a-165">Olá valores para **- home page** e **- IdentiferUris** são valores de marcador de posição e não são verificadas.</span><span class="sxs-lookup"><span data-stu-id="2f15a-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="2f15a-166">Criar um principal de serviço com o ID da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="2f15a-167">Conceda a raiz de Data Lake Store de toohello do acesso principal do serviço de Olá e todas as pastas de Olá no caminho da raiz Olá que especificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2f15a-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="2f15a-168">Utilize Olá os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="2f15a-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="2f15a-169">Criar um cluster do HDInsight com Linux com o Data Lake Store, como armazenamento de predefinido Olá</span><span class="sxs-lookup"><span data-stu-id="2f15a-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="2f15a-170">Nesta secção, vai criar um cluster do HDInsight Hadoop Linux com o Data Lake Store como armazenamento de predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="2f15a-171">Nesta versão, Olá cluster do HDInsight e Data Lake Store tem de constar Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="2f15a-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="2f15a-172">Obter o ID de inquilino de subscrição de Olá e armazena toouse mais tarde.</span><span class="sxs-lookup"><span data-stu-id="2f15a-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="2f15a-173">Crie cluster do HDInsight Olá utilizando Olá os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="2f15a-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="2f15a-174">Cmdlet Olá tenha sido concluída com êxito, deverá ver um resultado que lista os detalhes do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="2f15a-175">Executar tarefas de teste em Olá HDInsight cluster toouse Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f15a-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="2f15a-176">Depois de configurar um cluster do HDInsight, pode executar tarefas de teste no mesmo tooensure pode aceder a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2f15a-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="2f15a-177">toodo por isso, executar um toocreate de tarefa do Hive de exemplo a uma tabela que utiliza dados de exemplo de Olá que já se encontra disponíveis no Data Lake Store em  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="2f15a-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="2f15a-178">Nesta secção, efetuar uma ligação Secure Shell (SSH) para Olá cluster do HDInsight com Linux que criou e, em seguida, executar uma consulta do Hive de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2f15a-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="2f15a-179">Se estiver a utilizar um toomake de cliente do Windows uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="2f15a-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="2f15a-180">Se estiver a utilizar um toomake de cliente do Linux uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2f15a-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="2f15a-181">Depois de efetuar a ligação de Olá, inicie a interface de linha de comandos de ramo de registo de Olá (CLI) utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2f15a-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="2f15a-182">Olá tooenter utilize Olá CLI seguir as instruções toocreate uma nova tabela com o nome **veículos** utilizando dados de exemplo de Olá no Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="2f15a-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="2f15a-183">Deverá ver um resultado de consulta Olá na consola SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="2f15a-184">Olá dados de exemplo do caminho toohello no Olá precedente comando CREATE TABLE são `adl:///example/data/`, onde `adl:///` é Olá cluster raiz.</span><span class="sxs-lookup"><span data-stu-id="2f15a-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="2f15a-185">Exemplo de Olá de raiz do cluster de Olá que é especificado neste tutorial, os seguintes comandos Olá é `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="2f15a-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="2f15a-186">Pode utilizar alternativa mais curta Olá ou fornecer Olá caminho completo toohello cluster de raiz.</span><span class="sxs-lookup"><span data-stu-id="2f15a-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="2f15a-187">Aceder ao Data Lake Store utilizando comandos HDFS</span><span class="sxs-lookup"><span data-stu-id="2f15a-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="2f15a-188">Depois de ter configurado Olá HDInsight cluster toouse Data Lake Store, pode utilizar distribuídas ficheiro sistema Hadoop (HDFS) shell comandos tooaccess Olá arquivo.</span><span class="sxs-lookup"><span data-stu-id="2f15a-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="2f15a-189">Nesta secção, efetuar uma ligação SSH para Olá cluster do HDInsight com Linux que criou e, em seguida, executar os comandos HDFS Olá.</span><span class="sxs-lookup"><span data-stu-id="2f15a-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="2f15a-190">Se estiver a utilizar um toomake de cliente do Windows uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="2f15a-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="2f15a-191">Se estiver a utilizar um toomake de cliente do Linux uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2f15a-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="2f15a-192">Depois de efetuadas ligação Olá, listam os ficheiros de Olá no Data Lake Store utilizando Olá os seguintes comandos de sistema de ficheiros do HDFS.</span><span class="sxs-lookup"><span data-stu-id="2f15a-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="2f15a-193">Também pode utilizar Olá `hdfs dfs -put` comando tooupload alguns ficheiros tooData Lake Store e, em seguida, utilize `hdfs dfs -ls` tooverify se os ficheiros de Olá foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="2f15a-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="2f15a-194">Consultar também</span><span class="sxs-lookup"><span data-stu-id="2f15a-194">See also</span></span>
* [<span data-ttu-id="2f15a-195">Portal do Azure: criar um toouse de cluster do HDInsight Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f15a-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
