---
title: aaaCreate uma VM com Linux no Azure a partir de um modelo | Microsoft Docs
description: "Como toouse Olá, Azure CLI 2.0 toocreate uma VM com Linux a partir de um modelo do Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="3e6c6-103">Como toocreate uma máquina virtual do Linux com modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e6c6-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="3e6c6-104">Este artigo mostra como tooquickly implementar uma máquina virtual (VM) do Linux com modelos Azure Resource Manager e Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="3e6c6-105">Também pode executar estes passos com Olá [CLI do Azure 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3e6c6-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="3e6c6-106">Descrição geral de modelos</span><span class="sxs-lookup"><span data-stu-id="3e6c6-106">Templates overview</span></span>
<span data-ttu-id="3e6c6-107">Modelos Azure Resource Manager são ficheiros JSON que definem a infraestrutura de Olá e a configuração da sua solução do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="3e6c6-108">Ao utilizar um modelo, pode implementar repetidamente a solução durante o ciclo de vida da mesma e ter a confiança de que os recursos são implementados num estado consistente.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="3e6c6-109">toolearn mais informações sobre o formato de Olá do modelo de Olá e de como construir, consulte [criar o primeiro modelo Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="3e6c6-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="3e6c6-110">Olá tooview sintaxe JSON para tipos de recursos, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="3e6c6-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="3e6c6-111">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3e6c6-111">Create resource group</span></span>
<span data-ttu-id="3e6c6-112">Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="3e6c6-113">Um grupo de recursos tem de ser criado antes de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="3e6c6-114">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupVM* no Olá *eastus* região:</span><span class="sxs-lookup"><span data-stu-id="3e6c6-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="3e6c6-115">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3e6c6-115">Create virtual machine</span></span>
<span data-ttu-id="3e6c6-116">Olá exemplo seguinte cria uma VM a partir [este modelo Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) com [criar a implementação do grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="3e6c6-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="3e6c6-117">Forneça um valor Olá da sua própria chave pública SSH, como conteúdo Olá *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="3e6c6-118">Se precisar de toocreate um par de chaves SSH, consulte [como toocreate e utilizar um SSH par de chaves para VMs com Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="3e6c6-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="3e6c6-119">Neste exemplo, especificou um modelo armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="3e6c6-120">Também pode transferir ou criar um modelo e especifique um caminho local Olá com Olá mesmo `--template-file` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="3e6c6-121">tooSSH tooyour VM, obter o endereço IP público Olá com [mostrar de ip público de rede az](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="3e6c6-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="3e6c6-122">Pode, em seguida, SSH tooyour VM como normal:</span><span class="sxs-lookup"><span data-stu-id="3e6c6-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="3e6c6-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3e6c6-123">Next steps</span></span>
<span data-ttu-id="3e6c6-124">Neste exemplo, criou uma VM com Linux básico.</span><span class="sxs-lookup"><span data-stu-id="3e6c6-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="3e6c6-125">Para mais modelos do Resource Manager que incluem estruturas de aplicações ou criar ambientes mais complexas, procurar Olá [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="3e6c6-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
