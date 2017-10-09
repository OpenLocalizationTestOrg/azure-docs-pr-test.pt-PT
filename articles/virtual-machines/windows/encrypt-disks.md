---
title: discos aaaEncrypt uma VM do Windows no Azure | Microsoft Docs
description: "Como tooencrypt discos virtuais numa VM do Windows para avançada segurança com o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="9ef11-103">Como tooencrypt discos virtuais numa VM do Windows</span><span class="sxs-lookup"><span data-stu-id="9ef11-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="9ef11-104">Para segurança avançada máquina virtual (VM) e conformidade, discos virtuais no Azure podem ser encriptados.</span><span class="sxs-lookup"><span data-stu-id="9ef11-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="9ef11-105">Discos estão encriptados com as chaves criptográficas que são protegidas um cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef11-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="9ef11-106">Pode controla estas chaves criptográficas e pode auditar a sua utilização.</span><span class="sxs-lookup"><span data-stu-id="9ef11-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="9ef11-107">Este artigo detalhes como tooencrypt discos virtuais numa VM do Windows com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ef11-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="9ef11-108">Também pode [encriptar uma VM com Linux utilizando Olá Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9ef11-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="9ef11-109">Descrição geral de encriptação de disco</span><span class="sxs-lookup"><span data-stu-id="9ef11-109">Overview of disk encryption</span></span>
<span data-ttu-id="9ef11-110">Discos virtuais em VMs do Windows são encriptados em descanso ao utilizar o Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="9ef11-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="9ef11-111">Não há sem encargos de encriptação de discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef11-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="9ef11-112">As chaves criptográficas são armazenadas no Cofre de chaves do Azure utilizando a proteção de software, ou pode importar ou gerar as suas chaves nos módulos de segurança de Hardware (HSMs) certificadas tooFIPS normas de nível 2 140-2.</span><span class="sxs-lookup"><span data-stu-id="9ef11-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="9ef11-113">Estas chaves criptográficas são utilizado tooencrypt e desencriptar discos virtuais anexados tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="9ef11-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="9ef11-114">Manter o controlo destas chaves criptográficas e pode auditar a sua utilização.</span><span class="sxs-lookup"><span data-stu-id="9ef11-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="9ef11-115">Um principal de serviço do Azure Active Directory fornece um mecanismo seguro para emitir estas chaves criptográficas como VMs estão ligados à corrente ou desligar.</span><span class="sxs-lookup"><span data-stu-id="9ef11-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="9ef11-116">processo de Olá para encriptar uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9ef11-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="9ef11-117">Crie uma chave criptográfica num cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef11-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="9ef11-118">Configure Olá criptografia chave toobe utilizada para encriptação de discos.</span><span class="sxs-lookup"><span data-stu-id="9ef11-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="9ef11-119">chave de criptografia Olá tooread de Olá Cofre de chaves do Azure, criar um serviço do Azure Active Directory principal com as permissões adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="9ef11-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="9ef11-120">Emita Olá comando tooencrypt os discos virtuais, especificando o principal de serviço do Azure Active Directory Olá e adequada toobe chave criptográfica utilizada.</span><span class="sxs-lookup"><span data-stu-id="9ef11-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="9ef11-121">pedidos principais de serviço do Azure Active Directory de Olá Olá necessário chave criptográfica do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef11-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="9ef11-122">discos virtuais Olá estão encriptados com a chave criptográfica Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="9ef11-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="9ef11-123">Processo de encriptação</span><span class="sxs-lookup"><span data-stu-id="9ef11-123">Encryption process</span></span>
<span data-ttu-id="9ef11-124">Encriptação de disco depende Olá os seguintes componentes adicionais:</span><span class="sxs-lookup"><span data-stu-id="9ef11-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="9ef11-125">**O Cofre de chaves do Azure** -utilizado toosafeguard de chaves criptográficas e segredos utilizados para o processo de encriptação/desencriptação de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="9ef11-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="9ef11-126">Se existir, pode utilizar um cofre de chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="9ef11-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="9ef11-127">Não dispõe de toodedicate discos de tooencrypting um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="9ef11-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="9ef11-128">limites administrativos tooseparate e visibilidade chave, pode criar um cofre de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="9ef11-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="9ef11-129">**Azure Active Directory** - identificadores Olá segura de troca de chaves criptográficas necessárias e as ações de pedido de autenticação para.</span><span class="sxs-lookup"><span data-stu-id="9ef11-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="9ef11-130">Normalmente, pode utilizar uma instância existente do Azure Active Directory para o alojamento da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9ef11-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="9ef11-131">principal de serviço Olá fornece um mecanismo segura toorequest e chaves criptográficas adequada de Olá de ser emitido.</span><span class="sxs-lookup"><span data-stu-id="9ef11-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="9ef11-132">Não estiver a desenvolver uma aplicação real, que se integra com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ef11-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="9ef11-133">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="9ef11-133">Requirements and limitations</span></span>
<span data-ttu-id="9ef11-134">Cenários suportados e os requisitos para encriptação de disco de:</span><span class="sxs-lookup"><span data-stu-id="9ef11-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="9ef11-135">Ativar a encriptação em novas VMs do Windows de imagens do Azure Marketplace ou imagem personalizada do VHD.</span><span class="sxs-lookup"><span data-stu-id="9ef11-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="9ef11-136">Ativar a encriptação em VMs do Windows existente no Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef11-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="9ef11-137">Ativar a encriptação em VMs do Windows que são configurados utilizando os espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9ef11-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="9ef11-138">A desativação da encriptação nos dados e SO unidades para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="9ef11-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="9ef11-139">Todos os recursos (por exemplo, o Cofre de chaves, a conta de armazenamento e a VM) tem de constar Olá mesma região do Azure e subscrição.</span><span class="sxs-lookup"><span data-stu-id="9ef11-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="9ef11-140">O escalão Standard VMs, tais como uma, série D, DS, G e GS VMs.</span><span class="sxs-lookup"><span data-stu-id="9ef11-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="9ef11-141">Encriptação de disco não é atualmente suportada no Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="9ef11-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="9ef11-142">Escalão básico VMs.</span><span class="sxs-lookup"><span data-stu-id="9ef11-142">Basic tier VMs.</span></span>
* <span data-ttu-id="9ef11-143">VMs criadas utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="9ef11-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="9ef11-144">A atualizar as chaves criptográficas Olá numa VM já encriptada.</span><span class="sxs-lookup"><span data-stu-id="9ef11-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="9ef11-145">Integração com o serviço de gestão de chaves no local.</span><span class="sxs-lookup"><span data-stu-id="9ef11-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="9ef11-146">Criar Cofre de chaves do Azure e as chaves</span><span class="sxs-lookup"><span data-stu-id="9ef11-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="9ef11-147">Antes de começar, certifique-se de que essa versão mais recente Olá de Olá tenha sido instalado o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ef11-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="9ef11-148">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ef11-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="9ef11-149">Ao longo de exemplos de comando Olá, substitua todos os parâmetros de exemplo com os seus próprios nomes, localização e valores de chave.</span><span class="sxs-lookup"><span data-stu-id="9ef11-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="9ef11-150">Olá exemplos seguintes utilizam uma convenção de *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span><span class="sxs-lookup"><span data-stu-id="9ef11-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="9ef11-151">primeiro passo de Olá é toocreate toostore um cofre de chaves do Azure, as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="9ef11-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="9ef11-152">O Cofre de chaves do Azure pode armazenar as chaves, segredos, ou palavras-passe que lhe permitem toosecurely implementá-la nas suas aplicações e serviços.</span><span class="sxs-lookup"><span data-stu-id="9ef11-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="9ef11-153">Para a encriptação de disco virtual, crie um cofre de chaves toostore uma chave criptográfica que é utilizado tooencrypt ou desencriptar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="9ef11-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="9ef11-154">Ativar o fornecedor do Cofre de chaves do Azure Olá dentro da sua subscrição do Azure com [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), em seguida, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="9ef11-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="9ef11-155">Olá exemplo seguinte cria um nome de grupo de recursos *myResourceGroup* no Olá *EUA Leste* localização:</span><span class="sxs-lookup"><span data-stu-id="9ef11-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="9ef11-156">Olá, Olá Cofre de chaves do Azure que contêm Olá chaves criptográfico e computação associada recursos, tais como o armazenamento e Olá própria VM tem de residir na mesma região.</span><span class="sxs-lookup"><span data-stu-id="9ef11-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="9ef11-157">Criar um cofre de chaves do Azure com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e ativar Olá Cofre de chaves para utilização com a encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="9ef11-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="9ef11-158">Especifique um nome exclusivo do Cofre de chaves para *keyVaultName* da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="9ef11-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="9ef11-159">Pode armazenar as chaves criptográficas utilizando software ou proteção de modelo de segurança de Hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="9ef11-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="9ef11-160">Utilizar um HSM necessita de um cofre de chaves de premium.</span><span class="sxs-lookup"><span data-stu-id="9ef11-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="9ef11-161">Há um toocreating custos adicionais um premium Cofre de chaves em vez de padrão Cofre de chaves que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="9ef11-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="9ef11-162">toocreate um premium Cofre de chaves no Olá precedente passo adicionar Olá *- Sku "Premium"* parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9ef11-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="9ef11-163">Olá exemplo seguinte utiliza as chaves protegidas de software, uma vez que criámos um cofre de chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="9ef11-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="9ef11-164">Olá plataforma do Azure para ambos os modelos de proteção, tem de toobe concedido acesso Olá de toorequest chaves criptográficas quando Olá VM arranca discos virtuais do toodecrypt Olá.</span><span class="sxs-lookup"><span data-stu-id="9ef11-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="9ef11-165">Criar uma chave criptográfica no seu Cofre de chaves com [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="9ef11-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="9ef11-166">Olá exemplo seguinte cria uma chave denominada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="9ef11-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="9ef11-167">Criar Olá principal de serviço do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ef11-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="9ef11-168">Quando os discos virtuais são encriptados ou desencriptados, especifique uma autenticação da conta toohandle Olá e troca de chaves criptográficas do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="9ef11-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="9ef11-169">Esta conta, um principal de serviço do Azure Active Directory, permite Olá plataforma Azure toorequest Olá adequada as chaves criptográficas em nome Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9ef11-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="9ef11-170">Uma instância do Azure Active Directory predefinida está disponível na sua subscrição, apesar de muitas organizações têm dedicado diretórios do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ef11-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="9ef11-171">Criar um principal de serviço no Azure Active Directory com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="9ef11-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="9ef11-172">toospecify uma palavra-passe segura, siga Olá [políticas de palavra-passe e restrições no Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="9ef11-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="9ef11-173">toosuccessfully encriptar ou desencriptar discos virtuais, as permissões chave criptográfica Olá armazenados no Cofre de chaves tem de ser definido toopermit Olá do Azure Active Directory serviço principal tooread Olá chaves.</span><span class="sxs-lookup"><span data-stu-id="9ef11-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="9ef11-174">Definir as permissões no seu Cofre de chaves com [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="9ef11-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="9ef11-175">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ef11-175">Create virtual machine</span></span>
<span data-ttu-id="9ef11-176">tootest Olá o processo de encriptação, vamos criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="9ef11-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="9ef11-177">Olá exemplo seguinte cria uma VM chamada *myVM* utilizando um *Datacenter do Windows Server 2016* imagem:</span><span class="sxs-lookup"><span data-stu-id="9ef11-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="9ef11-178">Encriptar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ef11-178">Encrypt virtual machine</span></span>
<span data-ttu-id="9ef11-179">discos virtuais do Olá tooencrypt, colocar em conjunto todos os componentes de Olá anterior:</span><span class="sxs-lookup"><span data-stu-id="9ef11-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="9ef11-180">Especifique Olá principal de serviço do Azure Active Directory e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="9ef11-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="9ef11-181">Especifique Olá Cofre de chaves toostore Olá metadados para os discos encriptados.</span><span class="sxs-lookup"><span data-stu-id="9ef11-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="9ef11-182">Especifique Olá chaves criptográficas toouse para encriptação real Olá e a desencriptação.</span><span class="sxs-lookup"><span data-stu-id="9ef11-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="9ef11-183">Especifique se pretende tooencrypt disco de SO de Olá, discos de dados de Olá ou todos.</span><span class="sxs-lookup"><span data-stu-id="9ef11-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="9ef11-184">Encriptar a VM com [conjunto AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) utilizando a chave de Cofre de chaves do Azure Olá e as credenciais de principais de serviço do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ef11-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="9ef11-185">Olá exemplo seguinte obtém todas as informações de chave de Olá, em seguida, encripta Olá VM com o nome *myVM*:</span><span class="sxs-lookup"><span data-stu-id="9ef11-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="9ef11-186">Aceite Olá toocontinue linha de comandos com a encriptação de VM Olá.</span><span class="sxs-lookup"><span data-stu-id="9ef11-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="9ef11-187">Olá VM for reiniciado durante o processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9ef11-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="9ef11-188">Depois de concluir o processo de encriptação de Olá e hello VM foi reiniciado, reveja o estado de encriptação de Olá com [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="9ef11-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="9ef11-189">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9ef11-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="9ef11-190">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9ef11-190">Next steps</span></span>
* <span data-ttu-id="9ef11-191">Para obter mais informações sobre como gerir o Cofre de chaves do Azure, consulte [configurar o Cofre de chaves para máquinas virtuais](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9ef11-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="9ef11-192">Para obter mais informações sobre a encriptação de disco, tais como preparar uma encriptados personalizado VM tooupload tooAzure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="9ef11-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
