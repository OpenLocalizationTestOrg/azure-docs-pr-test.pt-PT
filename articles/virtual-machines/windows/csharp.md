---
title: aaaCreate e gerir uma Azure Virtual Machine utilizar c# | Microsoft Docs
description: "Utilize c# e do Azure Resource Manager toodeploy uma máquina virtual e todos os respetivos recursos de suporte."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="c40ab-103">Criar e gerir VMs do Windows no Azure com c#</span><span class="sxs-lookup"><span data-stu-id="c40ab-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="c40ab-104">Um [Máquina Virtual do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) tem vários recursos do Azure de suporte.</span><span class="sxs-lookup"><span data-stu-id="c40ab-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="c40ab-105">Este artigo abrange a criar, gerir e eliminar recursos VM através de c#.</span><span class="sxs-lookup"><span data-stu-id="c40ab-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="c40ab-106">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="c40ab-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c40ab-107">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c40ab-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="c40ab-108">Instalar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-108">Install hello package</span></span>
> * <span data-ttu-id="c40ab-109">Criar as credenciais</span><span class="sxs-lookup"><span data-stu-id="c40ab-109">Create credentials</span></span>
> * <span data-ttu-id="c40ab-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="c40ab-110">Create resources</span></span>
> * <span data-ttu-id="c40ab-111">Executar tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="c40ab-111">Perform management tasks</span></span>
> * <span data-ttu-id="c40ab-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="c40ab-112">Delete resources</span></span>
> * <span data-ttu-id="c40ab-113">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-113">Run hello application</span></span>

<span data-ttu-id="c40ab-114">Demora cerca de 20 minutos toodo estes passos.</span><span class="sxs-lookup"><span data-stu-id="c40ab-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="c40ab-115">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c40ab-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="c40ab-116">Se ainda não o fez, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="c40ab-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="c40ab-117">Selecione **desenvolvimento de ambiente de trabalho .NET** no Olá página de cargas de trabalho e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="c40ab-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="c40ab-118">Resumo de Olá, pode ver que **ferramentas de desenvolvimento do .NET Framework 4 4.6** é selecionado automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="c40ab-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="c40ab-119">Se já tiver instalado o Visual Studio, pode adicionar a carga de trabalho do .NET Olá utilizando Olá Iniciador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c40ab-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="c40ab-120">No Visual Studio, clique em **ficheiro** > **novo** > **projeto**.</span><span class="sxs-lookup"><span data-stu-id="c40ab-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="c40ab-121">No **modelos** > **Visual c#**, selecione **aplicação de consola (.NET Framework)**, introduza *myDotnetProject* para nome Olá do Olá projeto, localização Olá selecione do projeto de Olá e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c40ab-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="c40ab-122">Instalar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-122">Install hello package</span></span>

<span data-ttu-id="c40ab-123">Os pacotes de NuGet são Olá mais fácil forma tooinstall Olá bibliotecas que precisa de toofinish estes passos.</span><span class="sxs-lookup"><span data-stu-id="c40ab-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="c40ab-124">bibliotecas de Olá tooget que necessita no Visual Studio, execute estes passos:</span><span class="sxs-lookup"><span data-stu-id="c40ab-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="c40ab-125">Clique em **ferramentas** > **Gestor de pacotes Nuget**e, em seguida, clique em **consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="c40ab-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="c40ab-126">Escreva este comando na consola de Olá:</span><span class="sxs-lookup"><span data-stu-id="c40ab-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="c40ab-127">Criar as credenciais</span><span class="sxs-lookup"><span data-stu-id="c40ab-127">Create credentials</span></span>

<span data-ttu-id="c40ab-128">Antes de começar este passo, certifique-se de que tem acesso tooan [principal de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c40ab-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="c40ab-129">Deve também registar o ID da aplicação Olá, chave de autenticação de Olá e ID do inquilino Olá que precisa num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="c40ab-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="c40ab-130">Criar ficheiro de autorização de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-130">Create hello authorization file</span></span>

1. <span data-ttu-id="c40ab-131">No Explorador de soluções, faça duplo clique *myDotnetProject* > **adicionar** > **Novo Item**e, em seguida, selecione **doficheirodetexto** no *Visual c# itens*.</span><span class="sxs-lookup"><span data-stu-id="c40ab-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="c40ab-132">Ficheiro de Olá nome *azureauth.properties*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c40ab-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="c40ab-133">Adicione estas propriedades de autorização:</span><span class="sxs-lookup"><span data-stu-id="c40ab-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="c40ab-134">Substitua  **&lt;id de subscrição&gt;**  com o identificador de subscrição,  **&lt;id da aplicação&gt;**  com Olá aplicação do Active Directory Identificador,  **&lt;chave de autenticação&gt;**  com a chave da aplicação Olá, e  **&lt;id do inquilino&gt;**  com inquilino Olá Identificador.</span><span class="sxs-lookup"><span data-stu-id="c40ab-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="c40ab-135">Guarde o ficheiro de azureauth.properties Olá.</span><span class="sxs-lookup"><span data-stu-id="c40ab-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="c40ab-136">Defina uma variável de ambiente do Windows com o nome AZURE_AUTH_LOCATION com Olá caminho completo tooauthorization ficheiro que criou.</span><span class="sxs-lookup"><span data-stu-id="c40ab-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="c40ab-137">Por exemplo, pode ser utilizado Olá seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c40ab-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="c40ab-138">Criar o cliente de gestão de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-138">Create hello management client</span></span>

1. <span data-ttu-id="c40ab-139">Abrir o ficheiro Program.cs de Olá para o projeto de Olá que criou e, em seguida, adicione estas instruções de existente de toohello de instruções de utilização na parte superior do ficheiro de Olá:</span><span class="sxs-lookup"><span data-stu-id="c40ab-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="c40ab-140">cliente de gestão do toocreate Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="c40ab-141">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="c40ab-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="c40ab-142">Criar grupo de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-142">Create hello resource group</span></span>

<span data-ttu-id="c40ab-143">Todos os recursos tem de estar contidos num [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c40ab-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="c40ab-144">toospecify valores para Olá aplicação e criar o grupo de recursos de Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="c40ab-145">Criar conjunto de disponibilidade de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-145">Create hello availability set</span></span>

<span data-ttu-id="c40ab-146">[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para si toomaintain Olá máquinas virtuais utilizadas pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="c40ab-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="c40ab-147">disponibilidade de Olá toocreate definido, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="c40ab-148">Criar endereço IP público do Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-148">Create hello public IP address</span></span>

<span data-ttu-id="c40ab-149">A [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é toocommunicate necessário com a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="c40ab-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="c40ab-150">toocreate Olá público do endereço IP máquina virtual de Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="c40ab-151">Criar rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-151">Create hello virtual network</span></span>

<span data-ttu-id="c40ab-152">Uma máquina virtual tem de ser uma sub-rede de um [rede Virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c40ab-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="c40ab-153">toocreate uma sub-rede e uma rede virtual, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="c40ab-154">Criar a interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-154">Create hello network interface</span></span>

<span data-ttu-id="c40ab-155">Uma máquina virtual tem um toocommunicate de interface de rede na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="c40ab-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="c40ab-156">toocreate uma interface de rede, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-156">toocreate a network interface, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="c40ab-157">Criar máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-157">Create hello virtual machine</span></span>

<span data-ttu-id="c40ab-158">Agora que criou Olá todos os recursos de suporte, pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c40ab-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="c40ab-159">toocreate Olá máquina virtual, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="c40ab-160">Este tutorial cria uma máquina virtual com uma versão do sistema de operativo de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c40ab-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="c40ab-161">toolearn mais informações sobre a seleção de outras imagens, consulte [navegar e selecionar imagens da máquina virtual do Azure com o Windows PowerShell e Olá CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c40ab-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="c40ab-162">Se quiser toouse um disco existente, em vez de uma imagem do marketplace, utilize este código:</span><span class="sxs-lookup"><span data-stu-id="c40ab-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="c40ab-163">Executar tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="c40ab-163">Perform management tasks</span></span>

<span data-ttu-id="c40ab-164">Durante o ciclo de vida de Olá de uma máquina virtual, poderá ser útil toorun tarefas de gestão, tais como iniciar, parar ou eliminar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c40ab-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="c40ab-165">Além disso, poderá ser útil toocreate código tooautomate complexos ou repetitivos tarefas.</span><span class="sxs-lookup"><span data-stu-id="c40ab-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="c40ab-166">Quando precisar de toodo nada com Olá VM, é necessário tooget uma instância do mesmo:</span><span class="sxs-lookup"><span data-stu-id="c40ab-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="c40ab-167">Obter informações sobre Olá VM</span><span class="sxs-lookup"><span data-stu-id="c40ab-167">Get information about hello VM</span></span>

<span data-ttu-id="c40ab-168">tooget informações sobre a máquina virtual de Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="c40ab-169">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="c40ab-169">Stop hello VM</span></span>

<span data-ttu-id="c40ab-170">Pode parar uma máquina virtual e manter todas as respetivas definições, mas continuar toobe cobrada ou pode parar uma máquina virtual e desalocá-lo.</span><span class="sxs-lookup"><span data-stu-id="c40ab-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="c40ab-171">Quando uma máquina virtual está a ser desalocada, todos os recursos associados à mesma também são extremidades desalocadas e faturação para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="c40ab-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="c40ab-172">máquina virtual, Olá toostop sem desalocação, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="c40ab-173">Se pretender que a máquina de virtual toodeallocate Olá, altere o código de toothis Olá desligado chamada:</span><span class="sxs-lookup"><span data-stu-id="c40ab-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="c40ab-174">Iniciar Olá VM</span><span class="sxs-lookup"><span data-stu-id="c40ab-174">Start hello VM</span></span>

<span data-ttu-id="c40ab-175">toostart Olá máquina virtual, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="c40ab-176">Redimensionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="c40ab-176">Resize hello VM</span></span>

<span data-ttu-id="c40ab-177">Muitos aspetos de implementação devem ser considerados ao decidir sobre um tamanho para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c40ab-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="c40ab-178">Para obter mais informações, consulte [tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c40ab-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="c40ab-179">toochange tamanho da máquina virtual de Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="c40ab-180">Adicionar um toohello de disco de dados VM</span><span class="sxs-lookup"><span data-stu-id="c40ab-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="c40ab-181">tooadd uma máquina virtual toohello disco de dados, adicione este código toohello principal método tooadd um disco de dados é de 2 GB de tamanho, han um LUN de 0 e um tipo de colocação em cache de ReadWrite:</span><span class="sxs-lookup"><span data-stu-id="c40ab-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="c40ab-182">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="c40ab-182">Delete resources</span></span>

<span data-ttu-id="c40ab-183">Uma vez que os lhe é cobrados os recursos utilizados no Azure, é sempre recursos de toodelete boa prática que já não são necessárias.</span><span class="sxs-lookup"><span data-stu-id="c40ab-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="c40ab-184">Se pretender que as máquinas de virtuais toodelete Olá e Olá todos os recursos de suporte, todos os tiver toodo é eliminar grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="c40ab-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="c40ab-185">recurso de Olá toodelete grupo, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="c40ab-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="c40ab-186">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c40ab-186">Run hello application</span></span>

<span data-ttu-id="c40ab-187">Deve demorar cerca de cinco minutos para que este toorun de aplicação de consola completamente a partir do início toofinish.</span><span class="sxs-lookup"><span data-stu-id="c40ab-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="c40ab-188">aplicação de consola do toorun Olá, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="c40ab-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="c40ab-189">Antes de premir **Enter** toostart de recursos a eliminar, foi demorar alguns minutos a criação de Olá tooverify dos recursos de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c40ab-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="c40ab-190">Clique em Olá implementação Estado toosee obter informações sobre a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c40ab-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c40ab-191">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c40ab-191">Next steps</span></span>
* <span data-ttu-id="c40ab-192">Tirar partido da utilização de um modelo toocreate uma máquina virtual através da utilização de informações Olá [implementar uma máquina de Virtual do Azure com c# e um modelo do Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c40ab-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="c40ab-193">Saiba mais sobre como utilizar Olá [bibliotecas do Azure para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="c40ab-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

