---
title: "Criar e gerir uma Máquina Virtual do Azure utilizando Java | Microsoft Docs"
description: "Utilize o Java e o Azure Resource Manager para implementar uma máquina virtual e todos os respetivos recursos de suporte."
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
ms.openlocfilehash: b970b7a5e1db6d8580ede9699d4776a79e03c98f
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/08/2017
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
> * Executar a aplicação

Demora cerca de 20 minutos para executar estes passos.

## <a name="create-a-maven-project"></a>Criar um projeto Maven

1. Se ainda não o fez, instale [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2. Instalar [Maven](http://maven.apache.org/download.cgi).
3. Crie uma nova pasta e o projeto:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Adicione as dependências

1. Sob o `testAzureApp` pasta, abra o `pom.xml` de ficheiros e adicionar a configuração de compilação para &lt;projeto&gt; para permitir a criação da sua aplicação:

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

2. Adicione as dependências que são necessárias para aceder ao SDK Java do Azure.

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

3. Guarde o ficheiro.

## <a name="create-credentials"></a>Criar as credenciais

Antes de começar este passo, certifique-se de que tem acesso a um [principal de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Também deve registar o ID da aplicação, a chave de autenticação e o ID do inquilino que precisa num passo posterior.

### <a name="create-the-authorization-file"></a>Criar o ficheiro de autorização

1. Crie um ficheiro denominado `azureauth.properties` e adicionar-lhe estas propriedades:

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

    Substitua  **&lt;id de subscrição&gt;**  com o identificador de subscrição,  **&lt;id da aplicação&gt;**  com a aplicação do Active Directory Identificador,  **&lt;chave de autenticação&gt;**  com a chave de aplicação, e  **&lt;id do inquilino&gt;**  com o identificador de inquilino.

2. Guarde o ficheiro.
3. Defina uma variável de ambiente com o nome AZURE_AUTH_LOCATION na sua shell com o caminho completo para o ficheiro de autenticação.

### <a name="create-the-management-client"></a>Criar o cliente de gestão

1. Abra o `App.java` de ficheiros em `src\main\java\com\fabrikam` e certifique-se de que esta declaração de pacote na parte superior:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. Sob a instrução de pacote, adicione-os importar instruções:
   
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

2. Para criar as credenciais do Active Directory que necessita para fazer pedidos, adicione este código para o método principal da classe de aplicação:
   
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

### <a name="create-the-resource-group"></a>Criar o grupo de recursos

Todos os recursos tem de estar contidos num [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

Para especificar valores para a aplicação e criar o grupo de recursos, adicione este código para o bloco try no método principal:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-the-availability-set"></a>Criar o conjunto de disponibilidade

[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para si manter as máquinas virtuais utilizadas pela sua aplicação.

Para criar o conjunto de disponibilidade, adicione este código para o bloco try no método principal:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-the-public-ip-address"></a>Criar o endereço IP público

A [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessária para comunicar com a máquina virtual.

Para criar o endereço IP público para a máquina virtual, adicione este código para o bloco try no método principal:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-the-virtual-network"></a>Criar a rede virtual

Uma máquina virtual tem de ser uma sub-rede de um [rede Virtual](../../virtual-network/virtual-networks-overview.md).

Para criar uma sub-rede e uma rede virtual, adicione este código para o bloco try no método principal:

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

### <a name="create-the-network-interface"></a>Criar a interface de rede

Uma máquina virtual necessita de uma interface de rede para comunicar na rede virtual.

Para criar uma interface de rede, adicione este código para o bloco try no método principal:

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

### <a name="create-the-virtual-machine"></a>Criar a máquina virtual

Agora que criou todos os recursos de suporte, pode criar uma máquina virtual.

Para criar a máquina virtual, adicione este código para o bloco try no método principal:

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
System.out.println("Press enter to get information about the VM...");
input.nextLine();
```

> [!NOTE]
> Este tutorial cria uma máquina virtual com uma versão do sistema operativo Windows Server. Para obter mais informações sobre como selecionar outras imagens, consulte [navegar e selecionar imagens da máquina virtual do Azure com o Windows PowerShell e a CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se pretender utilizar um disco existente, em vez de uma imagem do marketplace, utilize este código: 

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

Durante o ciclo de vida de uma máquina virtual, poderá querer executar tarefas de gestão, tais como iniciar, parar ou eliminar uma máquina virtual. Além disso, pode querer criar código para automatizar tarefas repetitivas ou complexas.

Quando precisar de fazer nada, com a VM, terá de obter uma instância do mesmo. Adicione este código para o bloco try do método principal:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-the-vm"></a>Obter informações sobre a VM

Para obter informações sobre a máquina virtual, adicione este código para o bloco try no método principal:

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
System.out.println("Press enter to continue...");
input.nextLine();   
```

### <a name="stop-the-vm"></a>Parar a VM

Pode parar uma máquina virtual e manter todas as respetivas definições, mas continuam a ser-lhe cobrados-lo, ou pode parar uma máquina virtual e desalocá-lo. Quando uma máquina virtual está a ser desalocada, todos os recursos associados à mesma também são extremidades desalocadas e faturação para o mesmo.

Para parar a máquina virtual sem Desalocação-lo, adicione este código para o bloco try no método principal:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter to continue...");
input.nextLine();
```

Se pretender desalocar a máquina virtual, altere a chamada de desligado para este código:

```java
vm.deallocate();
```

### <a name="start-the-vm"></a>Iniciar a VM

Para iniciar a máquina virtual, adicione este código para o bloco try no método principal:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="resize-the-vm"></a>Redimensionar a VM

Muitos aspetos de implementação devem ser considerados ao decidir sobre um tamanho para a máquina virtual. Para obter mais informações, consulte [tamanhos de VM](sizes.md).  

Para alterar o tamanho da máquina virtual, adicione este código para o bloco try no método principal:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="add-a-data-disk-to-the-vm"></a>Adicionar um disco de dados para a VM

Para adicionar um disco de dados para a máquina virtual que é de 2 GB de tamanho, tem um LUN de 0 e um tipo de colocação em cache de ReadWrite, adicione este código para o bloco try no método principal:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter to delete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Eliminar recursos

Porque os lhe é cobrados os recursos utilizados no Azure, é sempre boa prática para eliminar os recursos que já não são necessárias. Se pretender eliminar as máquinas virtuais e todos os recursos de suporte, tudo o que precisa de executar é eliminar o grupo de recursos.

1. Para eliminar o grupo de recursos, adicione este código para o bloco try no método principal:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Guarde o ficheiro App.java.

## <a name="run-the-application"></a>Executar a aplicação

Deve demorar cerca de cinco minutos para esta aplicação de consola executar totalmente do início seja concluída.

1. Para executar a aplicação, utilize este comando Maven:

    ```
    mvn compile exec:java
    ```

2. Antes de premir **Enter** para iniciar a eliminação de recursos, pode demorar alguns minutos para verificar a criação dos recursos no portal do Azure. Clique no estado de implementação para ver informações sobre a implementação.


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre como utilizar o [bibliotecas do Azure para Java](https://docs.microsoft.com/java/azure/java-sdk-azure-overview).

