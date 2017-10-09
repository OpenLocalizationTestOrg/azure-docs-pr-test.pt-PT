---
title: "aaaEnable encriptação transparente de dados no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * ativar transparente dados encriptação * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Ativar a encriptação transparente de dados no Centro de segurança do Azure
Centro de segurança do Azure recomendará ativar encriptação de dados transparente (TDE) nas bases de dados do SQL Server se o TDE não estiver ativado. TDE protege os dados e ajuda a cumprir os requisitos de conformidade ao encriptar a sua base de dados, cópias de segurança associadas e os ficheiros de registo de transações inativos, sem necessidade de alterações tooyour aplicação. toolearn mais consulte [encriptação transparente de dados com a SQL Database do Azure](https://msdn.microsoft.com/library/dn948096).

Esta recomendação aplica-se toohello apenas; serviço do SQL do Azure não inclui o SQL Server em execução em máquinas virtuais.

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação.  Não se trata de um guia passo-a-passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá
1. No Olá **recomendações** painel, selecione **ativar a encriptação transparente de dados**.
   ![Ativar a Encriptação de Dados Transparente][1]
2. Esta ação abre Olá **ativar a encriptação de dados transparente em bases de dados do SQL Server** painel. Selecione um tooenable de base de dados do SQL Server TDE no.
   ![Selecione a base de dados SQL tooenable TDE no][2]
3. No Olá **encriptação transparente de dados** painel, selecione **ON** sob a encriptação de dados e selecione **guardar** no Friso de principais de Olá do painel de Olá.
   ![Ativar o TDE][3]

   Quando a TDE estiver ativada no Olá selecionado base de dados do SQL Server, hello **estado de encriptação** mudará demasiado**encriptado**.    

   ![Estado de encriptação][4]

## <a name="see-also"></a>Consultar também
Este artigo mostrou como tooimplement Olá recomendação do Centro de segurança "Ativar encriptação transparente de dados." toolearn mais informações sobre a SQL TDE, consulte o artigo seguinte Olá:

* [Encriptação transparente de dados com base de dados SQL do Azure](https://msdn.microsoft.com/library/dn948096)
* [Começar com encriptação de dados transparente (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) -obter Olá mais recentes notícias de segurança do Azure e informações.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
