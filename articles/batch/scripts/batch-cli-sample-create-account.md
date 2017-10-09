---
title: aaaAzure CLI Script de exemplo - criar uma conta do Batch | Microsoft Docs
description: Script CLI do Azure de exemplo - criar uma conta do Batch
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Criar uma conta do Batch com Olá CLI do Azure

Este script cria uma conta do Azure Batch e mostra como várias propriedades da conta de Olá podem ser consultadas e atualizadas.

## <a name="prerequisites"></a>Pré-requisitos

Instalação Olá CLI do Azure, utilizando instruções Olá fornecidas Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se ainda não o tiver feito.

## <a name="batch-account-sample-script"></a>Script de exemplo de conta do batch

Quando cria uma conta do Batch, por predefinição respetivos nós de computação são atribuídos internamente Olá serviço Batch. Nós de computação alocados será quota de núcleos separado de tooa do requerente e conta de Olá pode ser autenticada ou através de credenciais de chave partilhada ou um token de Dirctory Active Directory do Azure.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Conta do batch utilizar script de exemplo de subscrição de utilizador

Também pode optar pelas toohave Batch criar respetivos nós de computação na sua própria subscrição do Azure.
Contas que atribuem de processamento de nós na sua subscrição tem de ser autenticados através de um token do Azure Active Directory e nós de computação Olá alocados contabilizará-se a sua cota de subscrição. toocreate uma conta neste modo, um tem de especificar uma referência do Cofre de chaves ao criar a conta de Olá.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar qualquer uma das Olá acima scripts de exemplo, execute Olá tooremove de comando a seguir o grupo de recursos e recursos de todos os relacionados (incluindo as contas do Batch, contas de armazenamento do Azure e cofres de chaves do Azure).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, a conta do Batch e recursos relacionados todos os. Cada comando na documentação do Olá tabela ligações toocommand específicos.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [criar conta do batch AZ](https://docs.microsoft.com/cli/azure/batch/account#create) | Cria a conta do Batch Olá.  |
| [conjunto de conta do batch AZ](https://docs.microsoft.com/cli/azure/batch/account#set) | Atualiza as propriedades de Olá conta do Batch.  |
| [Mostrar de conta do batch AZ](https://docs.microsoft.com/cli/azure/batch/account#show) | Obtém detalhes de Olá especificar a conta do Batch.  |
| [lista de chaves de conta de batch AZ](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Obtém Olá chaves de acesso de Olá especificar a conta do Batch.  |
| [início de sessão de conta de batch de AZ](https://docs.microsoft.com/cli/azure/batch/account#login) | Autentica contra Olá especificado conta para obter mais interação do CLI do Batch.  |
| [criar conta de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/account#create) | Cria uma conta de armazenamento. |
| [Criar AZ keyvault](https://docs.microsoft.com/cli/azure/keyvault#create) | Cria um cofre de chaves. |
| [política de conjunto do keyvault AZ](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Atualize a política de segurança de Olá do Cofre de chaves especificado Olá. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/group#delete) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de Batch CLI adicionais podem ser encontrados na Olá [documentação da CLI do Azure Batch](../batch-cli-samples.md).
