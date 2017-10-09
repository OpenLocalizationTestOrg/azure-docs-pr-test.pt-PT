---
title: aaaCreate um Azure Service Fabric cluster a partir de um modelo | Microsoft Docs
description: "Este artigo descreve como tooset se um recurso de infraestrutura seguros do serviço de cluster no Azure utilizando o Azure Resource Manager, o Cofre de chaves do Azure e o Azure Active Directory (Azure AD) para autenticação de cliente."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="6e429-103">Criar um cluster do Service Fabric com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6e429-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e429-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6e429-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="6e429-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e429-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="6e429-106">Este guia passo a passo explica como configurar um cluster do Azure Service Fabric seguro no Azure utilizando o Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e429-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="6e429-107">Iremos reconhecer que esse artigo Olá é longo.</span><span class="sxs-lookup"><span data-stu-id="6e429-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="6e429-108">Contudo, a menos que já estejam exaustivamente familiarizado com o conteúdo de Olá, ser toofollow se cada passo cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="6e429-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="6e429-109">Guia de Olá abrange Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="6e429-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="6e429-110">Como configurar certificados de tooupload um cofre de chaves do Azure para a segurança do cluster e da aplicação</span><span class="sxs-lookup"><span data-stu-id="6e429-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="6e429-111">Criar um cluster protegido no Azure utilizando o Gestor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="6e429-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="6e429-112">Autenticação de utilizadores utilizando o Azure Active Directory (Azure AD) para gestão de clusters</span><span class="sxs-lookup"><span data-stu-id="6e429-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="6e429-113">Um cluster seguro é um cluster que impede a operações de toomanagement de acesso não autorizado.</span><span class="sxs-lookup"><span data-stu-id="6e429-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="6e429-114">Isto inclui a implementar, atualizar e aplicações a eliminar, serviços e dados de Olá contêm.</span><span class="sxs-lookup"><span data-stu-id="6e429-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="6e429-115">Um cluster não seguro é um cluster que qualquer pessoa pode ligar tooat qualquer altura e efetuar operações de gestão.</span><span class="sxs-lookup"><span data-stu-id="6e429-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="6e429-116">Embora seja possível toocreate um cluster não seguro, recomendamos vivamente que cria um cluster seguro de proposto Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="6e429-117">Devido um cluster não seguro não pode ser protegido mais tarde, tem de ser criado um novo cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="6e429-118">conceito de Olá de criação de clusters seguros é hello iguais, quer sejam clusters do Linux ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="6e429-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="6e429-119">Para mais informações e do programa auxiliar de scripts para criar clusters Linux seguros consulte [criação de clusters seguros no Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="6e429-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="6e429-120">Inicie sessão no tooyour a conta do Azure</span><span class="sxs-lookup"><span data-stu-id="6e429-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="6e429-121">Este guia utiliza [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="6e429-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="6e429-122">Quando inicia uma nova sessão do PowerShell, inicie sessão tooyour conta do Azure e selecionar a sua subscrição antes de executar os comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e429-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="6e429-123">A iniciar sessão tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="6e429-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6e429-124">Selecione a sua subscrição:</span><span class="sxs-lookup"><span data-stu-id="6e429-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="6e429-125">Configurar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6e429-125">Set up a key vault</span></span>
<span data-ttu-id="6e429-126">Esta secção explica como criar um cofre de chaves para um cluster do Service Fabric no Azure e para aplicações de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e429-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="6e429-127">Para obter um guia completo tooAzure Cofre de chaves, consulte toohello [Cofre de chaves guia de introdução][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="6e429-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="6e429-128">Service Fabric utiliza toosecure de certificados x. 509 um cluster e fornece funcionalidades de segurança da aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e429-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="6e429-129">Utilize certificados de toomanage do Cofre de chaves para clusters de Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e429-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="6e429-130">Quando um cluster é implementado no Azure, o fornecedor de recursos do Azure de Olá que é responsável pela criação de clusters de Service Fabric obtém certificados a partir do Cofre de chaves e instala-los num cluster de Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="6e429-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="6e429-131">Olá diagrama seguinte ilustra Olá relação entre o Cofre de chaves do Azure, um cluster do Service Fabric e fornecedor de recursos do Azure de Olá que utiliza certificados armazenados no Cofre de chaves quando cria um cluster:</span><span class="sxs-lookup"><span data-stu-id="6e429-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagrama de instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="6e429-133">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6e429-133">Create a resource group</span></span>
<span data-ttu-id="6e429-134">Step-by-Olá primeiro passo é toocreate um grupo de recursos especificamente para o seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="6e429-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="6e429-135">Recomendamos que colocar o Cofre de chaves Olá no seu próprio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6e429-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="6e429-136">Esta ação permite-lhe remover Olá computação e armazenamento grupos de recursos, incluindo o grupo de recursos de Olá que contém o cluster do Service Fabric, sem perder as chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="6e429-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="6e429-137">grupo de recursos de Olá que contém o seu Cofre de chaves _tem de ser Olá mesma região_ como cluster Olá que está a utilizar.</span><span class="sxs-lookup"><span data-stu-id="6e429-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="6e429-138">Se planear toodeploy clusters em várias regiões, sugerimos que, de nome de grupo de recursos de Olá e Cofre de chaves Olá de uma forma que indica a que região pertence.</span><span class="sxs-lookup"><span data-stu-id="6e429-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="6e429-139">saída de Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="6e429-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="6e429-140">Criar um cofre de chaves no novo grupo de recursos Olá</span><span class="sxs-lookup"><span data-stu-id="6e429-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="6e429-141">cofre da chave Olá _tem de estar ativado para a implementação_ tooallow Olá certificados da tooget de fornecedor de recursos de computação do mesmo e instalá-lo em instâncias de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="6e429-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="6e429-142">saída de Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="6e429-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="6e429-143">Utilize um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6e429-143">Use an existing key vault</span></span>

<span data-ttu-id="6e429-144">toouse um cofre de chaves, _necessário ativá-la para implementação_ tooallow Olá certificados da tooget de fornecedor de recursos de computação do mesmo e instalá-lo em nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="6e429-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="6e429-145">Adicionar o Cofre de chaves de tooyour de certificados</span><span class="sxs-lookup"><span data-stu-id="6e429-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="6e429-146">Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações.</span><span class="sxs-lookup"><span data-stu-id="6e429-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="6e429-147">Para obter mais informações sobre como os certificados são utilizados no Service Fabric, consulte [cenários de segurança de cluster do Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="6e429-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="6e429-148">Cluster e servidor de certificado (obrigatório)</span><span class="sxs-lookup"><span data-stu-id="6e429-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="6e429-149">Este certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit.</span><span class="sxs-lookup"><span data-stu-id="6e429-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="6e429-150">Fornece segurança de cluster de duas formas:</span><span class="sxs-lookup"><span data-stu-id="6e429-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="6e429-151">Autenticação do cluster: autentica o nó de nó de comunicação para a Federação de cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="6e429-152">Apenas nós que podem provar a sua identidade com este certificado podem associar cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="6e429-153">Autenticação de servidor: autentica Olá cluster pontos finais tooa gestão cliente de gestão, para hello cliente de gestão sabe que está a falar com toohello real cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="6e429-154">Este certificado fornece também um SSL para Olá API de gestão HTTPS e para o Service Fabric Explorer através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6e429-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="6e429-155">tooserve estes fins, certificado Olá têm de cumprir os requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="6e429-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="6e429-156">certificado de Olá tem de conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="6e429-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="6e429-157">certificado de Olá tem de ser criado para a troca de chaves, que é exportável tooa ficheiro Personal Information Exchange (. pfx).</span><span class="sxs-lookup"><span data-stu-id="6e429-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="6e429-158">nome do requerente do certificado Olá tem de corresponder ao domínio Olá que utilize o cluster do Service Fabric tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="6e429-159">Esta correspondência é necessário tooprovide um SSL para pontos finais de gestão do cluster Olá HTTPS e o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e429-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="6e429-160">Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para Olá. cloudapp.azure.com domínio.</span><span class="sxs-lookup"><span data-stu-id="6e429-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="6e429-161">Tem de obter um nome de domínio personalizado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="6e429-162">Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="6e429-163">Certificados de aplicação (opcionais)</span><span class="sxs-lookup"><span data-stu-id="6e429-163">Application certificates (optional)</span></span>
<span data-ttu-id="6e429-164">Qualquer número de certificados adicionais pode ser instalado num cluster por motivos de segurança da aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e429-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="6e429-165">Antes de criar o cluster, considere os cenários de segurança de aplicação Olá que requerem toobe um certificado instalado em nós de Olá, tal como:</span><span class="sxs-lookup"><span data-stu-id="6e429-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="6e429-166">A encriptação e desencriptação de valores de configuração de aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e429-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="6e429-167">Encriptação dos dados em nós durante a replicação.</span><span class="sxs-lookup"><span data-stu-id="6e429-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="6e429-168">Formatação certificados para utilização do fornecedor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="6e429-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="6e429-169">Pode adicionar e utilizar privados ficheiros de chave (. pfx) diretamente através do seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="6e429-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="6e429-170">No entanto, o fornecedor de recursos de computação do Azure Olá requer toobe chaves armazenada num formato especial JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="6e429-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="6e429-171">formato de Olá inclui Olá arquivo. pfx como uma cadeia com codificação 64 base e Olá chave palavra-passe privada.</span><span class="sxs-lookup"><span data-stu-id="6e429-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="6e429-172">tooaccommodate estes requisitos, Olá chaves tem de ser colocadas numa cadeia JSON e, em seguida, armazenadas como "segredos" na chave de Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="6e429-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="6e429-173">toomake este processo mais fácil, uma [módulo do PowerShell está disponível no GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="6e429-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="6e429-174">módulo de Olá toouse, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e429-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="6e429-175">Transferir o conteúdo completo de Olá do repositório de Olá para um diretório local.</span><span class="sxs-lookup"><span data-stu-id="6e429-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="6e429-176">Aceda toohello de diretório local.</span><span class="sxs-lookup"><span data-stu-id="6e429-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="6e429-177">Importe o módulo de ServiceFabricRPHelpers Olá na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6e429-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="6e429-178">Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell automaticamente formatos uma chave privada do certificado numa cadeia JSON e carrega-toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="6e429-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="6e429-179">Utilize o certificado de cluster do Olá comando tooadd Olá e qualquer Cofre de chaves de toohello de certificados adicionais de aplicações.</span><span class="sxs-lookup"><span data-stu-id="6e429-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="6e429-180">Repita este passo para todos os certificados adicionais que pretende tooinstall no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="6e429-181">Carregar um certificado existente</span><span class="sxs-lookup"><span data-stu-id="6e429-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="6e429-182">Se obtiver um erro, como Olá mostrado aqui, normalmente, significa que tem um conflito de URL de recurso.</span><span class="sxs-lookup"><span data-stu-id="6e429-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="6e429-183">conflito de Olá tooresolve, nome do Cofre de chaves de Olá de alteração.</span><span class="sxs-lookup"><span data-stu-id="6e429-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="6e429-184">Depois de resolver o conflito de Olá, saída Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="6e429-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="6e429-185">É necessário Olá três anterior cadeias, CertificateThumbprint, SourceVault e CertificateURL, tooset segurança de um cluster do Service Fabric segura e tooobtain quaisquer certificados de aplicação que possam estar a utilizar para a segurança da aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e429-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="6e429-186">Se não guarde cadeias Olá, pode ser difícil tooretrieve-los através da consulta chave Olá cofre mais tarde.</span><span class="sxs-lookup"><span data-stu-id="6e429-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="6e429-187">Criar um certificado autoassinado e carregá-lo toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6e429-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="6e429-188">Se já tiver carregado o seu Cofre de chaves de toohello de certificados, ignore este passo.</span><span class="sxs-lookup"><span data-stu-id="6e429-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="6e429-189">Este passo é para gerar um novo certificado autoassinado e carregá-lo tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="6e429-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="6e429-190">Depois de alterar parâmetros Olá Olá script a seguir e, em seguida, executá-lo, deve ser pedido para uma palavra-passe do certificado.</span><span class="sxs-lookup"><span data-stu-id="6e429-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="6e429-191">Se obtiver um erro, como Olá mostrado aqui, normalmente, significa que tem um conflito de URL de recurso.</span><span class="sxs-lookup"><span data-stu-id="6e429-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="6e429-192">conflito de Olá tooresolve, nome do Cofre de chaves de alteração Olá, nome RG e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="6e429-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="6e429-193">Depois de resolver o conflito de Olá, saída Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="6e429-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="6e429-194">É necessário Olá três anterior cadeias, CertificateThumbprint, SourceVault e CertificateURL, tooset segurança de um cluster do Service Fabric segura e tooobtain quaisquer certificados de aplicação que possam estar a utilizar para a segurança da aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e429-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="6e429-195">Se não guarde cadeias Olá, pode ser difícil tooretrieve-los através da consulta chave Olá cofre mais tarde.</span><span class="sxs-lookup"><span data-stu-id="6e429-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="6e429-196">Nesta fase, deve ter Olá seguintes elementos no local:</span><span class="sxs-lookup"><span data-stu-id="6e429-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="6e429-197">grupo de recursos do Olá Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="6e429-197">hello key vault resource group.</span></span>
* <span data-ttu-id="6e429-198">Olá Cofre de chaves e o respetivo URL (denominado SourceVault no Olá anterior a saída do PowerShell).</span><span class="sxs-lookup"><span data-stu-id="6e429-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="6e429-199">certificado de autenticação de servidor de cluster Olá e o respetivo URL no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="6e429-200">os URLs no Cofre de chaves Olá e certificados de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="6e429-201">Configurar o Azure Active Directory para autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="6e429-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="6e429-202">Azure AD permite tooapplications de acesso de utilizador de toomanage organizações (conhecido como inquilinos).</span><span class="sxs-lookup"><span data-stu-id="6e429-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="6e429-203">As aplicações são divididas aqueles com uma conta baseada na web IU de início de sessão e as pessoas com uma experiência de cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="6e429-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="6e429-204">Neste artigo, partimos do pressuposto que já criou um inquilino.</span><span class="sxs-lookup"><span data-stu-id="6e429-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="6e429-205">Se não tiver, comece por ler [como tooget um Azure Active Directory inquilino][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="6e429-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="6e429-206">Um cluster do Service Fabric oferece tooits de pontos de entrada várias funcionalidades de gestão, incluindo Olá baseada na web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] e [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="6e429-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="6e429-207">Como resultado, crie duas do Azure AD aplicações toocontrol acesso toohello cluster, uma aplicação web e uma aplicação nativa.</span><span class="sxs-lookup"><span data-stu-id="6e429-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="6e429-208">toosimplify alguns dos passos de Olá envolvidos na configuração do Azure AD com um cluster do Service Fabric, foi criado um conjunto de scripts do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e429-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="6e429-209">Tem de concluir Olá antes de criar o cluster de Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="6e429-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="6e429-210">Uma vez que scripts Olá esperam os nomes de clusters e os pontos finais, valores Olá deve ser planeadas e não os valores que já criou.</span><span class="sxs-lookup"><span data-stu-id="6e429-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="6e429-211">[Transfira scripts Olá] [ sf-aad-ps-script-download] tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="6e429-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="6e429-212">Contexto Olá ficheiro zip, selecione **propriedades**, selecione Olá **desbloqueio** caixa de verificação e, em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="6e429-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="6e429-213">Extraia o ficheiro zip Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="6e429-214">Executar `SetupApplications.ps1`e forneça Olá TenantId, ClusterName e WebApplicationReplyUrl como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="6e429-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="6e429-215">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6e429-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="6e429-216">Pode encontrar o TenantId executando o comando do PowerShell Olá `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="6e429-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="6e429-217">Executar este comando apresenta Olá TenantId para cada subscrição.</span><span class="sxs-lookup"><span data-stu-id="6e429-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="6e429-218">ClusterName é tooprefix utilizadas aplicações de Olá do Azure AD que são criadas pelo script de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="6e429-219">Não necessita de nome de cluster real toomatch Olá exatamente.</span><span class="sxs-lookup"><span data-stu-id="6e429-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="6e429-220">É toomake apenas pretendido-lo mais fácil toomap do Azure AD artefactos toohello cluster do Service Fabric que está a ser utilizados com.</span><span class="sxs-lookup"><span data-stu-id="6e429-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="6e429-221">WebApplicationReplyUrl é o ponto final da predefinição de Olá do Azure AD devolve tooyour utilizadores depois de concluir a iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="6e429-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="6e429-222">Defina este ponto final como ponto final do Service Fabric Explorer Olá para o cluster, o que, por predefinição, está:</span><span class="sxs-lookup"><span data-stu-id="6e429-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="6e429-223">https://&lt;cluster_domain&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="6e429-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="6e429-224">São toosign pedido na conta tooan que tenha privilégios administrativos para o inquilino Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e429-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="6e429-225">Depois de iniciar sessão, o script de Olá cria Olá web e de aplicações nativas toorepresent o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e429-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="6e429-226">Se observar a aplicações do inquilino Olá Olá [portal clássico do Azure][azure-classic-portal], deverá ver duas novas entradas:</span><span class="sxs-lookup"><span data-stu-id="6e429-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="6e429-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="6e429-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="6e429-228">*ClusterName*\_cliente</span><span class="sxs-lookup"><span data-stu-id="6e429-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="6e429-229">script de Olá imprime Olá JSON é necessário pelo modelo do Azure Resource Manager Olá quando criar o cluster de Olá na secção seguinte, Olá, pelo que é uma janela do PowerShell boa ideia tookeep Olá abrir.</span><span class="sxs-lookup"><span data-stu-id="6e429-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="6e429-230">Criar um modelo de Gestor de recursos de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e429-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="6e429-231">Nesta secção, Olá produz de Olá anterior comandos do PowerShell são utilizados num modelo de Gestor de recursos de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e429-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="6e429-232">Modelos de Gestor de recursos de exemplo estão disponíveis no Olá [Galeria de modelo de início rápido do Azure no GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="6e429-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="6e429-233">Estes modelos, podem ser utilizados como um ponto de partida para o modelo de cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="6e429-234">Criar modelo do Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="6e429-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="6e429-235">Este guia utiliza Olá [5-nó cluster segura] [ service-fabric-secure-cluster-5-node-1-nodetype] modelo de exemplo e os parâmetros do modelo.</span><span class="sxs-lookup"><span data-stu-id="6e429-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="6e429-236">Transferir `azuredeploy.json` e `azuredeploy.parameters.json` tooyour computador e abra ambos os ficheiros no seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="6e429-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="6e429-237">Adicione certificados</span><span class="sxs-lookup"><span data-stu-id="6e429-237">Add certificates</span></span>
<span data-ttu-id="6e429-238">Adicionar modelo de Gestor de recursos de cluster de tooa certificados consultando o Cofre de chaves Olá contém Olá chaves de certificado.</span><span class="sxs-lookup"><span data-stu-id="6e429-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="6e429-239">Recomendamos que coloque os valores do Cofre de chaves de Olá num ficheiro de parâmetros de modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6e429-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="6e429-240">Se o fizer, mantém Olá Gestor de recursos do ficheiro de modelo reutilizáveis e gratuita da implementação de tooa específico de valores.</span><span class="sxs-lookup"><span data-stu-id="6e429-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="6e429-241">Adicionar o que conjunto de dimensionamento de máquina virtual de toohello do todos os certificados de osProfile</span><span class="sxs-lookup"><span data-stu-id="6e429-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="6e429-242">Cada certificado que está instalado num cluster de Olá tem de ser configurado na secção de osProfile Olá do recurso de conjunto de dimensionamento de Olá (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="6e429-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="6e429-243">Esta ação dá instruções ao certificado Olá tooinstall de fornecedor de recursos de Olá no Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="6e429-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="6e429-244">Esta instalação inclui o certificado de cluster Olá e quaisquer certificados de segurança de aplicações que planeia toouse para as suas aplicações:</span><span class="sxs-lookup"><span data-stu-id="6e429-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="6e429-245">Configurar o certificado de cluster do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="6e429-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="6e429-246">certificado de autenticação do cluster Olá tem de ser configurado em ambos os recursos de cluster de Service Fabric Olá (Microsoft.ServiceFabric/clusters) e define Olá extensão do Service Fabric de dimensionamento da máquina virtual no recurso de conjunto de dimensionamento de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="6e429-247">Esta disposição permite tooconfigure de fornecedor de recursos de Service Fabric Olá-lo para ser utilizado para autenticação de cluster e autenticação de servidor para pontos finais de gestão.</span><span class="sxs-lookup"><span data-stu-id="6e429-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="6e429-248">Recurso de conjunto de dimensionamento de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="6e429-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="6e429-249">Recurso de infraestrutura de serviço:</span><span class="sxs-lookup"><span data-stu-id="6e429-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="6e429-250">Inserir a configuração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e429-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="6e429-251">configuração de Olá do Azure AD que criou anteriormente pode ser inserida diretamente no seu modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6e429-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="6e429-252">No entanto, recomendamos que primeiro extrair os valores de Olá para um parâmetros ficheiro tookeep Olá Resource Manager modelo reutilizáveis e gratuita da implementação de tooa específico de valores.</span><span class="sxs-lookup"><span data-stu-id="6e429-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="6e429-253">< um "Configurar-braço" ></a>parâmetros de modelo do Resource Manager configurar</span><span class="sxs-lookup"><span data-stu-id="6e429-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="6e429-254">Por fim, utilize os valores de saída de Olá do Cofre de chaves de Olá e o ficheiro de parâmetros do Azure AD PowerShell comandos toopopulate Olá:</span><span class="sxs-lookup"><span data-stu-id="6e429-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="6e429-255">Nesta fase, deve ter Olá seguintes elementos no local:</span><span class="sxs-lookup"><span data-stu-id="6e429-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="6e429-256">Grupo de recursos do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6e429-256">Key vault resource group</span></span>
  * <span data-ttu-id="6e429-257">Key Vault</span><span class="sxs-lookup"><span data-stu-id="6e429-257">Key vault</span></span>
  * <span data-ttu-id="6e429-258">Certificado de autenticação de servidor de cluster</span><span class="sxs-lookup"><span data-stu-id="6e429-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="6e429-259">Certificado de encriptação de dados</span><span class="sxs-lookup"><span data-stu-id="6e429-259">Data encipherment certificate</span></span>
* <span data-ttu-id="6e429-260">Inquilino do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e429-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="6e429-261">Aplicação Azure AD para a gestão baseada na web e o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="6e429-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="6e429-262">Aplicação Azure AD para a gestão de cliente nativo</span><span class="sxs-lookup"><span data-stu-id="6e429-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="6e429-263">Os utilizadores e as respetivas funções atribuídas</span><span class="sxs-lookup"><span data-stu-id="6e429-263">Users and their assigned roles</span></span>
* <span data-ttu-id="6e429-264">Modelo de Gestor de recursos de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e429-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="6e429-265">Certificados configurados por meio do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6e429-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="6e429-266">Azure Active Directory configurado</span><span class="sxs-lookup"><span data-stu-id="6e429-266">Azure Active Directory configured</span></span>

<span data-ttu-id="6e429-267">Olá seguinte diagrama ilustra onde ajustam o seu Cofre de chaves e a configuração do AD do Azure ao seu modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6e429-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mapa de dependência do Gestor de recursos][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="6e429-269">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="6e429-269">Create hello cluster</span></span>
<span data-ttu-id="6e429-270">Agora, está pronto toocreate cluster de Olá utilizando [implementação do modelo de recursos do Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="6e429-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="6e429-271">Testá-lo</span><span class="sxs-lookup"><span data-stu-id="6e429-271">Test it</span></span>
<span data-ttu-id="6e429-272">Utilize o modelo do Resource Manager com um ficheiro de parâmetros a Olá seguir tootest de comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6e429-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="6e429-273">Implementá-la</span><span class="sxs-lookup"><span data-stu-id="6e429-273">Deploy it</span></span>
<span data-ttu-id="6e429-274">Se passar de teste de modelo do Resource Manager Olá, utilize Olá seguir toodeploy de comando do PowerShell do modelo do Resource Manager com um ficheiro de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6e429-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="6e429-275">Atribuir utilizadores tooroles</span><span class="sxs-lookup"><span data-stu-id="6e429-275">Assign users tooroles</span></span>
<span data-ttu-id="6e429-276">Depois de criar Olá aplicações toorepresent o cluster, atribuir os seus utilizadores funções toohello suportadas pelo Service Fabric: só de leitura e administrador. Pode atribuir funções de Olá utilizando Olá [portal clássico do Azure][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="6e429-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="6e429-277">No portal do Azure Olá, aceda tooyour inquilino e, em seguida, selecione **aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6e429-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="6e429-278">Selecione a aplicação web Olá, que tem um nome como `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="6e429-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="6e429-279">Clique em Olá **utilizadores** separador.</span><span class="sxs-lookup"><span data-stu-id="6e429-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="6e429-280">Selecione um tooassign de utilizador e, em seguida, clique em Olá **atribuir** botão na Olá parte inferior do ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Atribuir botão tooroles de utilizadores][assign-users-to-roles-button]
5. <span data-ttu-id="6e429-282">Selecione Olá função tooassign toohello utilizador.</span><span class="sxs-lookup"><span data-stu-id="6e429-282">Select hello role tooassign toohello user.</span></span>

    ![Caixa de diálogo "Atribuir utilizadores"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="6e429-284">Para obter mais informações sobre as funções no Service Fabric, consulte [controlo de acesso baseado em funções para clientes de Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6e429-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="6e429-285">Criar clusters seguros no Linux</span><span class="sxs-lookup"><span data-stu-id="6e429-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="6e429-286">processo de Olá toomake mais fácil, fornecemos uma [script de programa auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="6e429-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="6e429-287">Antes de utilizar este script de programa auxiliar, certifique-se de que já tem interface de linha de comandos do Azure (CLI) instalado e é no seu caminho.</span><span class="sxs-lookup"><span data-stu-id="6e429-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="6e429-288">Certifique-se de que o script de Olá tem permissões tooexecute executando `chmod +x cert_helper.py` após transferindo-a.</span><span class="sxs-lookup"><span data-stu-id="6e429-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="6e429-289">Step-by-Olá primeiro passo é toosign no tooyour conta do Azure ao utilizar a CLI com Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="6e429-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="6e429-290">Depois de iniciarem sessão tooyour conta do Azure, o script de programa auxiliar de Olá utilização com a sua AC assinado certificado, como Olá comando mostra os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6e429-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="6e429-291">parâmetro de - ifile Olá pode demorar um ficheiro. pfx ou um ficheiro. pem como entrada, com o tipo de certificado Olá (pfx ou pem ou ss se se tratar de um certificado autoassinado).</span><span class="sxs-lookup"><span data-stu-id="6e429-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="6e429-292">Olá parâmetro -h imprime o texto de ajuda de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="6e429-293">Este comando devolve Olá seguintes três cadeias como saída Olá:</span><span class="sxs-lookup"><span data-stu-id="6e429-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="6e429-294">SourceVaultID, que é o ID de Olá para Olá novo ResourceGroup de KeyVault-criado para si</span><span class="sxs-lookup"><span data-stu-id="6e429-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="6e429-295">CertificateUrl para aceder ao certificado Olá</span><span class="sxs-lookup"><span data-stu-id="6e429-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="6e429-296">CertificateThumbprint, que é utilizado para autenticação</span><span class="sxs-lookup"><span data-stu-id="6e429-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="6e429-297">Olá seguinte exemplo mostra como toouse Olá, comando:</span><span class="sxs-lookup"><span data-stu-id="6e429-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="6e429-298">Executar Olá precedente fornecem comando Olá três cadeias da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6e429-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="6e429-299">nome do requerente do certificado Olá tem de corresponder ao domínio Olá que utilize o cluster do Service Fabric tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="6e429-300">Esta correspondência é necessário tooprovide um SSL para pontos finais de gestão do cluster Olá HTTPS e o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e429-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="6e429-301">Não é possível obter um certificado SSL a partir de uma AC para Olá `.cloudapp.azure.com` domínio.</span><span class="sxs-lookup"><span data-stu-id="6e429-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="6e429-302">Tem de obter um nome de domínio personalizado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="6e429-303">Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="6e429-304">Estes nomes de requerente são entradas Olá terá toocreate um cluster do Service Fabric seguro (do Azure AD), conforme descrito em [parâmetros de modelo do Resource Manager configurar](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="6e429-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="6e429-305">Pode ligar cluster segura toohello seguindo as instruções de Olá para [autenticar o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6e429-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="6e429-306">Clusters de pré-visualização do Linux não suportam a autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e429-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="6e429-307">Pode atribuir funções de administrador e cliente conforme descrito em Olá [atribuir funções toousers](#assign-roles) secção.</span><span class="sxs-lookup"><span data-stu-id="6e429-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="6e429-308">Quando especificar as funções de administrador e o cliente para um cluster de pré-visualização do Linux, tem tooprovide thumbprints de certificado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="6e429-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="6e429-309">(Não fornecer nome de requerente Olá, porque não está a ser efetuada nenhuma validação da cadeia ou revogação nesta versão de pré-visualização.)</span><span class="sxs-lookup"><span data-stu-id="6e429-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="6e429-310">Se quiser toouse um certificado autoassinado para fins de teste, pode utilizar Olá mesmo toogenerate script uma.</span><span class="sxs-lookup"><span data-stu-id="6e429-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="6e429-311">Em seguida, pode carregar o Cofre de chaves Olá certificado tooyour fornecendo o sinalizador de Olá `ss` em vez de fornecer o nome de caminho e o certificado do certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="6e429-312">Por exemplo, consulte Olá seguinte comando para criar e carregar um certificado autoassinado:</span><span class="sxs-lookup"><span data-stu-id="6e429-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="6e429-313">Este comando devolve Olá mesmas três cadeias: SourceVault, CertificateUrl e CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="6e429-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="6e429-314">Em seguida, pode utilizar Olá cadeias toocreate um cluster com Linux seguro e uma localização onde o certificado autoassinado Olá está colocado.</span><span class="sxs-lookup"><span data-stu-id="6e429-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="6e429-315">Terá de cluster do Olá certificado autoassinado tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="6e429-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="6e429-316">Pode ligar cluster segura toohello seguindo as instruções de Olá para [autenticar o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6e429-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="6e429-317">nome do requerente do certificado Olá tem de corresponder ao domínio Olá que utilize o cluster do Service Fabric tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="6e429-318">Esta correspondência é necessário tooprovide um SSL para pontos finais de gestão do cluster Olá HTTPS e o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e429-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="6e429-319">Não é possível obter um certificado SSL a partir de uma AC para Olá `.cloudapp.azure.com` domínio.</span><span class="sxs-lookup"><span data-stu-id="6e429-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="6e429-320">Tem de obter um nome de domínio personalizado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="6e429-321">Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.</span><span class="sxs-lookup"><span data-stu-id="6e429-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="6e429-322">Pode preencher os parâmetros de Olá do script de programa auxiliar de Olá no Olá portal do Azure, conforme descrito em Olá [cria um cluster no portal do Azure de Olá](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) secção.</span><span class="sxs-lookup"><span data-stu-id="6e429-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e429-323">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6e429-323">Next steps</span></span>
<span data-ttu-id="6e429-324">Neste momento, tiver um cluster seguro com fornecer autenticação de gestão do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6e429-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="6e429-325">Em seguida, [ligar tooyour cluster](service-fabric-connect-to-secure-cluster.md) e saber como demasiado[gerir segredos de aplicação](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="6e429-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="6e429-326">Resolver problemas de definição de cópia de segurança do Azure Active Directory para autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="6e429-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="6e429-327">Caso se depare com um problema enquanto estiver a configurar do Azure AD para autenticação de cliente, consulte possíveis soluções de Olá nesta secção.</span><span class="sxs-lookup"><span data-stu-id="6e429-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="6e429-328">Service Fabric Explorer pede-lhe tooselect um certificado</span><span class="sxs-lookup"><span data-stu-id="6e429-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="6e429-329">Problema</span><span class="sxs-lookup"><span data-stu-id="6e429-329">Problem</span></span>
<span data-ttu-id="6e429-330">Depois de iniciar sessão com êxito a tooAzure AD no Service Fabric Explorer, browser Olá devolve home page do toohello, mas uma mensagem pede-lhe tooselect um certificado.</span><span class="sxs-lookup"><span data-stu-id="6e429-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Caixa de diálogo do SFX selecione o certificado][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="6e429-332">Razão</span><span class="sxs-lookup"><span data-stu-id="6e429-332">Reason</span></span>
<span data-ttu-id="6e429-333">utilizador Olá não está atribuído uma função no Olá aplicação de cluster do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e429-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="6e429-334">Assim, a autenticação do Azure AD falha no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e429-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="6e429-335">Service Fabric Explorer retrocede toocertificate autenticação.</span><span class="sxs-lookup"><span data-stu-id="6e429-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="6e429-336">Solução</span><span class="sxs-lookup"><span data-stu-id="6e429-336">Solution</span></span>
<span data-ttu-id="6e429-337">Siga as instruções de Olá para configurar o Azure AD e atribuir funções de utilizador.</span><span class="sxs-lookup"><span data-stu-id="6e429-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="6e429-338">Além disso, recomendamos que ative "Aplicação utilizador atribuição tooaccess necessária," como `SetupApplications.ps1` does.</span><span class="sxs-lookup"><span data-stu-id="6e429-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="6e429-339">Falha da ligação com o PowerShell com um erro: "Olá especificado credenciais são inválidas"</span><span class="sxs-lookup"><span data-stu-id="6e429-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="6e429-340">Problema</span><span class="sxs-lookup"><span data-stu-id="6e429-340">Problem</span></span>
<span data-ttu-id="6e429-341">Quando utilizar o PowerShell tooconnect toohello cluster utilizando o modo de segurança "AzureActiveDirectory", depois de iniciar sessão com êxito tooAzure AD, falha na ligação de Olá com um erro: "Olá especificado que credenciais são inválidas."</span><span class="sxs-lookup"><span data-stu-id="6e429-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="6e429-342">Solução</span><span class="sxs-lookup"><span data-stu-id="6e429-342">Solution</span></span>
<span data-ttu-id="6e429-343">Esta solução é Olá que igual Olá anterior a um.</span><span class="sxs-lookup"><span data-stu-id="6e429-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="6e429-344">Service Fabric Explorer devolve uma falha ao iniciar sessão: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="6e429-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="6e429-345">Problema</span><span class="sxs-lookup"><span data-stu-id="6e429-345">Problem</span></span>
<span data-ttu-id="6e429-346">Quando tenta toosign no tooAzure AD no Service Fabric Explorer, a página Olá devolve uma falha: "AADSTS50011: Olá endereço de resposta &lt;url&gt; não correspondem aos endereços de resposta de Olá configurados para a aplicação Olá: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="6e429-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![Não corresponde ao endereço de resposta SFX][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="6e429-348">Razão</span><span class="sxs-lookup"><span data-stu-id="6e429-348">Reason</span></span>
<span data-ttu-id="6e429-349">aplicação de cluster (web) de Olá que representa o Service Fabric Explorer tenta tooauthenticate no Azure AD e como parte do pedido de Olá fornece URL de retorno de redirecionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="6e429-350">Mas Olá URL não está listado na aplicação Olá do Azure AD **URL de resposta** lista.</span><span class="sxs-lookup"><span data-stu-id="6e429-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="6e429-351">Solução</span><span class="sxs-lookup"><span data-stu-id="6e429-351">Solution</span></span>
<span data-ttu-id="6e429-352">No Olá **configurar** separador de Olá aplicação (web) do cluster, adicione Olá URL do Service Fabric Explorer toohello **URL de resposta** lista ou substituir um dos itens de Olá na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="6e429-353">Quando tiver terminado, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="6e429-353">When you have finished, save your change.</span></span>

![Url de resposta de aplicação Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="6e429-355">Ligue o cluster de Olá, utilizando a autenticação do Azure AD através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e429-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="6e429-356">Olá tooconnect cluster do Service Fabric, utilize Olá seguinte o exemplo de comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6e429-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="6e429-357">toolearn sobre Olá Connect-ServiceFabricCluster cmdlet, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e429-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="6e429-358">Pode reutilizar inquilino Olá mesmo Azure AD em vários clusters?</span><span class="sxs-lookup"><span data-stu-id="6e429-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="6e429-359">Sim.</span><span class="sxs-lookup"><span data-stu-id="6e429-359">Yes.</span></span> <span data-ttu-id="6e429-360">Mas, lembre-se a aplicação do tooadd Olá URL do Service Fabric Explorer tooyour cluster (web).</span><span class="sxs-lookup"><span data-stu-id="6e429-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="6e429-361">Caso contrário, o Service Fabric Explorer não funciona.</span><span class="sxs-lookup"><span data-stu-id="6e429-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="6e429-362">Por que motivo é ainda necessário um certificado de servidor ao Azure AD está ativado?</span><span class="sxs-lookup"><span data-stu-id="6e429-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="6e429-363">FabricClient e FabricGateway executará uma autenticação mútua.</span><span class="sxs-lookup"><span data-stu-id="6e429-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="6e429-364">Durante a autenticação do Azure AD, a integração do Azure AD fornece um cliente servidor toohello de identidade e o certificado de servidor Olá é identidade do servidor utilizado tooverify Olá.</span><span class="sxs-lookup"><span data-stu-id="6e429-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="6e429-365">Para obter mais informações sobre certificados de Service Fabric, consulte [certificados x. 509 e o Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="6e429-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

