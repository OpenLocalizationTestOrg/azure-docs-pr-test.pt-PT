---
title: certificados aaaSecure IIS com SSL no Azure | Microsoft Docs
description: "Saiba como toosecure Olá IIS web servidor com certificados SSL numa VM do Windows no Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="bef08-103">Proteger o servidor web IIS com certificados SSL na máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="bef08-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="bef08-104">servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser utilizado o tráfego da web tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="bef08-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="bef08-105">Estes certificados SSL podem ser armazenados no Cofre de chaves do Azure e permitem implementações seguras de máquinas virtuais (VMs) do certificados tooWindows no Azure.</span><span class="sxs-lookup"><span data-stu-id="bef08-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="bef08-106">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="bef08-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bef08-107">Criar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="bef08-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bef08-108">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="bef08-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="bef08-109">Criar uma VM e instalar o servidor de web IIS Olá</span><span class="sxs-lookup"><span data-stu-id="bef08-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="bef08-110">Inserir o certificado de Olá no Olá VM e configurar o IIS com um enlace SSL</span><span class="sxs-lookup"><span data-stu-id="bef08-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bef08-111">Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bef08-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bef08-112">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="bef08-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="bef08-113">Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bef08-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="bef08-114">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="bef08-114">Overview</span></span>
<span data-ttu-id="bef08-115">O Cofre de chaves do Azure salvaguarda as chaves criptográficas e segredos, esses certificados ou palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="bef08-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="bef08-116">O Cofre de chaves ajuda a simplificar o processo de gestão de certificados de Olá e permite-lhe controlo toomaintain das chaves de acesso esses certificados.</span><span class="sxs-lookup"><span data-stu-id="bef08-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="bef08-117">Pode criar um certificado autoassinado no interior do Cofre de chaves ou carregar um certificado existente, fidedigno que já possui.</span><span class="sxs-lookup"><span data-stu-id="bef08-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="bef08-118">Em vez de utilizar uma imagem de VM personalizada, incluindo certificados integrada-in, inserir certificados para uma VM em execução.</span><span class="sxs-lookup"><span data-stu-id="bef08-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="bef08-119">Este processo garante que os certificados mais atualizadas à sua Olá estão instalados num servidor web durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="bef08-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="bef08-120">Se renovar ou substituir um certificado, não tem também toocreate uma nova imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="bef08-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="bef08-121">certificados mais recentes Olá são automaticamente injetados como criar VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="bef08-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="bef08-122">Durante o processo de todo Olá, certificados de Olá nunca deixam Olá plataforma do Azure ou estão expostos num script, o histórico da linha de comandos ou o modelo.</span><span class="sxs-lookup"><span data-stu-id="bef08-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="bef08-123">Criar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="bef08-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="bef08-124">Antes de poder criar um cofre de chaves e certificados, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bef08-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bef08-125">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupSecureWeb* no Olá *EUA Leste* localização:</span><span class="sxs-lookup"><span data-stu-id="bef08-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="bef08-126">Em seguida, crie um cofre de chaves com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="bef08-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="bef08-127">Cada Cofre de chaves requer um nome exclusivo e deve ser todas as letras maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bef08-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="bef08-128">Substitua `<mykeyvault>` no Olá seguinte o exemplo com o seu próprio nome exclusivo do Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="bef08-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="bef08-129">Gerar um certificado e armazenar no Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="bef08-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="bef08-130">Para utilização em produção, deve importar um certificado válido assinado por um fornecedor fidedigno com [importação AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="bef08-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="bef08-131">Para este tutorial, hello exemplo seguinte mostra como pode gerar um certificado autoassinado com [adicionar AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) que utiliza Olá política de certificado predefinido do [ Novo AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="bef08-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="bef08-132">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bef08-132">Create a virtual machine</span></span>
<span data-ttu-id="bef08-133">Conjunto de um nome de utilizador administrador e a palavra-passe para Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="bef08-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bef08-134">Agora pode criar Olá VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bef08-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="bef08-135">Olá exemplo seguinte cria componentes de rede virtual Olá necessário, configuração de Olá SO e, em seguida, cria uma VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="bef08-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="bef08-136">Demora alguns minutos para Olá VM toobe criado.</span><span class="sxs-lookup"><span data-stu-id="bef08-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="bef08-137">Olá último passo utiliza Olá extensão de Script personalizado Azure tooinstall Olá servidor web IIS com [conjunto AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="bef08-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="bef08-138">Adicionar um tooVM de certificado a partir do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="bef08-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="bef08-139">certificado de Olá tooadd do Cofre de chaves tooa VM, obter o ID de Olá do certificado com [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="bef08-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="bef08-140">Adicionar Olá certificado toohello VM com [adicionar AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="bef08-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="bef08-141">Para configurar IIS toouse Olá</span><span class="sxs-lookup"><span data-stu-id="bef08-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="bef08-142">Utilize Olá extensão de Script personalizado com [conjunto AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) configuração do IIS tooupdate Olá.</span><span class="sxs-lookup"><span data-stu-id="bef08-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="bef08-143">Esta atualização aplica-se o certificado de Olá injetado do Cofre de chaves tooIIS e configura o enlace de web de Olá:</span><span class="sxs-lookup"><span data-stu-id="bef08-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="bef08-144">Aplicação de web seguro Olá de teste</span><span class="sxs-lookup"><span data-stu-id="bef08-144">Test hello secure web app</span></span>
<span data-ttu-id="bef08-145">Obter o endereço IP público Olá da sua VM com [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bef08-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bef08-146">Olá exemplo seguinte obtém o endereço IP Olá `myPublicIP` criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="bef08-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="bef08-147">Agora pode abrir um browser e introduza `https://<myPublicIP>` na barra de endereço Olá.</span><span class="sxs-lookup"><span data-stu-id="bef08-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="bef08-148">Aviso de segurança de Olá tooaccept se utilizou um certificado autoassinado, selecione **detalhes** e, em seguida, **aceda na página Web de toohello**:</span><span class="sxs-lookup"><span data-stu-id="bef08-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Aceitar o aviso de segurança do browser web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="bef08-150">O Web site do IIS protegido, em seguida, é apresentado como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="bef08-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Site do IIS está em execução segura vista](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="bef08-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bef08-152">Next steps</span></span>

<span data-ttu-id="bef08-153">Neste tutorial, protegidos por um servidor web do IIS com um certificado SSL armazenado no Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="bef08-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="bef08-154">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="bef08-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bef08-155">Criar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="bef08-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bef08-156">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="bef08-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="bef08-157">Criar uma VM e instalar o servidor de web IIS Olá</span><span class="sxs-lookup"><span data-stu-id="bef08-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="bef08-158">Inserir o certificado de Olá no Olá VM e configurar o IIS com um enlace SSL</span><span class="sxs-lookup"><span data-stu-id="bef08-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bef08-159">Siga este toosee ligação criadas previamente amostras de script da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bef08-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bef08-160">Exemplos de script de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="bef08-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)