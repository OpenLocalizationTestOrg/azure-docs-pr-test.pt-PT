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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a>Resolver problemas de Gateway de rede Virtual e ligações a utilizar o Azure rede observador Azure CLI 2.0

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observador de rede oferece muitas funcionalidades no que respeita toounderstanding os recursos de rede no Azure. Uma dessas funcionalidades é recursos de resolução de problemas. Resolução de problemas de recursos pode ser chamada através do portal de Olá, do PowerShell, CLI ou REST API. Quando chamado, o observador de rede inspeciona o estado de funcionamento de Olá de um Gateway de rede Virtual ou uma ligação e devolve conclusões.

Este artigo utiliza a nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá, Azure CLI 2.0, que está disponível para o Windows, Mac e Linux.

Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

Para obter uma lista de visita de tipos de gateway suportados, [tipos de Gateway suportado](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Descrição geral

Resolução de problemas de recursos oferece a capacidade de Olá resolver problemas que surgem com Gateways de rede Virtual e ligações. Quando é efetuado um pedido tooresource de resolução de problemas, registos estão a ser consultado e inspecioná-los. Quando a inspeção estiver concluída, resultados de Olá são devolvidos. Pedidos de recursos pedidos de resolução de problemas são execução longos, que pode demorar vários minutos tooreturn um resultado. os registos de Olá de resolução de problemas são armazenados num contentor numa conta de armazenamento que é especificado.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Obter uma ligação de Gateway de rede Virtual

Neste exemplo, a resolução de problemas de recursos está a ser foi executada numa ligação. Também pode transmiti-lo um Gateway de rede Virtual. Olá seguinte cmdlet apresenta uma lista de ligações vpn Olá num grupo de recursos.

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

Assim que tiver o nome de Olá da ligação de Olá, pode executar este comando tooget o Id do recurso:

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Resolução de problemas de recursos devolve dados sobre o estado de funcionamento de Olá dos recursos de Olá, ela também guarda registos tooa armazenamento conta toobe revisto. Neste passo, vamos criar uma conta de armazenamento, se existir uma conta de armazenamento existente poderá utilizá-lo.

1. Criar conta de armazenamento Olá

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. Obter chaves de conta de armazenamento Olá

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. Criar contentor de Olá

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Executar a resolução de problemas de recursos do observador de rede

Resolver problemas relacionados com os recursos com Olá `az network watcher troubleshooting` cmdlet. Podemos transmitir o grupo de recursos do Olá cmdlet Olá, hello nome Olá observador de rede, Olá Id da ligação de Olá, Olá Id da conta de armazenamento Olá e Olá do Olá caminho toohello blob toostore resolver os resultados no.

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

Depois de executar o cmdlet Olá, o observador de rede revê o estado de funcionamento do Olá recursos tooverify Olá. Este devolve resultados Olá toohello shell e armazena os registos de resultados de Olá na conta do storage Olá especificada.

## <a name="understanding-hello-results"></a>Compreender os resultados de Olá

o texto de ação de Olá fornece orientações gerais sobre como tooresolve Olá problema. Se uma ação pode ser levada para o problema de Olá, é fornecida uma ligação com orientações adicionais. No caso de Olá em que não existe nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um incidente de suporte.  Para obter mais informações sobre as propriedades de Olá de resposta Olá e que está incluído, visite [descrição geral de resolução de problemas de observador de rede](network-watcher-troubleshoot-overview.md)

Para obter instruções sobre como transferir ficheiros entre contas de armazenamento do azure, consulte demasiado[introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que pode ser utilizada é Explorador de armazenamento. Obter mais informações sobre o Explorador de armazenamento podem ser encontradas aqui em Olá seguinte hiperligação: [Explorador de armazenamento](http://storageexplorer.com/)

## <a name="next-steps"></a>Passos seguintes

Se foram alteradas as definições que conectividade VPN de parar, consulte o artigo [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que podem ser em questão.
