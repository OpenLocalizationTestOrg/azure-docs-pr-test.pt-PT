---
title: "infraestrutura básica aaaCreate no Azure utilizando Terraform | Microsoft Docs"
description: Saiba como toocreate Azure recursos utilizando Terraform
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Criar a infraestrutura básica no Azure utilizando Terraform
Este artigo descreve os passos de Olá tootake tooprovision uma máquina virtual, juntamente com a infraestrutura subjacente, é necessário no Azure. Ficará a saber como toowrite Terraform scripts e como toovisualize Olá alterações antes de torná-los na sua infraestrutura de nuvem. Também ficará a saber como toocreate infraestrutura no Azure utilizando Terraform.

tooget iniciado, crie um ficheiro chamado \terraform_azure101.tf no seu editor de texto escolhidas (Visual Studio código/Sublime/Vim/etc.). nome exato do Olá do ficheiro de Olá não é importante porque Terraform aceita o nome da pasta Olá como um parâmetro: todos os scripts na pasta Olá ser executados. Cole Olá seguinte código no ficheiro novo Olá:

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
No Olá `provider` secção Olá script, informe Terraform toouse recursos de tooprovision um fornecedor do Azure no script de Olá. valores de tooget subscription_id, appId, palavra-passe e tenant_id, consulte Olá [instalar e configurar Terraform](terraform-install-configure.md) guia. Se criou variáveis de ambiente para os valores de Olá este bloco, não precisa de tooinclude-lo. 

Olá `azurerm_resource_group` recursos dá instruções ao Terraform toocreate um novo grupo de recursos. Pode ver mais tipos de recursos que estão disponíveis no Terraform neste artigo.

## <a name="execute-hello-script"></a>Executar script de Olá
Depois de guardar o script de Olá, saída toohello consola/linha de comandos e escreva Olá seguinte:
```
terraform init
```
 tooinitialize Olá Terraform o fornecedor do Azure. Em seguida, altere o diretório de Olá demasiado**terraformscripts**, e Olá problema os seguintes comandos:
```
terraform plan
```
Utilizámos Olá `plan` Terraform comando, que analisa os recursos de Olá definidos em scripts de Olá. Compara-as informações de estado de toohello guardadas pelo Terraform e, em seguida, saídas Olá execução planeada _sem_ efetivamente a criar recursos no Azure. 

Depois de executar o comando anterior Olá, deverá ver algo semelhante Olá ecrã a seguir:

![Plano de Terraform](./media/terraform/tf_plan2.png)

Se tudo procura correto, aprovisionar este novo grupo de recursos no Azure executando Olá seguinte: 
```
terraform apply
```
No portal do Azure Olá, deverá ver Olá novo vazio grupo de recursos denominado `terraformtest`. Olá secção a seguir, adicione que uma máquina virtual e todos os Olá infraestrutura de suporte para esse grupo de recursos de toohello de máquina virtual.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Aprovisionar uma VM com Ubuntu com Terraform
Vamos expandir script de Terraform Olá que criámos com detalhes de Olá que são necessária tooprovision uma máquina virtual com Ubuntu. recursos de Olá que for aprovisionado no Olá secções a seguir são:

* Uma rede com uma única sub-rede
* Uma placa de interface de rede 
* Uma conta de armazenamento de diagnósticos de máquinas virtuais de Olá
* Um IP público
* Uma máquina virtual que utiliza todos os recursos de anterior Olá 

Para obter documentação detalhada para cada um dos recursos de Azure Terraform Olá, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).

versão completa do Olá do Olá [script de aprovisionamento](#complete-terraform-script) também são fornecidos por conveniência.

### <a name="extend-hello-terraform-script"></a>Expandir o script de Terraform Olá
Expanda o script de Olá que foi criado com Olá os seguintes recursos: 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
Olá o script anterior cria uma rede virtual e uma sub-rede na rede virtual. Tenha em atenção Olá referência toohello grupo de recursos que tenha criado já através de "${azurerm_resource_group.helloterraform.name}" na rede virtual Olá e definição de sub-rede Olá.

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
fragmentos de script anteriores Olá criar um IP público e uma interface de rede que utiliza o IP público Olá criado. Tenha em atenção Olá referências toosubnet_id e public_ip_address_id. Terraform tem toounderstand intelligence incorporado que Olá interface de rede tem uma dependência Olá recursos toobe essa necessidade criado antes da criação de Olá Olá da interface de rede.

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
Aqui, criou uma conta de armazenamento. Esta conta de armazenamento é onde a máquina virtual de Olá armazenará os detalhes do diagnóstico.

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
Por fim, fragmento de Olá anterior cria uma máquina virtual que utiliza todos os recursos de Olá já aprovisionados. É uma conta de armazenamento de diagnósticos de máquinas virtuais de Olá, uma interface de rede com o IP público e de sub-rede especificado e o grupo de recursos de Olá que já criou. Tenha em atenção a propriedade de vm_size Olá, onde o script de Olá Especifica um SKU DS1v2 Standard do Azure.

São necessário toosupply uma chave pública SSH. Coloque o valor de chave pública Olá na secção de Olá **... INTRODUZA A CHAVE PÚBLICA OPENSSH AQUI...**  acima. Pode utilizar um existente ssh par de chaves ou seguir Olá [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) par de chaves documentação toogenerate Olá.

### <a name="execute-hello-script"></a>Executar script de Olá
Com o script de completo Olá guardado, saia da linha de comando/consola toohello e escreva Olá seguinte:
```
terraform apply
```
Após algum tempo, recursos de Olá, incluindo uma máquina virtual, são apresentados no Olá `terraformtest` grupo de recursos no Olá portal do Azure.

## <a name="complete-terraform-script"></a>Script de Terraform concluída

Para sua comodidade, abaixo é Olá concluída Terraform script que Aprovisiona todos da infraestrutura de Olá abordadas neste artigo.

```
# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a>Passos seguintes
Criou infraestrutura básica no Azure utilizando Terraform. Para cenários mais complexos, incluindo exemplos que utilize balanceadores de carga e a máquina virtual Dimensionar conjuntos, consulte o artigo várias [Terraform exemplos do Azure](https://github.com/hashicorp/terraform/tree/master/examples). Para obter uma lista atualizada de fornecedores do Azure suportados, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).
