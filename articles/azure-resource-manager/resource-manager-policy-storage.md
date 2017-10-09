---
title: "as políticas de recursos de aaaAzure para contas do storage | Microsoft Docs"
description: "Descreve as políticas do Azure Resource Manager para gerir a implementação de Olá de contas do storage."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="d6c43-103">Aplicar a contas de toostorage de políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="d6c43-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="d6c43-104">Este tópico mostra várias [as políticas de recursos](resource-manager-policy.md) pode aplicar tooAzure contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d6c43-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="d6c43-105">Estas políticas garantir consistência Olá contas do storage implementada na sua organização.</span><span class="sxs-lookup"><span data-stu-id="d6c43-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="d6c43-106">Definir os tipos de conta de armazenamento permitido</span><span class="sxs-lookup"><span data-stu-id="d6c43-106">Define permitted storage account types</span></span>

<span data-ttu-id="d6c43-107">Olá seguinte política restringe o que [tipos de conta de armazenamento](../storage/common/storage-redundancy.md) pode ser implementado:</span><span class="sxs-lookup"><span data-stu-id="d6c43-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="d6c43-108">Uma regra de política semelhantes com um parâmetro para aceitar Olá permitido SKUs está disponível como uma definição de política incorporada.</span><span class="sxs-lookup"><span data-stu-id="d6c43-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="d6c43-109">política incorporada Olá possuem um ID de recurso Olá de `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="d6c43-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="d6c43-110">Definir a camada de acesso permitido</span><span class="sxs-lookup"><span data-stu-id="d6c43-110">Define permitted access tier</span></span>

<span data-ttu-id="d6c43-111">Olá política seguinte especifica Olá tipo de [camada de acesso](../storage/blobs/storage-blob-storage-tiers.md) que pode ser especificado para as contas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="d6c43-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="d6c43-112">Certifique-se de que a encriptação está ativada</span><span class="sxs-lookup"><span data-stu-id="d6c43-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="d6c43-113">Olá seguinte política requer que todos os tooenable de contas de armazenamento [encriptação do serviço de armazenamento](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="d6c43-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="d6c43-114">Esta regra de política também está disponível como uma definição de política incorporado com o ID de recurso Olá de `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="d6c43-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6c43-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d6c43-115">Next steps</span></span>
* <span data-ttu-id="d6c43-116">Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito.</span><span class="sxs-lookup"><span data-stu-id="d6c43-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="d6c43-117">âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="d6c43-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="d6c43-118">políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6c43-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="d6c43-119">políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="d6c43-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="d6c43-120">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d6c43-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

