---
title: "aaaAzure integração de registo com o Centro de segurança | Microsoft Docs"
description: "Saiba como trabalhar com a integração do registo de alertas do Centro de tooget segurança do Azure"
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
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Como tooget seu centro de segurança alertas na integração de registos do Azure
Este artigo fornece Olá passos necessários tooenable Olá a integração de registo do Azure service toopull alerta de segurança informações geradas pelo centro de segurança do Azure. Tem concluiu com êxito os passos de Olá Olá [começar](security-azure-log-integration-get-started.md) artigo antes de efetuar os passos de Olá neste artigo.

## <a name="detailed-steps"></a>Passos detalhados
Olá passos seguintes irão criar Olá necessário Principal de serviço de diretório do Azure Active Directory e permissões de leitura de atribuir Olá princípio de serviço, toohello subscrição:
1. Abra a linha de comandos Olá e navegue demasiado**c:\Program Files\Microsoft Azure registo integração**
2. Execute o comando de Olá``azlog createazureid``

    Este comando pede-lhe o início de sessão do Azure. comando de Olá, em seguida, cria um [Principal de serviço de diretório do Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) no Olá inquilinos do Azure do AD que alojam Olá subscrições do Azure na qual Olá a sessão de utilizador é um administrador, Coadministrador ou um proprietário. comando Olá falhará se Olá a sessão de utilizador é apenas um utilizador convidado na Olá inquilino do Azure AD. Autenticação tooAzure é feito através do Azure Active Directory (AD). Criar um principal de serviço para a integração de Azlog cria Olá identidade do Azure AD que irão ser-lhe concedida acesso tooread de subscrições do Azure.

2. Em seguida, executar um comando que atribui acesso de leitor na Olá subscrição toohello principal do serviço criado no passo 2. Se não especificar um ID de subscrição, o comando Olá tentará tooassign Olá serviço principal leitor função tooall subscrições toowhich tem qualquer acesso. </br></br>
``azlog authorize <SubscriptionID>`` </br> Por exemplo </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Poderá ver avisos se executar Olá autorizar comando imediatamente após o comando de createazureid Olá. Não há alguma latência entre quando é criada a conta de Olá do Azure AD e quando a conta de Olá está disponível para utilização. Se Aguarde 60 segundos depois de executar Olá do Olá createazureid comando toorun autorizar comando, em seguida, não deve ser apresentado estes avisos.

4. Verifique Olá seguir tooconfirm de pastas que Olá ficheiros de JSON do registo de auditoria existem:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Verifique Olá tooconfirm pastas alertas do Centro de segurança existentes nos mesmos os seguintes:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Caso se depare com problemas durante a instalação de Olá e a configuração, abra uma [pedido de suporte](/azure-supportability/how-to-create-azure-support-request.md), selecione **integração de registo** como serviço Olá para o qual está a pedir suporte.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a integração de registo do Azure, consulte Olá seguintes documentos:

* [Integração de registo do Microsoft Azure para os registos do Azure](https://www.microsoft.com/download/details.aspx?id=53324) – Centro de transferências para obter detalhes, requisitos de sistema e instalar as instruções na integração de registos do Azure.
* [Integração de registo de tooAzure introdução](security-azure-log-integration-overview.md) – este documento apresenta tooAzure integração de registo, as suas capacidades principais e como funciona.
* [Passos de configuração do parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – este blogue mostra-lhe como tooconfigure Azure registo toowork de integração com soluções de parceiros Splunk, HP ArcSight e IBM QRadar.
* [Registos do Azure integração perguntas mais frequentes (FAQ) do sobre](security-azure-log-integration-faq.md) -FAQ este respondem a dúvidas sobre a integração de registos do Azure.
* [Integrar o Centro de segurança de alertas com o Azure registo integração](../security-center/security-center-integrating-alerts-with-log-integration.md) – este documento mostra como alertas do Centro de segurança toosync, juntamente com eventos de segurança de máquina virtual recolhidos pelo diagnósticos do Azure e os registos de auditoria do Azure, com a sua análise de registos ou Solução do SIEM.
* [Novas funcionalidades de diagnóstico do Azure e os registos de auditoria do Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – esta mensagem de blogue apresenta os registos de auditoria tooAzure e outras funcionalidades que o ajudam a obterem informações acerca da operações Olá dos seus recursos Azure.
