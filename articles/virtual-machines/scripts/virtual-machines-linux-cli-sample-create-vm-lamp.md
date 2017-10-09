---
title: "aaaAzure CLI Script de exemplo - implementar Olá LAMP pilha num conjunto de dimensionamento Load-Balanced à Machin | Microsoft Docs"
description: "Utilize um Olá de toodeploy de extensão LAMP pilha de script personalizado numa carga = dimensionamento da máquina de virtual com balanceamento definida no Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Implementar a pilha LAMP Olá num conjunto de dimensionamento da máquina de virtual com balanceamento de carga

Este exemplo cria um conjunto de dimensionamento de máquina virtual e aplica-se de uma extensão que executa uma pilha de LAMP do script personalizado toodeploy Olá em cada máquina virtual num conjunto de dimensionamento de Olá.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Ligar

Utilize este toosee de código como definir tooconnect tooyour VMs e a escala.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá seguir o grupo de recursos do comando tooremove Olá, conjunto de dimensionamento de Olá e VMs e todos os recursos relacionados.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar AZ vmss](https://docs.microsoft.com/cli/azure/vmss#create) | Cria um conjunto de dimensionamento de máquina virtual |
| [Criar regra de lb AZ de rede](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Adicionar um ponto final com balanceamento de carga |
| [conjunto de extensão de vmss AZ](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Criar extensão Olá que executa o script personalizado Olá na implementação de uma VM |
| [instâncias de atualização do vmss AZ](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Executar script personalizado Olá em instâncias VM de Olá que foram implementadas antes de extensão de Olá foi aplicada toohello conjunto de dimensionamento. |
| [escala de vmss AZ](https://docs.microsoft.com/cli/azure/vmss#scale) | Aumentar verticalmente escala Olá definida adicionando mais instâncias VM. script personalizado Olá é executado nestes quando estão implementadas. |
| [lista de ip público de rede AZ](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Obter os endereços IP de Olá de Olá VMs criadas pelo exemplo Olá. |
| [Mostrar de lb AZ rede](https://docs.microsoft.com/cli/azure/network/lb#show) | Obter o front-end de Olá e back-end portas utilizadas pelo balanceador de carga Olá. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
