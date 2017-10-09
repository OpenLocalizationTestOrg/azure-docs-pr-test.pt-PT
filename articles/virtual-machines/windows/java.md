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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Criar e gerir VMs do Windows no Azure utilizando Java

Um [Máquina Virtual do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) tem vários recursos do Azure de suporte. Este artigo abrange a criar, gerir e eliminar recursos VM com o Java. Saiba como:

> [!div class="checklist"]
> * Criar um projeto Maven
> * Adicione as dependências
> * Criar as credenciais
> * Criar recursos
> * Executar tarefas de gestão
> * Eliminar recursos
> * Executar a aplicação Olá

Demora cerca de 20 minutos toodo estes passos.

## <a name="create-a-maven-project"></a>Criar um projeto Maven

1. Se ainda não o fez, instale [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2. Instalar [Maven](http://maven.apache.org/download.cgi).
3. Crie um novo projeto de pasta e Olá:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Adicione as dependências

1. Em Olá `testAzureApp` pasta, abra Olá `pom.xml` de ficheiros e adicionar configuração de compilação de Olá demasiado&lt;projeto&gt; edifício de Olá tooenable da sua aplicação:

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

2. Adicione as dependências de Olá que são necessários tooaccess Olá SDK Java do Azure.

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

3. Guarde o ficheiro de Olá.

## <a name="create-credentials"></a>Criar as credenciais

Antes de começar este passo, certifique-se de que tem acesso tooan [principal de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Deve também registar o ID da aplicação Olá, chave de autenticação de Olá e ID do inquilino Olá que precisa num passo posterior.

### <a name="create-hello-authorization-file"></a>Criar ficheiro de autorização de Olá

1. Crie um ficheiro denominado `azureauth.properties` e adicione tooit estas propriedades:

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

2. Guarde o ficheiro de Olá.
3. Defina uma variável de ambiente com o nome AZURE_AUTH_LOCATION na sua shell com o ficheiro de autenticação do Olá caminho completo toohello.

### <a name="create-hello-management-client"></a>Criar o cliente de gestão de Olá

1. Abra Olá `App.java` de ficheiros em `src\main\java\com\fabrikam` e certifique-se de que esta declaração de pacote na parte superior do Olá:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. Na declaração do pacote de Olá, adicione-os importar instruções:
   
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

2. toocreate Olá credenciais do Active Directory que tem de toomake pedidos, adicione este código toohello o método main de Olá classe de aplicação:
   
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

## <a name="create-resources"></a>Criar recursos

### <a name="create-hello-resource-group"></a>Criar grupo de recursos de Olá

Todos os recursos tem de estar contidos num [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

toospecify valores para Olá aplicação e criar o grupo de recursos de Olá, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Criar conjunto de disponibilidade de Olá

[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para si toomaintain Olá máquinas virtuais utilizadas pela sua aplicação.

disponibilidade de Olá toocreate definido, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Criar endereço IP público do Olá

A [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é toocommunicate necessário com a máquina virtual de Olá.

toocreate Olá público do endereço IP máquina virtual de Olá, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Criar rede virtual Olá

Uma máquina virtual tem de ser uma sub-rede de um [rede Virtual](../../virtual-network/virtual-networks-overview.md).

toocreate uma sub-rede e uma rede virtual, adicione este bloco de try toohello código no método principal de Olá:

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

### <a name="create-hello-network-interface"></a>Criar a interface de rede Olá

Uma máquina virtual tem um toocommunicate de interface de rede na rede virtual Olá.

toocreate uma interface de rede, adicione este bloco de try toohello código no método principal de Olá:

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

### <a name="create-hello-virtual-machine"></a>Criar máquina virtual de Olá

Agora que criou Olá todos os recursos de suporte, pode criar uma máquina virtual.

toocreate Olá máquina virtual, adicione este bloco de try toohello código no método principal de Olá:

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
> Este tutorial cria uma máquina virtual com uma versão do sistema de operativo de servidor do Windows hello. toolearn mais informações sobre a seleção de outras imagens, consulte [navegar e selecionar imagens da máquina virtual do Azure com o Windows PowerShell e Olá CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se quiser toouse um disco existente, em vez de uma imagem do marketplace, utilize este código: 

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

## <a name="perform-management-tasks"></a>Executar tarefas de gestão

Durante o ciclo de vida de Olá de uma máquina virtual, poderá ser útil toorun tarefas de gestão, tais como iniciar, parar ou eliminar uma máquina virtual. Além disso, poderá ser útil toocreate código tooautomate complexos ou repetitivos tarefas.

Quando precisar de toodo nada com Olá VM, terá de tooget uma instância do mesmo. Adicione este bloco de try toohello código do método principal de Olá:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Obter informações sobre Olá VM

tooget informações sobre a máquina virtual de Olá, adicione este bloco de try toohello código no método principal de Olá:

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

### <a name="stop-hello-vm"></a>Parar Olá VM

Pode parar uma máquina virtual e manter todas as respetivas definições, mas continuar toobe cobrada ou pode parar uma máquina virtual e desalocá-lo. Quando uma máquina virtual está a ser desalocada, todos os recursos associados à mesma também são extremidades desalocadas e faturação para o mesmo.

máquina virtual, Olá toostop sem desalocação, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Se pretender que a máquina de virtual toodeallocate Olá, altere o código de toothis Olá desligado chamada:

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Iniciar Olá VM

toostart Olá máquina virtual, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Redimensionar Olá VM

Muitos aspetos de implementação devem ser considerados ao decidir sobre um tamanho para a máquina virtual. Para obter mais informações, consulte [tamanhos de VM](sizes.md).  

toochange tamanho da máquina virtual de Olá, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Adicionar um toohello de disco de dados VM

tooadd uma máquina de virtual de toohello de disco de dados que é de 2 GB de tamanho, tem um LUN de 0 e um tipo de colocação em cache de ReadWrite, adicione este bloco de try toohello código no método principal de Olá:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Eliminar recursos

Uma vez que os lhe é cobrados os recursos utilizados no Azure, é sempre recursos de toodelete boa prática que já não são necessárias. Se pretender que as máquinas de virtuais toodelete Olá e Olá todos os recursos de suporte, todos os tiver toodo é eliminar grupo de recursos de Olá.

1. recurso de Olá toodelete grupo, adicione este bloco de try toohello código no método principal de Olá:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Guarde o ficheiro App.java de Olá.

## <a name="run-hello-application"></a>Executar a aplicação Olá

Deve demorar cerca de cinco minutos para que este toorun de aplicação de consola completamente a partir do início toofinish.

1. toorun Olá aplicação, utilize este comando Maven:

    ```
    mvn compile exec:java
    ```

2. Antes de premir **Enter** toostart de recursos a eliminar, foi demorar alguns minutos a criação de Olá tooverify dos recursos de Olá no Olá portal do Azure. Clique em Olá implementação Estado toosee obter informações sobre a implementação de Olá.


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre como utilizar Olá [bibliotecas do Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

