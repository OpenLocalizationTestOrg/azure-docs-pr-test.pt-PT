---
title: aaaCreate uma VM com Linux utilizando um modelo do Azure com a CLI do Azure 1.0 | Microsoft Docs
description: "Crie uma VM com Linux no Azure utilizando Olá CLI do Azure 1.0 e um modelo Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="2e75e-103">Como toocreate uma VM com Linux utilizando Olá CLI do Azure 1.0 um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e75e-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="2e75e-104">Este artigo mostra como tooquickly implementar uma Máquina Virtual de Linux utilizando Olá CLI do Azure 1.0 e um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2e75e-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="2e75e-105">artigo de Olá requer:</span><span class="sxs-lookup"><span data-stu-id="2e75e-105">hello article requires:</span></span>

* <span data-ttu-id="2e75e-106">uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="2e75e-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="2e75e-107">Olá [CLI do Azure 1.0](../../cli-install-nodejs.md) registado com `azure login`.</span><span class="sxs-lookup"><span data-stu-id="2e75e-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="2e75e-108">Olá CLI do Azure *tem de constar* modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="2e75e-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="2e75e-109">Pode também rapidamente implementar um modelo de VM com Linux utilizando Olá [portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e75e-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2e75e-110">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="2e75e-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="2e75e-111">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="2e75e-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="2e75e-112">[Azure CLI 1.0](#quick-command-summary) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="2e75e-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2e75e-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="2e75e-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="2e75e-114">Resumo do Comando Rápido</span><span class="sxs-lookup"><span data-stu-id="2e75e-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="2e75e-115">Instruções Detalhadas</span><span class="sxs-lookup"><span data-stu-id="2e75e-115">Detailed Walkthrough</span></span>
<span data-ttu-id="2e75e-116">Modelos permitem-lhe toocreate VMs no Azure com as definições que pretende que toocustomize durante a iniciação de Olá, definições, tais como nomes de utilizador e nomes de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="2e75e-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="2e75e-117">Para este artigo, vamos iniciar um modelo do Azure que utilize uma VM Ubuntu juntamente com um grupo de segurança de rede (NSG) com a porta 22 aberta para SSH.</span><span class="sxs-lookup"><span data-stu-id="2e75e-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="2e75e-118">Os modelos do Resource Manager do Azure são ficheiros JSON que podem ser utilizados para tarefas pontuais simples, como iniciar uma VM Ubuntu como efetuado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2e75e-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="2e75e-119">Os modelos do Azure também podem ser utilizado tooconstruct configurações do Azure complexas de ambientes completos, como uma pilha de implementação de teste, programador ou de produção.</span><span class="sxs-lookup"><span data-stu-id="2e75e-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="2e75e-120">Criar Olá VM com Linux</span><span class="sxs-lookup"><span data-stu-id="2e75e-120">Create hello Linux VM</span></span>
<span data-ttu-id="2e75e-121">Olá seguinte como exemplo de código mostra toocall `azure group create` toocreate um recurso do grupo e implementar uma VM de Linux protegidas por SSH ao hello mesmo tempo utilizando [este modelo Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="2e75e-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="2e75e-122">Lembre-se de que no exemplo tem nomes toouse ambiente tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="2e75e-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="2e75e-123">Este exemplo utiliza *myResourceGroup* como nome do grupo de recursos de Olá, e *myVM* como nome da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="2e75e-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="2e75e-124">saída de Olá deve aspeto Olá seguinte bloco de saída:</span><span class="sxs-lookup"><span data-stu-id="2e75e-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="2e75e-125">Este exemplo implementada uma VM utilizando Olá `--template-uri` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2e75e-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="2e75e-126">Também pode transferir ou criar um modelo localmente e passar o modelo de Olá utilizando Olá `--template-file` parâmetro com um ficheiro de modelo do caminho toohello como um argumento.</span><span class="sxs-lookup"><span data-stu-id="2e75e-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="2e75e-127">Olá CLI do Azure pede-lhe os parâmetros de Olá exigidos pelo modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e75e-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e75e-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2e75e-128">Next steps</span></span>
<span data-ttu-id="2e75e-129">Olá pesquisa [Galeria de modelos](https://azure.microsoft.com/documentation/templates/) toodiscover que toodeploy de estruturas de aplicações seguinte.</span><span class="sxs-lookup"><span data-stu-id="2e75e-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

