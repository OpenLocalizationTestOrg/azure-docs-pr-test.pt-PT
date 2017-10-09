---
title: "utilização de dados de aaaAnalyze no Log Analytics | Microsoft Docs"
description: "Utilize o dashboard de utilização de Olá na análise de registos tooview quantidade de dados estão a ser enviados toohello serviço de análise de registos e resolver problemas do porquê de grandes quantidades de dados estão a ser enviadas."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Analisar a utilização de dados do Log Analytics
Análise de registos inclui informações sobre a quantidade de Olá dos dados recolhidos, que computadores enviar dados Olá e Olá outro tipo de dados enviados.  Olá utilize **utilização de análise do registo** quantidade de Olá toosee dashboard de dados enviados toohello serviço de análise de registos. dashboard de Olá mostra quanto os dados são recolhidos por cada solução e a quantidade de dados, os seus computadores está a enviar.

## <a name="understand-hello-usage-dashboard"></a>Compreender o dashboard de utilização de Olá
Olá **utilização de análise de registos** dashboard apresenta Olá seguintes informações:

- Volume de dados
    - Volume de dados ao longo do tempo (baseado no seu âmbito de período de tempo atual)
    - Volume de dados por solução
    - Dados não associados a um computador
- Computadores
    - Computadores que estão a enviar dados
    - Computadores sem dados nas últimas 24 horas
- Ofertas
    - Nós Insight e Análise de Dados
    - Nós de Automatização e Controlo
    - Nós de segurança
- Desempenho
    - Tempo decorrido toocollect e índice de dados
- Lista de consultas

![dashboard de utilização](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork com dados de utilização
1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com) através da sua subscrição do Azure.
2. No Olá **Hub** menu, clique em **mais serviços** e, na lista de Olá de recursos, escreva **Log Analytics**. À medida que começa a escrever, Olá filtros de lista com base na sua entrada. Clique em **Log Analytics**.  
    ![Hub do Azure](./media/log-analytics-usage/hub.png)
3. Olá **Log Analytics** dashboard mostra uma lista dos seus áreas de trabalho. Selecione uma área de trabalho.
4. No Olá *área de trabalho* dashboard, clique em **utilização de análise de registos**.
5. No Olá **utilização de análise do registo** dashboard, clique em **tempo: últimas 24 horas** intervalo de tempo de Olá toochange.  
    ![intervalo de tempo](./media/log-analytics-usage/time.png)
6. Painéis categoria de utilização de Olá de vista que mostram áreas estiver interessado em. Escolha um painel e, em seguida, clique num item na mesma tooview mais detalhes no [pesquisa registo](log-analytics-log-searches.md).  
    ![exemplo de painel de utilização de dados](./media/log-analytics-usage/blade.png)
7. No dashboard da pesquisa de registo de Olá, reveja os resultados de Olá que são devolvidos a partir de pesquisa de Olá.  
    ![exemplo de pesquisa de registos de utilização](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Criar um alerta quando a recolha de dados for superior ao esperado
Esta secção descreve como toocreate um alerta se:
- O volume de dados exceder uma determinada quantidade.
- Volume de dados é tooexceed previsto um período especificado.

Os [alertas](log-analytics-alerts-creating.md) do Log Analytics utilizam consultas de pesquisa. Olá seguinte consulta tem um resultado quando existe mais de 100 GB de dados recolhidos nas Olá últimas 24 horas:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Olá seguinte consulta utiliza uma toopredict fórmula simple quando mais de 100 GB de dados será enviado um dia: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert num volume de dados diferente, altere Olá 100 Olá consultas toohello diversas GB pretende tooalert nos.

Utilize os passos de Olá descritos [criar uma regra de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notificado quando a recolha de dados é superior ao esperado.

Quando criar o alerta de Olá para a primeira consulta Olá – quando existe mais de 100 GB de dados nas 24 horas, defina o:
- **Nome** demasiado*volume de dados maior do que 100 GB nas 24 horas*
- **Gravidade** demasiado*aviso*
- **Consulta de pesquisa** demasiado`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Janela de tempo** demasiado*24 horas*.
- **Frequência de alerta** toobe uma hora, uma vez que os dados de utilização de Olá apenas atualizações uma vez por hora.
- **Gerar alerta com base em** toobe *número de resultados*
- **Número de resultados** toobe *maior que 0*

Utilize os passos de Olá descritos [adicionar regras de tooalert ações](log-analytics-alerts-actions.md) configurar uma ação de e-mail, o webhook ou o runbook para a regra de alerta Olá.

Quando criar Olá alerta para consulta de segundo Olá – quando é prever a que vai haver mais do que 100 GB de dados nas 24 horas, defina o:
- **Nome** demasiado*volume de dados esperado toogreater de 100 GB nas 24 horas*
- **Gravidade** demasiado*aviso*
- **Consulta de pesquisa** demasiado`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Janela de tempo** demasiado*3 horas*.
- **Frequência de alerta** toobe uma hora, uma vez que os dados de utilização de Olá apenas atualizações uma vez por hora.
- **Gerar alerta com base em** toobe *número de resultados*
- **Número de resultados** toobe *maior que 0*

Quando receber um alerta, utilize os passos de Olá Olá seguir tootroubleshoot secção por que razão a utilização é superior ao esperado.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Resolver o motivo pelo qual a utilização é superior ao esperado
dashboard de utilização de Olá ajuda-o a tooidentify por que motivo utilização (e, por conseguinte, custo) é superior ao está à espera.

A utilização superior deve-se a um ou a ambos os motivos abaixo:
- Mais dados do que esperado enviados tooLog análise
- Mais nós que o esperado enviar dados tooLog análise

### <a name="check-if-there-is-more-data-than-expected"></a>Verificar se há mais dados do que o esperado 
Existem duas secções principais da página de utilização de Olá ajudam a identificar a causa Olá maioria dos dados toobe recolhido.

Olá *volume de dados ao longo do tempo* gráfico mostra o volume total de Olá de dados enviados e computadores Olá enviar Olá maioria dos dados. gráfico de Olá na parte superior do Olá permite-lhe toosee se a utilização de dados global está a crescer, restantes gradual ou diminuir. Olá lista de computadores que mostra os computadores Olá 10 enviar Olá maioria dos dados.

Olá *volume de dados pela solução* gráfico mostra o volume de Olá de dados que são enviados por cada solução e soluções de Olá enviar Olá maioria dos dados. gráfico de Olá na parte superior do Olá mostra o volume total de Olá de dados que são enviados por cada solução ao longo do tempo. Estas informações permite-lhe tooidentify se uma solução está a enviar mais dados sobre Olá mesmo culmina de dados, ou menos dados ao longo do tempo. lista de Olá das soluções mostra soluções Olá 10 enviar Olá maioria dos dados. 

Estes dois gráficos apresentam todos os dados. Alguns dados estão sujeitos a faturação, enquanto outros dados são gratuitos. toofocus apenas nos dados que sujeito a faturação, modifique a consulta de Olá no Olá pesquisa página tooinclude `IsBillable=true`.  

![gráficos de volumes de dados](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Observe Olá *volume de dados ao longo do tempo* gráfico. soluções de Olá toosee e tipos de dados que estão a enviar Olá maioria dos dados para um computador específico, clique no nome de Olá do computador Olá. Clique no nome de Olá do computador de primeiro Olá na lista de Olá.

Na seguinte captura de ecrã de Olá, Olá *gestão do registo / desempenho* tipo de dados está a enviar Olá maioria dos dados para o computador de Olá. 

![volume de dados de um computador](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Em seguida, volte atrás toohello *utilização* dashboard e observe Olá *volume de dados pela solução* gráfico. computadores de Olá toosee enviar Olá maioria dos dados para uma solução, clique no nome de Olá da solução de Olá na lista de Olá. Clique no nome de Olá da solução de primeiro Olá na lista de Olá. 

Na seguinte captura de ecrã de Olá, confirma que esse Olá *acmetomcat* computador está a enviar Olá maioria dos dados para a solução de gestão do registo de Olá.

![volume de dados de uma solução](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Se for necessário, execute grandes volumes da análise adicional tooidentify dentro de um tipo de dados ou de solução. As consultas de exemplo incluem:

+ Solução de **Segurança**
  - `Type=SecurityEvent | measure count() by EventID`
+ Solução de **Gestão de Registos**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ Tipo de dados de **Desempenho**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ Tipo de dados de **Evento**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ Tipo de dados de **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ Tipo de dados de **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Utilize Olá seguinte passos tooreduce Olá volume de registos recolhidos:

| Origem do volume de dados elevado | Como volume de dados de tooreduce |
| -------------------------- | ------------------------- |
| Eventos de segurança            | Selecione [eventos de segurança comuns ou mínimos](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) <br> Alterar os eventos de toocollect apenas necessário de política de auditoria de segurança de Olá. Em particular, reveja Olá necessidade toocollect eventos <br> - [auditar a plataforma de filtragem](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [auditar o registo](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [auditar o sistema de ficheiros](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [auditar o objeto de kernel](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [auditar a manipulação de identificadores](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [auditar o armazenamento amovível](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Contadores de desempenho       | Altere a [configuração do contador de desempenho](log-analytics-data-sources-performance-counters.md) para: <br> -Reduza a frequência de Olá da coleção <br> - Reduzir o número de contadores de desempenho |
| Registos de eventos                 | Altere a [configuração do registo de eventos](log-analytics-data-sources-windows-events.md) para: <br> -Reduzir o número de Olá de registos de eventos recolhidos <br> - Recolher apenas níveis de eventos necessários. Por exemplo, não recolher eventos de nível *Informação* |
| Syslog                     | Altere a [configuração do syslog](log-analytics-data-sources-syslog.md) para: <br> -Reduzir o número de Olá das instalações recolhidos <br> - Recolher apenas níveis de eventos necessários. Por exemplo, não recolher eventos de nível *Informação* e *Depuração* |
| AzureDiagnostics           | Alterar a coleção de registo de recursos para: <br> -Reduzir o número de Olá de recursos enviar registos tooLog análise <br> - Recolher apenas registos necessários |
| Dados de solução de computadores que não precisam de solução Olá | Utilize [solução filtragem](../operations-management-suite/operations-management-suite-solution-targeting.md) dados toocollect apenas necessário nos grupos de computadores. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Verificar se há mais nós do que o esperado
Se tiver Olá *por nó (OMS)* preços camada, em seguida, são-lhe cobrados com base no número de Olá de nós e soluções que utilizar. Pode ver o número de nós de cada oferta estão a ser utilizados numa Olá *ofertas* secção do dashboard de utilização de Olá.

![dashboard de utilização](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Clique em **ver todos os...**  tooview Olá obter uma lista completa de enviar dados para a oferta selecionado Olá de computadores.

Utilize [solução filtragem](../operations-management-suite/operations-management-suite-solution-targeting.md) dados toocollect apenas necessário nos grupos de computadores.


## <a name="next-steps"></a>Passos seguintes
* Consulte [pesquisas de registo na análise de registos](log-analytics-log-searches.md) toolearn como toouse Olá procurar idioma. Pode utilizar a pesquisa consultas tooperform adicionais análise nos dados de utilização de Olá.
* Utilize os passos de Olá descritos [criar uma regra de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notificado quando um critério de pesquisa é cumprido
* Utilize [solução filtragem](../operations-management-suite/operations-management-suite-solution-targeting.md) dados toocollect apenas necessário nos grupos de computadores
* Selecione [eventos de segurança comuns ou mínimos](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)
* Altere a [configuração do contador de desempenho](log-analytics-data-sources-performance-counters.md)
* Altere a [configuração do registo de eventos](log-analytics-data-sources-windows-events.md)
* Altere a [configuração do syslog](log-analytics-data-sources-syslog.md)
