---
title: "aaaEnable auditoria e deteção de ameaças em SQL servers no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * deteção de ameaças e ativar a auditoria em servidores SQL *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Ativar a auditoria e deteção de ameaças em SQL servers no Centro de segurança do Azure
Centro de segurança do Azure recomendará que ativar a auditoria e deteção de ameaças para todas as bases de dados em servidores SQL do Azure se auditoria já não está ativada. Auditoria e ameaças deteção pode ajudar a manter a conformidade de regulamentação, compreender a atividade de base de dados e obter informações sobre discrepâncias e anomalias que poderão indicar preocupações para a empresa ou suspeitas de violação de segurança.

Uma vez que ativou a auditoria, pode configurar a deteção de ameaças definições e os e-mails tooreceive alertas de segurança. A deteção de ameaças Deteta atividades de base de dados anómalas, indicando potenciais segurança ameaças toohello base de dados do. Isto permite-lhe toodetect e responder a ameaças toopotential à medida que ocorrem.

Esta recomendação aplica-se toohello apenas; serviço do SQL do Azure não inclui o SQL Server em execução em máquinas virtuais nos serviços de infraestrutura do Azure (IaaS do Azure).

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação.  Não se trata de um guia passo-a-passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá
1. No Olá **recomendações** painel, selecione **deteção de ameaças e ativar a auditoria em servidores SQL**.  Esta ação abre Olá **deteção de ameaças e ativar a auditoria em servidores SQL** painel.

   ![Ativar a auditoria em servidores SQL][1]
2. Selecione uma SQL server tooenable auditoria e deteção de ameaças no. Esta ação abre Olá **a deteção de ameaças e auditoria** painel.

3. No Olá **a deteção de ameaças e auditoria** painel, selecione **ON** em **auditoria**.

   ![Ativar definições de auditoria][2]
4. Siga os passos Olá [Olá, a auditoria de base de dados SQL no portal do Azure](../sql-database/sql-database-auditing-portal.md) armazenamento tooconfigure onde serão armazenados os registos de auditoria. Olá conta de armazenamento da subscrição para recolha de dados é conta do storage predefinida Olá.
5. Siga os passos Olá [começar com deteção de ameaças de base de dados do SQL Server](../sql-database/sql-database-threat-detection.md) tooturn no e configurar a deteção de ameaças e a lista de Olá tooconfigure de e-mails que vão receber alertas de segurança mediante a deteção de atividades anómalas.

## <a name="see-also"></a>Consultar também
Este artigo mostrou como tooimplement Olá recomendação do Centro de segurança "Ativar a auditoria e Deteção em SQL servers de ameaças." toolearn mais informações sobre a proteger a sua base de dados do SQL Server, consulte o artigo seguinte Olá:

* [Securing your SQL Database (Proteger a sua Base de Dados SQL)](../sql-database/sql-database-security-overview.md)

toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) -obter Olá mais recentes notícias de segurança do Azure e informações.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
