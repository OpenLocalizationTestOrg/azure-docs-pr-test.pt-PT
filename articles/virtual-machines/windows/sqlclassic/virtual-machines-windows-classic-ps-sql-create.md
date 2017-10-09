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
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="d7fdc-104">Aprovisionar uma máquina virtual de SQL Server com o Azure PowerShell (clássica)</span><span class="sxs-lookup"><span data-stu-id="d7fdc-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="d7fdc-105">Este artigo fornece os passos para como toocreate uma máquina virtual do SQL Server, no Azure utilizando Olá cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d7fdc-106">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d7fdc-107">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d7fdc-108">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="d7fdc-109">Para a versão do Gestor de recursos de Olá deste tópico, consulte [aprovisionar uma máquina virtual de SQL Server utilizando o Gestor de recursos do Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="d7fdc-110">Instalar e configurar o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d7fdc-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="d7fdc-111">Se não tiver uma conta do Azure, aceda a [Versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="d7fdc-112">[Transfira e instale os comandos de Azure PowerShell mais recentes Olá](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="d7fdc-113">Inicie o Windows PowerShell e ligue-tooyour subscrição do Azure com Olá **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="d7fdc-114">Determinar a sua região do Azure de destino</span><span class="sxs-lookup"><span data-stu-id="d7fdc-114">Determine your target Azure region</span></span>

<span data-ttu-id="d7fdc-115">A Máquina Virtual do SQL Server será alojada num serviço em nuvem que reside numa região do Azure específica.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="d7fdc-116">Olá passos seguintes ajudam toodetermine a sua região, a conta de armazenamento e o serviço em nuvem que será utilizado para o resto Olá tutorial de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="d7fdc-117">Determine o Centro de dados de Olá que pretende toouse toohost a VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="d7fdc-118">Olá seguinte comando do PowerShell apresenta uma lista de nomes de região disponível.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="d7fdc-119">Depois de ter identificado a sua localização preferencial, definir uma variável com o nome **$dcLocation** toothat região.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="d7fdc-120">Por exemplo, Olá os seguintes comandos conjuntos Olá região demasiado "EUA Leste":</span><span class="sxs-lookup"><span data-stu-id="d7fdc-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="d7fdc-121">Definir a sua conta de armazenamento e de subscrição</span><span class="sxs-lookup"><span data-stu-id="d7fdc-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="d7fdc-122">Determine Olá irá utilizar para a máquina virtual nova do Olá de subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="d7fdc-123">Atribuir o toohello de subscrição do Azure de destino **$subscr** variável.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="d7fdc-124">Em seguida, defina esta opção como a sua subscrição do Azure atual.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="d7fdc-125">Em seguida, verifique a existência de contas do storage existentes.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="d7fdc-126">Olá script a seguir apresenta todas as contas de armazenamento que existem na sua região escolhido:</span><span class="sxs-lookup"><span data-stu-id="d7fdc-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="d7fdc-127">Se necessitar de uma nova conta de armazenamento, primeiro crie um nome de conta de armazenamento de todos os minúsculas com o comando de Olá AzureStorageAccount novo como no seguinte exemplo de Olá:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="d7fdc-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="d7fdc-128">Atribuir Olá destino armazenamento conta nome toohello **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="d7fdc-129">Em seguida, utilize **Set-AzureSubscription** tooset Olá subscrição e conta de armazenamento atual.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="d7fdc-130">Selecionar uma imagem de máquina virtual do SQL Server</span><span class="sxs-lookup"><span data-stu-id="d7fdc-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="d7fdc-131">Descubra a lista de Olá de imagens de máquinas virtuais do SQL Server disponíveis na Galeria de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="d7fdc-132">Estas imagens têm um **ImageFamily** propriedade que começa com "SQL Server".</span><span class="sxs-lookup"><span data-stu-id="d7fdc-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="d7fdc-133">seguinte Olá consulta apresenta Olá imagem família disponíveis tooyou com SQL Server pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="d7fdc-134">Quando encontrar família de imagem de máquina virtual de Olá, podem existir várias imagens publicadas nesta família.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="d7fdc-135">Seguinte Olá de utilização do script toofind Olá mais recente publicada imagem nome da máquina virtual para a sua família de imagem selecionada (tais como **SQL Server 2016 RTM para empresas no Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="d7fdc-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="d7fdc-136">Criar máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="d7fdc-136">Create hello virtual machine</span></span>

<span data-ttu-id="d7fdc-137">Por fim, crie a máquina virtual de Olá com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d7fdc-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="d7fdc-138">Criar uma nuvem serviço toohost Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="d7fdc-139">Tenha em atenção que também é possível toouse um serviço em nuvem existente em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="d7fdc-140">Criar uma nova variável **$svcname** com o nome abreviado do Olá do serviço de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="d7fdc-141">Especifique o nome da máquina virtual Olá e um tamanho.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="d7fdc-142">Para obter mais informações acerca dos tamanhos da máquina virtual, consulte [tamanhos de Máquina Virtual do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="d7fdc-143">Especifique a conta de administrador local Olá e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="d7fdc-144">Execute Olá máquina virtual do script toocreate Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="d7fdc-145">Para opções de configuração e explicação adicional, consulte Olá **criar o conjunto de comandos** secção [toocreate de utilização do Azure PowerShell e pré-configurar máquinas virtuais baseadas em Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="d7fdc-146">Script do PowerShell de exemplo</span><span class="sxs-lookup"><span data-stu-id="d7fdc-146">Example PowerShell script</span></span>

<span data-ttu-id="d7fdc-147">Olá script seguinte fornece um exemplo de um script completado que cria um **SQL Server 2016 RTM para empresas no Windows Server 2012 R2** máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="d7fdc-148">Se utilizar este script, tem de personalizar Olá inicial as variáveis com base nos passos anteriores Olá neste tópico.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

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

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="d7fdc-149">Estabelecer ligação com o ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="d7fdc-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="d7fdc-150">Crie Olá RDP ficheiros toolaunch de pasta de documentos do utilizador atual Olá programa de configuração de toocomplete estas máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="d7fdc-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="d7fdc-151">No diretório de documentos Olá, inicie o ficheiro RDP Olá.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="d7fdc-152">Estabelecer ligação com o nome de utilizador de administrador Olá e a palavra-passe fornecida anteriormente (por exemplo, se o seu nome de utilizador foi VMAdmin, especifique "\VMAdmin" como utilizador Olá e fornecer a palavra-passe de Olá).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="d7fdc-153">Configuração de Olá completa de Olá máquina do SQL Server para o acesso remoto</span><span class="sxs-lookup"><span data-stu-id="d7fdc-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="d7fdc-154">Depois de iniciar sessão na máquina de toohello com o ambiente de trabalho remoto, configurar o SQL Server com base nas instruções Olá [os passos para configurar a conectividade do SQL Server numa VM do Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7fdc-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d7fdc-155">Next steps</span></span>

<span data-ttu-id="d7fdc-156">Pode encontrar instruções adicionais para o aprovisionamento de máquinas virtuais com o PowerShell no Olá [documentação de virtual machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="d7fdc-157">Em muitos casos, o passo seguinte Olá é toomigrate toothis as bases de dados nova VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="d7fdc-158">Para obter orientações sobre a migração da base de dados, consulte [migrar uma base de dados tooSQL Server numa VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="d7fdc-159">Se também estiver interessado em utilizar Olá toocreate do portal do Azure, as máquinas virtuais do SQL Server, consulte [aprovisionamento de uma Máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="d7fdc-160">Tenha em atenção que tutorial Olá que explica como a através do portal Olá cria VMs utilizando Olá recomendada modelo do Resource Manager, em vez de modelo clássico Olá utilizados neste tópico do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7fdc-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="d7fdc-161">Além disso recursos toothese, recomendamos que reveja [outros tópicos relacionados com toorunning do SQL Server em Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7fdc-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
