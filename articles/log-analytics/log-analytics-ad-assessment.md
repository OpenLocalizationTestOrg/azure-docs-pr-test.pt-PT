---
title: aaaOptimize o ambiente do Active Directory com o Log Analytics do Azure | Microsoft Docs
description: "Pode utilizar Olá avaliação de diretório Active Directory solução tooassess Olá risco e estado de funcionamento dos seus ambientes de servidor num intervalo regular."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Otimizar o seu ambiente do Active Directory com Olá solução de avaliação do Active Directory na análise de registos

![Símbolo de avaliação do AD](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Pode utilizar Olá avaliação de diretório Active Directory solução tooassess Olá risco e estado de funcionamento dos seus ambientes de servidor num intervalo regular. Este artigo ajuda-o a instalar e utilizar a solução de Olá, de modo a que possa tomar medidas corretivas para potenciais problemas.

Esta solução fornece uma lista prioritária de infraestrutura de servidor implementado recomendações tooyour específico. recomendações de Olá são categorizadas em foco quatro áreas, que rapidamente a ajudar a compreender Olá risco e tomar medidas.

recomendações de Olá baseiam-se em conhecimentos Olá e experiência adquiridos por engenheiros de Microsoft de milhares de visitas de cliente. Cada recomendação fornece orientações sobre por que razão poderá importa tooyou a um problema e como tooimplement Olá sugerida alterações.

Pode escolher áreas que são mais importante tooyour organização e controlam o progresso em direção a executar um ambiente de livre e bom estado de funcionamento de risco.

Depois de acrescentar solução Olá e uma avaliação estiver concluída, resumo informações de áreas de foco são apresentadas na Olá **AD avaliação** dashboard para a infraestrutura de Olá no seu ambiente. Olá secções seguintes descrevem como toouse Olá informações sobre Olá **AD avaliação** dashboard, onde pode ver e, em seguida, tome as ações para a sua infraestrutura de servidor do Active Directory recomendadas.

![imagem do mosaico de avaliação do SQL Server](./media/log-analytics-ad-assessment/ad-tile.png)

![imagem do dashboard de avaliação do SQL Server](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalar e configurar a solução de Olá
Utilize Olá tooinstall informações a seguir e configurar Olá soluções.

* Os agentes devem ser instalados em controladores de domínio que são membros de Olá domínio toobe avaliada.
* Olá Active Directory avaliação, a solução requer uma versão suportada do .NET Framework 4 (4.5.2 ou posterior) instalado em cada computador que tenha um agente do OMS.
* Adicionar Olá avaliação do Active Directory solução tooyour OMS área de trabalho de [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).  Não há nenhuma configuração adicional.

  > [!NOTE]
  > Depois de acrescentar solução Olá, o ficheiro de AdvisorAssessment.exe Olá é adicionado tooservers com agentes. Dados de configuração é lido e, em seguida, enviados o serviço OMS toohello na nuvem de Olá para processamento. Lógica é aplicado toohello recebida dados e o serviço em nuvem Olá regista dados de Olá.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Detalhes de recolha de dados de avaliação de diretório Active Directory

Avaliação do Active Directory recolhe dados de Olá as seguintes origens com agentes de Olá que tiver ativado:

- Recoletores de registo
- Recoletores LDAP
- .NET framework
- Recoletores de registos de eventos
- Interfaces de serviço do Active Directory (ADSI)
- Windows PowerShell
- Recoletores de dados de ficheiro
- Windows Management Instrumentation (WMI)
- Ferramenta DCDIAG API
- API de serviço (NTFRS) de replicação de ficheiros
- Código personalizado c#


Olá tabela seguinte mostra os métodos de recolha de dados para os agentes, se o Operations Manager (SCOM) é necessário e como muitas vezes, os dados são recolhidos por um agente.

| Plataforma | Direcionar o agente | Agente do SCOM | Storage do Azure | SCOM necessário? | Dados de agente do SCOM enviados através do grupo de gestão | Frequência de recolha |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 dias |

## <a name="understanding-how-recommendations-are-prioritized"></a>Compreender a forma como as recomendações são prioritários
Cada recomendação efetuada é atribuída um valor de peso que identifica a importância relativa de Olá da recomendação Olá. Recomendações mais importantes de Olá 10 apenas são apresentadas.

### <a name="how-weights-are-calculated"></a>Como são calculadas ponderações
As ponderações são valores de agregação com base nas três principais fatores:

* Olá *probabilidade* que um problema identificado provoca problemas. Uma probabilidade superior equivale tooa maior pontuação geral para recomendação Olá.
* Olá *impacto* problema Olá na sua organização se provocar um problema. Um impacto superior equivale tooa maior pontuação geral para recomendação Olá.
* Olá *esforço* necessário recomendação de Olá tooimplement. Um maior esforço equivale tooa pontuação geral mais pequenas de recomendação Olá.

Olá weighting para cada recomendação é expresso como uma percentagem da classificação total Olá disponíveis para cada área de foco. Por exemplo, se uma recomendação na área de foco de conformidade e segurança de Olá tem uma pontuação de 5%, implementar dessa recomendação aumenta o geral de segurança e conformidade pontuação por 5%.

### <a name="focus-areas"></a>Áreas de foco
**Segurança e conformidade** -esta área de foco mostra recomendações para potenciais ameaças de segurança e falhas, políticas empresariais e requisitos de conformidade técnicos, jurídicos e regulamentares.

**Disponibilidade e continuidade do negócio** -esta área de foco mostra recomendações para a disponibilidade do serviço, a resiliência da sua infraestrutura e a proteção do negócio.

**Desempenho e escalabilidade** -esta área de foco mostra toohelp recomendações da sua organização infraestrutura de TI aumentar, certifique-se de que o ambiente de TI cumpre os requisitos de desempenho atuais e é capaz de toorespond toochanging Tem a infraestrutura.

**Atualizar, implementação e migração** - esta área de foco mostra toohelp recomendações atualizar, migrar e implementar a infraestrutura existente do Active Directory tooyour.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Deve, procure tooscore 100% cada área de foco?
Não necessariamente. recomendações de Olá baseiam-se em conhecimentos Olá e experiências adquiridas por engenheiros Microsoft entre milhares de visitas de cliente. No entanto, nenhum infraestruturas de duas servidor são Olá mesmo e ver as recomendações específicas podem ser maior ou menor relevante tooyou. Por exemplo, algumas recomendações de segurança poderão ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet. Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem a recolha de dados ad hoc de baixa prioridade e relatórios. Problemas que sejam negócio madura tooa importante poderão ser menos importante tooa arranque. Poderá pretender tooidentify áreas que são as prioridades e, em seguida, observar como as pontuações alteram ao longo do tempo.

Cada recomendação inclui orientações sobre por que motivo é importante. Deve utilizar esta orientação tooevaluate se implementar a recomendação de Olá é adequada para si, dada natureza Olá sua TI Olá e serviços empresariais precisam da sua organização.

## <a name="use-assessment-focus-area-recommendations"></a>Utilize as recomendações de área de foco de avaliação
Antes de poder utilizar uma solução de avaliação na OMS, tem de ter solução Olá instalada. tooread mais sobre a instalação de soluções, consulte [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md). Depois de ser instalado, pode ver o resumo de Olá das recomendações utilizando o mosaico de avaliação de Olá na página de descrição geral de Olá no OMS.

Olá vista resumida avaliações de conformidade para a sua infraestrutura e, em seguida, desagregação em recomendações.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendações de tooview para um foco área e Adote as medidas corretivas
1. No Olá **descrição geral** página, clique em Olá **avaliação** mosaico para a sua infraestrutura de servidor.
2. No Olá **avaliação** página, reveja as informações de resumo de Olá dos painéis de área de foco Olá e, em seguida, clique numa tooview recomendações para essa área de foco.
3. Em qualquer uma das páginas de área de foco Olá, pode ver as recomendações de Olá definida efetuadas para o seu ambiente. Clique numa recomendação em **Objetos afetados** tooview detalhes sobre a razão pela qual Olá recomendação é feita.  
    ![Imagem das recomendações de avaliação](./media/log-analytics-ad-assessment/ad-focus.png)
4. Pode executar ações corretivas sugeridas na **as ações sugeridas**. Quando tem sido resolvida item Olá, registos de avaliações posteriores que as ações recomendadas foram executados e irá aumentar a sua pontuação de conformidade. Itens corrigidas aparecem como **transmitido objetos**.

## <a name="ignore-recommendations"></a>Ignorar as recomendações
Se tiver recomendações que pretende que o tooignore, pode criar um ficheiro de texto que OMS utilizará tooprevent recomendações a apresentação nos resultados da avaliação.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recomendações de tooidentify que irão ignorar
1. Iniciar sessão na área de trabalho tooyour e abrir o registo de pesquisa. Utilize Olá seguir as recomendações de toolist de consulta que falharam por computadores no seu ambiente.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consulta alteraria toohello seguinte.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Segue-se uma consulta de pesquisa de registo que de captura de ecrã mostra Olá: ![falha recomendações](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Escolha as recomendações que pretende que o tooignore. Irá utilizar valores de Olá para RecommendationId no procedimento seguinte Olá.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e utilizar um ficheiro de texto IgnoreRecommendations.txt
1. Crie um ficheiro denominado IgnoreRecommendations.txt.
2. Colar ou escreva cada RecommendationId para cada recomendação pretende tooignore de análise de registos numa linha separada e, em seguida, guarde e feche o ficheiro de Olá.
3. Coloque o ficheiro Olá no Olá seguir pasta em cada computador onde pretende que as recomendações de tooignore OMS.
   * Em computadores com Olá Microsoft Monitoring Agent (ligado diretamente ou através do Operations Manager) - *SystemDrive*: \Programas\Microsoft Agent\Agent de monitorização
   * No servidor de gestão do Operations Manager Olá - *SystemDrive*: \Programas\Microsoft System Center 2012 R2\Operations \ Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que recomendações são ignoradas
Após a execução de Olá avaliação agendada seguinte, por predefinição, 7 dias, Olá especificado recomendações são marcadas *ignoradas* e não serão apresentados no dashboard de avaliação de Olá.

1. Pode utilizar Olá seguir toolist de consultas de pesquisa de registo todas as recomendações de Olá ignorada.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consulta alteraria toohello seguinte.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Se, posteriormente, decida que pretende que as recomendações de toosee ignorado, remova quaisquer ficheiros IgnoreRecommendations.txt ou pode remover RecommendationIDs dos mesmos.

## <a name="ad-assessment-solutions-faq"></a>Soluções de avaliação do AD FAQ
*Frequência executa uma avaliação?*

* avaliação de Olá é executado a cada 7 dias.

*Existe um tooconfigure de forma com que frequência avaliação Olá executa?*

* Neste momento, não.

*Se for detetado o outro servidor para depois posso adicionou uma solução de avaliação, irá este ser avaliado em matéria?*

* Sim, quando é detetado, é avaliado em matéria de, em seguida, no, 7 dias.

*Se um servidor é encerrado, quando irá este ser removido do assessment Olá?*

* Se um servidor não submeter dados durante 3 semanas, este é removido.

*O que é o nome de Olá do processo de Olá Olá a recolha de dados?*

* AdvisorAssessment.exe

*Quanto tempo demora para toobe dados recolhido?*

* recolha de dados real de Olá no servidor de Olá demora cerca de 1 hora. Pode demorar mais em servidores que tenham um grande número de servidores do Active Directory.

*Existe uma forma tooconfigure quando são recolhidos os dados?*

* Neste momento, não.

*Por que motivo apresentar apenas recomendações de 10 principais de Olá?*

* Em vez de dando-lhe uma lista exaustiva muito confuso das tarefas, recomendamos que lhe concentrar-se no endereçamento recomendações Olá definida primeiro. Depois de resolvê-los, recomendações adicionais deixará de estar disponíveis. Se preferir lista detalhada de Olá toosee, pode ver todas as recomendações com pesquisa de registo.

*Existe uma forma tooignore uma recomendação?*

* Sim, consulte [ignorar recomendações](#ignore-recommendations) secção acima.

## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados da avaliação do AD e recomendações.
