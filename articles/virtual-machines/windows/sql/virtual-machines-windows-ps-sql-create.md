---
title: "aaaCreate uma Máquina Virtual do SQL Server no Azure PowerShell (Resource Manager) | Microsoft Docs"
description: "Fornece os passos e scripts do PowerShell para criar uma VM do Azure com imagens de Galeria de máquina virtual do SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="eae1f-103">Aprovisionar uma máquina virtual de SQL Server com o Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="eae1f-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eae1f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="eae1f-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="eae1f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eae1f-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="eae1f-106">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="eae1f-106">Overview</span></span>
<span data-ttu-id="eae1f-107">Este tutorial mostra como toocreate utilizando uma única máquina virtual do Azure Olá **do Azure Resource Manager** modelo de implementação utilizando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae1f-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="eae1f-108">Neste tutorial, iremos criar uma máquina virtual utilizando uma única unidade de disco a partir de uma imagem no Olá galeria do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eae1f-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="eae1f-109">Iremos criar novos fornecedores de armazenamento de Olá, rede e recursos de computação que serão utilizados pela máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="eae1f-110">Se tiver fornecedores existentes para qualquer um destes recursos, pode utilizar em vez disso, os fornecedores.</span><span class="sxs-lookup"><span data-stu-id="eae1f-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="eae1f-111">Se precisar de hello versão clássica deste tópico, consulte o artigo [aprovisionar uma máquina virtual de SQL Server utilizando o Azure PowerShell clássico](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="eae1f-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eae1f-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eae1f-112">Prerequisites</span></span>
<span data-ttu-id="eae1f-113">Para este tutorial precisa de:</span><span class="sxs-lookup"><span data-stu-id="eae1f-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="eae1f-114">Uma conta do Azure e subscrição antes de começar.</span><span class="sxs-lookup"><span data-stu-id="eae1f-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="eae1f-115">Se não tiver uma, inscreva-se um [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eae1f-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="eae1f-116">[O Azure PowerShell)](/powershell/azure/overview), versão mínima do 1.4.0 ou posterior (Este tutorial escrita utilizando a versão 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="eae1f-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="eae1f-117">tooretrieve a versão, o tipo **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="eae1f-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="eae1f-118">Configurar a sua subscrição</span><span class="sxs-lookup"><span data-stu-id="eae1f-118">Configure your subscription</span></span>
<span data-ttu-id="eae1f-119">Abra o Windows PowerShell e estabelecer acesso tooyour conta do Azure executando o seguinte cmdlet de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="eae1f-120">Será apresentada com um início de sessão no ecrã tooenter as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="eae1f-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="eae1f-121">Utilize Olá mesmo correio eletrónico e palavra-passe que utilizam toosign no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae1f-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="eae1f-122">Após iniciar sessão com êxito a Verão algumas informações no ecrã que incluem o SubscriptionId Olá com a qual tem sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="eae1f-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="eae1f-123">Esta é a subscrição de Olá na qual serão criados recursos Olá para este tutorial, a menos que altere tooa outra subscrição.</span><span class="sxs-lookup"><span data-stu-id="eae1f-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="eae1f-124">Se tiver vários SubscriptionIds, execute uma lista de todos os seus SubscriptionIds Olá cmdlet tooreturn os seguintes:</span><span class="sxs-lookup"><span data-stu-id="eae1f-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="eae1f-125">toochange tooanother SubscriptionID, execute Olá seguintes cmdlet com o SubscriptionId pretendido.</span><span class="sxs-lookup"><span data-stu-id="eae1f-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="eae1f-126">Definir as variáveis de imagem</span><span class="sxs-lookup"><span data-stu-id="eae1f-126">Define image variables</span></span>
<span data-ttu-id="eae1f-127">toosimplify facilidade de utilização e a compreensão de script de Olá concluída este tutorial, iremos será iniciada, definindo um número de variáveis.</span><span class="sxs-lookup"><span data-stu-id="eae1f-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="eae1f-128">Alterar os valores de parâmetros de Olá como julgar, mas cuidado com de nomenclatura comprimentos de tooname relacionados restrições e os carateres especiais ao modificar os valores de Olá fornecidos.</span><span class="sxs-lookup"><span data-stu-id="eae1f-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="eae1f-129">Localização e grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="eae1f-129">Location and Resource Group</span></span>
<span data-ttu-id="eae1f-130">Utilize duas variáveis toodefine Olá dados região e Olá grupo de recursos no qual vai criar Olá outros recursos para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="eae1f-131">Modifique conforme pretendido e, em seguida, executar Olá os seguintes cmdlets tooinitialize estas variáveis.</span><span class="sxs-lookup"><span data-stu-id="eae1f-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="eae1f-132">Propriedades de armazenamento</span><span class="sxs-lookup"><span data-stu-id="eae1f-132">Storage properties</span></span>
<span data-ttu-id="eae1f-133">Utilize Olá variáveis toodefine Olá conta e Olá tipo de armazenamento de toobe de armazenamento utilizado pela máquina virtual de Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="eae1f-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="eae1f-134">Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.</span><span class="sxs-lookup"><span data-stu-id="eae1f-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="eae1f-135">Tenha em atenção que neste exemplo, estamos a utilizar [armazenamento Premium](../../../storage/common/storage-premium-storage.md), que é recomendada para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="eae1f-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="eae1f-136">Para obter detalhes sobre esta orientação e outras recomendações, consulte [práticas recomendadas do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="eae1f-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="eae1f-137">Propriedades da rede</span><span class="sxs-lookup"><span data-stu-id="eae1f-137">Network properties</span></span>
<span data-ttu-id="eae1f-138">Utilizar Olá seguir a interface de rede variáveis toodefine Olá, método de alocação de TCP/IP Olá, nome da rede virtual Olá, nome de sub-rede virtual Olá, Olá intervalo de endereços IP para a rede virtual Olá, Olá intervalo de endereços IP de sub-rede Olá e Olá toobe de etiqueta do nome de domínio público utilizada pela rede Olá na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="eae1f-139">Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.</span><span class="sxs-lookup"><span data-stu-id="eae1f-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="eae1f-140">Propriedades da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="eae1f-140">Virtual machine properties</span></span>
<span data-ttu-id="eae1f-141">Utilize Olá seguir o nome da máquina virtual variáveis toodefine Olá, o nome do computador Olá, o tamanho da máquina virtual Olá e o nome do disco de sistema operativo Olá para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="eae1f-142">Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.</span><span class="sxs-lookup"><span data-stu-id="eae1f-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="eae1f-143">Propriedades da imagem</span><span class="sxs-lookup"><span data-stu-id="eae1f-143">Image properties</span></span>
<span data-ttu-id="eae1f-144">Utilize Olá variáveis toodefine Olá imagem toouse para a máquina virtual de Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="eae1f-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="eae1f-145">Neste exemplo, a imagem do SQL Server 2016 Enterprise Olá é utilizada.</span><span class="sxs-lookup"><span data-stu-id="eae1f-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="eae1f-146">Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.</span><span class="sxs-lookup"><span data-stu-id="eae1f-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="eae1f-147">Tenha em atenção que pode obter uma lista completa das ofertas de imagem do SQL Server com o comando Get-AzureRmVMImageOffer de Olá:</span><span class="sxs-lookup"><span data-stu-id="eae1f-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="eae1f-148">E pode ver Olá Skus disponíveis para uma oferta com comando Olá Get AzureRmVMImageSku.</span><span class="sxs-lookup"><span data-stu-id="eae1f-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="eae1f-149">Olá comando seguinte apresenta todos os Skus disponíveis para Olá **SQL2014SP1 WS2012R2** oferecem.</span><span class="sxs-lookup"><span data-stu-id="eae1f-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="eae1f-150">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="eae1f-150">Create a resource group</span></span>
<span data-ttu-id="eae1f-151">Com o modelo de implementação do Resource Manager Olá, Olá o objeto primeiro que criou é o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="eae1f-152">Utilizaremos Olá [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate um grupo de recursos do Azure e os respetivos recursos com recurso de Olá grupo nome e localização definido pelo variáveis de Olá anteriormente inicializado.</span><span class="sxs-lookup"><span data-stu-id="eae1f-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="eae1f-153">Execute Olá seguintes cmdlet toocreate o novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="eae1f-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="eae1f-154">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="eae1f-154">Create a storage account</span></span>
<span data-ttu-id="eae1f-155">máquina virtual de Olá requer recursos de armazenamento para o disco do sistema operativo Olá e para Olá dados do SQL Server e os ficheiros de registo.</span><span class="sxs-lookup"><span data-stu-id="eae1f-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="eae1f-156">De simplicidade, iremos criar um único disco para ambos.</span><span class="sxs-lookup"><span data-stu-id="eae1f-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="eae1f-157">Pode anexar mais discos posteriormente utilizando Olá [Azure adicionar disco](/powershell/module/azure/add-azuredisk) cmdlet na ordem tooplace os dados do SQL Server e os ficheiros de registo no discos dedicados.</span><span class="sxs-lookup"><span data-stu-id="eae1f-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="eae1f-158">Utilizaremos Olá [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate um padrão de armazenamento e de contas no seu novo grupo de recursos com o nome de conta do storage Olá, nome de Sku de armazenamento e localização definidos utilizando variáveis de Olá que inicializar anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eae1f-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="eae1f-159">Execute Olá seguintes cmdlet toocreate a sua nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eae1f-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="eae1f-160">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="eae1f-160">Create network resources</span></span>
<span data-ttu-id="eae1f-161">máquina virtual de Olá requer um número de recursos de rede para conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="eae1f-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="eae1f-162">Cada máquina virtual necessita de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="eae1f-163">Uma rede virtual tem de ter pelo menos uma subrede definida.</span><span class="sxs-lookup"><span data-stu-id="eae1f-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="eae1f-164">Uma interface de rede tem de ser definida com um público ou um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="eae1f-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="eae1f-165">Criar uma configuração de sub-rede de rede virtual</span><span class="sxs-lookup"><span data-stu-id="eae1f-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="eae1f-166">Iremos irá começar por criar uma configuração de sub-rede para a nossa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="eae1f-167">Para o nosso tutorial, iremos criar uma sub-rede predefinida utilizando Olá [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eae1f-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="eae1f-168">Iremos criar a configuração de sub-rede de rede virtual com Olá nome e endereço prefixo de sub-rede definido utilizando variáveis de Olá anteriormente inicializado.</span><span class="sxs-lookup"><span data-stu-id="eae1f-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="eae1f-169">Pode definir propriedades adicionais de configuração de sub-rede de rede virtual Olá utilizar este cmdlet, mas que ultrapassa o âmbito de Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="eae1f-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="eae1f-170">Execute Olá seguintes cmdlet toocreate a configuração de sub-rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="eae1f-171">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="eae1f-171">Create a virtual network</span></span>
<span data-ttu-id="eae1f-172">Em seguida, iremos criar nossa rede virtual com o Olá [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eae1f-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="eae1f-173">Iremos criar nossa rede virtual no seu novo grupo de recursos, com o nome de Olá, a localização e o prefixo de endereço definidos utilizando variáveis de Olá anteriormente inicializado e utilizando a configuração de sub-rede Olá que definiu no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="eae1f-174">Execute Olá seguintes cmdlet toocreate a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="eae1f-175">Criar endereço IP público do Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-175">Create hello public IP address</span></span>
<span data-ttu-id="eae1f-176">Agora que temos nossa rede virtual definido, é necessário tooconfigure um endereço IP para a máquina de virtual toohello de conectividade.</span><span class="sxs-lookup"><span data-stu-id="eae1f-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="eae1f-177">Para este tutorial, iremos criar um endereço IP público utilizando toosupport conectividade à Internet de endereçamento de IP dinâmico.</span><span class="sxs-lookup"><span data-stu-id="eae1f-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="eae1f-178">Utilizaremos Olá [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Olá endereço IP público na Olá recursos grupo criado prevously e com o nome de Olá, localização, método de alocação e etiqueta de nome de domínio DNS definidos utilizando Olá variáveis que anteriormente inicializado.</span><span class="sxs-lookup"><span data-stu-id="eae1f-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="eae1f-179">Pode definir propriedades adicionais do endereço IP público Olá utilizar este cmdlet, mas que ultrapassa o âmbito de Olá deste tutorial inicial.</span><span class="sxs-lookup"><span data-stu-id="eae1f-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="eae1f-180">Pode também criar um endereço privado ou um endereço com um endereço estático, mas também que ultrapassa Olá âmbito deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="eae1f-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="eae1f-181">Execute Olá seguintes cmdlet toocreate o seu endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="eae1f-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="eae1f-182">Criar a interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-182">Create hello network interface</span></span>
<span data-ttu-id="eae1f-183">Estamos agora interface de rede de Olá toocreate pronto que irá utilizar o nosso máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="eae1f-184">Utilizaremos Olá [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate nossa interface de rede no grupo de recursos de Olá criada anteriormente e com o nome de Olá, localização, sub-rede e o endereço IP público definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eae1f-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="eae1f-185">Execute Olá seguintes cmdlet toocreate sua interface de rede.</span><span class="sxs-lookup"><span data-stu-id="eae1f-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="eae1f-186">Configurar um objeto VM</span><span class="sxs-lookup"><span data-stu-id="eae1f-186">Configure a VM object</span></span>
<span data-ttu-id="eae1f-187">Agora que temos de recursos de armazenamento e rede definidos, estamos prontos toodefine recursos de computação para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="eae1f-188">Para o nosso tutorial, iremos irá especificar várias propriedades do sistema operativo e o tamanho da máquina virtual Olá, especificar Olá interface de rede que criámos anteriormente, definir o armazenamento de BLOBs e, em seguida, especifique o disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="eae1f-189">Criar o objeto da VM Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-189">Create hello VM object</span></span>
<span data-ttu-id="eae1f-190">Iremos será iniciada, especificando o tamanho da máquina virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="eae1f-191">Para este tutorial, estamos a especificar um DS13.</span><span class="sxs-lookup"><span data-stu-id="eae1f-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="eae1f-192">Utilizaremos Olá [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate um objeto de configuráveis máquina virtual com o nome de Olá e tamanho definidos utilizando variáveis de Olá anteriormente inicializado.</span><span class="sxs-lookup"><span data-stu-id="eae1f-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="eae1f-193">Execute Olá seguinte objeto de máquina virtual do cmdlet toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="eae1f-194">Criar uma credencial do objeto toohold Olá e palavra-passe para as credenciais de administrador local Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="eae1f-195">Antes, pode definir propriedades do sistema operativo Olá para a máquina virtual de Olá, precisamos toosupply Olá das credenciais da conta de administrador local Olá como uma cadeia segura.</span><span class="sxs-lookup"><span data-stu-id="eae1f-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="eae1f-196">tooaccomplish isto, iremos utilizar Olá [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eae1f-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="eae1f-197">Executar o seguinte cmdlet de Olá e, na janela de pedido da credencial do Windows PowerShell Olá, escreva toouse de nome e palavra-passe de Olá Olá conta de administrador local na máquina de virtual do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="eae1f-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="eae1f-198">Definir as propriedades do sistema operativo Olá para a máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="eae1f-199">Agora vamos são propriedades do sistema operativo tooset pronto Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="eae1f-200">Utilizaremos Olá [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) tipo Olá de tooset de cmdlet do sistema operativo como Windows, necessita de Olá [agente da máquina virtual](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe instalado, especifique esse cmdlet Olá permite automática Atualizar e definir o nome da máquina virtual Olá, nome do computador Olá e as credenciais de Olá utilizando variáveis de Olá anteriormente inicializado.</span><span class="sxs-lookup"><span data-stu-id="eae1f-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="eae1f-201">Execute Olá seguintes cmdlet tooset Olá propriedades de sistema operativo para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="eae1f-202">Adicionar Olá rede interface toohello máquina</span><span class="sxs-lookup"><span data-stu-id="eae1f-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="eae1f-203">Em seguida, iremos adicionar a interface de rede de Olá que foi criada anteriormente toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="eae1f-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="eae1f-204">Utilizaremos Olá [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd Olá rede interface utilizando variável de interface de rede Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eae1f-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="eae1f-205">Execute Olá seguir a interface de rede do cmdlet tooset Olá para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="eae1f-206">Definir localização de armazenamento de BLOBs de Olá para Olá toobe de disco utilizado pela máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="eae1f-207">Em seguida, iremos irá definir localização de armazenamento de BLOBs de Olá para Olá toobe de disco utilizado pela máquina virtual de Olá utilizando variáveis de Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eae1f-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="eae1f-208">Execute Olá seguinte localização de armazenamento de Blobs do cmdlet tooset Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="eae1f-209">Definir o sistema de operativo Olá propriedades de disco para a máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="eae1f-210">Em seguida, iremos irá definir sistema de operativo Olá propriedades do disco para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="eae1f-211">Utilizaremos Olá [conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify cmdlet que Olá o sistema operativo da máquina virtual de Olá serão provenientes de uma imagem, tooset tooread apenas a colocação em cache (porque o SQL Server está a ser instalado no Olá mesmo disco) e defina nome da máquina virtual Olá e o disco do sistema operativo Olá definidos utilizando variáveis de Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eae1f-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="eae1f-212">Execute Olá seguintes propriedades de disco do sistema operativo do cmdlet tooset Olá para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="eae1f-213">Especifique a imagem de plataforma Olá para a máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="eae1f-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="eae1f-214">A nossa último passo da configuração é imagem de plataforma Olá toospecify nosso máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="eae1f-215">Para o nosso tutorial, estamos a utilizar imagem do SQL Server 2016 CTP mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="eae1f-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="eae1f-216">Utilizaremos Olá [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse esta imagem, conforme definido pelo variáveis de Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eae1f-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="eae1f-217">Execute Olá seguinte imagem de plataforma do cmdlet toospecify Olá para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="eae1f-218">Criar Olá VM do SQL Server</span><span class="sxs-lookup"><span data-stu-id="eae1f-218">Create hello SQL VM</span></span>
<span data-ttu-id="eae1f-219">Agora que tiver concluído os passos de configuração de Olá, está pronto toocreate Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="eae1f-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="eae1f-220">Utilizaremos Olá [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) máquina virtual cmdlet toocreate Olá utilizando variáveis de Olá que definiu.</span><span class="sxs-lookup"><span data-stu-id="eae1f-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="eae1f-221">Execute Olá seguintes cmdlet toocreate a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eae1f-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="eae1f-222">máquina virtual de Olá é criada.</span><span class="sxs-lookup"><span data-stu-id="eae1f-222">hello virtual machine is created.</span></span> <span data-ttu-id="eae1f-223">Tenha em atenção que é criada uma conta de armazenamento standard para diagnóstico de arranque porque Olá especificada a conta de armazenamento de disco da máquina virtual Olá é uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="eae1f-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="eae1f-224">Agora, pode ver esta máquina Olá Portal do Azure toosee [respetivo endereço IP público e o respetivo nome de domínio completamente qualificado](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="eae1f-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="eae1f-225">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="eae1f-225">Example script</span></span>
<span data-ttu-id="eae1f-226">Olá seguinte script contém Olá concluída script do PowerShell para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="eae1f-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="eae1f-227">Pressupõe que já tem a configuração Olá subscrição do Azure toouse com Olá **Add-AzureRmAccount** e **Select-AzureRmSubscription** comandos.</span><span class="sxs-lookup"><span data-stu-id="eae1f-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="eae1f-228">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="eae1f-228">Next steps</span></span>
<span data-ttu-id="eae1f-229">Depois de criar a máquina virtual de Olá, está pronto tooconnect toohello máquinas com conectividade RDP e o programa de configuração.</span><span class="sxs-lookup"><span data-stu-id="eae1f-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="eae1f-230">Para obter mais informações, consulte [ligar tooa Máquina Virtual do servidor SQL no Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="eae1f-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

