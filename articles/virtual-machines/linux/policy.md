---
title: "segurança aaaEnforce com as políticas em VMs do Linux no Azure | Microsoft Docs"
description: "Como tooapply tooan uma política do Azure Resource Manager máquina de Virtual com Linux"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>Aplicar políticas tooLinux VMs com o Azure Resource Manager
Ao utilizar políticas, uma organização pode aplicar vários convenções e regras em toda a empresa de Olá. Imposição de comportamento Olá pretendido pode ajudar a mitigar o risco ao contribuir toohello êxito da organização Olá. Neste artigo, vamos descrever como pode utilizar o comportamento do Azure Resource Manager políticas toodefine Olá pretendido para máquinas virtuais da sua organização.

Para um toopolicies de introdução, consulte [recursos toomanage de política de uso e controlar o acesso](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Máquinas virtuais permitidos
tooensure que as máquinas virtuais para a sua organização são compatíveis com uma aplicação, pode restringir Olá permitido sistemas operativos. No seguinte exemplo de política de Olá, permitir apenas Ubuntu 14.04.2-LTS as máquinas virtuais toobe criado.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

Utilize um Olá toomodify de caráter universal precedente política tooallow qualquer imagem Ubuntu LTS: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

Para obter informações sobre campos da política, consulte [aliases de política](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Managed disks

toorequire Olá utilização de discos geridos, Olá utilize seguinte política:

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>Imagens de máquinas virtuais

Por motivos de segurança, pode exigir que apenas imagens personalizadas aprovadas são implementadas no seu ambiente. Pode especificar o grupo de recursos de Olá que contém imagens de Olá aprovado ou imagens aprovadas específico de Olá.

Olá seguinte o exemplo requer imagens a partir de um grupo de recursos aprovados:

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

Olá seguinte exemplo Especifica Olá aprovado imagem IDs:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Extensões de máquina virtual

Poderá pretender tooforbid utilização de determinados tipos de extensões. Por exemplo, uma extensão não pode ser compatível com determinadas imagens de máquina virtual personalizada. Olá seguinte exemplo mostra como tooblock uma extensão específica. Utiliza toodetermine publicador e o tipo que tooblock de extensão.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a>Passos seguintes
* Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito. âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso. políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md). políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Para políticas de tooresource uma introdução, consulte [descrição geral da política de recurso](../../azure-resource-manager/resource-manager-policy.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](../../azure-resource-manager/resource-manager-subscription-governance.md).
