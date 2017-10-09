---
title: "atualizações do sistema aaaApply no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá as recomendações do Centro de segurança do Azure * * aplicar sistema atualizações * * e * * reinício após atualizações do sistema *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Aplicar atualizações do sistema no Centro de segurança do Azure
Centro de segurança do Azure diariamente monitoriza Windows e Linux as máquinas virtuais (VMs) em falta atualizações do sistema operativo. Centro de segurança obtém uma lista de atualizações críticas e de segurança disponíveis do Windows Update ou Windows Server Update Services (WSUS), dependendo de que o serviço está configurado numa VM do Windows.  Centro de segurança também verifica a existência de atualizações mais recentes Olá nos sistemas Linux. Se a VM está em falta uma atualização do sistema, o Centro de segurança recomendará que aplique a atualizações do sistema

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação.  Não se trata de um guia passo-a-passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá
1. No Olá **recomendações** painel, selecione **aplicar atualizações do sistema**.

   ![Aplicar atualizações do Sistema][1]
2. Olá **aplicar atualizações do sistema** painel abre-apresentar uma lista de VMs em falta atualizações do sistema. Selecione uma VM.

   ![Selecione uma VM][2]
3. É aberto um painel a apresentar uma lista de atualizações em falta para essa VM. Selecione uma atualização do sistema. Neste exemplo, vamos selecione KB3156016.

   ![Atualizações de segurança em falta][3]

4. Siga os passos de Olá Olá **de atualizações de segurança** painel tooapply Olá atualização em falta.

   ![Atualização de segurança][4]

## <a name="reboot-after-system-updates"></a>Reiniciar após atualizações do sistema
1. Devolver toohello **recomendações** painel. Uma nova entrada foi gerada depois de aplicar atualizações do sistema, denominadas **reinício após atualizações do sistema**. Esta entrada permite-lhe saber que precisa de processo do tooreboot Olá VM toocomplete Olá de aplicar atualizações do sistema.

   ![Reiniciar após atualizações do sistema][5]
2. Selecione **reinício após atualizações do sistema**. Esta ação abre **é de um reinício pendente toocomplete atualizações do sistema** painel a apresentar uma lista de VMs que precisa de toorestart toocomplete Olá aplicam-se o processo de atualizações do sistema.

   ![Reinício pendente][6]

Reinicie Olá VM do processo de Olá toocomplete do Azure.

## <a name="see-also"></a>Consultar também
toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre mensagens do Blogue acerca da segurança do Azure e conformidade.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
