---
title: "recuperação de aaaDisaster para a conta de integração de B2B - Azure Logic Apps | Microsoft Docs"
description: "Recuperação de desastres do Logic Apps B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="55232-103">Recuperação de desastre por várias regiões lógica B2B de aplicações</span><span class="sxs-lookup"><span data-stu-id="55232-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="55232-104">B2B cargas de trabalho envolvem transações dinheiro como encomendas pendentes e faturas.</span><span class="sxs-lookup"><span data-stu-id="55232-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="55232-105">Durante um evento de desastre, é essencial para uma Olá toomeet do negócio tooquickly recuperar que SLAs de nível empresarial acordadas com os respetivos parceiros.</span><span class="sxs-lookup"><span data-stu-id="55232-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="55232-106">Este artigo demonstra como planear a toobuild continuidade do negócio para cargas de trabalho B2B.</span><span class="sxs-lookup"><span data-stu-id="55232-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="55232-107">Preparação de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="55232-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="55232-108">Efetuar a ativação pós-falha toosecondary região durante um evento de desastre</span><span class="sxs-lookup"><span data-stu-id="55232-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="55232-109">Reverter tooprimary região após um evento de desastre</span><span class="sxs-lookup"><span data-stu-id="55232-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="55232-110">Preparação de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="55232-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="55232-111">Identifique uma região secundária e crie um [conta integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) na região secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="55232-112">Adicione parceiros, esquemas e contratos para fluxos de mensagens hello necessário onde Olá executar estado tem de toobe replicado toosecondary região integração conta.</span><span class="sxs-lookup"><span data-stu-id="55232-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="55232-113">Certifique-se de que existe consistência na Convenção de nomenclatura do artefacto de Olá, integração conta em regiões.</span><span class="sxs-lookup"><span data-stu-id="55232-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="55232-114">Olá toopull executar o estado da região primária Olá, criar uma aplicação lógica na região secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="55232-115">Esta aplicação lógica deve ter um *acionador* e um *ação*.</span><span class="sxs-lookup"><span data-stu-id="55232-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="55232-116">acionador Olá deve estabelecer ligação a conta de integração de região tooprimary e ação de Olá deve estabelecer ligação a conta de integração do toosecondary região.</span><span class="sxs-lookup"><span data-stu-id="55232-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="55232-117">Com base num intervalo de tempo de Olá, o acionador Olá consulta a tabela de estado de região primária executar Olá e obtém novos registos de Olá, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="55232-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="55232-118">ação de Olá atualiza-los a conta de integração de região toosecondary.</span><span class="sxs-lookup"><span data-stu-id="55232-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="55232-119">Isto ajuda-o estado de incremental runtime tooget da região de toosecondary região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="55232-120">Continuidade do negócio em Logic Apps é a conta de integração concebidos toosupport com base em protocolos de B2B - X12, AS2 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="55232-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="55232-121">passos de detalhado toofind, selecione Olá as respetivas ligações.</span><span class="sxs-lookup"><span data-stu-id="55232-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="55232-122">Olá recomendação é toodeploy todos os recursos de região primária numa região secundária demasiado.</span><span class="sxs-lookup"><span data-stu-id="55232-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="55232-123">Recursos de região primária incluem a SQL Database do Azure ou do Azure Cosmos DB, Service Bus do Azure e utilizado para as mensagens, a API Management do Azure e a funcionalidade de Azure Logic Apps Olá no App Service do Azure de Event Hubs do Azure.</span><span class="sxs-lookup"><span data-stu-id="55232-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="55232-124">Estabelece uma ligação a uma região secundária de tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="55232-125">Olá toopull executar estado a partir de uma região primária, criar uma aplicação lógica numa região secundária.</span><span class="sxs-lookup"><span data-stu-id="55232-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="55232-126">aplicação de lógica de Olá deve ter um acionador e uma ação.</span><span class="sxs-lookup"><span data-stu-id="55232-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="55232-127">acionador Olá deve ligar a conta de integração de região primária tooa.</span><span class="sxs-lookup"><span data-stu-id="55232-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="55232-128">ação de Olá deve estabelecer ligação a conta de integração do tooa região secundária.</span><span class="sxs-lookup"><span data-stu-id="55232-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="55232-129">Com base num intervalo de tempo de Olá, o acionador Olá consulta a tabela de estado de região primária executar Olá e obtém novos registos de Olá, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="55232-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="55232-130">ação de Olá atualiza-los a conta de integração de região secundária tooa.</span><span class="sxs-lookup"><span data-stu-id="55232-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="55232-131">Este processo ajuda-o estado de incremental runtime tooget da região secundária do Olá região primária toohello.</span><span class="sxs-lookup"><span data-stu-id="55232-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="55232-132">Continuidade do negócio numa conta integração Logic Apps fornece suporte com base em protocolos de B2B Olá X12, AS2 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="55232-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="55232-133">Para obter passos detalhados sobre como utilizar X12 e AS2, consulte [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="55232-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="55232-134">Efetuar a ativação pós-falha região secundária tooa durante um evento de desastre</span><span class="sxs-lookup"><span data-stu-id="55232-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="55232-135">Durante um evento de desastre, quando a região primária Olá não está disponível para a continuidade do negócio, região secundária do tráfego direta toohello.</span><span class="sxs-lookup"><span data-stu-id="55232-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="55232-136">Uma ajuda a região secundária toorecover um negócio rapidamente funciona toomeet Olá RPO/RTO acordada pelos respetivos parceiros.</span><span class="sxs-lookup"><span data-stu-id="55232-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="55232-137">Também minimiza os esforços toofail através da região de tooanother uma região.</span><span class="sxs-lookup"><span data-stu-id="55232-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="55232-138">Há uma latência esperada ao copiar os números de controlo de uma região secundária de tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="55232-139">tooavoid enviar duplicado controlo gerado números toopartners durante um evento de desastre, recomendação Olá seja tooincrement Olá controlo composto por números nos contratos de região secundária Olá utilizando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="55232-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="55232-140">Reverter eventos de pós-desastre tooa região primária</span><span class="sxs-lookup"><span data-stu-id="55232-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="55232-141">toofall tooa anterior a região primária quando estiver disponível, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="55232-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="55232-142">Pare a aceitação das mensagens de parceiros na região secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="55232-143">Incrementar números de controlo de Olá gerado para todos os contratos de região primária Olá utilizando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="55232-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="55232-144">Tráfego direto de região primária do Olá região secundária toohello.</span><span class="sxs-lookup"><span data-stu-id="55232-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="55232-145">Certifique-se de que aplicação de lógica de Olá criada numa região secundária de Olá para extrair a executar o estado da região primária Olá está ativada.</span><span class="sxs-lookup"><span data-stu-id="55232-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="55232-146">X12</span><span class="sxs-lookup"><span data-stu-id="55232-146">X12</span></span> 

<span data-ttu-id="55232-147">Continuidade do negócio para EDI X 12 documentos baseia-se em números de controlo:</span><span class="sxs-lookup"><span data-stu-id="55232-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="55232-148">Também pode utilizar Olá [X12 rápido iniciar modelo](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span><span class="sxs-lookup"><span data-stu-id="55232-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="55232-149">Criar contas de automatização primária e secundária são modelo de Olá toouse de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="55232-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="55232-150">Olá modelo ajuda as logic apps de dois toocreate, para números de controlo recebido e outra para números de controlo gerado.</span><span class="sxs-lookup"><span data-stu-id="55232-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="55232-151">Respetivos acionadores e ações são criadas no Olá as logic apps, ligar Olá acionador toohello integração primário contas e Olá ação toohello integração secundário.</span><span class="sxs-lookup"><span data-stu-id="55232-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="55232-152">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="55232-152">**Prerequisites**</span></span>

<span data-ttu-id="55232-153">recuperação de desastres tooenable para mensagens de entrada, selecione Olá duplicado Verifique as definições do receber definições do contrato de Olá X12.</span><span class="sxs-lookup"><span data-stu-id="55232-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Selecione as definições de verificação duplicado](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="55232-155">Criar um [aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) numa região secundária.</span><span class="sxs-lookup"><span data-stu-id="55232-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="55232-156">Pesquisar nos **X12**e selecione **X12-quando um número de controlo é modificado**.</span><span class="sxs-lookup"><span data-stu-id="55232-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Procure o X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="55232-158">acionador Olá solicita tooestablish uma conta de integração de tooan de ligação.</span><span class="sxs-lookup"><span data-stu-id="55232-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="55232-159">acionador Olá deve ser ligado a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="55232-160">Introduza um nome de ligação, selecione o *conta de integração de região primária* de Olá lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="55232-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Nome de conta de integração de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="55232-162">Olá **sincronização de número de controlo do DateTime toostart** definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="55232-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="55232-163">Olá **frequência** pode ser definido demasiado**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.</span><span class="sxs-lookup"><span data-stu-id="55232-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e a frequência](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="55232-165">Selecione **novo passo** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="55232-165">Select **New step** > **Add an action**.</span></span>

   ![Novo passo, adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="55232-167">Pesquisar nos **X12**e selecione **X12-adicionar ou atualizar os números de controlo**.</span><span class="sxs-lookup"><span data-stu-id="55232-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Adicionar ou atualizar os números de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="55232-169">Selecione tooconnect uma conta de integração do ação tooa região secundária, **Alterar ligação** > **Adicionar nova ligação** para obter uma lista de contas de integração disponível Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="55232-170">Introduza um nome de ligação, selecione o *conta de integração de região secundária* de Olá lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="55232-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Nome de conta de integração de região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="55232-172">Mudar tooraw entradas clicando no ícone de Olá no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="55232-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Comutador tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="55232-174">Selecione o corpo do Seletor de conteúdo dinâmico Olá e guardar a aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Campos de conteúdo dinâmicos](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="55232-176">Com base num intervalo de tempo de Olá, o acionador de Olá consulta a tabela de número de controlo do Olá região primária recebido e obtém novos registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="55232-177">ação de Olá atualiza os registos de Olá na conta de integração do Olá região secundária.</span><span class="sxs-lookup"><span data-stu-id="55232-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="55232-178">Se não existirem não existem atualizações, o estado de Acionador de Olá aparece como **ignorados**.</span><span class="sxs-lookup"><span data-stu-id="55232-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Tabela de número de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="55232-180">Com base num intervalo de tempo de Olá, estado de incremental runtime Olá replica a partir de uma região secundária de tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="55232-181">Durante um evento de desastre, quando a região primária Olá não é a região secundária de toohello tráfego disponível, direta para a continuidade do negócio.</span><span class="sxs-lookup"><span data-stu-id="55232-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="55232-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="55232-182">EDIFACT</span></span> 

<span data-ttu-id="55232-183">Continuidade do negócio para documentos EDI EDIFACT baseia-se em números de controlo.</span><span class="sxs-lookup"><span data-stu-id="55232-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="55232-184">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="55232-184">**Prerequisites**</span></span>

<span data-ttu-id="55232-185">tooenable recuperação de desastres para as mensagens de entrada, selecione Olá duplicado Verifique as definições do receber definições seu contrato EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="55232-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Selecione as definições de verificação duplicado](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="55232-187">Criar um [aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) numa região secundária.</span><span class="sxs-lookup"><span data-stu-id="55232-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="55232-188">Pesquisar nos **EDIFACT**e selecione **EDIFACT - quando um número de controlo é modificado**.</span><span class="sxs-lookup"><span data-stu-id="55232-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Procure EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="55232-190">acionador Olá solicita tooestablish uma conta de integração de tooan de ligação.</span><span class="sxs-lookup"><span data-stu-id="55232-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="55232-191">acionador Olá deve ser ligado a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="55232-192">Introduza um nome de ligação, selecione o *conta de integração de região primária* de Olá lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="55232-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Nome de conta de integração de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="55232-194">Olá **sincronização de número de controlo do DateTime toostart** definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="55232-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="55232-195">Olá **frequência** pode ser definido demasiado**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.</span><span class="sxs-lookup"><span data-stu-id="55232-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime e a frequência](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="55232-197">Selecione **novo passo** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="55232-197">Select **New step** > **Add an action**.</span></span>    

   ![Novo passo, adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="55232-199">Pesquisar nos **EDIFACT**e selecione **EDIFACT - adicionar ou atualizar os números de controlo**.</span><span class="sxs-lookup"><span data-stu-id="55232-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Adicionar ou atualizar os números de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="55232-201">Selecione tooconnect uma conta de integração do ação tooa região secundária, **Alterar ligação** > **Adicionar nova ligação** para obter uma lista de contas de integração disponível Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="55232-202">Introduza um nome de ligação, selecione o *conta de integração de região secundária* de Olá lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="55232-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome de conta de integração de região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="55232-204">Mudar tooraw entradas clicando no ícone de Olá no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="55232-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Comutador tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="55232-206">Selecione o corpo do Seletor de conteúdo dinâmico Olá e guardar a aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Campos de conteúdo dinâmicos](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="55232-208">Com base num intervalo de tempo de Olá, o acionador de Olá consulta a tabela de número de controlo do Olá região primária recebido e obtém novos registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="55232-209">ação de Olá atualiza a conta de integração do Olá registos toohello região secundária.</span><span class="sxs-lookup"><span data-stu-id="55232-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="55232-210">Se não existirem não existem atualizações, o estado de Acionador de Olá aparece como **ignorados**.</span><span class="sxs-lookup"><span data-stu-id="55232-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Tabela de número de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="55232-212">Com base num intervalo de tempo de Olá, estado de incremental runtime Olá replica a partir de uma região secundária de tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="55232-213">Durante um evento de desastre, quando a região primária Olá não é a região secundária de toohello tráfego disponível, direta para a continuidade do negócio.</span><span class="sxs-lookup"><span data-stu-id="55232-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="55232-214">AS2</span><span class="sxs-lookup"><span data-stu-id="55232-214">AS2</span></span> 

<span data-ttu-id="55232-215">Continuidade do negócio para documentos que utilizam o protocolo de AS2 Olá baseia-se no ID de mensagem de Olá e valor MIC Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="55232-216">Também pode utilizar Olá [AS2 início rápido modelo](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span><span class="sxs-lookup"><span data-stu-id="55232-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="55232-217">Criar contas de automatização primária e secundária são modelo de Olá toouse de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="55232-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="55232-218">modelo de Olá ajuda a criar uma aplicação lógica que tem um acionador e uma ação.</span><span class="sxs-lookup"><span data-stu-id="55232-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="55232-219">aplicação de lógica de Olá cria uma ligação a partir de uma conta do acionador tooa integração primária e uma conta de ação de integração secundário tooa.</span><span class="sxs-lookup"><span data-stu-id="55232-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="55232-220">Criar um [aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) na região secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="55232-221">Pesquisar nos **AS2**e selecione **AS2 - valor MIC de quando é criado**.</span><span class="sxs-lookup"><span data-stu-id="55232-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Procure AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="55232-223">Um acionador pede-lhe tooestablish uma conta de integração de tooan de ligação.</span><span class="sxs-lookup"><span data-stu-id="55232-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="55232-224">acionador Olá deve ser ligado a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="55232-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="55232-225">Introduza um nome de ligação, selecione o *conta de integração de região primária* de Olá lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="55232-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome de conta de integração de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="55232-227">Olá **sincronização de valor DateTime toostart MIC** definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="55232-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="55232-228">Olá **frequência** pode ser definido demasiado**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.</span><span class="sxs-lookup"><span data-stu-id="55232-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e a frequência](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="55232-230">Selecione **novo passo** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="55232-230">Select **New step** > **Add an action**.</span></span>  

   ![Novo passo, adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="55232-232">Pesquisar nos **AS2**e selecione **AS2 - adicionar ou atualizar o conteúdo do MIC**.</span><span class="sxs-lookup"><span data-stu-id="55232-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Adição de MIC ou atualização](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="55232-234">Selecione tooconnect conta de ação tooa integração secundária, **Alterar ligação** > **Adicionar nova ligação** para obter uma lista de contas de integração disponível Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="55232-235">Introduza um nome de ligação, selecione o *conta de integração de região secundária* de Olá lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="55232-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome de conta de integração de região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="55232-237">Mudar tooraw entradas clicando no ícone de Olá no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="55232-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Comutador tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="55232-239">Selecione o corpo do Seletor de conteúdo dinâmico Olá e guardar a aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="55232-241">Com base num intervalo de tempo de Olá, o acionador de Olá consulta a tabela de região primária Olá e obtém novos registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="55232-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="55232-242">ação de Olá atualiza-los a conta de integração de região secundária toohello.</span><span class="sxs-lookup"><span data-stu-id="55232-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="55232-243">Se não existirem não existem atualizações, o estado de Acionador de Olá aparece como **ignorados**.</span><span class="sxs-lookup"><span data-stu-id="55232-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Tabela de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="55232-245">Estado de incremental runtime Olá com base num intervalo de tempo de Olá, replica a região secundária do Olá região primária toohello.</span><span class="sxs-lookup"><span data-stu-id="55232-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="55232-246">Durante um evento de desastre, quando a região primária Olá não é a região secundária de toohello tráfego disponível, direta para a continuidade do negócio.</span><span class="sxs-lookup"><span data-stu-id="55232-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="55232-247">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="55232-247">Next steps</span></span>

[<span data-ttu-id="55232-248">Monitorizar mensagens B2B</span><span class="sxs-lookup"><span data-stu-id="55232-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

