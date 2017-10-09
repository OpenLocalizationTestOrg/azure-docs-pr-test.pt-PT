---
title: "Application Insights tootroubleshoot as políticas personalizadas - Azure AD B2C | Microsoft Docs"
description: "como toosetup Application Insights tootrace Olá a execução de políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="0c90a-103">B2C do Azure Active Directory: Recolher registos</span><span class="sxs-lookup"><span data-stu-id="0c90a-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="0c90a-104">Este artigo fornece os passos para recolher registos do Azure AD B2C, de modo a que pode diagnosticar problemas com as políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0c90a-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="0c90a-105">Atualmente, hello registos de atividade de detalhado descritos aqui concebidos **apenas** tooaid no desenvolvimento de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0c90a-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="0c90a-106">Utilize o modo de desenvolvimento em produção.</span><span class="sxs-lookup"><span data-stu-id="0c90a-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="0c90a-107">Os registos de recolhem todas as afirmações enviadas tooand de fornecedores de identidade Olá durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0c90a-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="0c90a-108">Se utilizar na produção, o Programador de Olá assume a responsabilidade para PII (privada informações de identificação) recolhida no registo de aplicação Insights Olá que possuem.</span><span class="sxs-lookup"><span data-stu-id="0c90a-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="0c90a-109">Estes registos detalhados apenas são recolhidos quando a política de Olá é colocada na **modo de desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="0c90a-110">Utilizar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0c90a-110">Use Application Insights</span></span>

<span data-ttu-id="0c90a-111">Azure AD B2C suporta uma funcionalidade para enviar dados tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="0c90a-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="0c90a-112">Application Insights fornece uma forma toodiagnose exceções e visualizar os problemas de desempenho de aplicações.</span><span class="sxs-lookup"><span data-stu-id="0c90a-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="0c90a-113">Configurar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0c90a-113">Setup Application Insights</span></span>

1. <span data-ttu-id="0c90a-114">Aceda toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c90a-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c90a-115">Certifique-se de que está no inquilino Olá com a sua subscrição do Azure (não o inquilino do Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="0c90a-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="0c90a-116">Clique em **+ novo** no menu de navegação esquerdo do Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="0c90a-117">Procure e selecione **Application Insights**, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="0c90a-118">Preencha o formulário de Olá e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="0c90a-119">Selecione **geral** para Olá **tipo de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="0c90a-120">Quando tem sido criado recursos Olá, abra o recurso do Application Insights Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="0c90a-121">Localizar **propriedades** Olá, no menu à esquerda e clique na mesma.</span><span class="sxs-lookup"><span data-stu-id="0c90a-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="0c90a-122">Olá cópia **chave de instrumentação** e guardá-lo para a secção seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="0c90a-123">Configurar a política personalizada do Olá</span><span class="sxs-lookup"><span data-stu-id="0c90a-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="0c90a-124">Abra o ficheiro RP Olá (por exemplo, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="0c90a-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="0c90a-125">Adicionar Olá seguintes atributos toohello `<TrustFrameworkPolicy>` elemento:</span><span class="sxs-lookup"><span data-stu-id="0c90a-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="0c90a-126">Se não existir já, adicionar um nó subordinado `<UserJourneyBehaviors>` toohello `<RelyingParty>` nós.</span><span class="sxs-lookup"><span data-stu-id="0c90a-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="0c90a-127">Tem de estar localizado imediatamente após Olá`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="0c90a-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="0c90a-128">Adicionar Olá seguir nó como elemento subordinado de Olá `<UserJourneyBehaviors>` elemento.</span><span class="sxs-lookup"><span data-stu-id="0c90a-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="0c90a-129">Certifique-se de que tooreplace `{Your Application Insights Key}` com Olá **chave de instrumentação** que obteve do Application Insights na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="0c90a-130">`DeveloperMode="true"`Indica a telemetria de Olá tooexpedite ApplicationInsights através do pipeline de processamento de Olá, aconselhável para o desenvolvimento, mas restrita em volumes elevadas.</span><span class="sxs-lookup"><span data-stu-id="0c90a-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="0c90a-131">`ClientEnabled="true"`envia o script do lado do cliente de ApplicationInsights de Olá para o registo de erros de vista e do lado do cliente de página (e não necessários).</span><span class="sxs-lookup"><span data-stu-id="0c90a-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="0c90a-132">`ServerEnabled="true"`envia Olá existente UserJourneyRecorder JSON como um tooApplication de evento personalizado Insights.</span><span class="sxs-lookup"><span data-stu-id="0c90a-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="0c90a-133">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c90a-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="0c90a-134">Carregar política Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="0c90a-135">Consulte os registos de Olá no Application Insights</span><span class="sxs-lookup"><span data-stu-id="0c90a-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="0c90a-136">Não há um curto atraso (menos de cinco minutos) antes de poder ver novos registos no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0c90a-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="0c90a-137">Abra o recurso do Application Insights Olá que criou no Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c90a-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="0c90a-138">No Olá **descrição geral** menu, clique em **análise**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="0c90a-139">Abra um novo separador no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0c90a-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="0c90a-140">Aqui está uma lista de consultas que pode utilizar toosee Olá registos</span><span class="sxs-lookup"><span data-stu-id="0c90a-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="0c90a-141">Consulta</span><span class="sxs-lookup"><span data-stu-id="0c90a-141">Query</span></span> | <span data-ttu-id="0c90a-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c90a-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="0c90a-143">Rastreios</span><span class="sxs-lookup"><span data-stu-id="0c90a-143">traces</span></span> | <span data-ttu-id="0c90a-144">Ver todos os registos de Olá gerados pelo Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0c90a-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="0c90a-145">os rastreios \\</span><span class="sxs-lookup"><span data-stu-id="0c90a-145">traces \\</span></span>| <span data-ttu-id="0c90a-146">onde timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="0c90a-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="0c90a-147">Ver todos os registos de Olá gerados pelo Azure AD B2C para Olá último dia</span><span class="sxs-lookup"><span data-stu-id="0c90a-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="0c90a-148">entradas de Olá poderão ser longas.</span><span class="sxs-lookup"><span data-stu-id="0c90a-148">hello entries may be long.</span></span>  <span data-ttu-id="0c90a-149">Exporte tooCSV para observá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="0c90a-150">Pode saber mais sobre a ferramenta de análise Olá [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="0c90a-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="0c90a-151">Comunidade Olá desenvolveu-se um utilizador journey Visualizador toohelp identidade aos programadores.</span><span class="sxs-lookup"><span data-stu-id="0c90a-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="0c90a-152">Não é suportada pela Microsoft e disponibilizado estritamente como-é.</span><span class="sxs-lookup"><span data-stu-id="0c90a-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="0c90a-153">Este lê a partir da sua instância do Application Insights e fornece uma vista de estrutura também dos eventos de journey Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="0c90a-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="0c90a-154">Obter o código de origem Olá e implementá-la na sua própria solução.</span><span class="sxs-lookup"><span data-stu-id="0c90a-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="0c90a-155">Atualmente, hello registos de atividade de detalhado descritos aqui concebidos **apenas** tooaid no desenvolvimento de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0c90a-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="0c90a-156">Utilize o modo de desenvolvimento em produção.</span><span class="sxs-lookup"><span data-stu-id="0c90a-156">Do not use development mode in production.</span></span>  <span data-ttu-id="0c90a-157">Os registos de recolhem todas as afirmações enviadas tooand de fornecedores de identidade Olá durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0c90a-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="0c90a-158">Se utilizar na produção, o Programador de Olá assume a responsabilidade para PII (privada informações de identificação) recolhida no registo de aplicação Insights Olá que possuem.</span><span class="sxs-lookup"><span data-stu-id="0c90a-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="0c90a-159">Estes registos detalhados apenas são recolhidos quando a política de Olá é colocada na **modo de desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="0c90a-160">Repositório do Github para exemplos de política personalizada não suportado e ferramentas relacionadas</span><span class="sxs-lookup"><span data-stu-id="0c90a-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="0c90a-161">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="0c90a-161">Next Steps</span></span>

<span data-ttu-id="0c90a-162">Explore os dados de Olá no toohelp Application Insights compreende Olá como o Framework de experiência de identidade B2C subjacente funciona toodeliver experiências de identidade do seu próprio.</span><span class="sxs-lookup"><span data-stu-id="0c90a-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
