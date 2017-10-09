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
# <a name="create-an-internal-load-balancer-using-a-template"></a>Criar um balanceador de carga interno com um modelo

> [!div class="op_single_selector"]
> * [Portal do Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez de Olá [modelo de implementação clássica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implementar a modelo Olá utilizando clique toodeploy

Olá modelo de exemplo disponível no repositório público Olá utiliza um ficheiro de parâmetros que contém as cenário de Olá valores utilizados de predefinição do Olá toogenerate descrito acima. toodeploy utilizando este modelo Clique toodeploy, siga [esta ligação](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), clique em **implementar tooAzure**, substitua os valores de parâmetros de predefinição Olá se necessário e siga as instruções de Olá no portal de Olá.

## <a name="deploy-hello-template-by-using-powershell"></a>Implementar a modelo de Olá utilizando o PowerShell

modelo de Olá toodeploy transferidas utilizando o PowerShell, siga os passos de Olá abaixo.

1. Se nunca tiver utilizado o Azure PowerShell, consulte o artigo [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções de Olá todos os toohello de forma Olá terminar toosign no Azure e selecionar a sua subscrição.
2. Transferir Olá parâmetros tooyour local o disco do ficheiro.
3. Edite o ficheiro de Olá e guardá-lo.
4. Executar Olá **New-AzureRmResourceGroupDeployment** toocreate cmdlet um grupo de recursos utilizando Olá modelo.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implementar a modelo de Olá utilizando Olá CLI do Azure

modelo de Olá toodeploy utilizando Olá CLI do Azure, siga os passos de Olá abaixo.

1. Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.
2. Executar Olá **modo de configuração do azure** comando tooswitch tooResource modo Manager, como mostrado abaixo.

    ```azurecli
    azure config mode arm
    ```

    O resultado para o comando de Olá acima Olá esperado é:

        info:    New mode is arm

3. Abra o ficheiro de parâmetros de Olá, selecione o seu conteúdo e guardá-lo tooa ficheiros no seu computador. Neste exemplo, foi guardado o ficheiro de parâmetros de Olá demasiado*Parameters. JSON*.
4. Executar Olá **criar a implementação do grupo do azure** toodeploy Olá novo Balanceador de carga interno utilizando o modelo de Olá e parâmetro de comando ficheiros que transferiu e alterou acima. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Passos seguintes

[Configurar um modo de distribuição de balanceador de carga com a afinidade do IP de origem](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

