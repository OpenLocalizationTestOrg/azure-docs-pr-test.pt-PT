---
title: "aaaManaging soluções de parceiros no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o Centro de segurança do Azure lhe permite monitorizar a um Estado de funcionamento de Olá rapidamente das suas soluções de parceiros integradas na sua subscrição do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Monitorizar soluções de parceiros com o Centro de Segurança do Azure
Este documento explica como como toomonitor Olá estado de funcionamento das suas soluções de parceiros no Centro de segurança do Azure.

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação. Este documento não é um guia passo a passo.
>
>

## <a name="monitoring-partner-solutions"></a>Monitorizar soluções de parceiros
Olá **soluções de parceiros** mosaico Olá **Centro de segurança** permite painel monitorizar um Estado de funcionamento de Olá rapidamente das suas soluções de parceiros estão integradas na sua subscrição do Azure.

![Mosaico Soluções de parceiros][1]

Olá **soluções de parceiros** mosaico mostra o número de Olá das soluções de parceiros integradas na sua subscrição. Se não existirem soluções integradas, o mosaico Olá mostra o número de Olá zero.

tooview Olá estado de funcionamento das suas soluções de parceiros:

1. Selecione Olá **soluções de parceiros** mosaico. Olá **soluções de parceiros** é aberto o painel a apresentar uma lista das suas soluções de parceiros ligadas tooSecurity Center.

   ![Soluções de parceiros][3]

   Estado de Olá de uma solução de parceiros pode ser:

   * Protegida (verde) – não existe nenhum problema de estado de funcionamento.
   * Mau estado de funcionamento (vermelho) – existe um problema de estado de funcionamento que exige atenção imediata.
   * Parado Reporting Services (cor de laranja) - solução Olá parou reporting o seu estado de funcionamento.
   * Estado de proteção desconhecido (cor de laranja) - Estado de funcionamento de Olá da solução de Olá é desconhecido neste momento devido a tooa falhada de processo de adicionar uma nova solução de toohello do recurso existente.
   * Não reportada (cinzento) – solução Olá tem ainda não, o estado de uma solução pode ser não reportado se recentemente foi ligada e ainda está a implementar.

2. Selecione uma solução de parceiros. Neste exemplo, permite que selecione Olá **Qualys** solução.  É aberto um painel que mostra o estado de Olá da solução de parceiros de Olá e uma solução de Olá recursos associados. Selecione **consola solução** experiência de gestão de parceiros de Olá tooopen para esta solução.

   ![Detalhe de solução de parceiros][4]
3. Voltar atrás toohello **Qualys** painel e selecione **ligação VM**. Olá **ligar aplicações** abre o painel. Aqui pode ligar-se a solução de parceiros de toohello de recursos.

   ![Ligação recursos toopartner solução][5]

## <a name="next-steps"></a>Passos seguintes
Neste documento, foram introduzida toohello **soluções de parceiros** mosaico no Centro de segurança. toolearn mais acerca do Centro de segurança, consulte Olá seguintes artigos:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) — Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) — Saiba como recomendações ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e respondeu.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — obter Olá mais recentes notícias de segurança do Azure e informações.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
