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
# <a name="azure-active-directory-b2c-collecting-logs"></a>B2C do Azure Active Directory: Recolher registos

Este artigo fornece os passos para recolher registos do Azure AD B2C, de modo a que pode diagnosticar problemas com as políticas personalizadas.

>[!NOTE]
>Atualmente, hello registos de atividade de detalhado descritos aqui concebidos **apenas** tooaid no desenvolvimento de políticas personalizadas. Utilize o modo de desenvolvimento em produção.  Os registos de recolhem todas as afirmações enviadas tooand de fornecedores de identidade Olá durante o desenvolvimento.  Se utilizar na produção, o Programador de Olá assume a responsabilidade para PII (privada informações de identificação) recolhida no registo de aplicação Insights Olá que possuem.  Estes registos detalhados apenas são recolhidos quando a política de Olá é colocada na **modo de desenvolvimento**.


## <a name="use-application-insights"></a>Utilizar o Application Insights

Azure AD B2C suporta uma funcionalidade para enviar dados tooApplication Insights.  Application Insights fornece uma forma toodiagnose exceções e visualizar os problemas de desempenho de aplicações.

### <a name="setup-application-insights"></a>Configurar o Application Insights

1. Aceda toohello [portal do Azure](https://portal.azure.com). Certifique-se de que está no inquilino Olá com a sua subscrição do Azure (não o inquilino do Azure AD B2C).
1. Clique em **+ novo** no menu de navegação esquerdo do Olá.
1. Procure e selecione **Application Insights**, em seguida, clique em **criar**.
1. Preencha o formulário de Olá e clique em **criar**. Selecione **geral** para Olá **tipo de aplicação**.
1. Quando tem sido criado recursos Olá, abra o recurso do Application Insights Olá.
1. Localizar **propriedades** Olá, no menu à esquerda e clique na mesma.
1. Olá cópia **chave de instrumentação** e guardá-lo para a secção seguinte Olá.

### <a name="set-up-hello-custom-policy"></a>Configurar a política personalizada do Olá

1. Abra o ficheiro RP Olá (por exemplo, SignUpOrSignin.xml).
1. Adicionar Olá seguintes atributos toohello `<TrustFrameworkPolicy>` elemento:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Se não existir já, adicionar um nó subordinado `<UserJourneyBehaviors>` toohello `<RelyingParty>` nós. Tem de estar localizado imediatamente após Olá`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Adicionar Olá seguir nó como elemento subordinado de Olá `<UserJourneyBehaviors>` elemento. Certifique-se de que tooreplace `{Your Application Insights Key}` com Olá **chave de instrumentação** que obteve do Application Insights na secção anterior Olá.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`Indica a telemetria de Olá tooexpedite ApplicationInsights através do pipeline de processamento de Olá, aconselhável para o desenvolvimento, mas restrita em volumes elevadas.
  * `ClientEnabled="true"`envia o script do lado do cliente de ApplicationInsights de Olá para o registo de erros de vista e do lado do cliente de página (e não necessários).
  * `ServerEnabled="true"`envia Olá existente UserJourneyRecorder JSON como um tooApplication de evento personalizado Insights.
Exemplo:

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

3. Carregar política Olá.

### <a name="see-hello-logs-in-application-insights"></a>Consulte os registos de Olá no Application Insights

>[!NOTE]
> Não há um curto atraso (menos de cinco minutos) antes de poder ver novos registos no Application Insights.

1. Abra o recurso do Application Insights Olá que criou no Olá [portal do Azure](https://portal.azure.com).
1. No Olá **descrição geral** menu, clique em **análise**.
1. Abra um novo separador no Application Insights.
1. Aqui está uma lista de consultas que pode utilizar toosee Olá registos

| Consulta | Descrição |
|---------------------|--------------------|
Rastreios | Ver todos os registos de Olá gerados pelo Azure AD B2C |
os rastreios \| onde timestamp > ago(1d) | Ver todos os registos de Olá gerados pelo Azure AD B2C para Olá último dia

entradas de Olá poderão ser longas.  Exporte tooCSV para observá.

Pode saber mais sobre a ferramenta de análise Olá [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Comunidade Olá desenvolveu-se um utilizador journey Visualizador toohelp identidade aos programadores.  Não é suportada pela Microsoft e disponibilizado estritamente como-é.  Este lê a partir da sua instância do Application Insights e fornece uma vista de estrutura também dos eventos de journey Olá utilizador.  Obter o código de origem Olá e implementá-la na sua própria solução.

>[!NOTE]
>Atualmente, hello registos de atividade de detalhado descritos aqui concebidos **apenas** tooaid no desenvolvimento de políticas personalizadas. Utilize o modo de desenvolvimento em produção.  Os registos de recolhem todas as afirmações enviadas tooand de fornecedores de identidade Olá durante o desenvolvimento.  Se utilizar na produção, o Programador de Olá assume a responsabilidade para PII (privada informações de identificação) recolhida no registo de aplicação Insights Olá que possuem.  Estes registos detalhados apenas são recolhidos quando a política de Olá é colocada na **modo de desenvolvimento**.

[Repositório do Github para exemplos de política personalizada não suportado e ferramentas relacionadas](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Passos Seguintes

Explore os dados de Olá no toohelp Application Insights compreende Olá como o Framework de experiência de identidade B2C subjacente funciona toodeliver experiências de identidade do seu próprio.
