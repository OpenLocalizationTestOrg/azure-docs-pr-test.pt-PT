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
# <a name="apply-resource-policies-toostorage-accounts"></a>Aplicar a contas de toostorage de políticas de recursos
Este tópico mostra várias [as políticas de recursos](resource-manager-policy.md) pode aplicar tooAzure contas de armazenamento. Estas políticas garantir consistência Olá contas do storage implementada na sua organização. 

## <a name="define-permitted-storage-account-types"></a>Definir os tipos de conta de armazenamento permitido

Olá seguinte política restringe o que [tipos de conta de armazenamento](../storage/common/storage-redundancy.md) pode ser implementado:

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

Uma regra de política semelhantes com um parâmetro para aceitar Olá permitido SKUs está disponível como uma definição de política incorporada. política incorporada Olá possuem um ID de recurso Olá de `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Definir a camada de acesso permitido

Olá política seguinte especifica Olá tipo de [camada de acesso](../storage/blobs/storage-blob-storage-tiers.md) que pode ser especificado para as contas de armazenamento:

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

## <a name="ensure-encryption-is-enabled"></a>Certifique-se de que a encriptação está ativada

Olá seguinte política requer que todos os tooenable de contas de armazenamento [encriptação do serviço de armazenamento](../storage/common/storage-service-encryption.md):

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

Esta regra de política também está disponível como uma definição de política incorporado com o ID de recurso Olá de `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Passos seguintes
* Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito. âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso. políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](resource-manager-policy-create-assign.md). 
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

