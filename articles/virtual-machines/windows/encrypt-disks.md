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
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Como tooencrypt discos virtuais numa VM do Windows
Para segurança avançada máquina virtual (VM) e conformidade, discos virtuais no Azure podem ser encriptados. Discos estão encriptados com as chaves criptográficas que são protegidas um cofre de chaves do Azure. Pode controla estas chaves criptográficas e pode auditar a sua utilização. Este artigo detalhes como tooencrypt discos virtuais numa VM do Windows com o Azure PowerShell. Também pode [encriptar uma VM com Linux utilizando Olá Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Descrição geral de encriptação de disco
Discos virtuais em VMs do Windows são encriptados em descanso ao utilizar o Bitlocker. Não há sem encargos de encriptação de discos virtuais no Azure. As chaves criptográficas são armazenadas no Cofre de chaves do Azure utilizando a proteção de software, ou pode importar ou gerar as suas chaves nos módulos de segurança de Hardware (HSMs) certificadas tooFIPS normas de nível 2 140-2. Estas chaves criptográficas são utilizado tooencrypt e desencriptar discos virtuais anexados tooyour VM. Manter o controlo destas chaves criptográficas e pode auditar a sua utilização. Um principal de serviço do Azure Active Directory fornece um mecanismo seguro para emitir estas chaves criptográficas como VMs estão ligados à corrente ou desligar.

processo de Olá para encriptar uma VM é o seguinte:

1. Crie uma chave criptográfica num cofre de chaves do Azure.
2. Configure Olá criptografia chave toobe utilizada para encriptação de discos.
3. chave de criptografia Olá tooread de Olá Cofre de chaves do Azure, criar um serviço do Azure Active Directory principal com as permissões adequadas Olá.
4. Emita Olá comando tooencrypt os discos virtuais, especificando o principal de serviço do Azure Active Directory Olá e adequada toobe chave criptográfica utilizada.
5. pedidos principais de serviço do Azure Active Directory de Olá Olá necessário chave criptográfica do Cofre de chaves do Azure.
6. discos virtuais Olá estão encriptados com a chave criptográfica Olá fornecido.

## <a name="encryption-process"></a>Processo de encriptação
Encriptação de disco depende Olá os seguintes componentes adicionais:

* **O Cofre de chaves do Azure** -utilizado toosafeguard de chaves criptográficas e segredos utilizados para o processo de encriptação/desencriptação de disco Olá. 
  * Se existir, pode utilizar um cofre de chaves do Azure existente. Não dispõe de toodedicate discos de tooencrypting um cofre de chaves.
  * limites administrativos tooseparate e visibilidade chave, pode criar um cofre de chaves dedicado.
* **Azure Active Directory** - identificadores Olá segura de troca de chaves criptográficas necessárias e as ações de pedido de autenticação para. 
  * Normalmente, pode utilizar uma instância existente do Azure Active Directory para o alojamento da sua aplicação.
  * principal de serviço Olá fornece um mecanismo segura toorequest e chaves criptográficas adequada de Olá de ser emitido. Não estiver a desenvolver uma aplicação real, que se integra com o Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisitos e limitações
Cenários suportados e os requisitos para encriptação de disco de:

* Ativar a encriptação em novas VMs do Windows de imagens do Azure Marketplace ou imagem personalizada do VHD.
* Ativar a encriptação em VMs do Windows existente no Azure.
* Ativar a encriptação em VMs do Windows que são configurados utilizando os espaços de armazenamento.
* A desativação da encriptação nos dados e SO unidades para VMs do Windows.
* Todos os recursos (por exemplo, o Cofre de chaves, a conta de armazenamento e a VM) tem de constar Olá mesma região do Azure e subscrição.
* O escalão Standard VMs, tais como uma, série D, DS, G e GS VMs.

Encriptação de disco não é atualmente suportada no Olá os seguintes cenários:

* Escalão básico VMs.
* VMs criadas utilizando o modelo de implementação clássica Olá.
* A atualizar as chaves criptográficas Olá numa VM já encriptada.
* Integração com o serviço de gestão de chaves no local.

## <a name="create-azure-key-vault-and-keys"></a>Criar Cofre de chaves do Azure e as chaves
Antes de começar, certifique-se de que essa versão mais recente Olá de Olá tenha sido instalado o módulo do Azure PowerShell. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Ao longo de exemplos de comando Olá, substitua todos os parâmetros de exemplo com os seus próprios nomes, localização e valores de chave. Olá exemplos seguintes utilizam uma convenção de *myResourceGroup*, *myKeyVault*, *myVM*, etc.

primeiro passo de Olá é toocreate toostore um cofre de chaves do Azure, as chaves criptográficas. O Cofre de chaves do Azure pode armazenar as chaves, segredos, ou palavras-passe que lhe permitem toosecurely implementá-la nas suas aplicações e serviços. Para a encriptação de disco virtual, crie um cofre de chaves toostore uma chave criptográfica que é utilizado tooencrypt ou desencriptar os discos virtuais. 

Ativar o fornecedor do Cofre de chaves do Azure Olá dentro da sua subscrição do Azure com [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), em seguida, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá exemplo seguinte cria um nome de grupo de recursos *myResourceGroup* no Olá *EUA Leste* localização:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Olá, Olá Cofre de chaves do Azure que contêm Olá chaves criptográfico e computação associada recursos, tais como o armazenamento e Olá própria VM tem de residir na mesma região. Criar um cofre de chaves do Azure com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e ativar Olá Cofre de chaves para utilização com a encriptação de disco. Especifique um nome exclusivo do Cofre de chaves para *keyVaultName* da seguinte forma:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

Pode armazenar as chaves criptográficas utilizando software ou proteção de modelo de segurança de Hardware (HSM). Utilizar um HSM necessita de um cofre de chaves de premium. Há um toocreating custos adicionais um premium Cofre de chaves em vez de padrão Cofre de chaves que armazena as chaves protegidas por software. toocreate um premium Cofre de chaves no Olá precedente passo adicionar Olá *- Sku "Premium"* parâmetros. Olá exemplo seguinte utiliza as chaves protegidas de software, uma vez que criámos um cofre de chaves padrão. 

Olá plataforma do Azure para ambos os modelos de proteção, tem de toobe concedido acesso Olá de toorequest chaves criptográficas quando Olá VM arranca discos virtuais do toodecrypt Olá. Criar uma chave criptográfica no seu Cofre de chaves com [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Olá exemplo seguinte cria uma chave denominada *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Criar Olá principal de serviço do Azure Active Directory
Quando os discos virtuais são encriptados ou desencriptados, especifique uma autenticação da conta toohandle Olá e troca de chaves criptográficas do Cofre de chaves. Esta conta, um principal de serviço do Azure Active Directory, permite Olá plataforma Azure toorequest Olá adequada as chaves criptográficas em nome Olá VM. Uma instância do Azure Active Directory predefinida está disponível na sua subscrição, apesar de muitas organizações têm dedicado diretórios do Azure Active Directory.

Criar um principal de serviço no Azure Active Directory com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify uma palavra-passe segura, siga Olá [políticas de palavra-passe e restrições no Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully encriptar ou desencriptar discos virtuais, as permissões chave criptográfica Olá armazenados no Cofre de chaves tem de ser definido toopermit Olá do Azure Active Directory serviço principal tooread Olá chaves. Definir as permissões no seu Cofre de chaves com [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Criar a máquina virtual
tootest Olá o processo de encriptação, vamos criar uma VM. Olá exemplo seguinte cria uma VM chamada *myVM* utilizando um *Datacenter do Windows Server 2016* imagem:

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


## <a name="encrypt-virtual-machine"></a>Encriptar a máquina virtual
discos virtuais do Olá tooencrypt, colocar em conjunto todos os componentes de Olá anterior:

1. Especifique Olá principal de serviço do Azure Active Directory e a palavra-passe.
2. Especifique Olá Cofre de chaves toostore Olá metadados para os discos encriptados.
3. Especifique Olá chaves criptográficas toouse para encriptação real Olá e a desencriptação.
4. Especifique se pretende tooencrypt disco de SO de Olá, discos de dados de Olá ou todos.

Encriptar a VM com [conjunto AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) utilizando a chave de Cofre de chaves do Azure Olá e as credenciais de principais de serviço do Azure Active Directory. Olá exemplo seguinte obtém todas as informações de chave de Olá, em seguida, encripta Olá VM com o nome *myVM*:

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

Aceite Olá toocontinue linha de comandos com a encriptação de VM Olá. Olá VM for reiniciado durante o processo de Olá. Depois de concluir o processo de encriptação de Olá e hello VM foi reiniciado, reveja o estado de encriptação de Olá com [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Olá de saída é semelhante toohello seguinte exemplo:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações sobre como gerir o Cofre de chaves do Azure, consulte [configurar o Cofre de chaves para máquinas virtuais](key-vault-setup.md).
* Para obter mais informações sobre a encriptação de disco, tais como preparar uma encriptados personalizado VM tooupload tooAzure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).
