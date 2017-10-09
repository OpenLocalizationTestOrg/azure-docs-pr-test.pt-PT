---
title: "as soluções de gestão do aaaAdd Log Analytics do Azure | Microsoft Docs"
description: "Operations Management Suite (OMS) soluções de gestão de análise de registos são uma coleção de regras de aquisição lógica, visualização e os dados que fornecem métricas pivoted em torno de uma área de problema específico."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Adicione a área de trabalho do Log Analytics do Azure management soluções tooyour

Soluções de gestão de análise do registo são uma coleção de **lógica**, **visualização**, e **regras de aquisição de dados** que fornece métricas pivoted em torno de um determinado área de problema. Este artigo apresenta uma lista de soluções de gestão suportadas pela análise de registos e mostra-lhe como tooadd e remover para uma área de trabalho utilizando Olá portal do Azure. Também pode adicionar soluções no portal do OMS Olá utilizando Olá soluções galeria.

Soluções de gestão permitem a informações mais aprofundadas para:

* Ajudar a investigar e resolver problemas operacionais mais rápida
* Recolher e correlacionar vários tipos de dados da máquina
* Ajudar a ser proativa com atividades que expõe solução Olá.

> [!NOTE]
> Análise de registos inclui funcionalidades de pesquisa de registo, por isso não terá de tooinstall um tooenable da solução de gestão-lo. No entanto, obter visualizações de dados, pesquisa sugerida e insights, adicionando a área de trabalho de tooyour de soluções de gestão.

Utilizar este artigo, adicione área tooa soluções de gestão utilizando Olá portal do Azure Marketplace. Depois de adicionar uma solução, os dados são recolhidos a partir de servidores de Olá na sua infraestrutura e enviados do serviço do toohello OMS. A processar por Olá serviço OMS demora, normalmente, a hora de tooan alguns minutos. Depois do serviço de Olá processa dados Olá, que o possa visualizar na OMS.

Pode remover facilmente uma solução de gestão quando este já não é necessário. Quando remover uma solução de gestão, os dados não são enviados tooOMS. Se estiverem em Olá livres escalão de preço, remover uma solução pode reduzir a quantidade de Olá de dados utilizados, ajudando-o a se manter no quota diária de dados.

## <a name="view-available-management-solutions"></a>Soluções de gestão disponíveis de vista

Hello do Azure marketplace contém Olá lista de [soluções de gestão para análise de registos](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Pode instalar as soluções de gestão do Azure marketplace, clicando em Olá **obtê-lo agora** ligação na parte inferior de Olá de cada solução.

## <a name="add-a-management-solution"></a>Adicionar uma solução de gestão
1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com) através da sua subscrição do Azure.
2. No Olá **novo** painel em **Marketplace**, selecione **monitorização + gestão**.
3. No Olá **monitorização + gestão** painel, clique em **ver todos os**.  
    ![Monitorização + painel de gestão](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello à direita dos **soluções de gestão**, clique em **mais**.
5. No Olá **soluções de gestão** painel, selecione uma solução de gestão que pretende que a área de trabalho do tooadd tooa.  
    ![Monitorização + painel de gestão](./media/log-analytics-add-solutions/management-solutions.png)  
6. No painel de solução de gestão de Olá, reveja as informações sobre a solução de gestão de Olá e, em seguida, clique em **criar**.
7. No Olá *nome da solução de gestão* painel, selecione uma área de trabalho que pretende que o tooassociate solução de gestão de Olá.
8. Opcionalmente, altere as definições da área de trabalho para Olá subscrição do Azure, grupo de recursos e localização. Também pode optar por **opções de automatização**. Clique em **Criar**.  
    ![área de trabalho da solução](./media/log-analytics-add-solutions/solution-workspace.png)  
9. toostart utilizando a solução de gestão de Olá que adicionou tooyour área de trabalho, navegue até demasiado**Log Analytics** > **subscrições** > ***nome da área de trabalho ***  >  **Descrição geral**. É apresentado um novo mosaico da sua solução de gestão. Clique em Olá mosaico tooopen-lo e começar a utilizar a solução de Olá após a recolha de dados para a solução de Olá.

## <a name="remove-a-management-solution"></a>Remover uma solução de gestão

1. No Olá [portal do Azure](https://portal.azure.com), navegue até demasiado**Log Analytics** > **subscrições** > ***nome da área de trabalho*** e, em seguida, no Olá ***nome da área de trabalho*** painel, clique em **soluções**.
2. Na lista de Olá das soluções de gestão, selecione solução Olá que pretende que o tooremove.
3. No painel de solução Olá para a sua área de trabalho, clique em **eliminar**.  
    ![eliminar a solução](./media/log-analytics-add-solutions/solution-delete.png)  
4. Na caixa de diálogo de confirmação Olá, clique em **Sim**.

## <a name="offers-and-pricing-tiers"></a>Ofertas e escalões de preços

Olá, a tabela seguinte identifica as soluções de gestão pertencem a oferta do tooeach Operations Management Suite.
tabela de Olá também identifica Olá escalões que estão disponíveis para cada solução de gestão de preço.
Estão disponíveis a partir da Olá Azure portal e Olá soluções da galeria no portal de análise de registos de Olá todas as soluções no Olá a tabela seguinte.

| Solução de gestão                                                                       | Oferta                                                                     | Escalões de preço<sup>1</sup>                                                 | Notas |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Log Analytics da Atividade](log-analytics-activity.md)                                                                   | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | 90 dias de dados estão disponíveis gratuitamente<br>Dados não do requerente toohello extremidade de escalão gratuito |
| [Avaliação do AD](log-analytics-ad-assessment.md)                                           | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Estado de Replicação do AD](log-analytics-ad-replication-status.md)                           | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Não está disponível tooadd do portal do Azure/marketplace. |
| [Agente de Funcionamento de Agente](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Dados não do requerente toohello extremidade de escalão gratuito<br> Não está disponível tooadd do portal do Azure/marketplace. |
| [Gestão de Alertas](log-analytics-solution-alert-management.md)                            | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Não está disponível tooadd do portal do Azure/marketplace. |
| [Conector do Application Insights (pré-visualização)](log-analytics-app-insights-connector.md)                                               | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Automatização de trabalho híbrida](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automatização e controlo</li></ul>                                  | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe ligado de área de trabalho de análise de registos conta de automatização |
| [Análise de Gateway de aplicação do Azure](log-analytics-azure-networking-analytics.md)    | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Análise de grupo de segurança de rede do Azure](log-analytics-azure-networking-analytics.md)     | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Análise de SQL do Azure (pré-visualização)](log-analytics-azure-sql.md)                                                       | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br>Por&nbsp;nó&nbsp;(OMS)                                                                          | Requer o tooan de toobe ligado de área de trabalho de análise de registos conta de automatização|
| [Análise de Aplicações Web do Azure](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
|[Cópia de segurança](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Conhecimentos aprofundados e análise</li></ul>                                   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)                                                                       | Necessita de um cofre de cópia de segurança clássico.<br> Não está disponível tooadd do portal do Azure/marketplace. |
| [Capacidade e o desempenho (pré-visualização)](log-analytics-capacity.md)                                                   | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Monitorização de Alterações](log-analytics-change-tracking.md)                                       | <ul><li>Automatização e controlo</li></ul>                                  | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe ligado de área de trabalho de análise de registos conta de automatização |
| [Contentores](log-analytics-containers.md)                                                 | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [IT Service conector de gestão (pré-visualização)](log-analytics-itsmc-overview.md)                                              | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)     | |
| Monitorização de HBase do HDInsight <br>(Pré-visualização)                                                  | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Análise do Cofre de Chaves](log-analytics-azure-key-vault.md)                   | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Não está disponível tooadd do portal do Azure/marketplace. |
| [Avaliação de Software Maligno](log-analytics-malware.md)                                            | <ul><li>Segurança e Conformidade</li></ul>                                 | Gratuito<br> Autónomo<br>Por&nbsp;nó&nbsp;(OMS)                                                                           | Se adicionar soluções de segurança e conformidade Olá após 19 de Junho de 2017 [faturação seja por nó](https://azure.microsoft.com/pricing/details/security-compliance/), independentemente da área de trabalho Olá escalão de preço. Olá primeiro 60 dias são gratuitos.  |
| [Monitor de Desempenho da Rede](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Conhecimentos aprofundados e análise</li></ul>                                   | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | |
| [Análise do Office 365 (pré-visualização)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Auditoria e segurança](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Segurança&nbsp;e&nbsp;conformidade</li></ul>                       | Gratuito<br> Autónomo<br>Por&nbsp;nó&nbsp;(OMS)                                                                           | Recolher registos de eventos de segurança requer que esta solução<br>Se adicionar soluções de segurança e conformidade Olá após 19 de Junho de 2017 [faturação seja por nó](https://azure.microsoft.com/pricing/details/security-compliance/), independentemente da área de trabalho Olá escalão de preço. Olá primeiro 60 dias são gratuitos. |
| [Análise de recursos de infraestrutura de serviço (pré-visualização)](log-analytics-service-fabric.md)                     | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Mapa de serviço (pré-visualização)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Conhecimentos aprofundados e análise</li></ul>                      | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | Disponível nos EUA leste, Europa Ocidental e EUA Centro Oeste    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Conhecimentos aprofundados e análise</li></ul>                                   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)                                                                       | Necessita de um cofre de recuperação de Site clássico.<br> Não está disponível tooadd do portal do Azure/marketplace. |
| [Avaliação do SQL](log-analytics-sql-assessment.md)                                         | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| Iniciar/Parar VMs durante horas de inatividade<br>(Pré-visualização)                                              | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe ligado de área de trabalho de análise de registos conta de automatização |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Não está disponível tooadd do portal do Azure/marketplace. |
| [O System Center Operations Manager Assessment (pré-visualização)](log-analytics-scom-assessment.md)  | <ul><li>Conhecimentos aprofundados e análise</li><li>Log Analytics</li></ul>        | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Gestão de Atualizações](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automatização e controlo</li></ul>                                  | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe ligado de área de trabalho de análise de registos conta de automatização |
| [Conformidade de atualização (pré-visualização)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Sem encargos de dados ou nós<br>Não, os dados do requerente toohello extremidade de escalão gratuito.<br> Não está disponível tooadd do portal do Azure/marketplace. |
| [Atualizar Preparação](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | Sem encargos de dados ou nós<br>Não, os dados do requerente toohello extremidade de escalão gratuito.<br> Não está disponível tooadd do portal do Azure/marketplace. |
| [VMware monitorização (pré-visualização)](log-analytics-vmware.md)                                | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(autónomo)<br> Por&nbsp;nó&nbsp;(OMS)   | |
| [Dados por fio 2.0 (pré-visualização)](log-analytics-wire-data.md)                                                                 | <ul><li>Conhecimentos aprofundados e análise</li></ul>                                   | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)                                                                         | Disponível nos EUA leste, Europa Ocidental e EUA Centro Oeste |

<sup>1</sup> Olá *padrão* e *Premium (OMS)* escalões de preço só estão disponível para os clientes que criou os respetivos tooSeptember-anterior de área de trabalho de análise de registos 21, 2016.

### <a name="community-provided-management-solutions"></a>Comunidade fornecida soluções de gestão

Soluções de Comunidade fornecida estão disponíveis no Olá [Galeria de modelo do Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) e direta de autores Olá.

| Solução de gestão               | Oferta                                                                     | Escalões de preço                         | Notas |
| ---                               | ---                                                                       | ---                                   | ---   |
| Todas as soluções de Comunidade fornecida  | <ul><li>Conhecimentos aprofundados&nbsp;e&nbsp;análise</li><li>Log Analytics</li></ul>   | Gratuito<br> Por&nbsp;nó&nbsp;(OMS)     |   Requer o tooan de toobe ligado de área de trabalho de análise de registos conta de automatização |




## <a name="data-collection-details"></a>Detalhes de recolha de dados
Olá tabelas seguintes mostram os métodos de recolha de dados e outros detalhes sobre como os dados são recolhidos para origens de dados e soluções de gestão de análise de registos. Olá tabelas são categorizadas por ofertas de solução, o que equacionar demasiado[subscrição escalões de preço](https://go.microsoft.com/fwlink/?linkid=827926). Olá solução de análise de registos de atividade é tooall disponível gratuitas escalões de preço.

Olá, o agente do Windows de análise do registo e hello do System Center Operations Manager agente são essencialmente iguais. o agente do Windows Hello inclui funcionalidades adicionais tooallow-tooconnect toohello OMS área de trabalho e encaminhar através de um proxy. Se utilizar um agente do Operations Manager, tem de ser visada como um toocommunicate de agente do OMS com o OMS. Agentes do Operations Manager nesta tabela são agentes do OMS que estão ligados tooOperations Manager. Consulte [ligar o Operations Manager tooLog análise](log-analytics-om-agents.md) para obter informações sobre como ligar o seu ambiente tooOMS existente do Operations Manager.

> [!NOTE]
> tipo de Olá do agente que utilizar determina a forma como são enviados dados tooOMS, com Olá seguintes condições:
> - Pode utiliza o agente do Windows hello ou um agente do OMS anexado no Operations Manager.
> - Quando o Operations Manager é necessário, dados de agente do Operations Manager para a solução de Olá é sempre enviados tooOMS utilizando o grupo de gestão do Operations Manager Olá. Além disso, quando o Operations Manager é necessário, apenas o agente do Gestor de operações Olá é utilizado pela solução de Olá.
> - Quando o Operations Manager não é necessário e tabela de Olá mostra o envio de dados de agente do Operations Manager tooOMS utilizando o grupo de gestão de Olá, em seguida, dados de agente do Operations Manager é sempre enviado tooOMS utilizando grupos de gestão. Agentes Windows ignorar o grupo de gestão de Olá e enviar os seus dados tooOMS diretamente.
> - Quando os dados de agente do Operations Manager não são enviados através de um grupo de gestão, em seguida, Olá dados são enviados diretamente tooOMS — ignorando o grupo de gestão de Olá.

### <a name="insight--analytics--log-analytics"></a>Conhecimentos aprofundados & análise / análise de registo

| Solução de gestão | Plataforma | Agente de monitorização da Microsoft | Agente do Operations Manager | Storage do Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Log Analytics de Atividades | Azure |   |   |   |   |   | na notificação |
| Avaliação do AD |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dias |
| Estado de Replicação do AD |Windows |&#8226; |&#8226; |  |  |&#8226; |5 dias |
| Estado de Funcionamento do Agente | Windows e Linux | &#8226; | &#8226; |   |   | &#8226; | um minuto |
| Gestão de alertas (da Nagios) |Linux |&#8226; |  |  |  |  |sobre chegada |
| Gestão de alertas (da Zabbix) |Linux |&#8226; |  |  |  |  |um minuto |
| Gestão de alertas (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minutos |
| Conector do Application Insights (pré-visualização) | Azure |   |   |   |   |   | na notificação |
| Análise de Gateway de aplicação do Azure | Azure |   |   |   |   |   | na notificação |
| Análise de grupo de segurança de rede do Azure | Azure |   |   |   |   |   | na notificação |
| Análise de SQL do Azure (pré-visualização) |Windows |  |  |  |  |  | 10 minutos |
| Gestão de Capacidade |Windows |&#8226; |&#8226; |  |  |&#8226; |sobre chegada |
| Contentores | Windows e Linux | &#8226; | &#8226; |   |   |   | 3 minutos |
| Análise do Cofre de chaves |Windows |  |  |  |  |  |na notificação |
| Monitor de Desempenho da Rede | Windows | &#8226; | &#8226; |   |   |   | TCP handshakes a cada cinco segundos, dados enviados a cada 3 minutos |
| Análise do Office 365 (pré-visualização) |Windows |  |  |  |  |  |na notificação |
| Análise de recursos de infraestrutura de serviço |Windows |  |  |&#8226; |  |  |5 minutos |
| Mapa de Serviços | Windows e Linux | &#8226; | &#8226; |   |   |   | 15 segundos |
| Avaliação do SQL |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dias |
| SurfaceHub |Windows |&#8226; |  |  |  |  |sobre chegada |
| O System Center Operations Manager Assessment (pré-visualização) | Windows | &#8226; | &#8226; |   |   | &#8226; | sete dias |
| Análise de atualização (pré-visualização) | Windows | &#8226; |   |   |   |   | 2 dias |
| VMware monitorização (pré-visualização) | Linux | &#8226; |   |   |   |   | 3 minutos |
| Ligar Dados |Windows (2012 R2 / 8.1 ou posterior) |&#8226; |&#8226; |  |  |  | um minuto |


### <a name="automation--control"></a>Automatização e controlo

| Solução de gestão | Plataforma | Agente de monitorização da Microsoft | Agente do Operations Manager | Storage do Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Automatização de trabalho híbrida | Windows | &#8226; | &#8226; |   |   |   | n/d |
| Monitorização de Alterações |Windows |&#8226; |&#8226; |  |  |&#8226; |hora a hora |
| Monitorização de Alterações |Linux |&#8226; |  |  |  |  |hora a hora |
| Gestão de Atualizações | Windows |&#8226; |&#8226; |  |  |&#8226; |pelo menos 2 vezes por dia e 15 minutos depois de instalar uma atualização |

### <a name="security--compliance"></a>Segurança e Conformidade

| Solução de gestão | Plataforma | Agente de monitorização da Microsoft | Agente do Operations Manager | Storage do Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Avaliação de antimalware |Windows |&#8226; |&#8226; |  |  |&#8226; |hora a hora |
| Auditoria e segurança<sup>1</sup> | Windows e Linux | parcial | parcial | parcial |   | parcial | vários |

<sup>1</sup> Olá segurança e a solução de auditoria pode recolher registos de agentes do Windows, o Operations Manager e o Linux. Consulte [origens de dados](#data-sources) para obter informações de recolha de dados sobre:

- Syslog
- Registos de eventos de segurança do Windows
- Registos de firewall do Windows
- Registos de eventos do Windows



### <a name="protection--recovery"></a>Proteção e Recuperação

| Solução de gestão | Plataforma | Agente de monitorização da Microsoft | Agente do Operations Manager | Storage do Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Cópia de segurança | Azure |   |   |   |   |   | n/d |
| Azure Site Recovery | Azure |   |   |   |   |   | n/d |


### <a name="data-sources"></a>Origens de dados


| Origem de dados | Plataforma | Agente de monitorização da Microsoft | Agente do Operations Manager | Storage do Azure | O Operations Manager necessárias? | Dados de agente do Operations Manager enviados através do grupo de gestão | Frequência da recolha |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Registos de atividade do Azure |Windows |  |  |  |  |  |na notificação |
| Registos de diagnóstico do Azure |Windows |  |  |  |  |  |na notificação |
| Métricas de diagnóstico do Azure |Windows |  |  |  |  |  |na notificação |
| ETW |Windows |  |  |&#8226; |  |  |5 minutos |
| Registos de IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minutos |
| Contadores de Desempenho |Windows |&#8226; |&#8226; |  |  |  |Mínimo de 10 segundos, conforme agendado |
| Contadores de Desempenho |Linux |&#8226; |  |  |  |  |Mínimo de 10 segundos, conforme agendado |
| Syslog |Linux |&#8226; |  |  |  |  |storage do Azure: 10 minutos; do agente: sobre chegada |
| Registos de eventos de segurança do Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |armazenamento do Azure: 10 min; para o agente de Olá: sobre chegada |
| Registos de firewall do Windows |Windows |&#8226; |&#8226; |  |  |  |sobre chegada |
| Registos de eventos do Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |armazenamento do Azure: 10 min; para o agente de Olá: sobre chegada |



## <a name="preview-management-solutions-and-features"></a>Funcionalidades e soluções de gestão de pré-visualização
Ao executar um serviço e seguir práticas de devops, mas é capaz de toopartner com clientes toodevelop funcionalidades e soluções.

Durante pré-visualização privada, atribua um pequeno grupo de clientes acesso tooan antecipado implementação dos comentários de Olá funcionalidade ou solução toogain e efetuar melhoramentos. Esta implementação antecipada tem mínimas funcionalidades e capacidades operacionais.

O nosso objetivo é tootry coisas rapidamente, para que possa encontrar o que funciona e o que não funciona. Iremos itere através deste processo até comentários de Olá de clientes de pré-visualização privada Olá informar-nos que está tudo prontos para uma versão de pré-visualização pública.

Durante a pré-visualização pública Olá, iremos tornar funcionalidade Olá ou solução disponível para todos os utilizadores tooget comentários mais e validar os nossos dimensionamento e eficiência. Durante esta fase:

* Funcionalidades de pré-visualização são apresentados no separador de definições de Olá e podem ser ativadas por qualquer utilizador.
* Pré-visualização soluções são adicionadas através da Galeria de Olá ou através de um script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>O que posso saber sobre as funcionalidades de pré-visualização e soluções?
Estamos entusiasmados sobre novas funcionalidades e soluções de gestão e iremos adoram trabalhar com a toodevelop-los.

Funcionalidades de pré-visualização e soluções não são mais adequadas para todos os utilizadores. Antes de pedir toojoin uma pré-visualização privada ou ativar uma versão de pré-visualização pública, certifique-se de que está a trabalhar OK com algo que está em desenvolvimento.

Quando ativar a funcionalidade de pré-visualização através do portal Olá, será apresentado um aviso reminding que Olá funcionalidade está em pré-visualização.

#### <a name="for-both-private-and-public-preview"></a>Para ambos *privada* e *pública* pré-visualização
Olá seguintes informações aplicam-se tooboth públicas e privadas previews:

* Coisas sempre podem não a funcionar corretamente.
  * Problemas de intervalo de ser um annoyance através de toosomething não está a funcionar em todas as secundária.
* Não há potencial para Olá pré-visualização toohave um impacto negativo sobre os sistemas / ambiente.
  * Vamos tentar coisas negativo tooavoid acontecer toohello sistemas que está a utilizar com o OMS, mas por vezes, inesperadas coisas ocorrerem.
* Perda de dados / poderão ocorrer danos.
* Vamos pode pedir que os registos de diagnóstico toocollect ou outro dados toohelp resolver problemas.
* funcionalidade de Olá ou solução, poderá ser removida (temporariamente ou permanentemente).
  * Com base no nosso learnings durante a pré-visualização de Olá, pode decidir a funcionalidade de Olá de versão toonot ou solução.
* Pré-visualizações poderão não funcionar ou poderão não foi testados com todas as configurações e poderá limitamos a:
  * Olá, sistemas operativos que podem ser utilizados (por exemplo, uma funcionalidade poderá só se aplicam tooLinux enquanto na pré-visualização).
  * Olá, tipo de agente (MMA, Operations Manager) que pode ser utilizada (por exemplo, uma funcionalidade poderá não funcionar com o Operations Manager em pré-visualização).  
* Soluções de pré-visualização e funcionalidades não são abrangidas por Olá contrato de nível de serviço.
* Utilização das funcionalidades de pré-visualização incorreu custos de utilização.
* Funcionalidades ou capacidades que necessita para a funcionalidade de Olá / solução toobe útil poderá estar em falta ou incompletas.
* Funcionalidades / soluções podem não estar disponíveis em todas as regiões.
* Funcionalidades / soluções não podem ser localizadas.
* Funcionalidades / soluções podem ter um limite no número de Olá de clientes ou dispositivos que podem utilizá-lo.
* Poderá ser necessário toouse scripts tooperform configuração e tooenable Olá solução/funcionalidade.
* interface de utilizador (IU) do Olá está incompleta e pode alterar a partir do dia tooday.
* Pré-visualizações públicos não podem ser apropriada para a produção / críticos sistemas.

#### <a name="for-private-preview"></a>Para *privada* pré-visualização
Adição toohello os itens acima, Olá informações a seguir é pré-visualizações tooprivate específico:

* Esperamos que tooprovide-nos com comentários sobre a sua experiência de modo a que podemos efetuar Olá funcionalidade/solução melhor.
* Iremos poderá contactá-lo para comentários utilizando inquéritos, chamadas de telefone ou e-mail.
* Coisas sempre não funcionam corretamente.
* Iremos pode necessitar de uma divulgação não contrato (contrato de confidencialidade) para participação ou pode incluir conteúdo confidencial.
  * Antes de blogging, tweeting ou, caso contrário a comunicar com terceiros, consulte o Olá Gestor de programa que é responsável por Olá pré-visualização toounderstand quaisquer restrições divulgação.
* Não execute produção / críticos sistemas.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Como obter acesso tooprivate pré-visualização funcionalidades e soluções?
Convidamo-pré-visualizações tooprivate de clientes através de várias maneiras diferentes dependendo da pré-visualização Olá.

* A resposta de inquéritos de cliente mensal Olá e nos dar permissão toofollow consigo melhora as possibilidades de que está a ser convidados tooa pré-visualização privada.
* A equipa da conta Microsoft para pode indicar-lhe.
* Pode inscrever-com base nos detalhes do publicadas no twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* Pode inscrever-com base em eventos de Comunidade partilhado detalhes – procure-nos em cumprem ups conferences e no comunidades online.

## <a name="next-steps"></a>Passos seguintes
* [Pesquisar registos](log-analytics-log-searches.md) tooview detalhadas informações recolhidas por soluções de gestão.
