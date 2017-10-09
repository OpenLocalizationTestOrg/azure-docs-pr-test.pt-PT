---
title: aaaOptimize ambiente do SQL Server com o Log Analytics do Azure | Microsoft Docs
description: "Análise de registos do Azure, pode utilizar Olá avaliação do SQL Server solução tooassess Olá risco e estado de funcionamento dos seus ambientes de servidor do SQL Server num intervalo regular."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Otimizar o seu ambiente do SQL Server com Olá solução de avaliação do SQL Server na análise de registos

![Símbolo de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

Pode utilizar Olá avaliação do SQL Server solução tooassess Olá risco e estado de funcionamento dos seus ambientes de servidor num intervalo regular. Este artigo irá ajudá-lo a instalar solução Olá, de modo a que possa tomar medidas corretivas para potenciais problemas.

Esta solução fornece uma lista prioritária de infraestrutura de servidor implementado recomendações tooyour específico. recomendações de Olá são categorizadas em seis foco áreas que rapidamente a ajudar a compreender Olá risco e tome as medidas corretivas.

recomendações de Olá efetuadas baseiam-se em conhecimentos Olá e experiência adquiridos por engenheiros de Microsoft de milhares de visitas de cliente. Cada recomendação fornece orientações sobre por que razão poderá importa tooyou a um problema e como tooimplement Olá sugerida alterações.

Pode escolher áreas que são mais importante tooyour organização e controlam o progresso em direção a executar um ambiente de livre e bom estado de funcionamento de risco.

Depois de acrescentar solução Olá e uma avaliação estiver concluída, resumo informações de áreas de foco são apresentadas na Olá **avaliação do SQL Server** dashboard para a infraestrutura de Olá no seu ambiente. Olá secções seguintes descrevem como toouse Olá informações sobre Olá **avaliação do SQL Server** dashboard, onde pode ver e, em seguida, tome as ações para a sua infraestrutura de servidor SQL recomendadas.

![imagem do mosaico de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![imagem do dashboard de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalar e configurar a solução de Olá
Avaliação do SQL Server funciona com todas as versões atualmente suportadas do SQL Server para as edições Standard, Developer e Enterprise do Olá.

Utilize Olá tooinstall informações a seguir e configurar a solução de Olá.

* Os agentes devem ser instalados em servidores que tenham o SQL Server instalada.
* Olá solução de avaliação do SQL Server necessita de uma versão suportada do .NET Framework 4 está instalado em cada computador que tenha um agente do OMS.
* Solução do ordem tooinstall Olá, Olá utilizador tem de ser um administrador ou de contribuinte toohello subscrição do Azure quando utilizar Olá portal do Azure. Além disso, Olá utilizador tem de ser um membro de Olá OMS área de trabalho contribuinte da função ou de administrador no portal do OMS Olá.
* Ao utilizar o agente do Operations Manager Olá com avaliação do SQL Server, terá de toouse uma conta de Run-As do Operations Manager. Consulte [do Operations Manager Run as contas do OMS](#operations-manager-run-as-accounts-for-oms) abaixo para obter mais informações.

  > [!NOTE]
  > agente MMA Olá não suporta contas do Operations Manager Run-As.
  >
  >
* Adicionar tooyour de solução de avaliação do SQL Server Olá área de trabalho do OMS através de Olá processo descrita no [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md). Não há nenhuma configuração adicional.

> [!NOTE]
> Depois de acrescentar solução Olá, o ficheiro de AdvisorAssessment.exe Olá é adicionado tooservers com agentes. Dados de configuração é lido e, em seguida, enviados o serviço OMS toohello na nuvem de Olá para processamento. Lógica é aplicado toohello recebida dados e o serviço em nuvem Olá regista dados de Olá.

## <a name="sql-assessment-data-collection-details"></a>Detalhes de recolha de dados de avaliação do SQL Server
Avaliação do SQL Server recolhe dados WMI, dados de registo, dados de desempenho e SQL Server gestão dinâmica ver os resultados utilizando os agentes de Olá que tiver ativado.

Olá tabela seguinte mostra os métodos de recolha de dados para os agentes, se o Operations Manager (SCOM) é necessário e como muitas vezes, os dados são recolhidos por um agente.

| Plataforma | Direcionar o agente | Agente do SCOM | Storage do Azure | SCOM necessário? | Dados de agente do SCOM enviados através do grupo de gestão | Frequência de recolha |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 dias |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Executar como contas do Operations Manager para OMS
Análise de registos na OMS utiliza Olá agente do Operations Manager e toocollect do grupo de gestão e enviar serviço de dados do toohello OMS. Compilações OMS após os pacotes de gestão para cargas de trabalho tooprovide de valor acrescentado serviços. Cada carga de trabalho necessita de pacotes de gestão de toorun de privilégios específico da carga de trabalho num contexto de segurança diferentes, tais como uma conta de domínio. Terá de informações de credencial tooprovide ao configurar uma conta do Operations Manager Run As.

Utilize Olá seguir informações tooset Olá do Operations Manager conta Run as para avaliação do SQL Server.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Definir Olá conta Run As para avaliação do SQL Server
 Se já estiver a utilizar Olá pacote de gestão do SQL Server, deve utilizar essa conta Run As.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>Olá tooconfigure SQL conta Run as na consola de operações de Olá
> [!NOTE]
> Se estiver a utilizar hello OMS direcionar o agente, em vez do agente do SCOM Olá, o pacote de gestão de Olá sempre é executado no contexto de segurança de Olá de Olá conta do sistema Local. Ignorar os passos 1 a 5 abaixo e execute Olá: exemplo de T-SQL ou o Powershell, especificando NT AUTHORITY\SYSTEM como nome de utilizador Olá.
>
>

1. No Operations Manager, abra a consola de operações de Olá e, em seguida, clique em **administração**.
2. Em **configuração de Run As**, clique em **perfis**e abra **OMS SQL avaliação perfil Run As**.
3. No Olá **contas Run as** página, clique em **adicionar**.
4. Selecione uma conta Run As do Windows que contém as credenciais de Olá necessárias para o SQL Server, ou clique em **novo** toocreate um.

   > [!NOTE]
   > Olá tipo conta Run As tem de ser Windows. Olá conta Run As tem de ser também parte do grupo de administradores Local em todos os servidores do Windows que aloja instâncias do SQL Server.
   >
   >
5. Clique em **Guardar**.
6. Modificar e, em seguida, executar Olá seguinte exemplo de T-SQL em cada instância do SQL Server toogrant permissões mínimas necessária tooRun como conta tooperform avaliação do SQL Server. No entanto, não precisa de toodo isto se uma conta Run As já faz parte da função de servidor sysadmin Olá nas instâncias do SQL Server.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>Olá tooconfigure SQL conta Run as com o Windows PowerShell
Abra uma janela do PowerShell e execute o seguinte script depois atualizou-lo com as suas informações de Olá:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Compreender a forma como as recomendações são prioritários
Cada recomendação efetuada é atribuída um valor de peso que identifica a importância relativa de Olá da recomendação Olá. São apresentadas apenas Olá dez mais importantes recomendações.

### <a name="how-weights-are-calculated"></a>Como são calculadas ponderações
As ponderações são valores de agregação com base nas três principais fatores:

* Olá *probabilidade* que um problema identificado causará problemas. Uma probabilidade superior equivale tooa maior pontuação geral para recomendação Olá.
* Olá *impacto* problema Olá na sua organização se provocar um problema. Um impacto superior equivale tooa maior pontuação geral para recomendação Olá.
* Olá *esforço* necessário recomendação de Olá tooimplement. Um maior esforço equivale tooa pontuação geral mais pequenas de recomendação Olá.

Olá weighting para cada recomendação é expresso como uma percentagem da classificação total Olá disponíveis para cada área de foco. Por exemplo, se uma recomendação na área de foco de conformidade e segurança de Olá tem uma pontuação de 5%, implementar dessa recomendação irá aumentar a sua geral de segurança e conformidade pontuação por 5%.

### <a name="focus-areas"></a>Áreas de foco
**Segurança e conformidade** -esta área de foco mostra recomendações para potenciais ameaças de segurança e falhas, políticas empresariais e requisitos de conformidade técnicos, jurídicos e regulamentares.

**Disponibilidade e continuidade do negócio** -esta área de foco mostra recomendações para a disponibilidade do serviço, a resiliência da sua infraestrutura e a proteção do negócio.

**Desempenho e escalabilidade** -esta área de foco mostra toohelp recomendações da sua organização infraestrutura de TI aumentar, certifique-se de que o ambiente de TI cumpre os requisitos de desempenho atuais e é capaz de toorespond toochanging Tem a infraestrutura.

**Atualizar, implementação e migração** - esta área de foco mostra toohelp recomendações atualizar, migrar e implementar a infraestrutura existente do SQL Server tooyour.

**Operações e monitorização** - esta área de foco mostra recomendações toohelp otimizar as operações de TI implementar manutenção preventiva e maximizar o desempenho.

**Gestão de configuração e alteração** -esta área de foco mostra recomendações toohelp Proteja as operações diárias, certifique-se de que as alterações não negativamente afetam a sua infraestrutura, estabeleça procedimentos de controlo de alterações e tootrack e de auditoria configurações do sistema.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Deve, procure tooscore 100% cada área de foco?
Não necessariamente. recomendações de Olá baseiam-se em conhecimentos Olá e experiências adquiridas por engenheiros Microsoft entre milhares de visitas de cliente. No entanto, nenhum infraestruturas de duas servidor são Olá mesmo e ver as recomendações específicas podem ser maior ou menor relevante tooyou. Por exemplo, algumas recomendações de segurança poderão ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet. Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem a recolha de dados ad hoc de baixa prioridade e relatórios. Problemas que sejam negócio madura tooa importante poderão ser menos importante tooa arranque. Poderá pretender tooidentify áreas que são as prioridades e, em seguida, observar como as pontuações alteram ao longo do tempo.

Cada recomendação inclui orientações sobre por que motivo é importante. Deve utilizar esta orientação tooevaluate se implementar a recomendação de Olá é adequada para si, dada natureza Olá sua TI Olá e serviços empresariais precisam da sua organização.

## <a name="use-assessment-focus-area-recommendations"></a>Utilize as recomendações de área de foco de avaliação
Antes de poder utilizar uma solução de avaliação na OMS, tem de ter solução Olá instalada. tooread mais sobre a instalação de soluções, consulte [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md). Depois de ser instalado, pode ver o resumo de Olá das recomendações utilizando o mosaico de avaliação do SQL Server Olá na página de descrição geral de Olá no OMS.

Olá vista resumida avaliações de conformidade para a sua infraestrutura e, em seguida, desagregação em recomendações.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendações de tooview para um foco área e Adote as medidas corretivas
1. No Olá **descrição geral** página, clique em Olá **avaliação do SQL Server** mosaico.
2. No Olá **avaliação do SQL Server** página, reveja as informações de resumo de Olá dos painéis de área de foco Olá e, em seguida, clique numa tooview recomendações para essa área de foco.
3. Em qualquer uma das páginas de área de foco Olá, pode ver as recomendações de Olá definida efetuadas para o seu ambiente. Clique numa recomendação em **Objetos afetados** tooview detalhes sobre a razão pela qual Olá recomendação é feita.  
    ![Imagem das recomendações de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. Pode executar ações corretivas sugeridas na **as ações sugeridas**. Quando tem sido resolvida item Olá, irão registar avaliações posteriores ações foram executadas e o modelo de pontuação de conformidade aumentam recomendadas. Itens corrigidas aparecem como **transmitido objetos**.

## <a name="ignore-recommendations"></a>Ignorar as recomendações
Se tiver recomendações que pretende que o tooignore, pode criar um ficheiro de texto que OMS utilizará tooprevent recomendações a apresentação nos resultados da avaliação.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recomendações de tooidentify que irão ignorar
1. Iniciar sessão na área de trabalho tooyour e abrir o registo de pesquisa. Utilize Olá seguir as recomendações de toolist de consulta que falharam por computadores no seu ambiente.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Segue-se uma consulta de pesquisa de registo que de captura de ecrã mostra Olá: ![falha recomendações](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Escolha as recomendações que pretende que o tooignore. Irá utilizar valores de Olá para RecommendationId no procedimento seguinte Olá.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e utilizar um ficheiro de texto IgnoreRecommendations.txt
1. Crie um ficheiro denominado IgnoreRecommendations.txt.
2. Colar ou escreva cada RecommendationId para cada recomendação pretende OMS tooignore numa linha separada e, em seguida, guarde e feche o ficheiro de Olá.
3. Coloque o ficheiro Olá no Olá seguir pasta em cada computador onde pretende que as recomendações de tooignore OMS.
   * Em computadores com Olá Microsoft Monitoring Agent (ligado diretamente ou através do Operations Manager) - *SystemDrive*: \Programas\Microsoft Agent\Agent de monitorização
   * No servidor de gestão do Operations Manager Olá - *SystemDrive*: \Programas\Microsoft System Center 2012 R2\Operations \ Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que recomendações são ignoradas
1. Após a execução de Olá avaliação agendada seguinte, por predefinição, 7 dias, Olá especificados recomendações são marcadas ignoradas e não serão apresentados no dashboard de avaliação de Olá.
2. Pode utilizar Olá seguir toolist de consultas de pesquisa de registo todas as recomendações de Olá ignorada.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Se, posteriormente, decida que pretende que as recomendações de toosee ignorado, remova quaisquer ficheiros IgnoreRecommendations.txt ou pode remover RecommendationIDs dos mesmos.

## <a name="sql-assessment-solution-faq"></a>Solução de avaliação do SQL Server FAQ
*Frequência executa uma avaliação?*

* avaliação de Olá é executado a cada 7 dias.

*Existe um tooconfigure de forma com que frequência avaliação Olá executa?*

* Neste momento, não.

*Se for detetado o outro servidor após posso adicionou Olá solução de avaliação do SQL Server, será-avaliada?*

* Sim, quando é detetado, é avaliado em matéria de, em seguida, no, 7 dias.

*Se um servidor é encerrado, quando irá este ser removido do assessment Olá?*

* Se um servidor não submeter dados durante 3 semanas, este é removido.

*O que é o nome de Olá do processo de Olá Olá a recolha de dados?*

* AdvisorAssessment.exe

*Quanto tempo demora para toobe dados recolhido?*

* recolha de dados real de Olá no servidor de Olá demora cerca de 1 hora. Pode demorar mais em servidores que tenham um grande número de instâncias do SQL Server ou bases de dados.

*Que tipo de dados é recolhido?*

* Olá, os seguintes tipos de dados é recolhido:
  * WMI
  * Registo
  * Contadores de desempenho
  * Vistas de gestão dinâmica do SQL Server (DMV).

*Existe uma forma tooconfigure quando são recolhidos os dados?*

* Neste momento, não.

*Por que motivo tenho tooconfigure uma conta Run As?*

* Para o SQL Server, um pequeno número de consultas SQL é executado. Serem toorun, uma conta Run As com VIEW SERVER STATE permissões tooSQL tem de ser utilizado.  Além disso, na ordem tooquery WMI, as credenciais de administrador local são necessárias.

*Por que motivo apresentar apenas recomendações de 10 principais de Olá?*

* Em vez de dando-lhe uma lista exaustiva muito confuso das tarefas, recomendamos que lhe concentrar-se no endereçamento recomendações Olá definida primeiro. Depois de resolvê-los, recomendações adicionais deixará de estar disponíveis. Se preferir lista detalhada de Olá toosee, pode ver todas as recomendações com pesquisa de registo do Olá OMS.

*Existe uma forma tooignore uma recomendação?*

* Sim, consulte [ignorar recomendações](#ignore-recommendations) secção acima.

## <a name="next-steps"></a>Passos seguintes
* [Pesquisar registos](log-analytics-log-searches.md) tooview detalhadas dados da avaliação do SQL Server e as recomendações.
