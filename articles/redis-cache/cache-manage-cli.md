---
title: aaaManage na Cache de Redis do Azure utilizando a CLI do Azure | Microsoft Docs
description: "Saiba como tooinstall Olá CLI do Azure em qualquer plataforma, como toouse-tooconnect tooyour conta do Azure e como toocreate e gerir uma cache de Redis do Olá CLI do Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="57979-103">Como toocreate e gerir a Cache de Redis do Azure utilizando Olá Interface de linha de comandos do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="57979-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57979-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="57979-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="57979-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="57979-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="57979-106">Olá CLI do Azure é uma excelente forma toomanage infraestrutura do Azure a partir de qualquer plataforma.</span><span class="sxs-lookup"><span data-stu-id="57979-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="57979-107">Este artigo mostra como toocreate e gerir as instâncias de Cache de Redis do Azure utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="57979-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="57979-108">Este artigo aplica-se a versão anterior do tooa da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="57979-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="57979-109">Para scripts de exemplo de Azure CLI 2.0 mais recentes do Olá, consulte [exemplos de cache de Redis do Azure CLI](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="57979-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="57979-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="57979-110">Prerequisites</span></span>
<span data-ttu-id="57979-111">toocreate e gerir instâncias de Cache de Redis do Azure utilizando a CLI do Azure, tem de concluir Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="57979-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="57979-112">Tem de ter uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="57979-112">You must have an Azure account.</span></span> <span data-ttu-id="57979-113">Se não tiver uma, pode criar um [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) dentro de alguns momentos.</span><span class="sxs-lookup"><span data-stu-id="57979-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="57979-114">[Instalar a CLI do Azure de Olá](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="57979-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="57979-115">Ligar a instalação da CLI do Azure com uma conta pessoal do Azure, ou com um trabalho ou escola conta do Azure e iniciar sessão a partir Olá CLI do Azure utilizando Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="57979-116">toounderstand Olá diferenças e escolher, consulte [ligar tooan subscrição do Azure a partir de Olá Interface de linha de comandos do Azure (CLI do Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="57979-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="57979-117">Antes de executar qualquer um dos seguintes comandos de Olá, mudar Olá CLI do Azure para o modo Resource Manager executando Olá `azure config mode arm` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="57979-118">Para obter mais informações, consulte [utilizar Olá CLI do Azure toomanage Azure recursos e os grupos de recurso](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="57979-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="57979-119">Propriedades da Cache de redis</span><span class="sxs-lookup"><span data-stu-id="57979-119">Redis Cache properties</span></span>
<span data-ttu-id="57979-120">Olá propriedades seguintes são utilizadas quando criar e atualizar instâncias de Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="57979-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="57979-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="57979-121">Property</span></span> | <span data-ttu-id="57979-122">Comutador</span><span class="sxs-lookup"><span data-stu-id="57979-122">Switch</span></span> | <span data-ttu-id="57979-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="57979-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57979-124">nome</span><span class="sxs-lookup"><span data-stu-id="57979-124">name</span></span> |<span data-ttu-id="57979-125">-n, – nome</span><span class="sxs-lookup"><span data-stu-id="57979-125">-n, --name</span></span> |<span data-ttu-id="57979-126">Nome do Olá a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="57979-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="57979-127">grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="57979-127">resource group</span></span> |<span data-ttu-id="57979-128">-g, - grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="57979-128">-g, --resource-group</span></span> |<span data-ttu-id="57979-129">Nome do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="57979-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="57979-130">localização</span><span class="sxs-lookup"><span data-stu-id="57979-130">location</span></span> |<span data-ttu-id="57979-131">-l, – localização</span><span class="sxs-lookup"><span data-stu-id="57979-131">-l, --location</span></span> |<span data-ttu-id="57979-132">Cache de toocreate de localização.</span><span class="sxs-lookup"><span data-stu-id="57979-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="57979-133">Tamanho</span><span class="sxs-lookup"><span data-stu-id="57979-133">size</span></span> |<span data-ttu-id="57979-134">-z, - tamanho</span><span class="sxs-lookup"><span data-stu-id="57979-134">-z, --size</span></span> |<span data-ttu-id="57979-135">Tamanho do Olá a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="57979-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="57979-136">Os valores válidos: [C0 C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="57979-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="57979-137">SKU</span><span class="sxs-lookup"><span data-stu-id="57979-137">sku</span></span> |<span data-ttu-id="57979-138">-x, - sku</span><span class="sxs-lookup"><span data-stu-id="57979-138">-x, --sku</span></span> |<span data-ttu-id="57979-139">SKU de redis.</span><span class="sxs-lookup"><span data-stu-id="57979-139">Redis SKU.</span></span> <span data-ttu-id="57979-140">Deve ser um dos: [básico, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="57979-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="57979-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="57979-141">EnableNonSslPort</span></span> |<span data-ttu-id="57979-142">-i, - enable-não--porta ssl</span><span class="sxs-lookup"><span data-stu-id="57979-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="57979-143">Propriedade EnableNonSslPort de Olá a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="57979-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="57979-144">Adicionar este sinalizador, se quiser tooenable Olá porta de SSL não para a sua cache</span><span class="sxs-lookup"><span data-stu-id="57979-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="57979-145">Configuração de redis</span><span class="sxs-lookup"><span data-stu-id="57979-145">Redis Configuration</span></span> |<span data-ttu-id="57979-146">-c - redis-configuração,</span><span class="sxs-lookup"><span data-stu-id="57979-146">-c, --redis-configuration</span></span> |<span data-ttu-id="57979-147">Configuração de redis.</span><span class="sxs-lookup"><span data-stu-id="57979-147">Redis Configuration.</span></span> <span data-ttu-id="57979-148">Introduza uma cadeia de formatação JSON de chaves de configuração e os valores aqui.</span><span class="sxs-lookup"><span data-stu-id="57979-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="57979-149">Formato: "{" ":""," ":" "}"</span><span class="sxs-lookup"><span data-stu-id="57979-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="57979-150">Configuração de redis</span><span class="sxs-lookup"><span data-stu-id="57979-150">Redis Configuration</span></span> |<span data-ttu-id="57979-151">-f, - ficheiro de configuração de redis</span><span class="sxs-lookup"><span data-stu-id="57979-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="57979-152">Configuração de redis.</span><span class="sxs-lookup"><span data-stu-id="57979-152">Redis Configuration.</span></span> <span data-ttu-id="57979-153">Introduza o caminho de Olá de um ficheiro que contém chaves de configuração e os valores aqui.</span><span class="sxs-lookup"><span data-stu-id="57979-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="57979-154">Formato de entrada do ficheiro Olá: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="57979-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="57979-155">Contagem de partições horizontais</span><span class="sxs-lookup"><span data-stu-id="57979-155">Shard Count</span></span> |<span data-ttu-id="57979-156">-r, - contagem de partições horizontais</span><span class="sxs-lookup"><span data-stu-id="57979-156">-r, --shard-count</span></span> |<span data-ttu-id="57979-157">Número de partições horizontais toocreate numa Cache de Cluster Premium com clustering.</span><span class="sxs-lookup"><span data-stu-id="57979-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="57979-158">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="57979-158">Virtual Network</span></span> |<span data-ttu-id="57979-159">-v, - rede virtual</span><span class="sxs-lookup"><span data-stu-id="57979-159">-v, --virtual-network</span></span> |<span data-ttu-id="57979-160">Quando a alojar a cache numa VNET, especifica Olá exato ARM ID de recurso de Olá de toodeploy de rede virtual Olá a cache de redis no.</span><span class="sxs-lookup"><span data-stu-id="57979-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="57979-161">Formato de exemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="57979-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="57979-162">tipo de chave</span><span class="sxs-lookup"><span data-stu-id="57979-162">key type</span></span> |<span data-ttu-id="57979-163">-t, - tipo de chave</span><span class="sxs-lookup"><span data-stu-id="57979-163">-t, --key-type</span></span> |<span data-ttu-id="57979-164">Tipo de chave toorenew.</span><span class="sxs-lookup"><span data-stu-id="57979-164">Type of key toorenew.</span></span> <span data-ttu-id="57979-165">Os valores válidos: [principal, secundária]</span><span class="sxs-lookup"><span data-stu-id="57979-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="57979-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="57979-166">StaticIP</span></span> |<span data-ttu-id="57979-167">-p, - ip estático < ip estático ></span><span class="sxs-lookup"><span data-stu-id="57979-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="57979-168">Quando a alojar a cache numa VNET, especifica um endereço IP exclusivo na sub-rede Olá para a cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="57979-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="57979-169">Se não for indicado, um valor é escolhido por si da sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="57979-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="57979-170">Subrede</span><span class="sxs-lookup"><span data-stu-id="57979-170">Subnet</span></span> |<span data-ttu-id="57979-171">t, – sub-rede<subnet></span><span class="sxs-lookup"><span data-stu-id="57979-171">t, --subnet <subnet></span></span> |<span data-ttu-id="57979-172">Quando a alojar a cache numa VNET, especifica o nome de Olá da sub-rede Olá na cache de Olá que toodeploy.</span><span class="sxs-lookup"><span data-stu-id="57979-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="57979-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="57979-173">VirtualNetwork</span></span> |<span data-ttu-id="57979-174">-v, - rede virtual <-rede virtual ></span><span class="sxs-lookup"><span data-stu-id="57979-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="57979-175">Quando a alojar a cache numa VNET, especifica Olá exato ARM ID de recurso de Olá de toodeploy de rede virtual Olá a cache de redis no.</span><span class="sxs-lookup"><span data-stu-id="57979-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="57979-176">Formato de exemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="57979-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="57979-177">Subscrição</span><span class="sxs-lookup"><span data-stu-id="57979-177">Subscription</span></span> |<span data-ttu-id="57979-178">-s, - subscrição</span><span class="sxs-lookup"><span data-stu-id="57979-178">-s, --subscription</span></span> |<span data-ttu-id="57979-179">Identificador de subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="57979-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="57979-180">Ver todos os comandos de Cache de Redis</span><span class="sxs-lookup"><span data-stu-id="57979-180">See all Redis Cache commands</span></span>
<span data-ttu-id="57979-181">toosee todos os comandos de Cache de Redis e os respetivos parâmetros, utilize Olá `azure rediscache -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="57979-182">Criar uma Cache de Redis</span><span class="sxs-lookup"><span data-stu-id="57979-182">Create a Redis Cache</span></span>
<span data-ttu-id="57979-183">toocreate uma Cache de Redis, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="57979-184">Para obter mais informações sobre este comando, execute Olá `azure rediscache create -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="57979-185">Eliminar uma Cache de Redis existente</span><span class="sxs-lookup"><span data-stu-id="57979-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="57979-186">toodelete uma Cache de Redis, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="57979-187">Para obter mais informações sobre este comando, execute Olá `azure rediscache delete -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="57979-188">Lista todas as Caches de Redis dentro da sua subscrição ou grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="57979-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="57979-189">toolist todas as Caches de Redis dentro da sua subscrição ou grupo de recursos, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="57979-190">Para obter mais informações sobre este comando, execute Olá `azure rediscache list -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="57979-191">Mostrar propriedades de uma Cache de Redis existente</span><span class="sxs-lookup"><span data-stu-id="57979-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="57979-192">tooshow propriedades de uma Cache de Redis existente, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="57979-193">Para obter mais informações sobre este comando, execute Olá `azure rediscache show -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="57979-194">Alterar as definições de uma Cache de Redis existente</span><span class="sxs-lookup"><span data-stu-id="57979-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="57979-195">definições de toochange de uma Cache de Redis existente, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="57979-196">Para obter mais informações sobre este comando, execute Olá `azure rediscache set -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="57979-197">Renovar a chave de autenticação de Olá para uma Cache de Redis existente</span><span class="sxs-lookup"><span data-stu-id="57979-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="57979-198">chave de autenticação do Olá toorenew para um existente a Cache de Redis, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="57979-199">Especifique `Primary` ou `Secondary` para `key-type`.</span><span class="sxs-lookup"><span data-stu-id="57979-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="57979-200">Para obter mais informações sobre este comando, execute Olá `azure rediscache renew-key -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="57979-201">Chaves de lista primário e secundário de uma Cache de Redis existente</span><span class="sxs-lookup"><span data-stu-id="57979-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="57979-202">as chaves de principais e secundários toolist de uma Cache de Redis existente, utilizar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="57979-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="57979-203">Para obter mais informações sobre este comando, execute Olá `azure rediscache list-keys -h` comando.</span><span class="sxs-lookup"><span data-stu-id="57979-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
