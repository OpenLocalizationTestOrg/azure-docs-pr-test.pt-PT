---
title: aaaCreate e gerir uma VM do Windows no Azure com o Python | Microsoft Docs
description: Saiba mais toouse Python toocreate e gerir uma VM do Windows no Azure.
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
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="4ba54-103">Criar e gerir VMs do Windows no Azure com o Python</span><span class="sxs-lookup"><span data-stu-id="4ba54-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="4ba54-104">Um [Máquina Virtual do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) tem vários recursos do Azure de suporte.</span><span class="sxs-lookup"><span data-stu-id="4ba54-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="4ba54-105">Este artigo abrange a criar, gerir e eliminar recursos da VM com o Python.</span><span class="sxs-lookup"><span data-stu-id="4ba54-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="4ba54-106">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="4ba54-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ba54-107">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ba54-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="4ba54-108">Instalar pacotes</span><span class="sxs-lookup"><span data-stu-id="4ba54-108">Install packages</span></span>
> * <span data-ttu-id="4ba54-109">Criar as credenciais</span><span class="sxs-lookup"><span data-stu-id="4ba54-109">Create credentials</span></span>
> * <span data-ttu-id="4ba54-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="4ba54-110">Create resources</span></span>
> * <span data-ttu-id="4ba54-111">Executar tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="4ba54-111">Perform management tasks</span></span>
> * <span data-ttu-id="4ba54-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="4ba54-112">Delete resources</span></span>
> * <span data-ttu-id="4ba54-113">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="4ba54-113">Run hello application</span></span>

<span data-ttu-id="4ba54-114">Demora cerca de 20 minutos toodo estes passos.</span><span class="sxs-lookup"><span data-stu-id="4ba54-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="4ba54-115">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ba54-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="4ba54-116">Se ainda não o fez, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="4ba54-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="4ba54-117">Selecione **desenvolvimento do Python** no Olá página de cargas de trabalho e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="4ba54-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="4ba54-118">Resumo de Olá, pode ver que **Python 3 64-bit (3.6.0)** é selecionado automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="4ba54-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="4ba54-119">Se já tiver instalado o Visual Studio, pode adicionar a carga de trabalho do Python Olá utilizando Olá Iniciador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ba54-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="4ba54-120">Depois de instalar e iniciar o Visual Studio, clique em **ficheiro** > **novo** > **projeto**.</span><span class="sxs-lookup"><span data-stu-id="4ba54-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="4ba54-121">Clique em **modelos** > **Python** > **aplicação Python**, introduza *myPythonProject* para o nome de Olá do projeto de Olá, selecionar localização de Olá do projeto de Olá e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ba54-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="4ba54-122">Instalar pacotes</span><span class="sxs-lookup"><span data-stu-id="4ba54-122">Install packages</span></span>

1. <span data-ttu-id="4ba54-123">No Explorador de soluções, em *myPythonProject*, faça duplo clique **ambientes do Python**e, em seguida, selecione **ambiente virtual adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4ba54-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="4ba54-124">No ecrã de adicionar ambiente Virtual Olá, aceite o nome de predefinido de Olá de *env*, certifique-se de que *Python 3.6 (64-bit)* está selecionado para o interpretador base Olá e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="4ba54-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="4ba54-125">Contexto Olá *env* ambiente que criou, clique em **Instalar pacote do Python**, introduza *azure* no Olá caixa de pesquisa e, em seguida, prima Enter.</span><span class="sxs-lookup"><span data-stu-id="4ba54-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="4ba54-126">Deverá ver no windows de saída Olá que pacotes hello do azure foram instalados com êxito.</span><span class="sxs-lookup"><span data-stu-id="4ba54-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="4ba54-127">Criar as credenciais</span><span class="sxs-lookup"><span data-stu-id="4ba54-127">Create credentials</span></span>

<span data-ttu-id="4ba54-128">Antes de começar este passo, certifique-se de que tem um [principal de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4ba54-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="4ba54-129">Deve também registar o ID da aplicação Olá, chave de autenticação de Olá e ID do inquilino Olá que precisa num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="4ba54-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="4ba54-130">Abra *myPythonProject.py* ficheiro que foi criado e, em seguida, adicionar este código tooenable toorun a aplicação:</span><span class="sxs-lookup"><span data-stu-id="4ba54-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="4ba54-131">código de Olá tooimport que é necessário, adicione estes topo de toohello instruções do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="4ba54-132">Em seguida no ficheiro. PY Olá, adicione as variáveis depois dos valores comuns de toospecify utilizados em declarações de importação de Olá Olá código:</span><span class="sxs-lookup"><span data-stu-id="4ba54-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="4ba54-133">Substitua **id de subscrição** com o identificador de subscrição.</span><span class="sxs-lookup"><span data-stu-id="4ba54-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="4ba54-134">toocreate Olá credenciais do Active Directory que tem de toomake pedidos, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="4ba54-135">Substitua **id da aplicação**, **chave de autenticação**, e **id do inquilino** com valores de Olá que reuniu anteriormente quando criou o seu Azure Active Directory principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="4ba54-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="4ba54-136">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="4ba54-137">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="4ba54-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="4ba54-138">Inicializar os clientes de gestão</span><span class="sxs-lookup"><span data-stu-id="4ba54-138">Initialize management clients</span></span>

<span data-ttu-id="4ba54-139">Os clientes de gestão são necessário toocreate e gerir recursos com Olá Python SDK no Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba54-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="4ba54-140">os clientes de gestão do toocreate Olá, adicione este código em Olá **se** instrução no fim, em seguida, do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="4ba54-141">Criar Olá VM e recursos de suporte</span><span class="sxs-lookup"><span data-stu-id="4ba54-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="4ba54-142">Todos os recursos tem de estar contidos num [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ba54-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="4ba54-143">toocreate um grupo de recursos, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="4ba54-144">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="4ba54-145">[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para si toomaintain Olá máquinas virtuais utilizadas pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4ba54-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="4ba54-146">toocreate um disponibilidade definido, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="4ba54-147">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="4ba54-148">A [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é toocommunicate necessário com a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ba54-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="4ba54-149">toocreate um endereço IP público para a máquina virtual de Olá, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="4ba54-150">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="4ba54-151">Uma máquina virtual tem de ser uma sub-rede de um [rede Virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ba54-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="4ba54-152">toocreate uma rede virtual, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="4ba54-153">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="4ba54-154">tooadd sub-rede toohello rede virtual, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="4ba54-155">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="4ba54-156">Uma máquina virtual tem um toocommunicate de interface de rede na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="4ba54-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="4ba54-157">toocreate uma interface de rede, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="4ba54-158">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="4ba54-159">Agora que criou Olá todos os recursos de suporte, pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ba54-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="4ba54-160">toocreate Olá máquina virtual, adicione esta função após Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="4ba54-161">Este tutorial cria uma máquina virtual com uma versão do sistema de operativo de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4ba54-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="4ba54-162">toolearn mais informações sobre a seleção de outras imagens, consulte [navegar e selecionar imagens da máquina virtual do Azure com o Windows PowerShell e Olá CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ba54-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="4ba54-163">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="4ba54-164">Executar tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="4ba54-164">Perform management tasks</span></span>

<span data-ttu-id="4ba54-165">Durante o ciclo de vida de Olá de uma máquina virtual, poderá ser útil toorun tarefas de gestão, tais como iniciar, parar ou eliminar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ba54-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="4ba54-166">Além disso, poderá ser útil toocreate código tooautomate complexos ou repetitivos tarefas.</span><span class="sxs-lookup"><span data-stu-id="4ba54-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="4ba54-167">Obter informações sobre Olá VM</span><span class="sxs-lookup"><span data-stu-id="4ba54-167">Get information about hello VM</span></span>

1. <span data-ttu-id="4ba54-168">tooget informações sobre a máquina virtual de Olá, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="4ba54-169">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="4ba54-170">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="4ba54-170">Stop hello VM</span></span>

<span data-ttu-id="4ba54-171">Pode parar uma máquina virtual e manter todas as respetivas definições, mas continuar toobe cobrada ou pode parar uma máquina virtual e desalocá-lo.</span><span class="sxs-lookup"><span data-stu-id="4ba54-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="4ba54-172">Quando uma máquina virtual está a ser desalocada, todos os recursos associados à mesma também são extremidades desalocadas e faturação para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="4ba54-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="4ba54-173">máquina virtual, Olá toostop sem desalocação, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="4ba54-174">Se pretender que a máquina de virtual toodeallocate Olá, altere o código de toothis Olá power_off chamada:</span><span class="sxs-lookup"><span data-stu-id="4ba54-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="4ba54-175">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="4ba54-176">Iniciar Olá VM</span><span class="sxs-lookup"><span data-stu-id="4ba54-176">Start hello VM</span></span>

1. <span data-ttu-id="4ba54-177">toostart Olá máquina virtual, adicione esta função após Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="4ba54-178">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="4ba54-179">Redimensionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="4ba54-179">Resize hello VM</span></span>

<span data-ttu-id="4ba54-180">Muitos aspetos de implementação devem ser considerados ao decidir sobre um tamanho para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ba54-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="4ba54-181">Para obter mais informações, consulte [tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4ba54-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="4ba54-182">toochange Olá tamanho de Olá máquina virtual, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="4ba54-183">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="4ba54-184">Adicionar um toohello de disco de dados VM</span><span class="sxs-lookup"><span data-stu-id="4ba54-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="4ba54-185">Máquinas virtuais podem ter um ou mais [discos de dados](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) que são armazenadas como VHDs.</span><span class="sxs-lookup"><span data-stu-id="4ba54-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="4ba54-186">tooadd uma máquina virtual toohello disco de dados, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="4ba54-187">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="4ba54-188">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="4ba54-188">Delete resources</span></span>

<span data-ttu-id="4ba54-189">Uma vez que os lhe é cobrados os recursos utilizados no Azure, é sempre recursos de toodelete uma boa prática que já não são necessárias.</span><span class="sxs-lookup"><span data-stu-id="4ba54-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="4ba54-190">Se pretender que as máquinas de virtuais toodelete Olá e Olá todos os recursos de suporte, todos os tiver toodo é eliminar grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ba54-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="4ba54-191">grupo de recursos de Olá toodelete e todos os recursos, adicione esta função depois Olá as variáveis no ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="4ba54-192">função de Olá toocall que adicionou anteriormente o, adicione este código em Olá **se** instrução no fim de Olá do ficheiro. PY Olá:</span><span class="sxs-lookup"><span data-stu-id="4ba54-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="4ba54-193">Guardar *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="4ba54-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="4ba54-194">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="4ba54-194">Run hello application</span></span>

1. <span data-ttu-id="4ba54-195">aplicação de consola do toorun Olá, clique em **iniciar** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ba54-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="4ba54-196">Prima **Enter** depois do Estado de Olá de cada recurso é devolvido.</span><span class="sxs-lookup"><span data-stu-id="4ba54-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="4ba54-197">Informações de estado de Olá, deverá ver uma **com êxito** estado de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="4ba54-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="4ba54-198">Depois de criar a máquina virtual de Olá, tiver Olá oportunidade toodelete todos os recursos de Olá que criar.</span><span class="sxs-lookup"><span data-stu-id="4ba54-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="4ba54-199">Antes de premir **Enter** toostart de recursos a eliminar, pode demorar alguns minutos tooverify a criação dos mesmos na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba54-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="4ba54-200">Se tiver hello open portal do Azure, poderá ter toorefresh Olá painel toosee novos recursos.</span><span class="sxs-lookup"><span data-stu-id="4ba54-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="4ba54-201">Deve demorar cerca de cinco minutos para que este toorun de aplicação de consola completamente a partir do início toofinish.</span><span class="sxs-lookup"><span data-stu-id="4ba54-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="4ba54-202">Poderá demorar vários minutos após a aplicação Olá foi concluída antes de todos os recursos de Olá e grupo de recursos de Olá são eliminados.</span><span class="sxs-lookup"><span data-stu-id="4ba54-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ba54-203">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4ba54-203">Next steps</span></span>

- <span data-ttu-id="4ba54-204">Se ocorreram problemas com a implementação de Olá, um passo seguinte será toolook em [resolução de problemas de implementações do grupo de recursos com o portal do Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4ba54-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="4ba54-205">Saiba mais sobre Olá [biblioteca Python do Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="4ba54-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

