---
title: "Criar uma Máquina Virtual do SQL Server no Azure PowerShell (clássica) | Microsoft Docs"
description: "Fornece os passos e scripts do PowerShell para criar uma VM do Azure com imagens de Galeria de máquina virtual do SQL Server. Este tópico utiliza o modo de implementação clássica."
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
ms.openlocfilehash: c3bd4329e8a22ce8503d6593560d29c2a3135e83
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Aprovisionar uma máquina virtual de SQL Server com o Azure PowerShell (clássica)

Este artigo fornece os passos para criar uma máquina virtual do SQL Server no Azure utilizando os cmdlets do PowerShell.

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica. A Microsoft recomenda que as implementações mais novas utilizem o modelo Resource Manager.

Para a versão do Gestor de recursos deste tópico, consulte [aprovisionar uma máquina virtual de SQL Server utilizando o Gestor de recursos do Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Instalar e configurar o PowerShell:
1. Se não tiver uma conta do Azure, aceda a [Versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Transfira e instale os comandos do Azure PowerShell mais recentes](/powershell/azure/overview).
3. Inicie o Windows PowerShell e ligue-o à sua subscrição do Azure com o **Add-AzureAccount** comando.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Determinar a sua região do Azure de destino

A Máquina Virtual do SQL Server será alojada num serviço em nuvem que reside numa região do Azure específica. Os passos seguintes ajudá-lo a determinar a sua conta de armazenamento, região e na nuvem de serviço que será utilizado para o resto do tutorial.

1. Determine o Centro de dados que pretende utilizar para alojar a VM do SQL Server. O comando do PowerShell seguinte mostra uma lista de nomes de região disponível.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Depois de ter identificado a sua localização preferencial, definir uma variável com o nome **$dcLocation** nessa região. Por exemplo, o comando seguinte define a região para "Leste EUA":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Definir a sua conta de armazenamento e de subscrição

1. Determine a subscrição do Azure que irá utilizar para a nova máquina virtual.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Atribuir a sua subscrição do Azure de destino para o **$subscr** variável. Em seguida, defina esta opção como a sua subscrição do Azure atual.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Em seguida, verifique a existência de contas do storage existentes. O script seguinte mostra todas as contas de armazenamento que existem na sua região escolhido:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Se necessitar de uma nova conta de armazenamento, primeiro crie um nome de conta de armazenamento de todos os minúsculas com o comando de novo AzureStorageAccount como no exemplo seguinte:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Atribuir o nome de conta de armazenamento de destino para o **$staccount**. Em seguida, utilize **Set-AzureSubscription** para definir a subscrição e a conta de armazenamento atual.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Selecionar uma imagem de máquina virtual do SQL Server

1. Determinar a lista de imagens de máquinas virtuais do SQL Server disponíveis na galeria do. Estas imagens têm um **ImageFamily** propriedade que começa com "SQL Server". A consulta seguinte apresenta a família de imagem disponível para si com o SQL Server pré-instalado.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Quando encontrar a família de imagem de máquina virtual, podem existir várias imagens publicadas nesta família. Utilize o seguinte script para encontrar o nome de imagem de máquinas de virtuais publicados mais recente para sua família de imagem selecionada (tais como **SQL Server 2016 RTM para empresas no Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a>Criar a máquina virtual

Por fim, crie a máquina virtual com o PowerShell:

1. Crie um serviço em nuvem para alojar a VM nova. Tenha em atenção que também é possível utilizar um serviço em nuvem existente em vez disso. Criar uma nova variável **$svcname** com o nome abreviado do serviço de nuvem.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Especifique o nome de máquina virtual e um tamanho. Para obter mais informações acerca dos tamanhos da máquina virtual, consulte [tamanhos de Máquina Virtual do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Especifique a conta de administrador local e a palavra-passe.

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Execute o script seguinte para criar a máquina virtual.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Para opções de configuração e explicação adicional, consulte o **criar o conjunto de comandos** secção [utilize o Azure PowerShell para criar e pré-configurar máquinas virtuais baseadas em Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Script do PowerShell de exemplo

O script seguinte fornece um exemplo de um script completado que cria um **SQL Server 2016 RTM para empresas no Windows Server 2012 R2** máquina virtual. Se utilizar este script, tem de personalizar as variáveis iniciais com base nos passos anteriores deste tópico.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set the current subscription and storage account
# Comment out the New-AzureStorageAccount line if the account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select the most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create the new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create the VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type the name and password of the local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create the SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Estabelecer ligação com o ambiente de trabalho remoto

1. Crie os ficheiros RDP na pasta de documentos do utilizador atual para iniciar estas máquinas virtuais para concluir a configuração:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. No diretório de documentos, inicie o ficheiro RDP. Estabelecer ligação com o nome de utilizador de administrador e a palavra-passe fornecida anteriormente (por exemplo, se o seu nome de utilizador foi VMAdmin, especifique "\VMAdmin" como o utilizador e fornecer a palavra-passe).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a>Concluir a configuração da máquina do SQL Server, para acesso remoto

Depois de iniciar sessão na máquina com o ambiente de trabalho remoto, configurar o SQL Server com base nas instruções no [os passos para configurar a conectividade do SQL Server numa VM do Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Passos seguintes

Pode encontrar instruções adicionais para o aprovisionamento de máquinas virtuais com o PowerShell no [documentação de virtual machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Em muitos casos, o passo seguinte é migrar as bases de dados para esta nova VM do SQL Server. Para obter orientações sobre a migração da base de dados, consulte [migrar uma base de dados para o SQL Server numa VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Se também estiver interessado em utilizar o portal do Azure para criar máquinas virtuais do SQL Server, consulte [aprovisionamento de uma Máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Tenha em atenção que o tutorial que o orienta através do portal cria VMs utilizando o modelo do Resource Manager recomendada, em vez do modelo clássico utilizados neste tópico do PowerShell.

Para além destes recursos, recomendamos que reveja [outros tópicos relacionados com a executar o SQL Server em Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
