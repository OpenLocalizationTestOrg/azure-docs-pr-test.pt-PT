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
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="92f0d-103">Ativar a encriptação transparente de dados no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="92f0d-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="92f0d-104">Centro de segurança do Azure recomendará ativar encriptação de dados transparente (TDE) nas bases de dados do SQL Server se o TDE não estiver ativado.</span><span class="sxs-lookup"><span data-stu-id="92f0d-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="92f0d-105">TDE protege os dados e ajuda a cumprir os requisitos de conformidade ao encriptar a sua base de dados, cópias de segurança associadas e os ficheiros de registo de transações inativos, sem necessidade de alterações tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="92f0d-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="92f0d-106">toolearn mais consulte [encriptação transparente de dados com a SQL Database do Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="92f0d-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="92f0d-107">Esta recomendação aplica-se toohello apenas; serviço do SQL do Azure não inclui o SQL Server em execução em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="92f0d-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="92f0d-108">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="92f0d-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="92f0d-109">Não se trata de um guia passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="92f0d-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="92f0d-110">Implementar a recomendação de Olá</span><span class="sxs-lookup"><span data-stu-id="92f0d-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="92f0d-111">No Olá **recomendações** painel, selecione **ativar a encriptação transparente de dados**.</span><span class="sxs-lookup"><span data-stu-id="92f0d-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="92f0d-112">![Ativar a Encriptação de Dados Transparente][1]</span><span class="sxs-lookup"><span data-stu-id="92f0d-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="92f0d-113">Esta ação abre Olá **ativar a encriptação de dados transparente em bases de dados do SQL Server** painel.</span><span class="sxs-lookup"><span data-stu-id="92f0d-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="92f0d-114">Selecione um tooenable de base de dados do SQL Server TDE no.</span><span class="sxs-lookup"><span data-stu-id="92f0d-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="92f0d-115">![Selecione a base de dados SQL tooenable TDE no][2]</span><span class="sxs-lookup"><span data-stu-id="92f0d-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="92f0d-116">No Olá **encriptação transparente de dados** painel, selecione **ON** sob a encriptação de dados e selecione **guardar** no Friso de principais de Olá do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="92f0d-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="92f0d-117">![Ativar o TDE][3]</span><span class="sxs-lookup"><span data-stu-id="92f0d-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="92f0d-118">Quando a TDE estiver ativada no Olá selecionado base de dados do SQL Server, hello **estado de encriptação** mudará demasiado**encriptado**.</span><span class="sxs-lookup"><span data-stu-id="92f0d-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Estado de encriptação][4]

## <a name="see-also"></a><span data-ttu-id="92f0d-120">Consultar também</span><span class="sxs-lookup"><span data-stu-id="92f0d-120">See also</span></span>
<span data-ttu-id="92f0d-121">Este artigo mostrou como tooimplement Olá recomendação do Centro de segurança "Ativar encriptação transparente de dados."</span><span class="sxs-lookup"><span data-stu-id="92f0d-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="92f0d-122">toolearn mais informações sobre a SQL TDE, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="92f0d-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="92f0d-123">Encriptação transparente de dados com base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="92f0d-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="92f0d-124">Começar com encriptação de dados transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="92f0d-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="92f0d-125">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="92f0d-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="92f0d-126">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="92f0d-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="92f0d-127">[Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="92f0d-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="92f0d-128">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="92f0d-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="92f0d-129">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="92f0d-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="92f0d-130">[Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="92f0d-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="92f0d-131">[FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="92f0d-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="92f0d-132">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) -obter Olá mais recentes notícias de segurança do Azure e informações.</span><span class="sxs-lookup"><span data-stu-id="92f0d-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
