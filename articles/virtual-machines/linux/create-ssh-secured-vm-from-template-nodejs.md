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
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Como toocreate uma VM com Linux utilizando Olá CLI do Azure 1.0 um modelo Azure Resource Manager
Este artigo mostra como tooquickly implementar uma Máquina Virtual de Linux utilizando Olá CLI do Azure 1.0 e um modelo Azure Resource Manager. artigo de Olá requer:

* uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).
* Olá [CLI do Azure 1.0](../../cli-install-nodejs.md) registado com `azure login`.
* Olá CLI do Azure *tem de constar* modo Azure Resource Manager `azure config mode arm`.

Pode também rapidamente implementar um modelo de VM com Linux utilizando Olá [portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá
Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

- [Azure CLI 1.0](#quick-command-summary) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá

## <a name="quick-command-summary"></a>Resumo do Comando Rápido
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Instruções Detalhadas
Modelos permitem-lhe toocreate VMs no Azure com as definições que pretende que toocustomize durante a iniciação de Olá, definições, tais como nomes de utilizador e nomes de anfitrião. Para este artigo, vamos iniciar um modelo do Azure que utilize uma VM Ubuntu juntamente com um grupo de segurança de rede (NSG) com a porta 22 aberta para SSH.

Os modelos do Resource Manager do Azure são ficheiros JSON que podem ser utilizados para tarefas pontuais simples, como iniciar uma VM Ubuntu como efetuado neste artigo.  Os modelos do Azure também podem ser utilizado tooconstruct configurações do Azure complexas de ambientes completos, como uma pilha de implementação de teste, programador ou de produção.

## <a name="create-hello-linux-vm"></a>Criar Olá VM com Linux
Olá seguinte como exemplo de código mostra toocall `azure group create` toocreate um recurso do grupo e implementar uma VM de Linux protegidas por SSH ao hello mesmo tempo utilizando [este modelo Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Lembre-se de que no exemplo tem nomes toouse ambiente tooyour exclusivo. Este exemplo utiliza *myResourceGroup* como nome do grupo de recursos de Olá, e *myVM* como nome da VM Olá.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

saída de Olá deve aspeto Olá seguinte bloco de saída:

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

Este exemplo implementada uma VM utilizando Olá `--template-uri` parâmetro.  Também pode transferir ou criar um modelo localmente e passar o modelo de Olá utilizando Olá `--template-file` parâmetro com um ficheiro de modelo do caminho toohello como um argumento. Olá CLI do Azure pede-lhe os parâmetros de Olá exigidos pelo modelo de Olá.

## <a name="next-steps"></a>Passos seguintes
Olá pesquisa [Galeria de modelos](https://azure.microsoft.com/documentation/templates/) toodiscover que toodeploy de estruturas de aplicações seguinte.

