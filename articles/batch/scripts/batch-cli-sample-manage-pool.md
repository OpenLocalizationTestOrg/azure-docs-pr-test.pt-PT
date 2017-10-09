---
title: aaaAzure CLI Script de exemplo - Gerir agrupamentos no Batch | Microsoft Docs
description: Exemplo de Script da CLI do Azure - Gerir agrupamentos no Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Gerir conjuntos do Azure Batch com a CLI do Azure

Estes scripts demonstra Algumas das ferramentas de Olá disponíveis no Olá CLI do Azure toocreate e gerir conjuntos de nós de computação no serviço do Azure Batch Olá.

> [!NOTE]
> comandos de Olá neste exemplo, criar máquinas virtuais do Azure. VMs em execução serão acumular conta tooyour de encargos. toominimize estes custos, eliminar as VMs de Olá quando tiver terminado o exemplo de Olá em execução. Consulte [limpar agrupamentos](#clean-up-pools).

Conjuntos do batch podem ser configurados de duas formas, com uma configuração de serviços em nuvem (apenas Windows) ou uma configuração de Máquina Virtual (Windows e Linux). scripts de exemplo de Olá abaixo mostram como toocreate agrupamentos com ambas as configurações.

## <a name="prerequisites"></a>Pré-requisitos

- Instalação Olá CLI do Azure, utilizando instruções Olá fornecidas Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se ainda não o tiver feito.
- Se ainda não tiver um, crie uma conta do Batch. Consulte [criar uma conta do Batch com Olá CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.
- Se ainda não o ainda feito, configure toorun uma aplicação de uma tarefa de início. Consulte [adicionar aplicações tooAzure Batch com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para um script de exemplo que cria uma aplicação e carrega um tooAzure do pacote de aplicação.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Conjunto com o script de exemplo de configuração de serviço de nuvem

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Conjunto com o script de exemplo de configuração de máquina virtual

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Limpar os agrupamentos

Depois de executar Olá acima script de exemplo, execute Olá conjuntos de Olá toodelete de comando a seguir.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate e manipular conjuntos do Batch.
Cada comando na documentação do Olá tabela ligações toocommand específicos.

| Comando | Notas |
|---|---|
| [início de sessão de conta de batch de AZ](https://docs.microsoft.com/cli/azure/batch/account#login) | Autenticar face a uma conta do Batch.  |
| [lista de resumo de aplicações de batch de AZ](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Listar Olá aplicações disponíveis na Olá conta do Batch.  |
| [Criar conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool#create) | Crie um conjunto de VMs.  |
| [conjunto de conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool#set) | Atualize propriedades de um conjunto.  |
| [lista de skus de agente de nó de conjunto de batch AZ](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Agente de listas de nó disponível SKUs e as informações da imagem.  |
| [redimensionamento de conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Redimensionamento Olá número de VMs em execução no Olá especificado agrupamento.  |
| [Mostrar de conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool#show) | Apresentar as propriedades de Olá de um conjunto.  |
| [eliminação de conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Eliminar Olá especificado agrupamento.  |
| [Ativar o dimensionamento automático de conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Ativar o dimensionamento automático num agrupamento e aplicar uma fórmula.  |
| [desativar o dimensionamento automático de conjunto do batch AZ](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Desative o dimensionamento automático num agrupamento.  |
| [lista de nós de batch AZ](https://docs.microsoft.com/cli/azure/batch/node#list) | Listar todas as nó de computação Olá Olá especificado agrupamento.  |
| [reinício do nó AZ batch](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Reinicie o nó de cálculo especificada de Olá.  |
| [eliminação de nó do batch AZ](https://docs.microsoft.com/cli/azure/batch/node#delete) | Eliminar Olá listado nós de Olá especificado agrupamento.  |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de Batch CLI adicionais podem ser encontrados na Olá [documentação da CLI do Azure Batch](../batch-cli-samples.md).

