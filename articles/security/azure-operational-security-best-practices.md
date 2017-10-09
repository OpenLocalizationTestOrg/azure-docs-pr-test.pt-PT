---
title: "os procedimentos de segurança operacional aaaAzure | Microsoft Docs"
description: "Este artigo fornece um conjunto de melhores práticas de segurança operacionais do Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Azure melhores práticas de segurança operacional
Segurança operacionais do Azure refere-se os serviços de toohello, controlos e toousers disponíveis funcionalidades para proteger os seus dados, aplicações e outros recursos no Microsoft Azure. Segurança operacionais do Azure é construída numa estrutura que incorpora o conhecimento de Olá adquirido através de várias funcionalidades que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Microsoft Security Response Center programa e deteção profunda de Olá atuais das ameaças.

Neste artigo, discutimos a uma coleção de práticas recomendadas de segurança de base de dados do Azure. Estas melhores práticas são derivadas da nossa experiência com a segurança da base de dados do Azure e experiências Olá dos clientes, como por si.

Para cada melhor prática, vamos explicar:
-   Que Olá melhor prática é
-   Motivo pelo qual pretende tooenable que melhor prática
-   Se falhar tooenable Olá prática recomendada, que poderá ser resultado de Olá
- Como pode saber tooenable Olá prática recomendada

Este artigo Azure operacional melhores práticas de segurança baseia-se no opinião um consenso e capacidades da plataforma do Azure e conjuntos de funcionalidades, tal como existem momento Olá que este artigo foi escrito. As tecnologias e opinions alteram ao longo do tempo e este artigo será atualizado num tooreflect regularmente essas alterações.

Azure operacional melhores práticas de segurança abordadas neste artigo incluem:

-   Monitorizar, gerir e proteger a infraestrutura de nuvem
-   Gerir identidades e implementa início de sessão único (SSO)
-   Pedidos de rastreio, analisar tendências de utilização e diagnosticar problemas
-   Monitorizar os serviços com uma solução de monitorização centralizada
-   Evitar, detetar e responder toothreats
-   Monitorização de rede com base no cenário de ponto a ponto
-   Implementação segura utilizando ferramentas de DevOps comprovadas

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Monitorizar, gerir e proteger a infraestrutura de nuvem
Operações de TI é responsável por gerir a infraestrutura de centro de dados, aplicações e dados, incluindo estabilidade Olá e segurança destes sistemas. No entanto, obter conhecimentos de segurança aprofundados em aumentar frequentemente complexas ambientes de TI requer que as organizações toocobble em conjunto dados de vários sistemas de segurança e gestão.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) é baseado na nuvem IT solução de gestão da Microsoft que o ajuda a gerir e proteger no local e a infraestrutura de nuvem.

[Solução de auditoria e segurança do OMS](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) permite IT tooactively monitorizar todos os recursos, o que podem ajudar a minimiza o impacto de Olá de incidentes de segurança. Auditoria e segurança do OMS tem domínios de segurança que podem ser utilizados para monitorizar os recursos.

Para obter mais informações sobre o OMS, leia o artigo de Olá [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp evitar, detetar e responder toothreats, [segurança Operations Management Suite (OMS) e a solução de auditoria](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) recolhe e processa dados sobre os recursos, que inclui:

-   Registo de eventos de segurança
-   Eventos de Rastreio de Eventos para o Windows (ETW)
-   Eventos de auditoria do AppLocker
-   Registo de Firewall do Windows
-   Eventos de Análise de Ameaças Avançada
-   Resultados da avaliação de linha de base
-   Resultados da avaliação de antimalware
-   Resultados da avaliação de atualização/correção
-   Fluxos de syslog explicitamente estão ativados no agente Olá


## <a name="manage-identity-and-implement-single-sign-on"></a>Gerir identidades e implementar o início de sessão único
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) é o diretório de nuvem multi-inquilino, com base da Microsoft e o serviço de gestão de identidade.

[Azure AD](https://azure.microsoft.com/services/active-directory/) também inclui um conjunto completo de [gestão de identidades](https://docs.microsoft.com/azure/security/security-identity-management-overview) capacidades, incluindo [autenticação multifator](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), registo de dispositivos, gestão de palavra-passe self-service, gestão de grupos self-service, gestão de contas com privilégios, controlo de acesso baseado em funções, monitorização, avançada de auditoria e segurança monitorização e alertas de utilização da aplicação.

Olá capacidades os seguintes pode ajudar a proteger aplicações baseado na nuvem, simplificar processos de TI, cortar os custos e ajudar a garantir que são cumpridos os objetivos de conformidade empresarial:

-   Gestão de identidades e acesso para a nuvem de Olá
-   Simplificar a aplicação de nuvem de tooany de acesso de utilizador
-   Proteger aplicações e dados confidenciais
-   Proporcionar autonomia aos empregados
-   Integrar com o Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Gestão de identidades e acesso para a nuvem de Olá
Azure Active Directory (Azure AD) é um abrangentes [solução de nuvem de gestão de identidades e acessos](https://www.microsoft.com/cloud-platform/identity-management), que lhe oferece um conjunto robusto de capacidades toomanage utilizadores e grupos. Ajuda a proteger o acesso tooon local e nuvem aplicações, incluindo os serviços de web do Microsoft como o Office 365 e o software que não sejam da Microsoft como um aplicações de serviço (SaaS).
toolearn como mais proteção de identidade tooenable no Azure AD, consulte [ativar o Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Simplificar a aplicação de nuvem de tooany de acesso de utilizador
[Ativar o início de sessão único](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify toothousands de acesso de utilizador das aplicações em nuvem de dispositivos Windows, Mac, Android e iOS. Os utilizadores podem iniciar aplicações a partir de um painel de acesso personalizados baseados na web ou aplicação móvel, utilizando as credenciais da empresa. Utilize toogo de módulo de Proxy da aplicação Olá do Azure AD para além de aplicações SaaS e publicar no local web aplicações tooprovide altamente acesso remoto seguro e o início de sessão único.

### <a name="protect-sensitive-data-and-applications"></a>Proteger aplicações e dados confidenciais
Ativar [Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent não autorizado aceder tooon local e as aplicações em nuvem, fornecendo um nível adicional de autenticação. Proteja o seu negócio e atenue potenciais ameaças com monitorização de segurança, alertas e relatórios baseados em aprendizagem automática que identificam padrões de acesso inconsistentes.

### <a name="enable-self-service-for-your-employees"></a>Proporcionar autonomia aos empregados
Delegar tarefas importantes tooyour que os funcionários, tal como repor palavras-passe e criar e gerir grupos. [Ativar a alteração de palavra-passe self-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), repor e self-service grupo de gestão com o Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Integrar com o Azure Active Directory
Expandir [do Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) e qualquer outro local diretórios tooAzure AD tooenable-início de sessão único para todas as aplicações baseadas na nuvem. Os atributos de utilizador podem ser o diretório em nuvem de tooyour automaticamente sincronizados a partir de todos os tipos de diretórios no local.

toolearn mais sobre a integração do Azure Active Directory e como tooenable, leia o artigo de Olá [integrar os diretórios no local ao Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Pedidos de rastreio, analisar tendências de utilização e diagnosticar problemas
[Análise de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-analytics) efetua o registo e fornece dados de métricas para uma conta de armazenamento. Pode utilizar esta pedidos de tootrace de dados, analisar tendências de utilização e diagnosticar problemas com a sua conta de armazenamento.

As métricas do Storage Analytics estão ativadas por predefinição para novas contas de armazenamento. Pode ativar o registo e configurar as métricas e registo no Olá portal do Azure; Para obter mais informações, consulte [monitorizar uma conta de armazenamento no portal do Azure de Olá](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Também pode ativar a análise de armazenamento através de programação através de Olá REST API ou biblioteca de clientes Olá. Utilize Olá definir propriedades de serviço operação tooenable análise de armazenamento individualmente para cada serviço.

Para um guia aprofundado sobre como utilizar a análise de armazenamento e outro tooidentify de ferramentas, diagnosticar e resolver problemas relacionados com o Storage do Azure, consulte [monitorizar, diagnosticar e resolver problemas de armazenamento do Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

toolearn mais sobre a integração do Azure Active Directory e como tooenable lê-lo, artigo Olá [ativar e configurar a análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Serviços de monitorização
Aplicações em nuvem são complexas com várias partes mover. A monitorização fornece tooensure de dados que a aplicação permanece cópias de segurança e em execução em bom estado. Também ajuda a toostave desativado potenciais problemas ou a resolução de problemas anteriores aqueles. Além disso, pode utilizar a monitorização dados toogain conhecimentos aprofundados sobre a sua aplicação. Conhecimentos podem ajudá-lo tooimprove do desempenho de aplicações ou maintainability ou automatizar ações que caso contrário necessitem intervenção manual.

### <a name="monitor-azure-resources"></a>Monitorizar os recursos do Azure
[Monitor do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) é Olá plataforma serviço que fornece uma única origem para monitorizar os recursos do Azure. Com a monitorização do Azure, pode visualizar, consultar, encaminhar, arquivar e tomar medidas em Olá nas métricas e registos proveniente de recursos no Azure. Pode trabalhar com estes dados utilizando o painel do portal Monitor Olá, [Cmdlets do PowerShell Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [CLI de várias plataformas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), ou [as APIs REST da Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Ativar o dimensionamento automático com a monitorização do Azure
Ativar [dimensionamento automático de Monitor do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) aplica-se apenas conjuntos de dimensionamento de máquina toovirtual (VMSS), cloud services, planos de serviço de aplicações e ambientes do app service.

### <a name="manage-roles-permissions-and-security"></a>Gerir funções de segurança e permissões
Tem de várias equipas toostrictly [limitá acesso toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) dados e definições. Por exemplo, se tiver os membros da equipa que trabalham exclusivamente no monitorização (engenheiros de suporte, os engenheiros de devops) ou se utilizar um fornecedor de serviço geridas, poderá ser útil toogrant-lhes aceder tooonly dados de monitorização ao restringir os respetivos toocreate de capacidade, modificar, ou Elimine recursos.

Isto mostra como tooquickly aplicar um incorporada monitorização RBAC função tooa utilizador no Azure ou criar a sua própria função personalizada para um utilizador que tem permissões de monitorização limitadas. -Descreve considerações de segurança para os seus recursos relacionados com o Monitor do Azure, em seguida, e como pode limitar o acesso toohello dados contêm.

## <a name="prevent-detect-and-respond-toothreats"></a>Evitar, detetar e responder toothreats
A deteção de ameaças do Centro de segurança funciona através da recolha automática de informações de segurança de recursos do Azure, rede Olá e soluções de parceiros ligadas. -Analyses desta informação, muitas vezes correlacionando informações de várias origens, tooidentify ameaças. Alertas de segurança são prioritários no Centro de segurança juntamente com recomendações sobre como tooremediate Olá ameaça.

-   [Configurar uma política de segurança](https://docs.microsoft.com/azure/security-center/security-center-policies) para a sua subscrição do Azure.
-   Olá utilize [recomendações no Centro de segurança](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp proteger os recursos do Azure.
-   Reveja e gerir o seu atual [alertas de segurança](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).

[Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Olá, ajuda a evitar, detetar e responder toothreats com uma maior visibilidade e controlo sobre a segurança dos seus recursos Azure. Fornece gestão de políticas e monitorização de segurança integrada nas suas subscrições do Azure, ajuda a detetar ameaças que caso contrário podem passar despercebidas e funciona com um ecossistema abrangente de soluções de segurança.

Centro de segurança proporciona capacidades de prevenção, a deteção e a resposta que estão incorporadas no tooAzure de ameaças eficiente e de fácil utilização. As principais capacidades são:

-   Compreender o estado de segurança da nuvem
-   Controle a segurança da cloud
-   Implemente facilmente soluções de segurança da cloud integradas
-   Detete ameaças e responda com rapidez

### <a name="understand-cloud-security-state"></a>Compreender o estado de segurança da nuvem
Utilização do Centro de segurança do Azure tooget uma vista de estado de segurança de Olá de todos os seus recursos do Azure central. De forma rápida, certifique-se de que controlos de segurança adequados Olá estão no local e configurado corretamente e identificam rapidamente quaisquer recursos, que requerem atenção.

### <a name="take-control-of-cloud-security"></a>Controle a segurança da cloud
Definir [políticas de segurança](https://docs.microsoft.com/azure/security-center/security-center-policies) para as subscrições do Azure em conformidade com a empresa tooyour da segurança de nuvem necessidades, adaptados toohello tipo de aplicações ou sensibilidade dos dados de Olá em cada subscrição. Utilize os proprietários de recursos de tooguide recomendações orientadas por políticas através do processo de Olá de implementação de controlos necessários — demorar guesswork Olá fora de segurança de nuvem.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Implemente facilmente soluções de segurança da cloud integradas
[Permitir soluções de segurança](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) da Microsoft e respetivos parceiros, incluindo antimalware e firewalls líder da indústria. Utilize está mais simples de soluções de segurança do aprovisionamento toodeploy — alterações de redes, mesmo que estão configuradas por si. Os seus eventos de segurança de soluções de parceiros são automaticamente recolhidos para análise e alerta.

### <a name="detect-threats-and-respond-fast"></a>Detete ameaças e responda com rapidez
Esteja um passo à frente das ameaças atuais e emergentes que surgem na cloud com uma abordagem integrada e voltada para a análise. Ao combinar o Microsoft global [ameaça intelligence](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) e conhecimentos, com informações sobre eventos relacionados com a segurança da nuvem entre as implementações do Azure, o Centro de segurança ajuda-o a detetar ameaças reais numa fase inicial e reduzir os falsos positivos. Alertas de segurança de nuvem dão-lhe informações sobre a campanha de ataque Olá, incluindo eventos relacionados e os recursos afetados e sugerir formas tooremediate problemas e a recuperação rápida.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Monitorização de rede com base no cenário de ponto a ponto
Os clientes criar uma rede ponto a ponto no Azure através da orquestração e composição vários recursos de rede individuais, tais como VNet, ExpressRoute, Gateway de aplicação, balanceadores de carga e muito mais. A monitorização está disponível em cada um dos recursos de rede Olá.

[Observador de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) é um serviço regional que permite-lhe toomonitor e diagnosticar condições num nível do cenário de rede no, a e do Azure. Diagnóstico de rede e ferramentas de visualização disponíveis com o observador de rede ajudam-na compreender, diagnosticar e obter a rede de tooyour insights no Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Automatize a monitorização remota de redes com a captura de pacotes
Monitorizar e diagnosticar problemas de rede sem o registo no tooyour as máquinas virtuais (VMs) com o observador de rede. Acionador [captura de pacotes](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) ao definir alertas e obter informações de desempenho do tempo tooreal de acesso ao nível de pacotes hello. Quando se deparar com um problema, pode investigar em pormenor para obter melhores diagnósticos.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Obtenha informações sobre o seu tráfego de rede com os registos de fluxo
Criar uma compreensão mais aprofundada do seu tráfego de rede padrão com [registos de fluxo do grupo de segurança de rede](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). Informações fornecidas pelo fluxo registos ajudam a recolher dados de conformidade, auditoria e monitorização do seu perfil de segurança de rede.

### <a name="diagnose-vpn-connectivity-issues"></a>Diagnostique problemas da conectividade VPN
Observador de rede fornece Olá capacidade demasiado[diagnosticar os problemas mais comuns de Gateway de VPN e ligações](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Olá, permitindo-lhe não só tooidentify Olá problema, mas também toouse detalhadas de registos criado toohelp mais investigar.

mais informações sobre como toolearn tooconfigure observador de rede e como tooenable, leia o artigo de Olá [configurar observador de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Implementação segura utilizando ferramentas de DevOps comprovadas
Estas são algumas das Olá lista do Azure DevOps práticas neste espaço Microsoft Cloud, o que faz com que as empresas e equipas produtivos e eficiente.

-   **Infraestrutura como código (IaC):** infraestrutura como o código é um conjunto de técnicas e práticas, que ajudam os profissionais de TI remover fardo Olá associado a compilação de tooday Olá dia e a gestão de infraestrutura modular. Isto permite que os profissionais de TI toobuild e manter o respetivo ambiente server moderno de uma forma que é semelhante a forma como os programadores de software criar e manter o código da aplicação. Para o Azure, temos [do Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) permite-lhe tooprovision das suas aplicações com um modelo declarativo. Num único modelo, pode implementar vários serviços, bem como as respetivas dependências. Utilizar Olá mesmo modelo toorepeatedly implementar a aplicação durante cada fase do ciclo de vida de aplicação de Olá.
-   **A integração e a implementação contínua:** pode configurar os Visual Studio Online projetos de equipa demasiado[criar e implementar automaticamente](https://www.visualstudio.com/docs/build/overview) tooAzure web aplicações ou serviços em nuvem. VSO implementa automaticamente binários Olá depois de efetuar uma compilação tooAzure após cada dar entrada no código. Olá pacote compilação processo descrito aqui é equivalente toohello comando do pacote no Visual Studio e passos publicação Olá são equivalentes toohello comandos de publicar no Visual Studio.
-   **Gestão de versões:** Visual Studio [versão gestão](https://msdn.microsoft.com/library/vs/alm/release/overview) é uma excelente solução para automatizar a implementação de vários fase e gerir Olá versão processo. Crie a implementação contínua gerido pipelines toorelease rapidamente, facilmente e frequentemente. Com a gestão de versão, é muito pode automatizar o processo nossa versão e pode ter predefinidas fluxos de trabalho de aprovação. Implementar no local e toohello na nuvem, expandir e personalizar conforme necessário.
-   **Monitorização de desempenho da aplicação:** detetar problemas, resolver problemas e melhorar continuamente as suas aplicações. Diagnostique rapidamente quaisquer problemas na sua aplicação em direto. Compreenda o que os utilizadores fazem com isso. A configuração é fácil independentemente de adicionar código JS e uma entrada de webconfig e verá resultados dentro de minutos no portal de Olá com todos os detalhes de Olá. [Insights aplicação](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) ajuda as empresas deteção mais rápidos de problemas de & remediação.
-   **Carregar teste & dimensionamento automático:** que possa encontrar problemas de desempenho no nosso qualidade de implementação de tooimprove de aplicação e toomake se de que a nossa aplicação está sempre disponível ou se toocater toohello necessidades. Certifique-se a que sua aplicação pode processar o tráfego para a sua campanha de início ou de marketing seguinte. Iniciar a execução de baseado na nuvem [carregar testes](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) em quase sem tempo com o Visual Studio Online.

## <a name="next-steps"></a>Passos seguintes
- Saiba mais sobre [segurança operacionais do Azure](https://docs.microsoft.com/azure/security/azure-operational-security).
- tooLearn mais [Operations Management Suite | Segurança e conformidade](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Introdução ao Operations Management Suite segurança e a solução de auditoria](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).
