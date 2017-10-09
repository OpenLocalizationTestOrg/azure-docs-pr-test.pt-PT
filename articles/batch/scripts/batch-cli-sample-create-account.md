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
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="68b0f-103">Criar uma conta do Batch com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="68b0f-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="68b0f-104">Este script cria uma conta do Azure Batch e mostra como várias propriedades da conta de Olá podem ser consultadas e atualizadas.</span><span class="sxs-lookup"><span data-stu-id="68b0f-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68b0f-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68b0f-105">Prerequisites</span></span>

<span data-ttu-id="68b0f-106">Instalação Olá CLI do Azure, utilizando instruções Olá fornecidas Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se ainda não o tiver feito.</span><span class="sxs-lookup"><span data-stu-id="68b0f-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="68b0f-107">Script de exemplo de conta do batch</span><span class="sxs-lookup"><span data-stu-id="68b0f-107">Batch account sample script</span></span>

<span data-ttu-id="68b0f-108">Quando cria uma conta do Batch, por predefinição respetivos nós de computação são atribuídos internamente Olá serviço Batch.</span><span class="sxs-lookup"><span data-stu-id="68b0f-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="68b0f-109">Nós de computação alocados será quota de núcleos separado de tooa do requerente e conta de Olá pode ser autenticada ou através de credenciais de chave partilhada ou um token de Dirctory Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="68b0f-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="68b0f-110">Conta do batch utilizar script de exemplo de subscrição de utilizador</span><span class="sxs-lookup"><span data-stu-id="68b0f-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="68b0f-111">Também pode optar pelas toohave Batch criar respetivos nós de computação na sua própria subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="68b0f-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="68b0f-112">Contas que atribuem de processamento de nós na sua subscrição tem de ser autenticados através de um token do Azure Active Directory e nós de computação Olá alocados contabilizará-se a sua cota de subscrição.</span><span class="sxs-lookup"><span data-stu-id="68b0f-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="68b0f-113">toocreate uma conta neste modo, um tem de especificar uma referência do Cofre de chaves ao criar a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="68b0f-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="68b0f-114">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="68b0f-114">Clean up deployment</span></span>

<span data-ttu-id="68b0f-115">Depois de executar qualquer uma das Olá acima scripts de exemplo, execute Olá tooremove de comando a seguir o grupo de recursos e recursos de todos os relacionados (incluindo as contas do Batch, contas de armazenamento do Azure e cofres de chaves do Azure).</span><span class="sxs-lookup"><span data-stu-id="68b0f-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="68b0f-116">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="68b0f-116">Script explanation</span></span>

<span data-ttu-id="68b0f-117">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, a conta do Batch e recursos relacionados todos os.</span><span class="sxs-lookup"><span data-stu-id="68b0f-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="68b0f-118">Cada comando na documentação do Olá tabela ligações toocommand específicos.</span><span class="sxs-lookup"><span data-stu-id="68b0f-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="68b0f-119">Comando</span><span class="sxs-lookup"><span data-stu-id="68b0f-119">Command</span></span> | <span data-ttu-id="68b0f-120">Notas</span><span class="sxs-lookup"><span data-stu-id="68b0f-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="68b0f-121">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="68b0f-122">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="68b0f-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="68b0f-123">criar conta do batch AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="68b0f-124">Cria a conta do Batch Olá.</span><span class="sxs-lookup"><span data-stu-id="68b0f-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="68b0f-125">conjunto de conta do batch AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="68b0f-126">Atualiza as propriedades de Olá conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="68b0f-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="68b0f-127">Mostrar de conta do batch AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="68b0f-128">Obtém detalhes de Olá especificar a conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="68b0f-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="68b0f-129">lista de chaves de conta de batch AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="68b0f-130">Obtém Olá chaves de acesso de Olá especificar a conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="68b0f-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="68b0f-131">início de sessão de conta de batch de AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="68b0f-132">Autentica contra Olá especificado conta para obter mais interação do CLI do Batch.</span><span class="sxs-lookup"><span data-stu-id="68b0f-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="68b0f-133">criar conta de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="68b0f-134">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="68b0f-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="68b0f-135">Criar AZ keyvault</span><span class="sxs-lookup"><span data-stu-id="68b0f-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="68b0f-136">Cria um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="68b0f-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="68b0f-137">política de conjunto do keyvault AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="68b0f-138">Atualize a política de segurança de Olá do Cofre de chaves especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="68b0f-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="68b0f-139">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="68b0f-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="68b0f-140">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="68b0f-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68b0f-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="68b0f-141">Next steps</span></span>

<span data-ttu-id="68b0f-142">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="68b0f-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="68b0f-143">Exemplos de script de Batch CLI adicionais podem ser encontrados na Olá [documentação da CLI do Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="68b0f-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
