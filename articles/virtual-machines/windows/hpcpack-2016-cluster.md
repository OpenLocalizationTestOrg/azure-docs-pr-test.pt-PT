---
title: aaaHPC 2016 de pacote do cluster no Azure | Microsoft Docs
description: Saiba como toodeploy um 2016 de pacote HPC cluster no Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="c865c-103">Implementar um cluster HPC Pack 2016 no Azure</span><span class="sxs-lookup"><span data-stu-id="c865c-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="c865c-104">Siga os passos de Olá toodeploy este artigo um [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="c865c-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="c865c-105">Pacote HPC é solução HPC gratuita da Microsoft incorporada no Microsoft Azure e o Windows Server tecnologias e suporta um cargas de trabalho de intervalo HPC wide.</span><span class="sxs-lookup"><span data-stu-id="c865c-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="c865c-106">Utilize um dos Olá [modelos Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de Olá HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="c865c-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="c865c-107">Existem várias opções de topologia de cluster com números diferentes de nós principais do cluster e com o Linux ou nós de computação do Windows.</span><span class="sxs-lookup"><span data-stu-id="c865c-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c865c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c865c-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="c865c-109">Certificado PFX</span><span class="sxs-lookup"><span data-stu-id="c865c-109">PFX certificate</span></span>

<span data-ttu-id="c865c-110">Um cluster do Microsoft HPC Pack 2016 requer uma comunicação do Personal Information (Exchange PFX) certificado toosecure Olá entre os nós HPC Olá.</span><span class="sxs-lookup"><span data-stu-id="c865c-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="c865c-111">certificado Olá tem de cumprir os requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="c865c-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="c865c-112">Tem de ter uma chave privada com capacidade de troca de chaves</span><span class="sxs-lookup"><span data-stu-id="c865c-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="c865c-113">A utilização de chaves inclui a assinatura Digital e cifragem</span><span class="sxs-lookup"><span data-stu-id="c865c-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="c865c-114">Utilização de chave avançada incluem autenticação de cliente e a autenticação de servidor</span><span class="sxs-lookup"><span data-stu-id="c865c-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="c865c-115">Se ainda não tiver um certificado que cumpra estes requisitos, pode pedir o certificado de Olá de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="c865c-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="c865c-116">Em alternativa, pode utilizar Olá os seguintes comandos toogenerate Olá certificado autoassinado com base no sistema de operativo Olá no qual executar o comando de Olá e exportar um certificado PFX formato Olá com chave privada.</span><span class="sxs-lookup"><span data-stu-id="c865c-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="c865c-117">**Para Windows 10 ou Windows Server 2016**, execute Olá incorporada **New-SelfSignedCertificate** cmdlet do PowerShell da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="c865c-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="c865c-118">**Para sistemas operativos anteriores ao Windows 10 ou Windows Server 2016**, transferir Olá [gerador do certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de Olá Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="c865c-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="c865c-119">Extraia os conteúdos e execute Olá os seguintes comandos numa linha de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c865c-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="c865c-120">Carregar o certificado tooan Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="c865c-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="c865c-121">Antes de implementar o cluster HPC de Olá, carregar Olá certificado tooan [Cofre de chaves do Azure](../../key-vault/index.md) como um Olá secreta e registo seguintes informações para utilização durante a implementação de Olá: **nome do cofre**,  **Grupo de recursos do cofre**, **URL de certificado**, e **thumbprint do certificado**.</span><span class="sxs-lookup"><span data-stu-id="c865c-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="c865c-122">Um certificado de Olá tooupload de script de PowerShell de exemplo seguinte.</span><span class="sxs-lookup"><span data-stu-id="c865c-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="c865c-123">Para obter mais informações sobre como carregar um certificado tooan Cofre de chaves do Azure, consulte [introdução ao Cofre de chaves do Azure](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c865c-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="c865c-124">Topologias suportadas</span><span class="sxs-lookup"><span data-stu-id="c865c-124">Supported topologies</span></span>

<span data-ttu-id="c865c-125">Escolha uma das Olá [modelos Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de Olá HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="c865c-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="c865c-126">Seguem-se arquiteturas de alto nível das três topologias de cluster suportadas.</span><span class="sxs-lookup"><span data-stu-id="c865c-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="c865c-127">Topologias de elevada disponibilidade incluem vários nós principais do cluster.</span><span class="sxs-lookup"><span data-stu-id="c865c-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="c865c-128">Cluster de elevada disponibilidade com o domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c865c-128">High-availability cluster with Active Directory domain</span></span>

    ![Cluster do HA no domínio do AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="c865c-130">Cluster de elevada disponibilidade sem o domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c865c-130">High-availability cluster without Active Directory domain</span></span>

    ![Cluster do HA sem domínio AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="c865c-132">Cluster com um único nó principal</span><span class="sxs-lookup"><span data-stu-id="c865c-132">Cluster with a single head node</span></span>

   ![Cluster com o único nó principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="c865c-134">Implementar um cluster</span><span class="sxs-lookup"><span data-stu-id="c865c-134">Deploy a cluster</span></span>

<span data-ttu-id="c865c-135">cluster de Olá toocreate, escolha um modelo e clique em **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c865c-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="c865c-136">No Olá [portal do Azure](https://portal.azure.com), especifique os parâmetros para o modelo de Olá, conforme descrito em Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="c865c-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="c865c-137">Cada modelo cria todos os recursos do Azure necessários para a infraestrutura de cluster HPC Olá.</span><span class="sxs-lookup"><span data-stu-id="c865c-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="c865c-138">Recursos incluem uma Azure virtual network, pública IP endereços, o Balanceador de carga (apenas para um cluster de elevada disponibilidade), interfaces de rede, conjuntos de disponibilidade, contas de armazenamento e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c865c-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="c865c-139">Passo 1: Selecione a subscrição de Olá, localização e grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c865c-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="c865c-140">Olá **subscrição** e Olá **localização** tem de ser o mesmo que especificou quando carregou o certificado do PFX (consulte pré-requisitos).</span><span class="sxs-lookup"><span data-stu-id="c865c-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="c865c-141">Recomendamos que crie um **grupo de recursos** para a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c865c-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="c865c-142">Passo 2: Especificar as definições de parâmetro de Olá</span><span class="sxs-lookup"><span data-stu-id="c865c-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="c865c-143">Introduza ou altere os valores de parâmetros de modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="c865c-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="c865c-144">Clique em Olá ícone seguinte tooeach parâmetro informações de ajuda.</span><span class="sxs-lookup"><span data-stu-id="c865c-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="c865c-145">Consulte também as orientações de Olá para [tamanhos VM disponíveis](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c865c-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="c865c-146">Especifique os valores de Olá que registou no Olá pré-requisitos para seguir os parâmetros de Olá: **nome do cofre**, **grupo de recursos do cofre**, **URL de certificado**e **Thumbprint do certificado**.</span><span class="sxs-lookup"><span data-stu-id="c865c-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="c865c-147">Passo 3.</span><span class="sxs-lookup"><span data-stu-id="c865c-147">Step 3.</span></span> <span data-ttu-id="c865c-148">Reveja os termos legais e criar</span><span class="sxs-lookup"><span data-stu-id="c865c-148">Review legal terms and create</span></span>
<span data-ttu-id="c865c-149">Clique em **consultar termos legais** termos de Olá tooreview.</span><span class="sxs-lookup"><span data-stu-id="c865c-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="c865c-150">Se concordar, clique em **Compra**e, em seguida, clique em **criar** implementação de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="c865c-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="c865c-151">Ligue o cluster de toohello</span><span class="sxs-lookup"><span data-stu-id="c865c-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="c865c-152">Após a implementação de cluster HPC Pack de Olá, aceda toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c865c-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c865c-153">Clique em **grupos de recursos**e encontrar o grupo de recursos de Olá que Olá cluster foi implementado.</span><span class="sxs-lookup"><span data-stu-id="c865c-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="c865c-154">Pode encontrar Olá máquinas de virtuais do nó principal.</span><span class="sxs-lookup"><span data-stu-id="c865c-154">You can find hello head node virtual machines.</span></span>

    ![Nós principais do cluster no portal de Olá](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="c865c-156">Clique num nó principal (num cluster de elevada disponibilidade, clique em qualquer um de nós principais Olá).</span><span class="sxs-lookup"><span data-stu-id="c865c-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="c865c-157">No **Essentials**, pode encontrar o endereço IP público Olá ou nome DNS completo de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="c865c-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Definições de ligação de cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="c865c-159">Clique em **Connect** toolog no tooany de nós principais Olá através de ambiente de trabalho remoto com o seu nome de utilizador de administrador especificadas.</span><span class="sxs-lookup"><span data-stu-id="c865c-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="c865c-160">Se tiver cluster Olá implementou um domínio do Active Directory, o nome de utilizador de Olá tem o formato de Olá <privateDomainName> \<adminUsername > (por exemplo, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="c865c-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c865c-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c865c-161">Next steps</span></span>
* <span data-ttu-id="c865c-162">Submeta cluster tooyour de tarefas.</span><span class="sxs-lookup"><span data-stu-id="c865c-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="c865c-163">Consulte [submeter tarefas tooHPC um cluster HPC Pack no Azure](hpcpack-cluster-submit-jobs.md) e [gerir um cluster HPC Pack 2016 no Azure utilizando o Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c865c-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

