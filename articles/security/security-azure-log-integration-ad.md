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
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3cee9-103">Integrar os registos de auditoria do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cee9-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="3cee9-104">Eventos de auditoria do Azure Active Directory (Azure AD) ajudam a identificar ações privilegiadas ocorridas no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3cee9-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="3cee9-105">Pode ver os tipos de Olá dos eventos que pode controlar revendo [eventos de relatório de auditoria do Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="3cee9-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3cee9-106">Antes de tentar passos Olá neste artigo, tem de consultar Olá [começar](security-azure-log-integration-get-started.md) artigo e executar passos de Olá não existe.</span><span class="sxs-lookup"><span data-stu-id="3cee9-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3cee9-107">Registos de auditoria do Azure Active directory do passos toointegrate</span><span class="sxs-lookup"><span data-stu-id="3cee9-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="3cee9-108">Abra a linha de comandos Olá e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="3cee9-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="3cee9-109">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="3cee9-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="3cee9-110">Este comando pede-lhe o início de sessão do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cee9-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="3cee9-111">Olá comando, em seguida, cria um Azure Active Directory principal de serviço no inquilinos Olá do Azure AD que alojam Olá subscrições do Azure na qual Olá utilizador com sessão iniciada é um administrador, coadministrador ou a um proprietário.</span><span class="sxs-lookup"><span data-stu-id="3cee9-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="3cee9-112">comando Olá irá falhar se o utilizador com sessão iniciada Olá é apenas um utilizador convidado no inquilino do Azure AD Olá.</span><span class="sxs-lookup"><span data-stu-id="3cee9-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="3cee9-113">Autenticação tooAzure é feito através do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cee9-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="3cee9-114">Criar um principal de serviço para a integração de registo do Azure cria Olá identidade do Azure AD, que é dado acesso tooread de subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cee9-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="3cee9-115">Executar Olá tooprovide de comando a seguir o ID do inquilino.</span><span class="sxs-lookup"><span data-stu-id="3cee9-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="3cee9-116">Terá de membro de toobe do comando de Olá de toorun de função Administrador inquilino Olá.</span><span class="sxs-lookup"><span data-stu-id="3cee9-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="3cee9-117">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3cee9-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="3cee9-118">Verifique Olá seguir tooconfirm de pastas que Olá os ficheiros do JSON de registo de auditoria do Azure Active Directory é criado nos mesmos:</span><span class="sxs-lookup"><span data-stu-id="3cee9-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="3cee9-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="3cee9-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="3cee9-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="3cee9-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="3cee9-121">Olá vídeo seguinte demonstra os passos de Olá abordados neste artigo:</span><span class="sxs-lookup"><span data-stu-id="3cee9-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="3cee9-122">Para obter instruções específicas sobre colocar informações de Olá nos ficheiros JSON Olá ao seu informações de segurança e o sistema de gestão (SIEM) de eventos, contacte o fabricante do SIEM.</span><span class="sxs-lookup"><span data-stu-id="3cee9-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="3cee9-123">A assistência de Comunidade está disponível através de Olá [fórum MSDN do Azure registo integração](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="3cee9-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="3cee9-124">Neste fórum permite que as pessoas da Olá a integração de registo do Azure da Comunidade toosupport entre si com perguntas, respostas, sugestões e truques.</span><span class="sxs-lookup"><span data-stu-id="3cee9-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="3cee9-125">Além disso, a equipa de integração de registo do Azure Olá monitoriza neste fórum e ajuda a sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="3cee9-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="3cee9-126">Também pode abrir um [pedido de suporte](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="3cee9-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="3cee9-127">Selecione **integração de registo** como serviço Olá para o qual está a pedir suporte.</span><span class="sxs-lookup"><span data-stu-id="3cee9-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cee9-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3cee9-128">Next steps</span></span>
<span data-ttu-id="3cee9-129">toolearn mais informações sobre a integração de registo do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="3cee9-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="3cee9-130">[Integração de registo do Microsoft Azure para os registos do Azure](https://www.microsoft.com/download/details.aspx?id=53324): página do Centro de transferências este fornece detalhes, requisitos de sistema e as instruções de instalação para a integração de registo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cee9-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="3cee9-131">[Introdução tooAzure integração de registo](security-azure-log-integration-overview.md): Este artigo apresenta tooAzure integração de registo, as suas capacidades principais e como funciona.</span><span class="sxs-lookup"><span data-stu-id="3cee9-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="3cee9-132">[Passos de configuração do parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): Este blogue mostra-lhe como tooconfigure toowork de integração de registo do Azure com parceiros soluções Splunk, HP ArcSight e IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="3cee9-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="3cee9-133">[FAQ sobre integração do registo do Azure](security-azure-log-integration-faq.md): Este artigo responde a questões sobre a integração de registo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cee9-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="3cee9-134">[Integração de alertas do Centro de segurança com a integração de registo do Azure](../security-center/security-center-integrating-alerts-with-log-integration.md): Este artigo mostra como alertas do Centro de segurança toosync, juntamente com eventos de segurança de máquina virtual recolhidos por diagnósticos do Azure e os registos de auditoria do Azure, com a análise de registos ou Solução do SIEM.</span><span class="sxs-lookup"><span data-stu-id="3cee9-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="3cee9-135">[Registos de auditoria de novas funcionalidades de diagnóstico do Azure e Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta mensagem de blogue apresenta os registos de auditoria tooAzure e outras funcionalidades que o ajudam a obterem informações sobre nas operações de Olá dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="3cee9-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
