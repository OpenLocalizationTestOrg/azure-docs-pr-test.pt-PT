---
title: "aaaAzure integração de registo com os registos de auditoria do Azure Active Directory | Microsoft Docs"
description: "Saiba como tooinstall Olá o serviço de integração de registo do Azure e integrar os registos de registos de auditoria do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Integrar os registos de auditoria do Azure Active Directory

Eventos de auditoria do Azure Active Directory (Azure AD) ajudam a identificar ações privilegiadas ocorridas no Azure Active Directory. Pode ver os tipos de Olá dos eventos que pode controlar revendo [eventos de relatório de auditoria do Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Antes de tentar passos Olá neste artigo, tem de consultar Olá [começar](security-azure-log-integration-get-started.md) artigo e executar passos de Olá não existe.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Registos de auditoria do Azure Active directory do passos toointegrate

1. Abra a linha de comandos Olá e execute este comando:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Execute este comando: 
 
   ``azlog createazureid``

   Este comando pede-lhe o início de sessão do Azure. Olá comando, em seguida, cria um Azure Active Directory principal de serviço no inquilinos Olá do Azure AD que alojam Olá subscrições do Azure na qual Olá utilizador com sessão iniciada é um administrador, coadministrador ou a um proprietário. comando Olá irá falhar se o utilizador com sessão iniciada Olá é apenas um utilizador convidado no inquilino do Azure AD Olá. Autenticação tooAzure é feito através do Azure AD. Criar um principal de serviço para a integração de registo do Azure cria Olá identidade do Azure AD, que é dado acesso tooread de subscrições do Azure.

3. Executar Olá tooprovide de comando a seguir o ID do inquilino. Terá de membro de toobe do comando de Olá de toorun de função Administrador inquilino Olá.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Exemplo:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Verifique Olá seguir tooconfirm de pastas que Olá os ficheiros do JSON de registo de auditoria do Azure Active Directory é criado nos mesmos:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Olá vídeo seguinte demonstra os passos de Olá abordados neste artigo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Para obter instruções específicas sobre colocar informações de Olá nos ficheiros JSON Olá ao seu informações de segurança e o sistema de gestão (SIEM) de eventos, contacte o fabricante do SIEM.

A assistência de Comunidade está disponível através de Olá [fórum MSDN do Azure registo integração](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Neste fórum permite que as pessoas da Olá a integração de registo do Azure da Comunidade toosupport entre si com perguntas, respostas, sugestões e truques. Além disso, a equipa de integração de registo do Azure Olá monitoriza neste fórum e ajuda a sempre que possível.

Também pode abrir um [pedido de suporte](../azure-supportability/how-to-create-azure-support-request.md). Selecione **integração de registo** como serviço Olá para o qual está a pedir suporte.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a integração de registo do Azure, consulte:

* [Integração de registo do Microsoft Azure para os registos do Azure](https://www.microsoft.com/download/details.aspx?id=53324): página do Centro de transferências este fornece detalhes, requisitos de sistema e as instruções de instalação para a integração de registo do Azure.
* [Introdução tooAzure integração de registo](security-azure-log-integration-overview.md): Este artigo apresenta tooAzure integração de registo, as suas capacidades principais e como funciona.
* [Passos de configuração do parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): Este blogue mostra-lhe como tooconfigure toowork de integração de registo do Azure com parceiros soluções Splunk, HP ArcSight e IBM QRadar.
* [FAQ sobre integração do registo do Azure](security-azure-log-integration-faq.md): Este artigo responde a questões sobre a integração de registo do Azure.
* [Integração de alertas do Centro de segurança com a integração de registo do Azure](../security-center/security-center-integrating-alerts-with-log-integration.md): Este artigo mostra como alertas do Centro de segurança toosync, juntamente com eventos de segurança de máquina virtual recolhidos por diagnósticos do Azure e os registos de auditoria do Azure, com a análise de registos ou Solução do SIEM.
* [Registos de auditoria de novas funcionalidades de diagnóstico do Azure e Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta mensagem de blogue apresenta os registos de auditoria tooAzure e outras funcionalidades que o ajudam a obterem informações sobre nas operações de Olá dos seus recursos Azure.
