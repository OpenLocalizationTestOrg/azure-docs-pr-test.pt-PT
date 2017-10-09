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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="c6044-103">Criar a infraestrutura básica no Azure utilizando Terraform</span><span class="sxs-lookup"><span data-stu-id="c6044-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="c6044-104">Este artigo descreve os passos de Olá tootake tooprovision uma máquina virtual, juntamente com a infraestrutura subjacente, é necessário no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6044-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="c6044-105">Ficará a saber como toowrite Terraform scripts e como toovisualize Olá alterações antes de torná-los na sua infraestrutura de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6044-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="c6044-106">Também ficará a saber como toocreate infraestrutura no Azure utilizando Terraform.</span><span class="sxs-lookup"><span data-stu-id="c6044-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="c6044-107">tooget iniciado, crie um ficheiro chamado \terraform_azure101.tf no seu editor de texto escolhidas (Visual Studio código/Sublime/Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="c6044-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="c6044-108">nome exato do Olá do ficheiro de Olá não é importante porque Terraform aceita o nome da pasta Olá como um parâmetro: todos os scripts na pasta Olá ser executados.</span><span class="sxs-lookup"><span data-stu-id="c6044-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="c6044-109">Cole Olá seguinte código no ficheiro novo Olá:</span><span class="sxs-lookup"><span data-stu-id="c6044-109">Paste hello following code in hello new file:</span></span>

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
<span data-ttu-id="c6044-110">No Olá `provider` secção Olá script, informe Terraform toouse recursos de tooprovision um fornecedor do Azure no script de Olá.</span><span class="sxs-lookup"><span data-stu-id="c6044-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="c6044-111">valores de tooget subscription_id, appId, palavra-passe e tenant_id, consulte Olá [instalar e configurar Terraform](terraform-install-configure.md) guia.</span><span class="sxs-lookup"><span data-stu-id="c6044-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="c6044-112">Se criou variáveis de ambiente para os valores de Olá este bloco, não precisa de tooinclude-lo.</span><span class="sxs-lookup"><span data-stu-id="c6044-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="c6044-113">Olá `azurerm_resource_group` recursos dá instruções ao Terraform toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6044-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="c6044-114">Pode ver mais tipos de recursos que estão disponíveis no Terraform neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c6044-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="c6044-115">Executar script de Olá</span><span class="sxs-lookup"><span data-stu-id="c6044-115">Execute hello script</span></span>
<span data-ttu-id="c6044-116">Depois de guardar o script de Olá, saída toohello consola/linha de comandos e escreva Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6044-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="c6044-117">tooinitialize Olá Terraform o fornecedor do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6044-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="c6044-118">Em seguida, altere o diretório de Olá demasiado**terraformscripts**, e Olá problema os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c6044-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="c6044-119">Utilizámos Olá `plan` Terraform comando, que analisa os recursos de Olá definidos em scripts de Olá.</span><span class="sxs-lookup"><span data-stu-id="c6044-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="c6044-120">Compara-as informações de estado de toohello guardadas pelo Terraform e, em seguida, saídas Olá execução planeada _sem_ efetivamente a criar recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6044-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="c6044-121">Depois de executar o comando anterior Olá, deverá ver algo semelhante Olá ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6044-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Plano de Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="c6044-123">Se tudo procura correto, aprovisionar este novo grupo de recursos no Azure executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6044-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="c6044-124">No portal do Azure Olá, deverá ver Olá novo vazio grupo de recursos denominado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="c6044-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="c6044-125">Olá secção a seguir, adicione que uma máquina virtual e todos os Olá infraestrutura de suporte para esse grupo de recursos de toohello de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6044-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="c6044-126">Aprovisionar uma VM com Ubuntu com Terraform</span><span class="sxs-lookup"><span data-stu-id="c6044-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="c6044-127">Vamos expandir script de Terraform Olá que criámos com detalhes de Olá que são necessária tooprovision uma máquina virtual com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c6044-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="c6044-128">recursos de Olá que for aprovisionado no Olá secções a seguir são:</span><span class="sxs-lookup"><span data-stu-id="c6044-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="c6044-129">Uma rede com uma única sub-rede</span><span class="sxs-lookup"><span data-stu-id="c6044-129">A network with a single subnet</span></span>
* <span data-ttu-id="c6044-130">Uma placa de interface de rede</span><span class="sxs-lookup"><span data-stu-id="c6044-130">A network interface card</span></span> 
* <span data-ttu-id="c6044-131">Uma conta de armazenamento de diagnósticos de máquinas virtuais de Olá</span><span class="sxs-lookup"><span data-stu-id="c6044-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="c6044-132">Um IP público</span><span class="sxs-lookup"><span data-stu-id="c6044-132">A public IP</span></span>
* <span data-ttu-id="c6044-133">Uma máquina virtual que utiliza todos os recursos de anterior Olá</span><span class="sxs-lookup"><span data-stu-id="c6044-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="c6044-134">Para obter documentação detalhada para cada um dos recursos de Azure Terraform Olá, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c6044-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="c6044-135">versão completa do Olá do Olá [script de aprovisionamento](#complete-terraform-script) também são fornecidos por conveniência.</span><span class="sxs-lookup"><span data-stu-id="c6044-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="c6044-136">Expandir o script de Terraform Olá</span><span class="sxs-lookup"><span data-stu-id="c6044-136">Extend hello Terraform script</span></span>
<span data-ttu-id="c6044-137">Expanda o script de Olá que foi criado com Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c6044-137">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="c6044-138">Olá o script anterior cria uma rede virtual e uma sub-rede na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c6044-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="c6044-139">Tenha em atenção Olá referência toohello grupo de recursos que tenha criado já através de "${azurerm_resource_group.helloterraform.name}" na rede virtual Olá e definição de sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="c6044-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="c6044-140">fragmentos de script anteriores Olá criar um IP público e uma interface de rede que utiliza o IP público Olá criado.</span><span class="sxs-lookup"><span data-stu-id="c6044-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="c6044-141">Tenha em atenção Olá referências toosubnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="c6044-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="c6044-142">Terraform tem toounderstand intelligence incorporado que Olá interface de rede tem uma dependência Olá recursos toobe essa necessidade criado antes da criação de Olá Olá da interface de rede.</span><span class="sxs-lookup"><span data-stu-id="c6044-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="c6044-143">Aqui, criou uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6044-143">Here, you created a storage account.</span></span> <span data-ttu-id="c6044-144">Esta conta de armazenamento é onde a máquina virtual de Olá armazenará os detalhes do diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c6044-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="c6044-145">Por fim, fragmento de Olá anterior cria uma máquina virtual que utiliza todos os recursos de Olá já aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="c6044-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="c6044-146">É uma conta de armazenamento de diagnósticos de máquinas virtuais de Olá, uma interface de rede com o IP público e de sub-rede especificado e o grupo de recursos de Olá que já criou.</span><span class="sxs-lookup"><span data-stu-id="c6044-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="c6044-147">Tenha em atenção a propriedade de vm_size Olá, onde o script de Olá Especifica um SKU DS1v2 Standard do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6044-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="c6044-148">São necessário toosupply uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="c6044-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="c6044-149">Coloque o valor de chave pública Olá na secção de Olá **... INTRODUZA A CHAVE PÚBLICA OPENSSH AQUI...**  acima.</span><span class="sxs-lookup"><span data-stu-id="c6044-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="c6044-150">Pode utilizar um existente ssh par de chaves ou seguir Olá [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) par de chaves documentação toogenerate Olá.</span><span class="sxs-lookup"><span data-stu-id="c6044-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="c6044-151">Executar script de Olá</span><span class="sxs-lookup"><span data-stu-id="c6044-151">Execute hello script</span></span>
<span data-ttu-id="c6044-152">Com o script de completo Olá guardado, saia da linha de comando/consola toohello e escreva Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6044-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="c6044-153">Após algum tempo, recursos de Olá, incluindo uma máquina virtual, são apresentados no Olá `terraformtest` grupo de recursos no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6044-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="c6044-154">Script de Terraform concluída</span><span class="sxs-lookup"><span data-stu-id="c6044-154">Complete Terraform script</span></span>

<span data-ttu-id="c6044-155">Para sua comodidade, abaixo é Olá concluída Terraform script que Aprovisiona todos da infraestrutura de Olá abordadas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c6044-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c6044-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c6044-156">Next steps</span></span>
<span data-ttu-id="c6044-157">Criou infraestrutura básica no Azure utilizando Terraform.</span><span class="sxs-lookup"><span data-stu-id="c6044-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="c6044-158">Para cenários mais complexos, incluindo exemplos que utilize balanceadores de carga e a máquina virtual Dimensionar conjuntos, consulte o artigo várias [Terraform exemplos do Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="c6044-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="c6044-159">Para obter uma lista atualizada de fornecedores do Azure suportados, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c6044-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
