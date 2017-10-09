---
title: "aaaCreate e gerir um Java de através da Máquina Virtual do Azure | Microsoft Docs"
description: "Utilize toodeploy Java e o Azure Resource Manager, uma máquina virtual e todos os respetivos recursos de suporte."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="9579c-103">Criar e gerir VMs do Windows no Azure utilizando Java</span><span class="sxs-lookup"><span data-stu-id="9579c-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="9579c-104">Um [Máquina Virtual do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) tem vários recursos do Azure de suporte.</span><span class="sxs-lookup"><span data-stu-id="9579c-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="9579c-105">Este artigo abrange a criar, gerir e eliminar recursos VM com o Java.</span><span class="sxs-lookup"><span data-stu-id="9579c-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="9579c-106">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="9579c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9579c-107">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="9579c-107">Create a Maven project</span></span>
> * <span data-ttu-id="9579c-108">Adicione as dependências</span><span class="sxs-lookup"><span data-stu-id="9579c-108">Add dependencies</span></span>
> * <span data-ttu-id="9579c-109">Criar as credenciais</span><span class="sxs-lookup"><span data-stu-id="9579c-109">Create credentials</span></span>
> * <span data-ttu-id="9579c-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="9579c-110">Create resources</span></span>
> * <span data-ttu-id="9579c-111">Executar tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="9579c-111">Perform management tasks</span></span>
> * <span data-ttu-id="9579c-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="9579c-112">Delete resources</span></span>
> * <span data-ttu-id="9579c-113">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-113">Run hello application</span></span>

<span data-ttu-id="9579c-114">Demora cerca de 20 minutos toodo estes passos.</span><span class="sxs-lookup"><span data-stu-id="9579c-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="9579c-115">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="9579c-115">Create a Maven project</span></span>

1. <span data-ttu-id="9579c-116">Se ainda não o fez, instale [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="9579c-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="9579c-117">Instalar [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="9579c-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="9579c-118">Crie um novo projeto de pasta e Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="9579c-119">Adicione as dependências</span><span class="sxs-lookup"><span data-stu-id="9579c-119">Add dependencies</span></span>

1. <span data-ttu-id="9579c-120">Em Olá `testAzureApp` pasta, abra Olá `pom.xml` de ficheiros e adicionar configuração de compilação de Olá demasiado&lt;projeto&gt; edifício de Olá tooenable da sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="9579c-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="9579c-121">Adicione as dependências de Olá que são necessários tooaccess Olá SDK Java do Azure.</span><span class="sxs-lookup"><span data-stu-id="9579c-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="9579c-122">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="9579c-123">Criar as credenciais</span><span class="sxs-lookup"><span data-stu-id="9579c-123">Create credentials</span></span>

<span data-ttu-id="9579c-124">Antes de começar este passo, certifique-se de que tem acesso tooan [principal de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9579c-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="9579c-125">Deve também registar o ID da aplicação Olá, chave de autenticação de Olá e ID do inquilino Olá que precisa num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="9579c-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="9579c-126">Criar ficheiro de autorização de Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-126">Create hello authorization file</span></span>

1. <span data-ttu-id="9579c-127">Crie um ficheiro denominado `azureauth.properties` e adicione tooit estas propriedades:</span><span class="sxs-lookup"><span data-stu-id="9579c-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="9579c-128">Substitua  **&lt;id de subscrição&gt;**  com o identificador de subscrição,  **&lt;id da aplicação&gt;**  com Olá aplicação do Active Directory Identificador,  **&lt;chave de autenticação&gt;**  com a chave da aplicação Olá, e  **&lt;id do inquilino&gt;**  com inquilino Olá Identificador.</span><span class="sxs-lookup"><span data-stu-id="9579c-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="9579c-129">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-129">Save hello file.</span></span>
3. <span data-ttu-id="9579c-130">Defina uma variável de ambiente com o nome AZURE_AUTH_LOCATION na sua shell com o ficheiro de autenticação do Olá caminho completo toohello.</span><span class="sxs-lookup"><span data-stu-id="9579c-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="9579c-131">Criar o cliente de gestão de Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-131">Create hello management client</span></span>

1. <span data-ttu-id="9579c-132">Abra Olá `App.java` de ficheiros em `src\main\java\com\fabrikam` e certifique-se de que esta declaração de pacote na parte superior do Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="9579c-133">Na declaração do pacote de Olá, adicione-os importar instruções:</span><span class="sxs-lookup"><span data-stu-id="9579c-133">Under hello package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="9579c-134">toocreate Olá credenciais do Active Directory que tem de toomake pedidos, adicione este código toohello o método main de Olá classe de aplicação:</span><span class="sxs-lookup"><span data-stu-id="9579c-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="9579c-135">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="9579c-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="9579c-136">Criar grupo de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-136">Create hello resource group</span></span>

<span data-ttu-id="9579c-137">Todos os recursos tem de estar contidos num [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9579c-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="9579c-138">toospecify valores para Olá aplicação e criar o grupo de recursos de Olá, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="9579c-139">Criar conjunto de disponibilidade de Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-139">Create hello availability set</span></span>

<span data-ttu-id="9579c-140">[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para si toomaintain Olá máquinas virtuais utilizadas pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9579c-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="9579c-141">disponibilidade de Olá toocreate definido, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="9579c-142">Criar endereço IP público do Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-142">Create hello public IP address</span></span>

<span data-ttu-id="9579c-143">A [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é toocommunicate necessário com a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="9579c-144">toocreate Olá público do endereço IP máquina virtual de Olá, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="9579c-145">Criar rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-145">Create hello virtual network</span></span>

<span data-ttu-id="9579c-146">Uma máquina virtual tem de ser uma sub-rede de um [rede Virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9579c-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="9579c-147">toocreate uma sub-rede e uma rede virtual, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="9579c-148">Criar a interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-148">Create hello network interface</span></span>

<span data-ttu-id="9579c-149">Uma máquina virtual tem um toocommunicate de interface de rede na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="9579c-150">toocreate uma interface de rede, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="9579c-151">Criar máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-151">Create hello virtual machine</span></span>

<span data-ttu-id="9579c-152">Agora que criou Olá todos os recursos de suporte, pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9579c-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="9579c-153">toocreate Olá máquina virtual, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="9579c-154">Este tutorial cria uma máquina virtual com uma versão do sistema de operativo de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9579c-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="9579c-155">toolearn mais informações sobre a seleção de outras imagens, consulte [navegar e selecionar imagens da máquina virtual do Azure com o Windows PowerShell e Olá CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9579c-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="9579c-156">Se quiser toouse um disco existente, em vez de uma imagem do marketplace, utilize este código:</span><span class="sxs-lookup"><span data-stu-id="9579c-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="9579c-157">Executar tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="9579c-157">Perform management tasks</span></span>

<span data-ttu-id="9579c-158">Durante o ciclo de vida de Olá de uma máquina virtual, poderá ser útil toorun tarefas de gestão, tais como iniciar, parar ou eliminar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9579c-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="9579c-159">Além disso, poderá ser útil toocreate código tooautomate complexos ou repetitivos tarefas.</span><span class="sxs-lookup"><span data-stu-id="9579c-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="9579c-160">Quando precisar de toodo nada com Olá VM, terá de tooget uma instância do mesmo.</span><span class="sxs-lookup"><span data-stu-id="9579c-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="9579c-161">Adicione este bloco de try toohello código do método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="9579c-162">Obter informações sobre Olá VM</span><span class="sxs-lookup"><span data-stu-id="9579c-162">Get information about hello VM</span></span>

<span data-ttu-id="9579c-163">tooget informações sobre a máquina virtual de Olá, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="9579c-164">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="9579c-164">Stop hello VM</span></span>

<span data-ttu-id="9579c-165">Pode parar uma máquina virtual e manter todas as respetivas definições, mas continuar toobe cobrada ou pode parar uma máquina virtual e desalocá-lo.</span><span class="sxs-lookup"><span data-stu-id="9579c-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="9579c-166">Quando uma máquina virtual está a ser desalocada, todos os recursos associados à mesma também são extremidades desalocadas e faturação para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="9579c-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="9579c-167">máquina virtual, Olá toostop sem desalocação, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="9579c-168">Se pretender que a máquina de virtual toodeallocate Olá, altere o código de toothis Olá desligado chamada:</span><span class="sxs-lookup"><span data-stu-id="9579c-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="9579c-169">Iniciar Olá VM</span><span class="sxs-lookup"><span data-stu-id="9579c-169">Start hello VM</span></span>

<span data-ttu-id="9579c-170">toostart Olá máquina virtual, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="9579c-171">Redimensionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="9579c-171">Resize hello VM</span></span>

<span data-ttu-id="9579c-172">Muitos aspetos de implementação devem ser considerados ao decidir sobre um tamanho para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9579c-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="9579c-173">Para obter mais informações, consulte [tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="9579c-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="9579c-174">toochange tamanho da máquina virtual de Olá, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="9579c-175">Adicionar um toohello de disco de dados VM</span><span class="sxs-lookup"><span data-stu-id="9579c-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="9579c-176">tooadd uma máquina de virtual de toohello de disco de dados que é de 2 GB de tamanho, tem um LUN de 0 e um tipo de colocação em cache de ReadWrite, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="9579c-177">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="9579c-177">Delete resources</span></span>

<span data-ttu-id="9579c-178">Uma vez que os lhe é cobrados os recursos utilizados no Azure, é sempre recursos de toodelete boa prática que já não são necessárias.</span><span class="sxs-lookup"><span data-stu-id="9579c-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="9579c-179">Se pretender que as máquinas de virtuais toodelete Olá e Olá todos os recursos de suporte, todos os tiver toodo é eliminar grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="9579c-180">recurso de Olá toodelete grupo, adicione este bloco de try toohello código no método principal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9579c-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="9579c-181">Guarde o ficheiro App.java de Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="9579c-182">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="9579c-182">Run hello application</span></span>

<span data-ttu-id="9579c-183">Deve demorar cerca de cinco minutos para que este toorun de aplicação de consola completamente a partir do início toofinish.</span><span class="sxs-lookup"><span data-stu-id="9579c-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="9579c-184">toorun Olá aplicação, utilize este comando Maven:</span><span class="sxs-lookup"><span data-stu-id="9579c-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="9579c-185">Antes de premir **Enter** toostart de recursos a eliminar, foi demorar alguns minutos a criação de Olá tooverify dos recursos de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9579c-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="9579c-186">Clique em Olá implementação Estado toosee obter informações sobre a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="9579c-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9579c-187">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9579c-187">Next steps</span></span>
* <span data-ttu-id="9579c-188">Saiba mais sobre como utilizar Olá [bibliotecas do Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="9579c-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

