---
title: "aaaTroubleshoot ligações - Azure CLI 2.0 e de Gateway de rede Virtual do Azure | Microsoft Docs"
description: "Esta página explica como toouse Olá observador de rede de Azure resolver Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="c2dc8-103">Resolver problemas de Gateway de rede Virtual e ligações a utilizar o Azure rede observador Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c2dc8-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c2dc8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c2dc8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="c2dc8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2dc8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="c2dc8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c2dc8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="c2dc8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c2dc8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="c2dc8-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c2dc8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="c2dc8-109">Observador de rede oferece muitas funcionalidades no que respeita toounderstanding os recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="c2dc8-110">Uma dessas funcionalidades é recursos de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="c2dc8-111">Resolução de problemas de recursos pode ser chamada através do portal de Olá, do PowerShell, CLI ou REST API.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="c2dc8-112">Quando chamado, o observador de rede inspeciona o estado de funcionamento de Olá de um Gateway de rede Virtual ou uma ligação e devolve conclusões.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="c2dc8-113">Este artigo utiliza a nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá, Azure CLI 2.0, que está disponível para o Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="c2dc8-114">Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c2dc8-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c2dc8-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c2dc8-115">Before you begin</span></span>

<span data-ttu-id="c2dc8-116">Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="c2dc8-117">Para obter uma lista de visita de tipos de gateway suportados, [tipos de Gateway suportado](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="c2dc8-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="c2dc8-118">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="c2dc8-118">Overview</span></span>

<span data-ttu-id="c2dc8-119">Resolução de problemas de recursos oferece a capacidade de Olá resolver problemas que surgem com Gateways de rede Virtual e ligações.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-119">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="c2dc8-120">Quando é efetuado um pedido tooresource de resolução de problemas, registos estão a ser consultado e inspecioná-los.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-120">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="c2dc8-121">Quando a inspeção estiver concluída, resultados de Olá são devolvidos.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-121">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="c2dc8-122">Pedidos de recursos pedidos de resolução de problemas são execução longos, que pode demorar vários minutos tooreturn um resultado.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-122">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="c2dc8-123">os registos de Olá de resolução de problemas são armazenados num contentor numa conta de armazenamento que é especificado.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-123">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="c2dc8-124">Obter uma ligação de Gateway de rede Virtual</span><span class="sxs-lookup"><span data-stu-id="c2dc8-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="c2dc8-125">Neste exemplo, a resolução de problemas de recursos está a ser foi executada numa ligação.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="c2dc8-126">Também pode transmiti-lo um Gateway de rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="c2dc8-127">Olá seguinte cmdlet apresenta uma lista de ligações vpn Olá num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-127">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="c2dc8-128">Assim que tiver o nome de Olá da ligação de Olá, pode executar este comando tooget o Id do recurso:</span><span class="sxs-lookup"><span data-stu-id="c2dc8-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="c2dc8-129">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c2dc8-129">Create a storage account</span></span>

<span data-ttu-id="c2dc8-130">Resolução de problemas de recursos devolve dados sobre o estado de funcionamento de Olá dos recursos de Olá, ela também guarda registos tooa armazenamento conta toobe revisto.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="c2dc8-131">Neste passo, vamos criar uma conta de armazenamento, se existir uma conta de armazenamento existente poderá utilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="c2dc8-132">Criar conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="c2dc8-132">Create hello storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="c2dc8-133">Obter chaves de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="c2dc8-133">Get hello storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="c2dc8-134">Criar contentor de Olá</span><span class="sxs-lookup"><span data-stu-id="c2dc8-134">Create hello container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="c2dc8-135">Executar a resolução de problemas de recursos do observador de rede</span><span class="sxs-lookup"><span data-stu-id="c2dc8-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="c2dc8-136">Resolver problemas relacionados com os recursos com Olá `az network watcher troubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-136">You troubleshoot resources with hello `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="c2dc8-137">Podemos transmitir o grupo de recursos do Olá cmdlet Olá, hello nome Olá observador de rede, Olá Id da ligação de Olá, Olá Id da conta de armazenamento Olá e Olá do Olá caminho toohello blob toostore resolver os resultados no.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="c2dc8-138">Depois de executar o cmdlet Olá, o observador de rede revê o estado de funcionamento do Olá recursos tooverify Olá.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="c2dc8-139">Este devolve resultados Olá toohello shell e armazena os registos de resultados de Olá na conta do storage Olá especificada.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="c2dc8-140">Compreender os resultados de Olá</span><span class="sxs-lookup"><span data-stu-id="c2dc8-140">Understanding hello results</span></span>

<span data-ttu-id="c2dc8-141">o texto de ação de Olá fornece orientações gerais sobre como tooresolve Olá problema.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="c2dc8-142">Se uma ação pode ser levada para o problema de Olá, é fornecida uma ligação com orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="c2dc8-143">No caso de Olá em que não existe nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um incidente de suporte.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="c2dc8-144">Para obter mais informações sobre as propriedades de Olá de resposta Olá e que está incluído, visite [descrição geral de resolução de problemas de observador de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c2dc8-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="c2dc8-145">Para obter instruções sobre como transferir ficheiros entre contas de armazenamento do azure, consulte demasiado[introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c2dc8-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c2dc8-146">Outra ferramenta que pode ser utilizada é Explorador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="c2dc8-147">Obter mais informações sobre o Explorador de armazenamento podem ser encontradas aqui em Olá seguinte hiperligação: [Explorador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="c2dc8-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2dc8-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c2dc8-148">Next steps</span></span>

<span data-ttu-id="c2dc8-149">Se foram alteradas as definições que conectividade VPN de parar, consulte o artigo [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que podem ser em questão.</span><span class="sxs-lookup"><span data-stu-id="c2dc8-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
