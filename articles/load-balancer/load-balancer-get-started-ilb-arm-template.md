---
title: aaaCreate um balanceador de carga interno - modelo Azure | Microsoft Docs
description: Saiba como o utilizando um modelo no Gestor de recursos de Balanceador de carga de toocreate um interno
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="35d8f-103">Criar um balanceador de carga interno com um modelo</span><span class="sxs-lookup"><span data-stu-id="35d8f-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35d8f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="35d8f-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="35d8f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35d8f-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="35d8f-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="35d8f-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="35d8f-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="35d8f-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="35d8f-108">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="35d8f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="35d8f-109">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez de Olá [modelo de implementação clássica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35d8f-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="35d8f-110">Implementar a modelo Olá utilizando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="35d8f-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="35d8f-111">Olá modelo de exemplo disponível no repositório público Olá utiliza um ficheiro de parâmetros que contém as cenário de Olá valores utilizados de predefinição do Olá toogenerate descrito acima.</span><span class="sxs-lookup"><span data-stu-id="35d8f-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="35d8f-112">toodeploy utilizando este modelo Clique toodeploy, siga [esta ligação](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá se necessário e siga as instruções de Olá no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="35d8f-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="35d8f-113">Implementar a modelo de Olá utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="35d8f-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="35d8f-114">modelo de Olá toodeploy transferidas utilizando o PowerShell, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="35d8f-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="35d8f-115">Se nunca tiver utilizado o Azure PowerShell, consulte o artigo [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções de Olá todos os toohello de forma Olá terminar toosign no Azure e selecionar a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="35d8f-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="35d8f-116">Transferir Olá parâmetros tooyour local o disco do ficheiro.</span><span class="sxs-lookup"><span data-stu-id="35d8f-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="35d8f-117">Edite o ficheiro de Olá e guardá-lo.</span><span class="sxs-lookup"><span data-stu-id="35d8f-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="35d8f-118">Executar Olá **New-AzureRmResourceGroupDeployment** toocreate cmdlet um grupo de recursos utilizando Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="35d8f-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="35d8f-119">Implementar a modelo de Olá utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="35d8f-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="35d8f-120">modelo de Olá toodeploy utilizando Olá CLI do Azure, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="35d8f-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="35d8f-121">Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="35d8f-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="35d8f-122">Executar Olá **modo de configuração do azure** comando tooswitch tooResource modo Manager, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="35d8f-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="35d8f-123">O resultado para o comando de Olá acima Olá esperado é:</span><span class="sxs-lookup"><span data-stu-id="35d8f-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="35d8f-124">Abra o ficheiro de parâmetros de Olá, selecione o seu conteúdo e guardá-lo tooa ficheiros no seu computador.</span><span class="sxs-lookup"><span data-stu-id="35d8f-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="35d8f-125">Neste exemplo, foi guardado o ficheiro de parâmetros de Olá demasiado*Parameters. JSON*.</span><span class="sxs-lookup"><span data-stu-id="35d8f-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="35d8f-126">Executar Olá **criar a implementação do grupo do azure** toodeploy Olá novo Balanceador de carga interno utilizando o modelo de Olá e parâmetro de comando ficheiros que transferiu e alterou acima.</span><span class="sxs-lookup"><span data-stu-id="35d8f-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="35d8f-127">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="35d8f-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="35d8f-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="35d8f-128">Next steps</span></span>

[<span data-ttu-id="35d8f-129">Configurar um modo de distribuição de balanceador de carga com a afinidade do IP de origem</span><span class="sxs-lookup"><span data-stu-id="35d8f-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="35d8f-130">Configurar definições de tempo limite TCP inativo para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="35d8f-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

