---
title: "as políticas de recursos de aaaAzure para as convenções de nomenclatura | Microsoft Docs"
description: "Descreve as políticas do Azure Resource Manager para as convenções de nomenclatura de recursos."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Aplicar políticas de recursos de nomes e texto
Este tópico mostra várias [as políticas de recursos](resource-manager-policy.md) pode aplicar tooestablish convenções de atribuição de nomes e texto. Estas políticas garantir consistência para os nomes de recursos e valores de etiqueta. 

## <a name="set-naming-convention-with-wildcard"></a>Definir a Convenção de nomenclatura com carateres universais
Olá exemplo seguinte mostra Olá utilização do caráter universal, que é suportado pelo Olá **como** condição. Olá condição Estados que se hello nome corresponde ao padrão mencionadas Olá (namePrefix\*nameSuffix) negar o pedido de Olá:

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Definir a Convenção de nomenclatura com o padrão

toospecify que os nomes de recursos correspondem um padrão, utilize Olá correspondem à condição. Olá seguinte exemplo requer nomes toostart com `contoso` e conter seis letras adicionais:

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Padrão de data de conjunto para o valor da etiqueta

toorequire um padrão de data de dois dígitos, traço, três letras, dash e quatro dígitos, utilize:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Passos seguintes
* Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito. âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso. políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](resource-manager-policy-create-assign.md). 
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

