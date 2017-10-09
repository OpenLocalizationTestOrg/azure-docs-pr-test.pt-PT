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
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Como toocreate e gerir a Cache de Redis do Azure utilizando Olá Interface de linha de comandos do Azure (CLI do Azure)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [CLI do Azure](cache-manage-cli.md)
>
>

Olá CLI do Azure é uma excelente forma toomanage infraestrutura do Azure a partir de qualquer plataforma. Este artigo mostra como toocreate e gerir as instâncias de Cache de Redis do Azure utilizando Olá CLI do Azure.

> [!NOTE]
> Este artigo aplica-se a versão anterior do tooa da CLI do Azure. Para scripts de exemplo de Azure CLI 2.0 mais recentes do Olá, consulte [exemplos de cache de Redis do Azure CLI](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toocreate e gerir instâncias de Cache de Redis do Azure utilizando a CLI do Azure, tem de concluir Olá os seguintes passos.

* Tem de ter uma conta do Azure. Se não tiver uma, pode criar um [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) dentro de alguns momentos.
* [Instalar a CLI do Azure de Olá](../cli-install-nodejs.md).
* Ligar a instalação da CLI do Azure com uma conta pessoal do Azure, ou com um trabalho ou escola conta do Azure e iniciar sessão a partir Olá CLI do Azure utilizando Olá `azure login` comando. toounderstand Olá diferenças e escolher, consulte [ligar tooan subscrição do Azure a partir de Olá Interface de linha de comandos do Azure (CLI do Azure)](../xplat-cli-connect.md).
* Antes de executar qualquer um dos seguintes comandos de Olá, mudar Olá CLI do Azure para o modo Resource Manager executando Olá `azure config mode arm` comando. Para obter mais informações, consulte [utilizar Olá CLI do Azure toomanage Azure recursos e os grupos de recurso](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Propriedades da Cache de redis
Olá propriedades seguintes são utilizadas quando criar e atualizar instâncias de Cache de Redis.

| Propriedade | Comutador | Descrição |
| --- | --- | --- |
| nome |-n, – nome |Nome do Olá a Cache de Redis. |
| grupo de recursos |-g, - grupo de recursos |Nome do grupo de recursos de Olá. |
| localização |-l, – localização |Cache de toocreate de localização. |
| Tamanho |-z, - tamanho |Tamanho do Olá a Cache de Redis. Os valores válidos: [C0 C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| SKU |-x, - sku |SKU de redis. Deve ser um dos: [básico, Standard, Premium] |
| EnableNonSslPort |-i, - enable-não--porta ssl |Propriedade EnableNonSslPort de Olá a Cache de Redis. Adicionar este sinalizador, se quiser tooenable Olá porta de SSL não para a sua cache |
| Configuração de redis |-c - redis-configuração, |Configuração de redis. Introduza uma cadeia de formatação JSON de chaves de configuração e os valores aqui. Formato: "{" ":""," ":" "}" |
| Configuração de redis |-f, - ficheiro de configuração de redis |Configuração de redis. Introduza o caminho de Olá de um ficheiro que contém chaves de configuração e os valores aqui. Formato de entrada do ficheiro Olá: {"": "","": ""} |
| Contagem de partições horizontais |-r, - contagem de partições horizontais |Número de partições horizontais toocreate numa Cache de Cluster Premium com clustering. |
| Rede Virtual |-v, - rede virtual |Quando a alojar a cache numa VNET, especifica Olá exato ARM ID de recurso de Olá de toodeploy de rede virtual Olá a cache de redis no. Formato de exemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| tipo de chave |-t, - tipo de chave |Tipo de chave toorenew. Os valores válidos: [principal, secundária] |
| StaticIP |-p, - ip estático < ip estático > |Quando a alojar a cache numa VNET, especifica um endereço IP exclusivo na sub-rede Olá para a cache de Olá. Se não for indicado, um valor é escolhido por si da sub-rede Olá. |
| Subrede |t, – sub-rede<subnet> |Quando a alojar a cache numa VNET, especifica o nome de Olá da sub-rede Olá na cache de Olá que toodeploy. |
| VirtualNetwork |-v, - rede virtual <-rede virtual > |Quando a alojar a cache numa VNET, especifica Olá exato ARM ID de recurso de Olá de toodeploy de rede virtual Olá a cache de redis no. Formato de exemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Subscrição |-s, - subscrição |Identificador de subscrição de Olá. |

## <a name="see-all-redis-cache-commands"></a>Ver todos os comandos de Cache de Redis
toosee todos os comandos de Cache de Redis e os respetivos parâmetros, utilize Olá `azure rediscache -h` comando.

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

## <a name="create-a-redis-cache"></a>Criar uma Cache de Redis
toocreate uma Cache de Redis, utilize Olá os seguintes comandos:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Para obter mais informações sobre este comando, execute Olá `azure rediscache create -h` comando.

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

## <a name="delete-an-existing-redis-cache"></a>Eliminar uma Cache de Redis existente
toodelete uma Cache de Redis, utilize Olá os seguintes comandos:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Para obter mais informações sobre este comando, execute Olá `azure rediscache delete -h` comando.

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

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Lista todas as Caches de Redis dentro da sua subscrição ou grupo de recursos
toolist todas as Caches de Redis dentro da sua subscrição ou grupo de recursos, utilize Olá os seguintes comandos:

    azure rediscache list [options]

Para obter mais informações sobre este comando, execute Olá `azure rediscache list -h` comando.

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

## <a name="show-properties-of-an-existing-redis-cache"></a>Mostrar propriedades de uma Cache de Redis existente
tooshow propriedades de uma Cache de Redis existente, utilize Olá os seguintes comandos:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Para obter mais informações sobre este comando, execute Olá `azure rediscache show -h` comando.

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

## <a name="change-settings-of-an-existing-redis-cache"></a>Alterar as definições de uma Cache de Redis existente
definições de toochange de uma Cache de Redis existente, utilize Olá os seguintes comandos:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Para obter mais informações sobre este comando, execute Olá `azure rediscache set -h` comando.

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

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Renovar a chave de autenticação de Olá para uma Cache de Redis existente
chave de autenticação do Olá toorenew para um existente a Cache de Redis, Olá utilize os seguintes comandos:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Especifique `Primary` ou `Secondary` para `key-type`.

Para obter mais informações sobre este comando, execute Olá `azure rediscache renew-key -h` comando.

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

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Chaves de lista primário e secundário de uma Cache de Redis existente
as chaves de principais e secundários toolist de uma Cache de Redis existente, utilizar Olá os seguintes comandos:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Para obter mais informações sobre este comando, execute Olá `azure rediscache list-keys -h` comando.

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
