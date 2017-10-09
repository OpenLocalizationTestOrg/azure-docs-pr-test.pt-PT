---
title: "cluster de aaaCreate Service Fabric no Olá portal do Azure | Microsoft Docs"
description: "Este artigo descreve como tooset configurar um cluster do Service Fabric seguro no Azure com Olá portal do Azure e o Cofre de chaves do Azure."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="da443-103">Criar um cluster do Service Fabric no Azure utilizando o Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da443-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da443-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="da443-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="da443-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da443-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="da443-106">Este é um guia passo a passo que explica Olá passos de configuração de um cluster do Service Fabric seguro no Azure utilizando o Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="da443-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="da443-107">Este guia explica Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="da443-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="da443-108">Configure as chaves de toomanage do Cofre de chaves de segurança do cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="da443-109">Crie um cluster protegido no Azure através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="da443-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="da443-110">Autentica os administradores a utilização de certificados.</span><span class="sxs-lookup"><span data-stu-id="da443-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="da443-111">Para opções de segurança mais avançadas, como a autenticação de utilizador no Azure Active Directory e como configurar certificados para a segurança da aplicação, [criar o cluster com o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="da443-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="da443-112">Um cluster seguro é um cluster que impede que as operações de acesso não autorizado toomanagement, que inclui implementar, atualizar e eliminar dados de Olá contêm, serviços e aplicações.</span><span class="sxs-lookup"><span data-stu-id="da443-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="da443-113">Um cluster não seguro é um cluster que qualquer pessoa pode ligar tooat qualquer altura e efetuar operações de gestão.</span><span class="sxs-lookup"><span data-stu-id="da443-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="da443-114">Embora seja possível toocreate um cluster não seguro, é **altamente recomendado toocreate um cluster seguro**.</span><span class="sxs-lookup"><span data-stu-id="da443-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="da443-115">Um cluster não seguro **não pode ser protegida mais tarde** -tem de ser criado um novo cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="da443-116">conceitos de Olá são Olá iguais para a criação de clusters seguros, quer clusters Olá clusters do Linux ou clusters do Windows.</span><span class="sxs-lookup"><span data-stu-id="da443-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="da443-117">Para mais informações e do programa auxiliar de scripts para a criação de clusters seguros do Linux, consulte [criação de clusters seguros no Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="da443-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="da443-118">Olá parâmetros obtidos pelo script de programa auxiliar de Olá fornecida podem ser introduzidos diretamente no portal de Olá conforme descrito na secção de Olá [cria um cluster no portal do Azure de Olá](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="da443-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="da443-119">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="da443-119">Log in tooAzure</span></span>
<span data-ttu-id="da443-120">Este guia utiliza [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="da443-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="da443-121">Ao iniciar uma nova sessão do PowerShell, inicie sessão no tooyour a conta do Azure e selecionar a sua subscrição antes de executar os comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="da443-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="da443-122">Inicie sessão na conta tooyour do azure:</span><span class="sxs-lookup"><span data-stu-id="da443-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="da443-123">Selecione a sua subscrição:</span><span class="sxs-lookup"><span data-stu-id="da443-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="da443-124">Configurar o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="da443-124">Set up Key Vault</span></span>
<span data-ttu-id="da443-125">Esta parte do guia de Olá explica como criar um cofre de chave para um cluster do Service Fabric no Azure e para aplicações de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="da443-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="da443-126">Para obter um guia completo no Cofre de chaves, consulte Olá [Cofre de chaves guia de introdução][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="da443-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="da443-127">O Service Fabric utiliza toosecure de certificados x. 509 um cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="da443-128">O Cofre de chaves do Azure é toomanage utilizados certificados para clusters de Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="da443-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="da443-129">Quando um cluster é implementado no Azure, o fornecedor de recursos do Azure de Olá responsável pela criação de clusters de Service Fabric obtém certificados a partir do Cofre de chaves e instala-los num cluster de Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="da443-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="da443-130">Olá diagrama seguinte ilustra Olá relação entre o Cofre de chaves, um cluster do Service Fabric e fornecedor de recursos do Azure de Olá que utiliza certificados armazenados no Cofre de chaves quando cria um cluster:</span><span class="sxs-lookup"><span data-stu-id="da443-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="da443-132">Criar um Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="da443-132">Create a Resource Group</span></span>
<span data-ttu-id="da443-133">Step-by-Olá primeiro passo é toocreate um novo grupo de recursos especificamente para o Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="da443-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="da443-134">Colocar o Cofre de chaves ao seu próprio grupo de recursos é recomendado, para que possa remover grupos de recursos de computação e armazenamento - como grupo de recursos de Olá que tenha o seu cluster do Service Fabric - sem perder as chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="da443-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="da443-135">grupo de recursos de Olá que tenha o seu Cofre de chaves tem de constar Olá mesma região que o cluster de Olá que está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="da443-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="da443-136">Criar Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="da443-136">Create Key Vault</span></span>
<span data-ttu-id="da443-137">Crie um cofre de chaves no novo grupo de recursos Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="da443-138">Olá Cofre de chaves **tem de estar ativado para a implementação** tooallow Olá certificados tooget de fornecedor de recursos do Service Fabric do mesmo e instalar em nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="da443-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

<span data-ttu-id="da443-139">Se tiver um cofre de chaves existente, pode ativá-la para implementação utilizando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="da443-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="da443-140">Adicione certificados tooKey Cofre</span><span class="sxs-lookup"><span data-stu-id="da443-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="da443-141">Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações.</span><span class="sxs-lookup"><span data-stu-id="da443-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="da443-142">Para obter mais informações sobre como os certificados são utilizados no Service Fabric, consulte [cenários de segurança de cluster do Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="da443-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="da443-143">Cluster e servidor de certificado (obrigatório)</span><span class="sxs-lookup"><span data-stu-id="da443-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="da443-144">Este certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit.</span><span class="sxs-lookup"><span data-stu-id="da443-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="da443-145">Fornece segurança de cluster de algumas formas:</span><span class="sxs-lookup"><span data-stu-id="da443-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="da443-146">**Autenticação do cluster:** autentica o nó de nó de comunicação para a Federação de cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="da443-147">Apenas nós que podem provar a sua identidade com este certificado podem associar cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="da443-148">**Autenticação de servidor:** autentica Olá cluster pontos finais tooa gestão cliente de gestão, para hello cliente de gestão sabe que está a falar com toohello real cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="da443-149">Este certificado fornece também SSL para Olá API de gestão HTTPS e para o Service Fabric Explorer através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da443-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="da443-150">tooserve estes fins, certificado Olá têm de cumprir os requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="da443-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="da443-151">certificado de Olá tem de conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="da443-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="da443-152">certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).</span><span class="sxs-lookup"><span data-stu-id="da443-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="da443-153">Olá nome do requerente do certificado deve corresponder ao cluster do Service Fabric Olá domínio utilizado tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="da443-154">Este é necessário tooprovide SSL para do cluster Olá pontos finais de gestão HTTPS e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="da443-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="da443-155">Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para Olá `.cloudapp.azure.com` domínio.</span><span class="sxs-lookup"><span data-stu-id="da443-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="da443-156">Adquirir um nome de domínio personalizado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="da443-157">Quando solicita um certificado do nome do requerente de um certificado de Olá de AC tem de corresponder ao nome de domínio personalizado de Olá utilizado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="da443-158">Certificados de autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="da443-158">Client authentication certificates</span></span>
<span data-ttu-id="da443-159">Certificados de cliente adicionais autenticar os administradores para tarefas de gestão do cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="da443-160">Serviço de recursos de infraestrutura tem dois níveis de acesso: **admin** e **utilizador só de leitura**.</span><span class="sxs-lookup"><span data-stu-id="da443-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="da443-161">No mínimo, um único certificado para acesso administrativo deve ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="da443-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="da443-162">Para acesso de nível de utilizador adicionais, tem de ser fornecido um certificado diferente.</span><span class="sxs-lookup"><span data-stu-id="da443-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="da443-163">Para obter mais informações sobre funções de acesso, consulte [controlo de acesso baseado em funções para clientes de Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="da443-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="da443-164">Não é necessário tooupload cliente autenticação certificados tooKey cofre toowork com o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="da443-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="da443-165">Estes certificados basta toobe fornecido toousers que têm autorização para gestão de clusters.</span><span class="sxs-lookup"><span data-stu-id="da443-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="da443-166">Azure Active Directory é Olá recomendado clientes tooauthenticate de forma para o cluster operações de gestão.</span><span class="sxs-lookup"><span data-stu-id="da443-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="da443-167">toouse do Azure Active Directory, tem de [criar um cluster com o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="da443-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="da443-168">Certificados de aplicação (opcionais)</span><span class="sxs-lookup"><span data-stu-id="da443-168">Application certificates (optional)</span></span>
<span data-ttu-id="da443-169">Qualquer número de certificados adicionais pode ser instalado num cluster por motivos de segurança da aplicação.</span><span class="sxs-lookup"><span data-stu-id="da443-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="da443-170">Antes de criar o cluster, considere os cenários de segurança de aplicação Olá que requerem toobe um certificado instalado em nós de Olá, tal como:</span><span class="sxs-lookup"><span data-stu-id="da443-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="da443-171">Encriptação e desencriptação de valores de configuração de aplicação</span><span class="sxs-lookup"><span data-stu-id="da443-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="da443-172">Encriptação dos dados em nós durante a replicação</span><span class="sxs-lookup"><span data-stu-id="da443-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="da443-173">Certificados de aplicação não podem ser configurados quando criar um cluster através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="da443-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="da443-174">certificados de aplicação tooconfigure no momento da configuração de cluster, tem de [criar um cluster com o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="da443-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="da443-175">Também pode adicionar o cluster de toohello de certificados de aplicação depois de terem sido criadas.</span><span class="sxs-lookup"><span data-stu-id="da443-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="da443-176">Formatação certificados para utilização do fornecedor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="da443-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="da443-177">Ficheiros de chave privados (. pfx) podem ser adicionados e podem ser utilizados diretamente através do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="da443-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="da443-178">No entanto, o fornecedor de recursos do Azure de Olá requer toobe chaves armazenada no formato JSON especial que inclui. pfx de Olá como uma base-64 codificada cadeia e Olá privada chave palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="da443-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="da443-179">tooaccommodate estes requisitos, as chaves têm de ser colocados numa cadeia JSON e, em seguida, armazenados como *segredos* no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="da443-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="da443-180">toomake este processo mais fácil, um módulo do PowerShell está [está disponível no GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="da443-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="da443-181">Siga o módulo de Olá de toouse estes passos:</span><span class="sxs-lookup"><span data-stu-id="da443-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="da443-182">Transferir o conteúdo completo de Olá do repositório de Olá para um diretório local.</span><span class="sxs-lookup"><span data-stu-id="da443-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="da443-183">Importe o módulo Olá na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="da443-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="da443-184">Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell automaticamente formatos uma chave privada do certificado numa cadeia JSON e carrega-tooKey cofre.</span><span class="sxs-lookup"><span data-stu-id="da443-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="da443-185">Utilize-o certificado de cluster de Olá tooadd e qualquer tooKey de certificados de aplicação adicional cofre.</span><span class="sxs-lookup"><span data-stu-id="da443-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="da443-186">Repita este passo para todos os certificados adicionais que pretende tooinstall no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="da443-187">Estes são todos os pré-requisitos do Cofre de chaves de Olá para configurar um modelo de Gestor de recursos de cluster de Service Fabric que instala os certificados para autenticação de nó, segurança ponto a ponto de gestão e a autenticação e qualquer segurança adicional das aplicações funcionalidades que utilizam certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="da443-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="da443-188">Neste momento, agora, deve ter Olá a seguinte configuração no Azure:</span><span class="sxs-lookup"><span data-stu-id="da443-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="da443-189">Grupo de recursos do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="da443-189">Key Vault resource group</span></span>
  * <span data-ttu-id="da443-190">Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="da443-190">Key Vault</span></span>
    * <span data-ttu-id="da443-191">Certificado de autenticação de servidor de cluster</span><span class="sxs-lookup"><span data-stu-id="da443-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="da443-192">< /a "Criar-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="da443-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="da443-193">Criar cluster no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da443-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="da443-194">Procurar Olá recurso de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="da443-194">Search for hello Service Fabric cluster resource</span></span>
![Procure o modelo de cluster do Service Fabric no Olá portal do Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="da443-196">Inicie sessão no toohello [portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="da443-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="da443-197">Clique em **novo** tooadd um novo modelo de recursos.</span><span class="sxs-lookup"><span data-stu-id="da443-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="da443-198">Pesquisa para o modelo de Cluster do Service Fabric Olá no Olá **Marketplace** em **tudo**.</span><span class="sxs-lookup"><span data-stu-id="da443-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="da443-199">Selecione **Cluster do Service Fabric** da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="da443-200">Navegue toohello **Cluster do Service Fabric** painel, clique em **criar**,</span><span class="sxs-lookup"><span data-stu-id="da443-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="da443-201">Olá **cluster do Service Fabric criar** painel tem Olá quatro passos a seguir.</span><span class="sxs-lookup"><span data-stu-id="da443-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="da443-202">1. Noções básicas</span><span class="sxs-lookup"><span data-stu-id="da443-202">1. Basics</span></span>
![Captura de ecrã da criação de um novo grupo de recursos.][CreateRG]

<span data-ttu-id="da443-204">No painel de noções básicas de Olá terá detalhes básicos do tooprovide Olá para o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="da443-205">Introduza o nome de Olá do cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="da443-206">Introduza um **nome de utilizador** e **palavra-passe** para ambiente de trabalho remoto para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="da443-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="da443-207">Certifique-se de que tooselect Olá **subscrição** que pretende que o toobe cluster implementada, especialmente se tiver várias subscrições.</span><span class="sxs-lookup"><span data-stu-id="da443-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="da443-208">Criar um **novo grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="da443-208">Create a **new resource group**.</span></span> <span data-ttu-id="da443-209">É melhor toogive-Olá mesmo nome do cluster de Olá, uma vez que o ajuda a localizar mais tarde, especialmente quando estiver a tentar toomake alterações tooyour implementação ou eliminar o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da443-210">Embora, pode decidir toouse um grupo de recursos existente, é uma boa prática toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="da443-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="da443-211">Isto torna toodelete fácil clusters que não é necessário.</span><span class="sxs-lookup"><span data-stu-id="da443-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="da443-212">Selecione Olá **região** do qual pretende que o cluster de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="da443-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="da443-213">Tem de utilizar Olá consta mesma região que a chave do cofre.</span><span class="sxs-lookup"><span data-stu-id="da443-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="da443-214">2. Configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="da443-214">2. Cluster configuration</span></span>
![Criar um tipo de nó][CreateNodeType]

<span data-ttu-id="da443-216">Configure os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-216">Configure your cluster nodes.</span></span> <span data-ttu-id="da443-217">Definem os tipos de nó tamanhos de VM Olá, Olá número de VMs e as respetivas propriedades.</span><span class="sxs-lookup"><span data-stu-id="da443-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="da443-218">O cluster pode ter mais do que um tipo de nó, mas o tipo de nó principal Olá (Olá primeiro uma por si no portal de Olá) tem de ter, pelo menos, cinco VMs, que é o tipo de nó olá onde são colocados serviços do sistema de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="da443-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="da443-219">Não configure **as propriedades de colocação** porque uma propriedade de posicionamento predefinido de "NodeTypeName" é adicionada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="da443-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="da443-220">Um cenário comum para vários tipos de nó é uma aplicação que contém um serviço front-end e um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="da443-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="da443-221">Pretende que o serviço de front-end Olá tooput em VMs mais pequenos (tamanhos de VM, como D2) com portas abertas toohello Internet, mas quiser o serviço de back-end de Olá tooput em VMs maior (com tamanhos de VM, como D4, D6, D15 e assim sucessivamente) com não abrir as portas para a Internet.</span><span class="sxs-lookup"><span data-stu-id="da443-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="da443-222">Escolha um nome para o seu tipo de nó (1 too12 carateres apenas letras e números).</span><span class="sxs-lookup"><span data-stu-id="da443-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="da443-223">Olá mínimo **tamanho** de VMs para o nó principal Olá, tipo é suscitada pelo departamento por Olá **durabilidade** camada que escolher para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="da443-224">predefinição de Olá para o escalão de durabilidade Olá é bronze.</span><span class="sxs-lookup"><span data-stu-id="da443-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="da443-225">Para obter mais informações sobre a durabilidade, consulte [como toochoose Olá Service Fabric fiabilidade e cluster durabilidade][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="da443-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="da443-226">Selecione o tamanho da VM Olá e escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="da443-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="da443-227">VMs de série D tem unidades SSD e são altamente recomendadas para aplicações com monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="da443-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="da443-228">Não utilizar qualquer SKU de VM que tenha núcleos parciais ou de ter menos de 7 GB de capacidade de disco disponível.</span><span class="sxs-lookup"><span data-stu-id="da443-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="da443-229">Olá mínimo **número** de VMs para o nó principal Olá, tipo é suscitada pelo departamento por Olá **fiabilidade** camada que escolher.</span><span class="sxs-lookup"><span data-stu-id="da443-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="da443-230">predefinição de Olá para o escalão de fiabilidade Olá é Silver.</span><span class="sxs-lookup"><span data-stu-id="da443-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="da443-231">Para obter mais informações sobre a fiabilidade, consulte [como toochoose Olá Service Fabric fiabilidade e cluster durabilidade][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="da443-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="da443-232">Escolha o número de Olá de VMs para o tipo de nó Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="da443-233">Pode aumentar ou reduzir verticalmente o número de Olá de VMs num tipo de nó mais tarde, mas no tipo de nó principal Olá, Olá mínimo é controlada por nível de fiabilidade Olá que escolheu.</span><span class="sxs-lookup"><span data-stu-id="da443-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="da443-234">Outros tipos de nó podem ter um mínimo de 1 VM.</span><span class="sxs-lookup"><span data-stu-id="da443-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="da443-235">Configure pontos finais personalizados.</span><span class="sxs-lookup"><span data-stu-id="da443-235">Configure custom endpoints.</span></span> <span data-ttu-id="da443-236">Este campo permite-lhe tooenter uma lista separada por vírgulas de portas que pretende que o tooexpose Olá toohello de Balanceador de carga do Azure através da Internet pública para as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="da443-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="da443-237">Por exemplo, se planear toodeploy um cluster de tooyour de aplicação web, introduza "80" aqui tooallow tráfego na porta 80 para o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="da443-238">Para obter mais informações sobre os pontos finais, consulte [comunicar com aplicações][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="da443-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="da443-239">Configurar o cluster **diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="da443-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="da443-240">Por predefinição, o diagnóstico está ativado no seu tooassist de cluster com a resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="da443-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="da443-241">Se quiser toodisable diagnóstico alterar Olá **estado** alternar demasiado**desativar**.</span><span class="sxs-lookup"><span data-stu-id="da443-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="da443-242">Desativar diagnostics é **não** recomendado.</span><span class="sxs-lookup"><span data-stu-id="da443-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="da443-243">Selecione Olá pretende que o cluster de conjunto o modo de atualização de recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="da443-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="da443-244">Selecione **automática**, se pretende Olá sistema tooautomatically escolha segurança Olá versão mais recente disponível e tente tooupgrade tooit o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="da443-245">Definir o modo de Olá demasiado**Manual**, se pretender toochoose uma versão suportada.</span><span class="sxs-lookup"><span data-stu-id="da443-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="da443-246">Suportamos apenas os clusters que executam versões suportadas do serviço de recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="da443-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="da443-247">Ao selecionar Olá **Manual** modo, que está a efetuar no Olá responsabilidade tooupgrade a versão de tooa suportada do cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="da443-248">Para obter mais detalhes sobre o modo de atualização de recursos de infraestrutura do Olá Consulte Olá [documento de serviço--cluster-atualização do fabric.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="da443-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="da443-249">3. Segurança</span><span class="sxs-lookup"><span data-stu-id="da443-249">3. Security</span></span>
![Captura de ecrã das configurações de segurança no portal do Azure.][SecurityConfigs]

<span data-ttu-id="da443-251">passo final Olá é tooprovide certificado informações toosecure Olá de cluster utilizando Olá Cofre de chaves e certificados informações criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="da443-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="da443-252">Preencher os campos de certificados primários de Olá com a saída de Olá obtida a partir do carregamento Olá **certificado de cluster** tooKey cofre utilizando Olá `Invoke-AddCertToKeyVault` comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da443-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="da443-253">Verifique Olá **configurar as definições avançada** caixa tooenter certificados de cliente para **admin cliente** e **clientes apenas de leitura**.</span><span class="sxs-lookup"><span data-stu-id="da443-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="da443-254">Nestes campos, introduza o thumbprint Olá do seu certificado de cliente de administrador e thumbprint Olá do seu certificado de cliente de utilizador só de leitura, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="da443-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="da443-255">Quando os administradores tentam tooconnect toohello cluster, são concedidos acesso apenas se tiverem um certificado com um thumbprint que corresponda a valores de thumbprint Olá introduzido aqui.</span><span class="sxs-lookup"><span data-stu-id="da443-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="da443-256">4. Resumo</span><span class="sxs-lookup"><span data-stu-id="da443-256">4. Summary</span></span>
![<span data-ttu-id="da443-257">Captura de ecrã do painel de início de Olá apresentar "Implementar Cluster do Service Fabric."</span><span class="sxs-lookup"><span data-stu-id="da443-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="da443-258">criação do cluster de toocomplete Olá, clique em **resumo** configurações de Olá toosee que forneceu ou transferir Olá modelo Azure Resource Manager que que utilizado toodeploy o cluster.</span><span class="sxs-lookup"><span data-stu-id="da443-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="da443-259">Depois de ter fornecido definições obrigatórias Olá, Olá **OK** botão fica verde e pode iniciar o processo de criação do cluster Olá clicando nela.</span><span class="sxs-lookup"><span data-stu-id="da443-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="da443-260">Pode ver o progresso da criação Olá em notificações Olá.</span><span class="sxs-lookup"><span data-stu-id="da443-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="da443-261">(Clique ícone de campainha"Olá" junto da barra de estado de Olá na Olá canto superior direito do ecrã). Se clicou em **Pin tooStartboard** ao criar o cluster de Olá, verá **implementação de Cluster do Service Fabric** afixado toohello **iniciar** quadro.</span><span class="sxs-lookup"><span data-stu-id="da443-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="da443-262">Ver o estado do cluster</span><span class="sxs-lookup"><span data-stu-id="da443-262">View your cluster status</span></span>
![Captura de ecrã dos detalhes de cluster no dashboard de Olá.][ClusterDashboard]

<span data-ttu-id="da443-264">Depois do cluster foi criado, pode inspecionar o seu cluster no portal de Olá:</span><span class="sxs-lookup"><span data-stu-id="da443-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="da443-265">Aceda demasiado**procurar** e clique em **Clusters de recursos de infraestrutura de serviço**.</span><span class="sxs-lookup"><span data-stu-id="da443-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="da443-266">Localize o seu cluster e clique no mesmo.</span><span class="sxs-lookup"><span data-stu-id="da443-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="da443-267">Agora, pode ver os detalhes de Olá do cluster no dashboard de Olá, incluindo o ponto de final público do cluster Olá e tooService uma ligação Explorador de recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="da443-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="da443-268">Olá **Monitor nó** secção no painel de dashboard do cluster Olá indica o número de Olá de VMs que fazem o bom estado de funcionamento e não em bom estado.</span><span class="sxs-lookup"><span data-stu-id="da443-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="da443-269">Pode encontrar mais detalhes sobre o estado de funcionamento do cluster Olá em [introdução de modelo de estado de funcionamento do Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="da443-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="da443-270">Clusters de Service Fabric necessitam de um determinado número de nós toobe segurança sempre toomaintain disponibilidade e preservar o estado - tooas referenciado "manter o quórum".</span><span class="sxs-lookup"><span data-stu-id="da443-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="da443-271">Therfore, normalmente, não é seguro tooshut baixo todas as máquinas do cluster de Olá, exceto se tiver efetuado primeiro um [cópia de segurança completa do seu estado][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="da443-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="da443-272">Remoto ligar a instância de conjunto de dimensionamento da Máquina Virtual tooa ou um nó de cluster</span><span class="sxs-lookup"><span data-stu-id="da443-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="da443-273">Cada um dos Olá NodeTypes especificou nos resultados de cluster num conjunto de dimensionamento de Máquina Virtual ao obter a configuração.</span><span class="sxs-lookup"><span data-stu-id="da443-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="da443-274">Consulte [remoto ligar a instância de conjunto de dimensionamento da Máquina Virtual tooa] [ remote-connect-to-a-vm-scale-set] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="da443-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da443-275">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="da443-275">Next steps</span></span>
<span data-ttu-id="da443-276">Neste momento, tiver um cluster seguro que utilizar certificados para autenticação de gestão.</span><span class="sxs-lookup"><span data-stu-id="da443-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="da443-277">Em seguida, [ligar tooyour cluster](service-fabric-connect-to-secure-cluster.md) e saber como demasiado[gerir segredos de aplicação](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="da443-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="da443-278">Além disso, saiba mais sobre [as opções de suporte do Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="da443-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
