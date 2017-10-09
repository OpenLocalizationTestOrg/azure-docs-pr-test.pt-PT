---
title: "integração de registo de alertas do Centro de segurança do Azure aaaIntegrating com o Azure | Microsoft Docs"
description: "Este artigo ajuda-o a começar a utilizar a integração de alertas do Centro de segurança com a integração de registos do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>A integração de alertas do Centro de segurança do Azure com a integração de registos do Azure
Muitas operações de segurança e as equipas de resposta a incidentes dependem de uma solução Security Information and Event Management (SIEM) como Olá ponto para a triagem e investigar alertas de segurança de partida. Com a integração de registo do Azure, pode integrar alertas do Centro de segurança do Azure com a sua solução do SIEM.

Integração de registos do Azure suporta atualmente HP ArcSight, Splunk e IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>Os registos que pode a integrar
Azure produz um vasto conjunto registo para cada serviço. Estes registos são categorizados como:

* **Registos de controlo/gestão** que dar visibilidade Olá operações do Azure Resource Manager criar, UPDATE e DELETE. Estes eventos de plane controlo estão anexados no Olá registos de atividade do Azure
* **Dados Plane registos** que dar visibilidade sobre os eventos de Olá gerados ao utilizar um recurso do Azure. Um exemplo é o registo de eventos do Windows hello, onde pode obter informações sobre eventos de segurança de canal de segurança do Visualizador de eventos Olá. Eventos de plane de dados (que foram gerados por uma máquina virtual ou um serviço do Azure) estão anexados por registos de diagnóstico do Azure.

Integração de registos do Azure suporta atualmente a integração de Olá de:

* Registos de VM do Azure
* Registos de auditoria do Azure
* Alertas do Centro de segurança do Azure

## <a name="install-azure-log-integration"></a>Instalar a integração de registos do Azure
Transferir [integração de registos do Azure](https://www.microsoft.com/download/details.aspx?id=53324).

Olá serviço de integração de registos do Azure recolhe dados telemétricos da máquina de Olá no qual está instalado.  Os dados telemétricos recolhidos são:

* Exceções que ocorrem durante a execução de integração de registos do Azure
* Métricas sobre Olá diversas consultas e eventos processados
* Estatísticas sobre qual Azlog.exe Opções da linha de comandos estão a ser utilizadas

> [!NOTE]
> Pode desativar a recolha de dados de telemetria desmarcando esta opção.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Integrar alertas do Centro de segurança e os registos de auditoria do Azure
1. Linha de comandos aberta Olá e **cd** para **c:\Program Files\Microsoft Azure registo integração**.
2. Executar Olá **azlog createazureid** comando toocreate um [Principal de serviço de diretório do Azure Active Directory](../active-directory/active-directory-application-objects.md) no Azure Active Directory (AD) de Olá inquilinos que alojam Olá subscrições do Azure.

    É-lhe pedido para o início de sessão do Azure.

   > [!NOTE]
   > Tem de ser subscrição Olá proprietário ou Coadministrador da subscrição Olá.
   >
   >

    Autenticação tooAzure é feito através do Azure AD.  Criar um principal de serviço para a integração de registos do Azure cria Olá do Azure AD identity que é dado acesso tooread de subscrições do Azure.
3. Executar Olá **azlog autorizar <SubscriptionID>**  comando acesso de leitor tooassign em Olá subscrição toohello principal do serviço criado no passo 2. Se não especificar um **SubscriptionID**, em seguida, o principal de serviço Olá é atribuído Olá leitor função tooall subscrições toowhich tem acesso.

   > [!NOTE]
   > Poderá ver avisos se executar Olá **autorizar** comando imediatamente após Olá **createazureid** comando. Não há alguma latência entre quando é criada a conta de Olá do Azure AD e quando a conta de Olá está disponível para utilização. Se Aguarde cerca de 10 segundos depois de executar Olá **createazureid** Olá do comando toorun **autorizar** comando, em seguida, a não deve ser apresentado estes avisos.
   >
   >
4. Verifique Olá seguir tooconfirm de pastas que Olá ficheiros de JSON do registo de auditoria existem:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Verifique Olá tooconfirm pastas alertas do Centro de segurança existentes nos mesmos os seguintes:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Configure Olá SIEM ficheiro reencaminhador conector toohello pasta adequados. procedimento Olá irão variar em Olá SIEM estiver a utilizar.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre os registos de atividade do Azure e definições de propriedades, consulte:

* [Auditar operações com o Resource Manager](../azure-resource-manager/resource-group-audit.md)

toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e respondeu.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — obter Olá mais recentes notícias de segurança do Azure e informações.
