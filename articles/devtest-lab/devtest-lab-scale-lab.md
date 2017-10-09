---
title: "aaaScale quotas e limites no laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooscale um laboratório no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Quotas e limites de escala no DevTest Labs
À medida que trabalha no DevTest Labs, poderá reparar que existem determinada toosome de limites de predefinição recursos do Azure, o que podem afetar o serviço de DevTest Labs Olá. Estes limites são referidos tooas **quotas**.

> [!NOTE]
> Olá serviço DevTest Labs não impõe quaisquer quotas. Quaisquer quotas que podem surgir são restrições predefinidas de Olá subscrição global do Azure.

Pode utilizar cada recurso do Azure, até atingir a quota. Cada subscrição tem quotas separadas e utilização é controlada por subscrição.

Por exemplo, cada subscrição tem uma quota de predefinição de 20 núcleos. Por isso, se estiver a criar VMs no seu laboratório com quatro núcleos, em seguida, pode criar apenas cinco VMs. 

[Subscrição e limites de serviço da Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits) lista algumas das quotas mais comuns de Olá para recursos do Azure. Olá recursos normalmente utilizados num laboratório de e para que poderá encontrar quotas incluem núcleos VM, endereços IP públicos, interface de rede, discos geridos, atribuição de função RBAC e circuitos do ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Ver a sua utilização e quotas
Estes passos mostram como tooview Olá as quotas atuais na sua subscrição para recursos do Azure específicos e toosee que percentagem de cada quota que utilizou.

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **faturação** da lista de Olá.
1. No painel de faturação Olá, selecione uma subscrição.
4. Selecione **utilização + quotas**.

   ![Botão de utilização e quotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Olá utilização + quotas é apresentado o painel, listagem diferentes recursos disponíveis nessa percentagem de subscrição e Olá de quota de Olá que está a ser utilizado por recurso.

   ![Quotas e utilização](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Pedir mais recursos na sua subscrição
Se atingir um limite de quota, limite predefinido de Olá de um recurso de uma subscrição pode ser aumentado segurança limite máximo de tooa, conforme descrito em [subscrição do Azure e limites de serviço](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Estes passos mostram como toorequest uma quota aumentar através de Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**, selecione **faturação**e, em seguida, selecione **utilização + quotas**.
1. Na utilização de Olá + painel de quotas, selecione Olá **pedido aumentar** botão.

   ![Botão de aumento de pedido](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete e submeter pedido Olá, preencha as informações Olá necessário em todos os três separadores de Olá **novo pedido de suporte** formulário.

   ![Formulário de pedido de aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Noções sobre Azure limites e aumenta](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fornece mais informações sobre como contactar o suporte do Azure toorequest uma quota de aumento.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Passos seguintes
* Explorar Olá [Galeria de modelo de início rápido do DevTest Labs do Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
