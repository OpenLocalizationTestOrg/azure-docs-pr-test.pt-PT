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
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a><span data-ttu-id="8193c-103">Aplicar políticas tooLinux VMs com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8193c-103">Apply policies tooLinux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="8193c-104">Ao utilizar políticas, uma organização pode aplicar vários convenções e regras em toda a empresa de Olá.</span><span class="sxs-lookup"><span data-stu-id="8193c-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="8193c-105">Imposição de comportamento Olá pretendido pode ajudar a mitigar o risco ao contribuir toohello êxito da organização Olá.</span><span class="sxs-lookup"><span data-stu-id="8193c-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="8193c-106">Neste artigo, vamos descrever como pode utilizar o comportamento do Azure Resource Manager políticas toodefine Olá pretendido para máquinas virtuais da sua organização.</span><span class="sxs-lookup"><span data-stu-id="8193c-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="8193c-107">Para um toopolicies de introdução, consulte [recursos toomanage de política de uso e controlar o acesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8193c-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="8193c-108">Máquinas virtuais permitidos</span><span class="sxs-lookup"><span data-stu-id="8193c-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="8193c-109">tooensure que as máquinas virtuais para a sua organização são compatíveis com uma aplicação, pode restringir Olá permitido sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="8193c-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="8193c-110">No seguinte exemplo de política de Olá, permitir apenas Ubuntu 14.04.2-LTS as máquinas virtuais toobe criado.</span><span class="sxs-lookup"><span data-stu-id="8193c-110">In hello following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines toobe created.</span></span>

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

<span data-ttu-id="8193c-111">Utilize um Olá toomodify de caráter universal precedente política tooallow qualquer imagem Ubuntu LTS:</span><span class="sxs-lookup"><span data-stu-id="8193c-111">Use a wild card toomodify hello preceding policy tooallow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="8193c-112">Para obter informações sobre campos da política, consulte [aliases de política](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="8193c-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="8193c-113">Managed disks</span><span class="sxs-lookup"><span data-stu-id="8193c-113">Managed disks</span></span>

<span data-ttu-id="8193c-114">toorequire Olá utilização de discos geridos, Olá utilize seguinte política:</span><span class="sxs-lookup"><span data-stu-id="8193c-114">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="8193c-115">Imagens de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8193c-115">Images for Virtual Machines</span></span>

<span data-ttu-id="8193c-116">Por motivos de segurança, pode exigir que apenas imagens personalizadas aprovadas são implementadas no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8193c-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="8193c-117">Pode especificar o grupo de recursos de Olá que contém imagens de Olá aprovado ou imagens aprovadas específico de Olá.</span><span class="sxs-lookup"><span data-stu-id="8193c-117">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="8193c-118">Olá seguinte o exemplo requer imagens a partir de um grupo de recursos aprovados:</span><span class="sxs-lookup"><span data-stu-id="8193c-118">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="8193c-119">Olá seguinte exemplo Especifica Olá aprovado imagem IDs:</span><span class="sxs-lookup"><span data-stu-id="8193c-119">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="8193c-120">Extensões de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8193c-120">Virtual Machine extensions</span></span>

<span data-ttu-id="8193c-121">Poderá pretender tooforbid utilização de determinados tipos de extensões.</span><span class="sxs-lookup"><span data-stu-id="8193c-121">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="8193c-122">Por exemplo, uma extensão não pode ser compatível com determinadas imagens de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="8193c-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="8193c-123">Olá seguinte exemplo mostra como tooblock uma extensão específica.</span><span class="sxs-lookup"><span data-stu-id="8193c-123">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="8193c-124">Utiliza toodetermine publicador e o tipo que tooblock de extensão.</span><span class="sxs-lookup"><span data-stu-id="8193c-124">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="8193c-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8193c-125">Next steps</span></span>
* <span data-ttu-id="8193c-126">Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito.</span><span class="sxs-lookup"><span data-stu-id="8193c-126">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="8193c-127">âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="8193c-127">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="8193c-128">políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8193c-128">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="8193c-129">políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="8193c-129">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="8193c-130">Para políticas de tooresource uma introdução, consulte [descrição geral da política de recurso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8193c-130">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="8193c-131">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="8193c-131">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
