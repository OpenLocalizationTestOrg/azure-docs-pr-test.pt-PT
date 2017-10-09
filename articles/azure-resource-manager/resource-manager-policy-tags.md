---
title: "as políticas de recursos de aaaAzure para etiquetas | Microsoft Docs"
description: "Fornece exemplos de políticas de recursos para gerir etiquetas de recursos"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Aplicar políticas de recursos de etiquetas

Este tópico fornece as regras de política comum que pode aplicar a utilização consistente tooensure etiquetas nos recursos.

Aplicar um grupo de recursos de tooa de política de etiqueta ou uma subscrição com os recursos existentes não retroactively aplicam-se recursos de toothose Olá política. políticas de Olá tooenforce esses recursos, acionar um toohello de atualização existente recursos. Este artigo inclui um exemplo do PowerShell para acionar uma atualização.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Certifique-se de que todos os recursos num grupo de recursos tem um tag/valor

Um requisito comum é que todos os recursos num grupo de recursos tem uma tag específica e o valor. Este requisito é frequentemente necessário tootrack custos pelo departamento. Olá seguintes condições deve ser cumprido:

* Olá necessário etiqueta valor são toonew anexado e atualizar recursos que não tem tag de Olá.
* Olá necessário tag e valor não é possível remover quaisquer recursos existentes.

Concretizar este requisito aplicando o grupo de recursos de tooa do duas políticas incorporadas.

| ID | Descrição |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Aplica-se uma tag necessária e o respetivo valor predefinido se não for especificada pelo utilizador Olá. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Impõe uma tag necessária e o respetivo valor. |

### <a name="powershell"></a>PowerShell

Olá seguinte script do PowerShell atribui o grupo de recursos do Olá política incorporada duas definições tooa. Antes de executar o script de Olá, atribua o grupo de recursos toohello etiquetas necessárias de todos os. Cada etiqueta no grupo de recursos de Olá é necessária para os recursos de Olá no grupo de Olá. grupos de recursos de tooall tooassign na sua subscrição, não fornecem Olá `-Name` parâmetro ao obter grupos de recursos de Olá.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Depois de atribuir políticas de Olá, pode acionar um tooall de atualização existente recursos tooenforce Olá tag as políticas que adicionou. Olá seguinte script mantém outras etiquetas que existiam recursos Olá:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Exigir etiquetas para um tipo de recurso
Olá seguinte exemplo mostra como toonest operadores lógicos toorequire uma aplicação tag para apenas um tipo de recurso especificado (neste caso, contas de armazenamento).

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Exigir etiqueta
Olá política seguinte nega pedidos que não tenham uma etiqueta que contém a chave "costCenter" (pode ser aplicada a qualquer valor):

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Passos seguintes
* Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito. âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso. políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](resource-manager-policy-create-assign.md).
* Para políticas de tooresource uma introdução, consulte [descrição geral da política de recurso](resource-manager-policy.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

