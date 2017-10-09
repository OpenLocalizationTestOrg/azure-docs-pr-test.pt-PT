---
title: "alertas de estado de funcionamento do aaaResolve endpoint protection no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * Endpoint Protection resolver o estado de funcionamento alertas * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Resolver alertas de estado de funcionamento do endpoint protection no Centro de segurança do Azure
Centro de segurança do Azure recomendará que resolver alertas de estado de funcionamento de proteção de ponto final detetado.  Centro de segurança permite-lhe toosee que máquinas virtuais (VMs) ter falhas do endpoint protection e o número de falhas.

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação. Não se trata de um guia passo-a-passo.
> 
> 

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá
1. No Olá **painel recomendações**, selecione **alertas de estado de funcionamento do Endpoint Protection resolver**.
   ![Resolver alertas de estado de funcionamento do endpoint protection][1]
2. Esta ação abre o painel de Olá **falha de Endpoint Protection** que apresenta uma lista de VMs com falhas e número de Olá de falhas para cada VM. Selecione uma VM Olá lista.
   ![Falha de proteção de ponto final][2]
3. A **lista de falhas** painel abre para Olá selecionado VM, que apresenta uma lista de falhas. Selecione uma falha de Olá lista toolearn mais. Esta ação abre um painel com informações sobre a falha de Olá selecionado.
   ![Lista de falhas][3]
   ![eventos de falha][4]

## <a name="see-also"></a>Consultar também
toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md)– Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de Segurança do Azure](security-center-recommendations.md) – Saiba como as recomendações o ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md)– encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)-obter Olá mais recentes notícias de segurança do Azure e informações.

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
