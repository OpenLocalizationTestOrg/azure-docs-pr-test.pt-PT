---
title: "aaaOperations Management Suite segurança e de segurança de dados de solução de auditoria | Microsoft Docs"
description: "Este documento explica como os dados são geridos e guardados de forma segura no Operations Management Suite Security e na Solução de Segurança e Auditoria."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="af984-103">Segurança de dados da solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="af984-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="af984-104">os clientes de toohelp evitar, detetar e responder toothreats, [segurança Operations Management Suite (OMS) e a solução de auditoria](operations-management-suite-overview.md) recolhe e processa dados sobre os recursos, que inclui:</span><span class="sxs-lookup"><span data-stu-id="af984-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="af984-105">Registo de eventos de segurança</span><span class="sxs-lookup"><span data-stu-id="af984-105">Security event log</span></span>
* <span data-ttu-id="af984-106">Eventos de Rastreio de Eventos para o Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="af984-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="af984-107">Eventos de auditoria do AppLocker</span><span class="sxs-lookup"><span data-stu-id="af984-107">AppLocker auditing events</span></span>
* <span data-ttu-id="af984-108">Registo de Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="af984-108">Windows Firewall log</span></span>
* <span data-ttu-id="af984-109">Eventos de Análise de Ameaças Avançada</span><span class="sxs-lookup"><span data-stu-id="af984-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="af984-110">Resultados da avaliação de linha de base</span><span class="sxs-lookup"><span data-stu-id="af984-110">Results of baseline assessment</span></span>
* <span data-ttu-id="af984-111">Resultados da avaliação de antimalware</span><span class="sxs-lookup"><span data-stu-id="af984-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="af984-112">Resultados da avaliação de atualização/correção</span><span class="sxs-lookup"><span data-stu-id="af984-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="af984-113">Fluxos de auditáveis explicitamente estão ativados no agente Olá</span><span class="sxs-lookup"><span data-stu-id="af984-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="af984-114">Iremos tornar-se ao privacidade de Olá compromissos forte tooprotect e segurança destes dados.</span><span class="sxs-lookup"><span data-stu-id="af984-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="af984-115">Microsoft respeita diretrizes de conformidade e segurança toostrict — desde a codificação toooperating um serviço.</span><span class="sxs-lookup"><span data-stu-id="af984-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="af984-116">Este artigo explica como os dados são geridos e guardados de forma segura na Solução de Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="af984-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="af984-117">Origens de dados</span><span class="sxs-lookup"><span data-stu-id="af984-117">Data sources</span></span>
<span data-ttu-id="af984-118">Solução de auditoria e de segurança do OMS analisam dados de máquinas virtuais e físicos computadores onde está instalado Olá agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="af984-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="af984-119">A Solução de Segurança e Auditoria do OMS pode recolher informações de configuração sobre eventos de segurança, tais como eventos do Windows, registos de auditoria, registos do IIS e mensagens syslog.</span><span class="sxs-lookup"><span data-stu-id="af984-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="af984-120">Os exemplos destes dados incluem: tipo e versão do sistema operativo, processos em execução, nome da máquina, endereços IP, utilizador com sessão iniciada e ID do inquilino.</span><span class="sxs-lookup"><span data-stu-id="af984-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="af984-121">Proteção de dados</span><span class="sxs-lookup"><span data-stu-id="af984-121">Data protection</span></span>
<span data-ttu-id="af984-122">**A segregação de dados**: dados são mantidos separados de forma lógica em cada componente em todo o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="af984-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="af984-123">Todos os dados são etiquetados por organização.</span><span class="sxs-lookup"><span data-stu-id="af984-123">All data is tagged per organization.</span></span> <span data-ttu-id="af984-124">Este tipo de etiquetagem persiste por todo o ciclo de vida do Olá dados e é imposto em cada camada de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="af984-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="af984-125">**Acesso a dados**: tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, a equipa da Microsoft pode aceder a informações recolhidas ou analisadas pelos serviços.</span><span class="sxs-lookup"><span data-stu-id="af984-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="af984-126">Respeitamos toohello [termos de licenciamento Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e [declaração de privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), quais estipulam que Microsoft não irá utilizar dados de cliente ou derivará informações dos mesmos para qualquer publicidade ou semelhantes fins comerciais.</span><span class="sxs-lookup"><span data-stu-id="af984-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="af984-127">recomendações de segurança tooprovide e investigar potenciais ameaças de segurança, a equipa da Microsoft pode aceder a informações recolhidas ou analisadas pelos serviços.</span><span class="sxs-lookup"><span data-stu-id="af984-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="af984-128">Apenas utilizamos os dados de cliente como tooprovide necessário, com o Azure serviços, incluindo fins compatíveis com o fornecimento desses serviços.</span><span class="sxs-lookup"><span data-stu-id="af984-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="af984-129">Manter todos os dados própria de tooyour direitos.</span><span class="sxs-lookup"><span data-stu-id="af984-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="af984-130">**Utilização de dados**: a Microsoft utiliza os padrões e ameaças vistas através dos vários inquilinos tooenhance nossas capacidades de prevenção e deteção; podemos fazê-lo de acordo com os compromissos de privacidade de Olá descritos na nossa [privacidade Instrução](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="af984-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="af984-131">Localização de dados é configurada ao nível da área de trabalho OMS Olá, durante a criação de área de trabalho Olá, o que faz parte do Olá inicial auditoria e segurança do OMS o processo de configuração.</span><span class="sxs-lookup"><span data-stu-id="af984-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="af984-132">Consultar também</span><span class="sxs-lookup"><span data-stu-id="af984-132">See also</span></span>
<span data-ttu-id="af984-133">Através deste documento aprendeu como os dados são geridos e salvaguardados no OMS.</span><span class="sxs-lookup"><span data-stu-id="af984-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="af984-134">toolearn mais informações sobre a segurança do OMS e a solução de auditoria, consulte:</span><span class="sxs-lookup"><span data-stu-id="af984-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="af984-135">Descrição geral do Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="af984-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="af984-136">Monitorização e responder tooSecurity alertas no Operations Management Suite segurança e a solução de auditoria</span><span class="sxs-lookup"><span data-stu-id="af984-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="af984-137">Recursos de Monitorização na Solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="af984-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

