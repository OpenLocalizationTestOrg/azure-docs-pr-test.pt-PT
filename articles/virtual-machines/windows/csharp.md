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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Criar e gerir VMs do Windows no Azure com c# #

Um [Máquina Virtual do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) tem vários recursos do Azure de suporte. Este artigo abrange a criar, gerir e eliminar recursos VM através de c#. Saiba como:

> [!div class="checklist"]
> * Criar um projeto do Visual Studio
> * Instalar o pacote de Olá
> * Criar as credenciais
> * Criar recursos
> * Executar tarefas de gestão
> * Eliminar recursos
> * Executar a aplicação Olá

Demora cerca de 20 minutos toodo estes passos.

## <a name="create-a-visual-studio-project"></a>Criar um projeto do Visual Studio

1. Se ainda não o fez, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecione **desenvolvimento de ambiente de trabalho .NET** no Olá página de cargas de trabalho e, em seguida, clique em **instalar**. Resumo de Olá, pode ver que **ferramentas de desenvolvimento do .NET Framework 4 4.6** é selecionado automaticamente para si. Se já tiver instalado o Visual Studio, pode adicionar a carga de trabalho do .NET Olá utilizando Olá Iniciador do Visual Studio.
2. No Visual Studio, clique em **ficheiro** > **novo** > **projeto**.
3. No **modelos** > **Visual c#**, selecione **aplicação de consola (.NET Framework)**, introduza *myDotnetProject* para nome Olá do Olá projeto, localização Olá selecione do projeto de Olá e, em seguida, clique em **OK**.

## <a name="install-hello-package"></a>Instalar o pacote de Olá

Os pacotes de NuGet são Olá mais fácil forma tooinstall Olá bibliotecas que precisa de toofinish estes passos. bibliotecas de Olá tooget que necessita no Visual Studio, execute estes passos:

1. Clique em **ferramentas** > **Gestor de pacotes Nuget**e, em seguida, clique em **consola do Gestor de pacotes**.
2. Escreva este comando na consola de Olá:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Criar as credenciais

Antes de começar este passo, certifique-se de que tem acesso tooan [principal de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Deve também registar o ID da aplicação Olá, chave de autenticação de Olá e ID do inquilino Olá que precisa num passo posterior.

### <a name="create-hello-authorization-file"></a>Criar ficheiro de autorização de Olá

1. No Explorador de soluções, faça duplo clique *myDotnetProject* > **adicionar** > **Novo Item**e, em seguida, selecione **doficheirodetexto** no *Visual c# itens*. Ficheiro de Olá nome *azureauth.properties*e, em seguida, clique em **adicionar**.
2. Adicione estas propriedades de autorização:

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

    Substitua  **&lt;id de subscrição&gt;**  com o identificador de subscrição,  **&lt;id da aplicação&gt;**  com Olá aplicação do Active Directory Identificador,  **&lt;chave de autenticação&gt;**  com a chave da aplicação Olá, e  **&lt;id do inquilino&gt;**  com inquilino Olá Identificador.

3. Guarde o ficheiro de azureauth.properties Olá. 
4. Defina uma variável de ambiente do Windows com o nome AZURE_AUTH_LOCATION com Olá caminho completo tooauthorization ficheiro que criou. Por exemplo, pode ser utilizado Olá seguinte comando do PowerShell:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Criar o cliente de gestão de Olá

1. Abrir o ficheiro Program.cs de Olá para o projeto de Olá que criou e, em seguida, adicione estas instruções de existente de toohello de instruções de utilização na parte superior do ficheiro de Olá:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. cliente de gestão do toocreate Olá, adicione este código toohello método Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Criar recursos

### <a name="create-hello-resource-group"></a>Criar grupo de recursos de Olá

Todos os recursos tem de estar contidos num [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

toospecify valores para Olá aplicação e criar o grupo de recursos de Olá, adicione este código toohello método Main:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Criar conjunto de disponibilidade de Olá

[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para si toomaintain Olá máquinas virtuais utilizadas pela sua aplicação.

disponibilidade de Olá toocreate definido, adicione este código toohello método Main:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Criar endereço IP público do Olá

A [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é toocommunicate necessário com a máquina virtual de Olá.

toocreate Olá público do endereço IP máquina virtual de Olá, adicione este código toohello método Main:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Criar rede virtual Olá

Uma máquina virtual tem de ser uma sub-rede de um [rede Virtual](../../virtual-network/virtual-networks-overview.md).

toocreate uma sub-rede e uma rede virtual, adicione este código toohello método Main:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Criar a interface de rede Olá

Uma máquina virtual tem um toocommunicate de interface de rede na rede virtual Olá.

toocreate uma interface de rede, adicione este código toohello método Main:

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

### <a name="create-hello-virtual-machine"></a>Criar máquina virtual de Olá

Agora que criou Olá todos os recursos de suporte, pode criar uma máquina virtual.

toocreate Olá máquina virtual, adicione este código toohello método Main:

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
> Este tutorial cria uma máquina virtual com uma versão do sistema de operativo de servidor do Windows hello. toolearn mais informações sobre a seleção de outras imagens, consulte [navegar e selecionar imagens da máquina virtual do Azure com o Windows PowerShell e Olá CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se quiser toouse um disco existente, em vez de uma imagem do marketplace, utilize este código:

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

## <a name="perform-management-tasks"></a>Executar tarefas de gestão

Durante o ciclo de vida de Olá de uma máquina virtual, poderá ser útil toorun tarefas de gestão, tais como iniciar, parar ou eliminar uma máquina virtual. Além disso, poderá ser útil toocreate código tooautomate complexos ou repetitivos tarefas.

Quando precisar de toodo nada com Olá VM, é necessário tooget uma instância do mesmo:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Obter informações sobre Olá VM

tooget informações sobre a máquina virtual de Olá, adicione este código toohello método Main:

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

### <a name="stop-hello-vm"></a>Parar Olá VM

Pode parar uma máquina virtual e manter todas as respetivas definições, mas continuar toobe cobrada ou pode parar uma máquina virtual e desalocá-lo. Quando uma máquina virtual está a ser desalocada, todos os recursos associados à mesma também são extremidades desalocadas e faturação para o mesmo.

máquina virtual, Olá toostop sem desalocação, adicione este código toohello método Main:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Se pretender que a máquina de virtual toodeallocate Olá, altere o código de toothis Olá desligado chamada:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Iniciar Olá VM

toostart Olá máquina virtual, adicione este código toohello método Main:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Redimensionar Olá VM

Muitos aspetos de implementação devem ser considerados ao decidir sobre um tamanho para a máquina virtual. Para obter mais informações, consulte [tamanhos de VM](sizes.md).  

toochange tamanho da máquina virtual de Olá, adicione este código toohello método Main:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Adicionar um toohello de disco de dados VM

tooadd uma máquina virtual toohello disco de dados, adicione este código toohello principal método tooadd um disco de dados é de 2 GB de tamanho, han um LUN de 0 e um tipo de colocação em cache de ReadWrite:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Eliminar recursos

Uma vez que os lhe é cobrados os recursos utilizados no Azure, é sempre recursos de toodelete boa prática que já não são necessárias. Se pretender que as máquinas de virtuais toodelete Olá e Olá todos os recursos de suporte, todos os tiver toodo é eliminar grupo de recursos de Olá.

recurso de Olá toodelete grupo, adicione este código toohello método Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Executar a aplicação Olá

Deve demorar cerca de cinco minutos para que este toorun de aplicação de consola completamente a partir do início toofinish. 

1. aplicação de consola do toorun Olá, clique em **iniciar**.

2. Antes de premir **Enter** toostart de recursos a eliminar, foi demorar alguns minutos a criação de Olá tooverify dos recursos de Olá no Olá portal do Azure. Clique em Olá implementação Estado toosee obter informações sobre a implementação de Olá.

## <a name="next-steps"></a>Passos seguintes
* Tirar partido da utilização de um modelo toocreate uma máquina virtual através da utilização de informações Olá [implementar uma máquina de Virtual do Azure com c# e um modelo do Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Saiba mais sobre como utilizar Olá [bibliotecas do Azure para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

