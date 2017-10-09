---
title: alertas de base de dados SQL do Azure portal toocreate aaaUse | Microsoft Docs
description: "Utilize alertas de base de dados SQL do Olá toocreate portal do Azure, que podem acionar notificações ou automatização quando forem cumpridas condições Olá que especificar."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Utilizar alertas toocreate portal do Azure para a SQL Database do Azure e do armazém de dados

## <a name="overview"></a>Descrição geral
Este artigo mostra como tooset configurar alertas de SQL Database do Azure e do armazém de dados utilizando Olá portal do Azure. Este artigo também fornece as melhores práticas para definir períodos de alerta.    

Pode receber um alerta com base na monitorização métricas para ou eventos nos seus serviços do Azure.

* **Valores métricos** - hello acionadores de alertas quando o valor de Olá de uma métrica especificada atravesse um limiar atribuir em qualquer direção. Ou seja, aciona ambas quando Olá primeiro condição e, em seguida, posteriormente quando condição que é já não está a ser cumprido.    
* **Eventos de registo de atividade** -pode acionar um alerta num *cada* eventos ou, se ocorre um determinado número de eventos.

Pode configurar um alerta toodo Olá a seguir quando aciona:

* enviar o administrador de serviços de toohello de notificações de e-mail e coadministradores
* envie correio eletrónico tooadditional e-mails que especificar.
* Chamar um webhook

Pode configurar e obter informações sobre regras de alerta utilizando

* [Portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [interface de linha de comandos (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [API de REST de Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Criar uma regra de alerta numa métrica com Olá portal do Azure
1. No Olá [portal](https://portal.azure.com/), localize recursos Olá estiver interessado na monitorização e selecione-o.
2. Este passo é diferente para a base de dados SQL e conjuntos elásticos em comparação com o armazém de dados do SQL Server: 

   - **& Apenas para conjuntos elásticos SQL DB**: selecione **alertas** ou **regras de alerta** em Olá secção monitorização. ícone de texto de Olá e podem variar devido às ligeiramente diferentes recursos.  
   
     ![Monitorização](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **Armazém de dados SQL só**: selecione **monitorização** em Olá secção de tarefas comuns. Clique em Olá **DWU utilização** gráfico.

     ![TAREFAS COMUNS](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Selecione Olá **Adicionar alerta** de comandos e preencha os campos de Olá.
   
    ![Adicionar o alerta](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. **Nome** o alerta de regra e escolha um **Descrição**, que também mostra nos e-mails de notificação.
5. Selecione Olá **métrica** pretende toomonitor, em seguida, escolha um **condição** e **limiar** valor para a métrica de Olá. Também escolhido Olá **período** de tempo que Olá métrica regra deve ser satisfeita antes de acionadores de alerta de Olá. Por isso, por exemplo, se utilizar o período de Olá "PT5M" e o alerta procura CPU superior a 80%, o alerta Olá aciona quando Olá da CPU foi consistentemente acima 80% para 5 minutos. Depois de ocorre o acionador primeiro Olá, novamente acionado quando Olá CPU permanece inferior a 80% para 5 minutos. Olá medida de CPU ocorre a cada 1 minuto.   
6. Verifique **proprietários de E-Mail...**  se pretender que os administradores e coadministradores toobe enviado por e-mail quando Olá desencadeado alerta.
7. Se pretender que os e-mails adicionais tooreceive uma notificação quando hello é desencadeado um alerta, adicioná-los no Olá **administrador adicionais email(s)** campo. Separe várias mensagens de correio eletrónico com ponto e vírgula -  *email@contoso.com;email2@contoso.com*
8. Colocar um URI válido no Olá **Webhook** campo se quiser chamado Olá quando é desencadeado alerta.
9. Selecione **OK** quando toocreate efectuada Olá alerta.   

Dentro de alguns minutos, o alerta de Olá está ativa e aciona conforme descrito anteriormente.

## <a name="managing-your-alerts"></a>Gerir os alertas
Assim que tiver criado um alerta, pode selecionar e:

* Ver um gráfico com o limiar de métrica de Olá Olá real valores e de Olá dia anterior.
* Editar ou eliminá-lo.
* **Desativar** ou **ativar** -se de que pretende parar de tootemporarily ou retomar a receção de notificações para esse alerta.


## <a name="sql-database-alert-values"></a>Valores de alerta de base de dados SQL

| Tipo de Recurso | Nome da métrica | Nome amigável | Tipo de agregação | Janela de tempo mínimo de alerta|
| --- | --- | --- | --- | --- |
| Base de dados SQL | cpu_percent | Percentagem de CPU | Média | 5 minutos |
| Base de dados SQL | physical_data_read_percent | Percentagem de ES de Dados | Média | 5 minutos |
| Base de dados SQL | log_write_percent | Percentagem de es do registo | Média | 5 minutos |
| Base de dados SQL | dtu_consumption_percent | Percentagem de DTU | Média | 5 minutos |
| Base de dados SQL | Armazenamento | Tamanho total da base de dados | Máximo | 30 minutos |
| Base de dados SQL | connection_successful | Ligações com êxito | Total | 10 minutos |
| Base de dados SQL | connection_failed | Falha de ligações | Total | 10 minutos |
| Base de dados SQL | blocked_by_firewall | Bloqueado pela Firewall | Total | 10 minutos |
| Base de dados SQL | impasse | Impasses | Total | 10 minutos |
| Base de dados SQL | storage_percent | Percentagem de tamanho da Base de Dados | Máximo | 30 minutos |
| Base de dados SQL | xtp_storage_percent | Percent(Preview) de armazenamento do OLTP dentro da memória | Média | 5 minutos |
| Base de dados SQL | workers_percent | Percentagem de trabalhadores | Média | 5 minutos |
| Base de dados SQL | sessions_percent | Percentagem de sessões | Média | 5 minutos |
| Base de dados SQL | dtu_limit | Limite DTU | Média | 5 minutos |
| Base de dados SQL | dtu_used | DTU utilizado | Média | 5 minutos |
||||||
| Agrupamento elástico | cpu_percent | Percentagem de CPU | Média | 10 minutos |
| Agrupamento elástico | physical_data_read_percent | Percentagem de ES de Dados | Média | 10 minutos |
| Agrupamento elástico | log_write_percent | Percentagem de es do registo | Média | 10 minutos |
| Agrupamento elástico | dtu_consumption_percent | Percentagem de DTU | Média | 10 minutos |
| Agrupamento elástico | storage_percent | Percentagem de armazenamento | Média | 10 minutos |
| Agrupamento elástico | workers_percent | Percentagem de trabalhadores | Média | 10 minutos |
| Agrupamento elástico | eDTU_limit | limite de eDTU | Média | 10 minutos |
| Agrupamento elástico | storage_limit | Limite de armazenamento | Média | 10 minutos |
| Agrupamento elástico | eDTU_used | eDTU utilizado | Média | 10 minutos |
| Agrupamento elástico | storage_used | Armazenamento utilizado | Média | 10 minutos |
||||||               
| O SQL data warehouse | cpu_percent | Percentagem de CPU | Média | 10 minutos |
| O SQL data warehouse | physical_data_read_percent | Percentagem de ES de Dados | Média | 10 minutos |
| O SQL data warehouse | Armazenamento | Tamanho total da base de dados | Máximo | 10 minutos |
| O SQL data warehouse | connection_successful | Ligações com êxito | Total | 10 minutos |
| O SQL data warehouse | connection_failed | Falha de ligações | Total | 10 minutos |
| O SQL data warehouse | blocked_by_firewall | Bloqueado pela Firewall | Total | 10 minutos |
| O SQL data warehouse | service_level_objective | Objetivo de nível de serviço da base de dados de Olá | Total | 10 minutos |
| O SQL data warehouse | dwu_limit | limite de dwu | Máximo | 10 minutos |
| O SQL data warehouse | dwu_consumption_percent | Percentagem DWU | Média | 10 minutos |
| O SQL data warehouse | dwu_used | DWU utilizado | Média | 10 minutos |
||||||


## <a name="next-steps"></a>Passos seguintes
* [Obter uma descrição geral da monitorização do Azure](../monitoring-and-diagnostics/monitoring-overview.md) , incluindo os tipos de Olá de informações que pode recolher e monitorizar.
* Saiba mais sobre [configurar webhooks alertas](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Obter um [descrição geral dos registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) e recolher métricas de alta frequência detalhadas do seu serviço.
* Obter um [descrição geral da coleção de métricas](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake se o serviço está disponível e reativa.
