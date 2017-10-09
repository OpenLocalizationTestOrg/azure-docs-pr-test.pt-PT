---
title: "recomendações de custo de Advisor aaaAzure | Microsoft Docs"
description: "Utilize o custo de Olá toooptimize Azure Advisor das implementações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Recomendações de custo do Assistente

Ajuda-o Advisor otimizar e reduzir o Azure geral passam por identificar recursos inativos e subutilizados. Pode obter custo recomendações da Olá **custo** separador no dashboard do Olá do Advisor.

![Separador de custo do Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Otimizar a máquina virtual passam por redimensionamento subutilizadas instâncias 
Apesar de determinados cenários de aplicação podem resultar numa utilização baixa por predefinição, muitas vezes, pode poupar dinheiro ao gerir tamanho Olá e o número de máquinas virtuais. Advisor monitoriza a utilização da máquina virtual nos últimos 14 dias e, em seguida, identifica as máquinas virtuais de baixa utilização. Máquinas virtuais cuja utilização do CPU é 5 porcento ou menos e utilização de rede é 7 MB ou menos, de quatro ou mais dias são considerados máquinas de virtuais baixa utilização.

Apresenta o Advisor Olá custo estimado continuar toorun a máquina virtual, para que possa escolher tooshut-pendente ou redimensioná-la.  

![Advisor custo recomendações para redimensionar máquinas virtuais](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Utilizar uma solução económica toomanage desempenho objetivos várias bases de dados do SQL Server
Advisor identifica as instâncias do SQL Server que podem beneficiar do criar conjuntos de bases de dados elásticas. Conjuntos de bases de dados elásticas fornecem uma solução simples e rentável toomanage objetivos de desempenho de Olá de várias bases de dados que tenham diferentes padrões de utilização. Para obter mais informações sobre conjuntos elásticos do Azure, consulte [o que é um conjunto elástico do Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Advisor custo recomendações para conjuntos de bases de dados elásticas](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Como tooaccess custo recomendações no Azure Advisor

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).

2. No painel esquerdo Olá, clique em **mais serviços**.

3. Olá serviço em Painel de menu, **monitorização e gestão**, clique em **Azure Advisor**.  
 dashboard de Advisor Olá é apresentado.

4. No dashboard do Advisor Olá, clique em Olá **custo** separador.

5. Selecione a subscrição Olá para o qual pretende tooreceive recomendações e, em seguida, clique em **obter recomendações**.

> [!NOTE]
> tooaccess recomendações do assistente, tem primeiro *registar a sua subscrição* com o Advisor. Uma subscrição é registada quando um *subscrição proprietário* inicia Olá Olá de dashboard e os cliques em Advisor **obter recomendações** botão. Este é um *operação única*. Depois de subscrição de Olá está registada, pode aceder recomendações do assistente como *proprietário*, *contribuinte*, ou *leitor* para uma subscrição, um grupo de recursos, ou um recurso específico.

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre as recomendações do Advisor, consulte:
* [Introdução tooAdvisor](advisor-overview.md)
* [Introdução](advisor-get-started.md)
* [Recomendações de desempenho do Assistente](advisor-cost-recommendations.md)
* [Recomendações de elevada disponibilidade do Assistente](advisor-cost-recommendations.md)
* [Recomendações de segurança do Advisor](advisor-cost-recommendations.md)
