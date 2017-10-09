---
title: "aaaAlerts validação no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o a alertas de segurança de Olá toovalidate no Centro de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="2e7d8-103">Validação de Alertas no Centro de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="2e7d8-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="2e7d8-104">Este documento ajuda-o a saber como tooverify se o sistema está configurado corretamente para alertas do Centro de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="2e7d8-105">O que são alertas de segurança?</span><span class="sxs-lookup"><span data-stu-id="2e7d8-105">What are security alerts?</span></span>
<span data-ttu-id="2e7d8-106">Automaticamente o Centro de segurança recolhe, analisa e integra-se os dados de registo de recursos do Azure, rede Olá e soluções de parceiros ligadas, como soluções de proteção de ponto final e firewall, toodetect e alerta, toothreats.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="2e7d8-107">Leitura [toosecurity está a responder e gerir alertas no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) para obter mais informações sobre alertas de segurança e ler [Noções sobre alertas de segurança no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn mais sobre Olá diferentes tipos de alertas.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="2e7d8-108">Validação de alertas</span><span class="sxs-lookup"><span data-stu-id="2e7d8-108">Alert validation</span></span>
<span data-ttu-id="2e7d8-109">Após instalação do agente do Centro de segurança no seu computador, siga os passos de Olá abaixo do computador olá onde pretende que o recurso de Olá atacado toobe de alerta de Olá:</span><span class="sxs-lookup"><span data-stu-id="2e7d8-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="2e7d8-110">Copie o ambiente de trabalho de um computador toohello executável (por exemplo calc.exe) ou outro diretório da sua comodidade.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="2e7d8-111">Mudar o nome deste ficheiro demasiado**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="2e7d8-112">Abra a linha de comandos Olá e executar este ficheiro com um argumento (apenas um nome argumento falsificados), tal como: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="2e7d8-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="2e7d8-113">Aguarde 5 minutos too10 e abra alertas do Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="2e7d8-114">Não existe deve encontrar um alerta toofollowing semelhante uma:</span><span class="sxs-lookup"><span data-stu-id="2e7d8-114">There you should find an alert similar toofollowing one:</span></span>

    ![Validação de Alertas](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="2e7d8-116">Ao rever este alerta, certifique-se de campo Olá argumentos auditoria ativada é apresentado como true.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="2e7d8-117">Se mostra FALSO, terá de argumentos da linha de comandos tooenable auditoria.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="2e7d8-118">Pode ativar esta opção utilizando Olá seguinte linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="2e7d8-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="2e7d8-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="2e7d8-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="2e7d8-120">Consultar também</span><span class="sxs-lookup"><span data-stu-id="2e7d8-120">See also</span></span>
<span data-ttu-id="2e7d8-121">Este artigo introduzida toohello processo de validação de alertas.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="2e7d8-122">Agora que está familiarizado com esta validação, experimente Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="2e7d8-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="2e7d8-123">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="2e7d8-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="2e7d8-124">Saiba como toomanage alertas e respondeu toosecurity incidentes no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="2e7d8-125">[Monitorização de estado de funcionamento de segurança no Centro de Segurança do Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="2e7d8-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="2e7d8-126">Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="2e7d8-127">[Compreender os alertas de segurança no Centro de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="2e7d8-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="2e7d8-128">Saiba mais sobre os diferentes tipos Olá de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="2e7d8-129">[Guia de Resolução de Problemas do Centro de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="2e7d8-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="2e7d8-130">Saiba como tootroubleshoot comuns problemas no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="2e7d8-131">[Centro de Segurança do Azure FAQ (FAQ do Centro de Segurança do Azure)](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2e7d8-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="2e7d8-132">Localize perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="2e7d8-133">[Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="2e7d8-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="2e7d8-134">Encontre mensagens do blogue acerca da segurança e conformidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7d8-134">Find blog posts about Azure security and compliance.</span></span>

