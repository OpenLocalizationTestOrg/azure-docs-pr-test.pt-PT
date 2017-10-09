---
title: "escala de aaaAutomatically unidades de débito de Event Hubs do Azure | Microsoft Docs"
description: "Ativar automaticamente-inflate numa escala tooautomatically espaço de nomes unidades de débito"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="9b110-103">Dimensionar automaticamente unidades de débito de Event Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="9b110-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="9b110-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="9b110-104">Overview</span></span>

<span data-ttu-id="9b110-105">Os Hubs de eventos do Azure é uma plataforma de transmissão em fluxo de dados altamente dimensionáveis.</span><span class="sxs-lookup"><span data-stu-id="9b110-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="9b110-106">Como tal, os clientes de Event Hubs, muitas vezes, aumentam a respetiva utilização após integração toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="9b110-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="9b110-107">Essa aumenta requerem crescente Olá predetermined débito unidades (TUs) tooscale Event Hubs e processar taxas de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="9b110-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="9b110-108">Olá *Auto-inflate* funcionalidade dos Event Hubs automaticamente ajusta-se o número de Olá de necessidades de utilização de toomeet TUs.</span><span class="sxs-lookup"><span data-stu-id="9b110-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="9b110-109">Aumentar TUs impede cenários, na qual a limitação:</span><span class="sxs-lookup"><span data-stu-id="9b110-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="9b110-110">Entrada de dados excedem as taxas de definir TUs.</span><span class="sxs-lookup"><span data-stu-id="9b110-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="9b110-111">Pedido de saída de dados excedem as taxas de definir TUs.</span><span class="sxs-lookup"><span data-stu-id="9b110-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="9b110-112">Como funciona o inflate de automática</span><span class="sxs-lookup"><span data-stu-id="9b110-112">How Auto-inflate works</span></span>

<span data-ttu-id="9b110-113">Tráfego de Hubs de eventos é controlado pelas unidades de débito.</span><span class="sxs-lookup"><span data-stu-id="9b110-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="9b110-114">Um único TU permite 1 MB por segundo de entrada e de duas vezes que quantidade de saída.</span><span class="sxs-lookup"><span data-stu-id="9b110-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="9b110-115">Hubs de eventos Standard pode ser configurados com 1-20 unidades de débito.</span><span class="sxs-lookup"><span data-stu-id="9b110-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="9b110-116">Auto-inflate permite-lhe toostart pequeno com unidades de débito necessário mínimo Olá.</span><span class="sxs-lookup"><span data-stu-id="9b110-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="9b110-117">funcionalidade de Olá dimensiona, em seguida, automaticamente toohello limite máximo de unidades de débito que precisa, consoante Olá aumento no tráfego.</span><span class="sxs-lookup"><span data-stu-id="9b110-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="9b110-118">Auto-inflate fornece Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="9b110-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="9b110-119">Um toostart de mecanismo dimensionamento eficiente pequeno e o trabalho de dimensionamento como aumentar.</span><span class="sxs-lookup"><span data-stu-id="9b110-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="9b110-120">Dimensione o limite superior especificado toohello sem problemas de limitação.</span><span class="sxs-lookup"><span data-stu-id="9b110-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="9b110-121">Mais controlam sobre o dimensionamento, como pode controlar quando e quantidade tooscale.</span><span class="sxs-lookup"><span data-stu-id="9b110-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="9b110-122">Ativar o inflate de automaticamente um espaço de nomes</span><span class="sxs-lookup"><span data-stu-id="9b110-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="9b110-123">Pode ativar ou desativar a inflate de automática de mensagens em fila um espaço de nomes utilizando um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="9b110-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="9b110-124">Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b110-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b110-125">Um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b110-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="9b110-126">Ativar automaticamente-inflate através do portal Olá</span><span class="sxs-lookup"><span data-stu-id="9b110-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="9b110-127">Pode ativar Olá Auto-inflate funcionalidade num espaço de nomes ao criar um espaço de nomes de Hubs de eventos:</span><span class="sxs-lookup"><span data-stu-id="9b110-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="9b110-128">Com esta opção ativada, pode começar por algo pequeno nas suas unidades de débito e dimensione à medida que a utilização da necessidades aumento.</span><span class="sxs-lookup"><span data-stu-id="9b110-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="9b110-129">Olá limite superior para inflation não afeta os preços, que depende do número de Olá de TUs utilizada por hora.</span><span class="sxs-lookup"><span data-stu-id="9b110-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="9b110-130">Também pode ativar Auto-inflate utilizando Olá **escala** opção no painel de definições de Olá no portal de Olá:</span><span class="sxs-lookup"><span data-stu-id="9b110-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="9b110-131">Ativar Inflate automático utilizando um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b110-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="9b110-132">Pode ativar inflate de automática durante uma implementação de modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b110-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="9b110-133">Por exemplo, o conjunto Olá `isAutoInflateEnabled` propriedade demasiado**verdadeiro** e defina `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="9b110-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="9b110-134">Para o modelo completo Olá, consulte Olá [criar Hubs de eventos espaço de nomes e ativar inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modelo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="9b110-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b110-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9b110-135">Next steps</span></span>

<span data-ttu-id="9b110-136">Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="9b110-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="9b110-137">Descrição geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="9b110-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9b110-138">Criar um Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="9b110-138">Create an Event Hub</span></span>](event-hubs-create.md)
