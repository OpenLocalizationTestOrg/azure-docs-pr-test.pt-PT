---
title: "aaaCreate uma Máquina Virtual do SQL Server no Azure PowerShell (clássica) | Microsoft Docs"
description: "Fornece os passos e scripts do PowerShell para criar uma VM do Azure com imagens de Galeria de máquina virtual do SQL Server. Este tópico utiliza o modo de implementação clássica Olá."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Aprovisionar uma máquina virtual de SQL Server com o Azure PowerShell (clássica)

Este artigo fornece os passos para como toocreate uma máquina virtual do SQL Server, no Azure utilizando Olá cmdlets do PowerShell.

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

Para a versão do Gestor de recursos de Olá deste tópico, consulte [aprovisionar uma máquina virtual de SQL Server utilizando o Gestor de recursos do Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Instalar e configurar o PowerShell:
1. Se não tiver uma conta do Azure, aceda a [Versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Transfira e instale os comandos de Azure PowerShell mais recentes Olá](/powershell/azure/overview).
3. Inicie o Windows PowerShell e ligue-tooyour subscrição do Azure com Olá **Add-AzureAccount** comando.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Determinar a sua região do Azure de destino

A Máquina Virtual do SQL Server será alojada num serviço em nuvem que reside numa região do Azure específica. Olá passos seguintes ajudam toodetermine a sua região, a conta de armazenamento e o serviço em nuvem que será utilizado para o resto Olá tutorial de Olá.

1. Determine o Centro de dados de Olá que pretende toouse toohost a VM do SQL Server. Olá seguinte comando do PowerShell apresenta uma lista de nomes de região disponível.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Depois de ter identificado a sua localização preferencial, definir uma variável com o nome **$dcLocation** toothat região. Por exemplo, Olá os seguintes comandos conjuntos Olá região demasiado "EUA Leste":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Definir a sua conta de armazenamento e de subscrição

1. Determine Olá irá utilizar para a máquina virtual nova do Olá de subscrição do Azure.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Atribuir o toohello de subscrição do Azure de destino **$subscr** variável. Em seguida, defina esta opção como a sua subscrição do Azure atual.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Em seguida, verifique a existência de contas do storage existentes. Olá script a seguir apresenta todas as contas de armazenamento que existem na sua região escolhido:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Se necessitar de uma nova conta de armazenamento, primeiro crie um nome de conta de armazenamento de todos os minúsculas com o comando de Olá AzureStorageAccount novo como no seguinte exemplo de Olá:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Atribuir Olá destino armazenamento conta nome toohello **$staccount**. Em seguida, utilize **Set-AzureSubscription** tooset Olá subscrição e conta de armazenamento atual.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Selecionar uma imagem de máquina virtual do SQL Server

1. Descubra a lista de Olá de imagens de máquinas virtuais do SQL Server disponíveis na Galeria de Olá. Estas imagens têm um **ImageFamily** propriedade que começa com "SQL Server". seguinte Olá consulta apresenta Olá imagem família disponíveis tooyou com SQL Server pré-instalado.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Quando encontrar família de imagem de máquina virtual de Olá, podem existir várias imagens publicadas nesta família. Seguinte Olá de utilização do script toofind Olá mais recente publicada imagem nome da máquina virtual para a sua família de imagem selecionada (tais como **SQL Server 2016 RTM para empresas no Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Criar máquina virtual de Olá

Por fim, crie a máquina virtual de Olá com o PowerShell:

1. Criar uma nuvem serviço toohost Olá nova VM. Tenha em atenção que também é possível toouse um serviço em nuvem existente em vez disso. Criar uma nova variável **$svcname** com o nome abreviado do Olá do serviço de nuvem Olá.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Especifique o nome da máquina virtual Olá e um tamanho. Para obter mais informações acerca dos tamanhos da máquina virtual, consulte [tamanhos de Máquina Virtual do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Especifique a conta de administrador local Olá e a palavra-passe.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Execute Olá máquina virtual do script toocreate Olá a seguir.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Para opções de configuração e explicação adicional, consulte Olá **criar o conjunto de comandos** secção [toocreate de utilização do Azure PowerShell e pré-configurar máquinas virtuais baseadas em Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Script do PowerShell de exemplo

Olá script seguinte fornece um exemplo de um script completado que cria um **SQL Server 2016 RTM para empresas no Windows Server 2012 R2** máquina virtual. Se utilizar este script, tem de personalizar Olá inicial as variáveis com base nos passos anteriores Olá neste tópico.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Estabelecer ligação com o ambiente de trabalho remoto

1. Crie Olá RDP ficheiros toolaunch de pasta de documentos do utilizador atual Olá programa de configuração de toocomplete estas máquinas virtuais:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. No diretório de documentos Olá, inicie o ficheiro RDP Olá. Estabelecer ligação com o nome de utilizador de administrador Olá e a palavra-passe fornecida anteriormente (por exemplo, se o seu nome de utilizador foi VMAdmin, especifique "\VMAdmin" como utilizador Olá e fornecer a palavra-passe de Olá).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Configuração de Olá completa de Olá máquina do SQL Server para o acesso remoto

Depois de iniciar sessão na máquina de toohello com o ambiente de trabalho remoto, configurar o SQL Server com base nas instruções Olá [os passos para configurar a conectividade do SQL Server numa VM do Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Passos seguintes

Pode encontrar instruções adicionais para o aprovisionamento de máquinas virtuais com o PowerShell no Olá [documentação de virtual machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Em muitos casos, o passo seguinte Olá é toomigrate toothis as bases de dados nova VM do SQL Server. Para obter orientações sobre a migração da base de dados, consulte [migrar uma base de dados tooSQL Server numa VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Se também estiver interessado em utilizar Olá toocreate do portal do Azure, as máquinas virtuais do SQL Server, consulte [aprovisionamento de uma Máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Tenha em atenção que tutorial Olá que explica como a através do portal Olá cria VMs utilizando Olá recomendada modelo do Resource Manager, em vez de modelo clássico Olá utilizados neste tópico do PowerShell.

Além disso recursos toothese, recomendamos que reveja [outros tópicos relacionados com toorunning do SQL Server em Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
