---
title: "aaaGet iniciada com uma escala automática através da métrica personalizada no Azure | Microsoft Docs"
description: "Saiba como tooscale o recurso da métrica personalizada no Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Começar com uma escala automática da métrica personalizada no Azure
Este artigo descreve como tooscale seu recurso por uma métrica personalizada no portal do Azure.

Escala de automática de Monitor do Azure aplicam-se apenas tooVirtual conjuntos de dimensionamento de máquina (VMSS), cloud services, planos de serviço de aplicações e ambientes do app service. 

# <a name="lets-get-started"></a>Permite começar a utilizar
Este artigo pressupõe que tem uma aplicação web com o application insights configurados. Se ainda não tiver uma, pode [configurar o Application Insights para o seu Web site ASP.NET][1]

- Abra [portal do Azure][2]
- Clique no ícone de Monitor do Azure no painel de navegação esquerdo Olá.
  ![Iniciar o Monitor do Azure][3]
- Clique na definição tooview todos os recursos de Olá para que automaticamente a escala é aplicável, juntamente com o respetivo estado atual do dimensionamento automático de dimensionamento automático ![detetar escala automática no monitor do Azure][4]
- Abra o painel de 'dimensionamento automático' no Monitor do Azure e selecione um recurso pretende tooscale
> Nota: os passos de Olá abaixo utilizam um plano de serviço de aplicação associado uma aplicação web que tem informações de aplicação configuradas.
- No painel de definição de dimensionamento de Olá para o recurso de Olá, tenha em atenção que a contagem atual de instâncias de Olá é 1. Clique em 'Ativar dimensionamento automático'.
  ![Definição de dimensionamento para a nova aplicação web][5]
- Forneça um nome para a definição de dimensionamento de Olá e Olá, clique em "Adicionar uma regra". Tenha em atenção Olá escala opções da regra que abre-se como um painel de contexto Olá lado direito. Por predefinição, define Olá opção tooscale sua instância contagem por 1 se Olá CPU percetage do recurso de Olá exceder 70%. Origem de métrica de Olá de alteração na parte superior do Olá demasiado "Application Insights", selecione Olá app insights recurso Olá 'Resource' pendente e métrica personalizada, em seguida, selecione de Olá com base no qual pretende tooscale.
  ![Dimensionar por métrica personalizada][6]
- Semelhante passo toohello acima, adicione uma regra de escala que irá aumentar no e diminuir a contagem de escalas Olá por 1 se a métrica personalizada Olá está abaixo de um limiar.
  ![Escala com base na cpu][7]
- Definir Olá instância limites. Por exemplo, se quiser tooscale entre instâncias de 2 a 5 consoante flutuações de métrica personalizada Olá, definir 'mínima' demasiado '2', 'máximo' demasiado '5' e 'default' demasiado '2'
> Nota: no caso de existir um problema ao ler métricas de recurso Olá e capacidade atual da Olá é inferior a capacidade predefinida de Olá, em seguida, disponibilidade de Olá tooensure do recurso de Olá, dimensionamento automático irá aumentar horizontalmente valor predefinido de toohello. Se a capacidade atual da Olá já é superior à capacidade predefinida, o dimensionamento automático não será dimensionado no.
- Clique em 'Guardar'

Parabéns! Agora agora com êxito criado a sua tooauto de definição de dimensionamento dimensionamento da sua aplicação web com base numa métrica personalizada.

> Nota: Olá mesmos passos são aplicável tooget iniciada com uma função de serviço VMSS ou nuvem.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
