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
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Como toocreate uma máquina virtual do Linux com modelos Azure Resource Manager
Este artigo mostra como tooquickly implementar uma máquina virtual (VM) do Linux com modelos Azure Resource Manager e Olá Azure CLI 2.0. Também pode executar estes passos com Olá [CLI do Azure 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Descrição geral de modelos
Modelos Azure Resource Manager são ficheiros JSON que definem a infraestrutura de Olá e a configuração da sua solução do Azure. Ao utilizar um modelo, pode implementar repetidamente a solução durante o ciclo de vida da mesma e ter a confiança de que os recursos são implementados num estado consistente. toolearn mais informações sobre o formato de Olá do modelo de Olá e de como construir, consulte [criar o primeiro modelo Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). Olá tooview sintaxe JSON para tipos de recursos, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Criar grupo de recursos
Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos. Um grupo de recursos tem de ser criado antes de uma máquina virtual. Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupVM* no Olá *eastus* região:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Criar a máquina virtual
Olá exemplo seguinte cria uma VM a partir [este modelo Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) com [criar a implementação do grupo az](/cli/azure/group/deployment#create). Forneça um valor Olá da sua própria chave pública SSH, como conteúdo Olá *~/.ssh/id_rsa.pub*. Se precisar de toocreate um par de chaves SSH, consulte [como toocreate e utilizar um SSH par de chaves para VMs com Linux no Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

Neste exemplo, especificou um modelo armazenado no GitHub. Também pode transferir ou criar um modelo e especifique um caminho local Olá com Olá mesmo `--template-file` parâmetro.

tooSSH tooyour VM, obter o endereço IP público Olá com [mostrar de ip público de rede az](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Pode, em seguida, SSH tooyour VM como normal:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Passos seguintes
Neste exemplo, criou uma VM com Linux básico. Para mais modelos do Resource Manager que incluem estruturas de aplicações ou criar ambientes mais complexas, procurar Olá [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).
