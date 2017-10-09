---
title: "tooPower de dados de análise de registos de aaaExport BI | Microsoft Docs"
description: "Power BI é um serviço de análise de negócio baseada na nuvem da Microsoft que fornece visualizações otimizadas e relatórios para análise dos diferentes conjuntos de dados.  Análise de registos pode continuamente exportar dados do repositório OMS Olá no Power BI para pode tirar partido do respetivo visualizações e ferramentas de análise.  Este artigo descreve como tooconfigure consulta na análise de registos automaticamente exportar tooPower BI em intervalos regulares."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Exportar dados de análise de registos tooPower BI

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, este processo para exportar dados de análise de registos tooPower BI deixará de funcionar.  As agendas existentes que criou antes de atualizar irão tornar-se desativada. 
>
> Após a atualização, utiliza de análise de registos do Azure Olá a mesma plataforma como Application Insights e utilizar o mesmo processo consultas de análise de registos tooexport tooPower BI como de Olá [Olá processo tooexport Application Insights consulta tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  Pode optar por exportar consulta Olá utilizando a consola de análise de Olá, conforme descrito nesse artigo ou pode selecionar Olá **Power BI** botão, Olá parte superior do ecrã de Olá no portal de registo de pesquisa de Olá.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) é um serviço de análise de negócio baseada na nuvem da Microsoft que fornece visualizações otimizadas e relatórios para análise dos diferentes conjuntos de dados.  Análise de registos pode automaticamente exportar dados do repositório OMS Olá no Power BI para pode tirar partido do respetivo visualizações e ferramentas de análise.

Quando configura o Power BI com a análise de registos, pode criar consultas de registo que exportar os conjuntos de dados de toocorresponding resultados no Power BI.  consulta de Olá e exportação continua tooautomatically com base numa agenda que definem o conjunto de dados do tookeep Olá segurança toodate com dados mais recentes Olá recolhidos pelo registo de análise.

![Análise de registo tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Agendas do Power BI
A *Power BI agenda* inclui uma pesquisa de registo que exporta um conjunto de dados de Olá OMS repositório tooa correspondente conjunto de dados no Power BI e uma agenda que define a frequência esta pesquisa é executada tookeep Olá dataset atual.

Olá os campos do conjunto de dados de Olá corresponderá propriedades Olá de registos de Olá devolvidos pela pesquisa de Olá de registo.  Se pesquisa Olá devolve os registos de diferentes tipos, em seguida, o conjunto de dados de Olá incluirá todas as propriedades de Olá de cada um dos Olá incluídas tipos de registos.  

> [!NOTE]
> É uma melhor toouse de prática uma consulta de pesquisa de registo que devolve dados não processados como tooperforming oposição ao qualquer consolidação através de comandos, como [medidas](log-analytics-search-reference.md#measure).  Pode efetuar qualquer agregação e cálculos no Power BI a partir dos dados não processados Olá.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Ligar tooPower de área de trabalho do OMS BI
Pode exportar da análise de registos tooPower BI, tem de ligar a conta de tooyour área de trabalho do OMS Power BI com Olá procedimento a seguir.  

1. Na consola do OMS Olá clique Olá **definições** mosaico.
2. Selecione **contas**.
3. No Olá **informações de área de trabalho** secção clique **ligar tooPower conta BI**.
4. Introduza as credenciais de Olá para a sua conta Power BI.

## <a name="create-a-power-bi-schedule"></a>Criar uma agenda do Power BI
Crie uma agenda de Power BI para cada conjunto de dados utilizando Olá procedimento a seguir.

1. Na consola do OMS Olá clique Olá **pesquisa registo** mosaico.
2. Escreva uma nova consulta ou selecione uma pesquisa guardada que devolve Olá dados que pretende que tooexport demasiado**Power BI**.  
3. Clique em Olá **Power BI** botão, Olá parte superior do Olá de tooopen de página Olá **Power BI** caixa de diálogo.
4. Fornecer informações de Olá na Olá seguinte tabela e clique em **guardar**.

| Propriedade | Descrição |
|:--- |:--- |
| Nome |Nome tooidentify Olá agenda ao ver a lista de Olá de agendas do Power BI. |
| Pesquisa guardada |Olá toorun de pesquisa de registo.  Pode selecionar a consulta atual Olá ou selecionar uma pesquisa guardada existente a partir da caixa de lista pendente de Olá. |
| Agenda |Frequência Olá toorun guardar pesquisa e exportar o conjunto de dados do toohello Power BI.  valor de Olá tem de estar entre 15 minutos e 24 horas. |
| Nome do conjunto de dados |nome de Olá do conjunto de dados de Olá no Power BI.  Será criado se não existir e atualizada se existir. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Visualizar e remover as agendas do Power BI
Ver a lista de Olá de agendas de BI de energia existentes com Olá procedimento a seguir.

1. Na consola do OMS Olá clique Olá **definições** mosaico.
2. Selecione **Power BI**.

Além disso agendar toohello detalhes de Olá, Olá diversas vezes que Olá agenda está em execução no Olá na última semana e estado Olá da última sincronização de Olá são apresentados.  Se a sincronização de Olá detectados erros, pode clicar em Olá ligação toorun uma pesquisa de registo de registos com detalhes do erro Olá.

Pode remover uma agenda ao clicar no Olá **X** no Olá **Remover coluna**.  Pode desativar uma agenda selecionando **desativar**.  toomodify uma agenda tem de removê-lo e recriá-lo com as novas definições Olá.

![Agendas do Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Instruções de exemplo
Olá secção seguinte explica um exemplo de criar uma agenda do Power BI e utilizando o respetivo conjunto de dados toocreate um relatório simples.  Neste exemplo, todos os dados de desempenho para um conjunto de computadores é exportado tooPower BI e, em seguida, um gráfico de linha é criado a utilização do processador toodisplay.

### <a name="create-log-search"></a>Criar a pesquisa de registo
Iremos começar por criar uma pesquisa de registo de dados de Olá que queremos toosend toohello dataset.  Neste exemplo, vamos utilizar uma consulta que devolva todos os dados de desempenho para computadores com um nome que começa com *srv*.  

![Agendas do Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Criar a pesquisa do Power BI
Clicarmos em Olá **Power BI** botão caixa de diálogo do tooopen Olá Power BI e fornecer informações de Olá necessário.  Iremos pretende toorun esta pesquisa uma vez por hora e criar um conjunto de dados denominado *Contoso desempenho*.  Uma vez que já temos Olá pesquisa open que cria dados Olá queremos, vamos manter predefinição Olá *consulta de pesquisa atual utilize* para **pesquisa guardada**.

![Pesquisa do Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Certifique-se de pesquisa do Power BI
tooverify que criámos agenda Olá corretamente, vamos ver lista de Olá do Power BI pesquisas em Olá **definições** mosaico no dashboard do Olá OMS.  Iremos aguarde vários minutos e atualizar esta vista até mesmo os relatórios que a sincronização de Olá foi executada.

![Pesquisa do Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Verificar o dataset de Olá no Power BI
Vamos iniciar sessão na nossa conta em [powerbi.microsoft.com](http://powerbi.microsoft.com/) e desloque-se demasiado**conjuntos de dados** em Olá parte inferior do painel esquerdo Olá.  É possível ver que Olá *Contoso desempenho* conjunto de dados está listado com a indicação de que o nosso exportação foi executada com êxito.

![O conjunto de dados do Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Criar o relatório com base no conjunto de dados
Iremos selecionar Olá **Contoso desempenho** conjunto de dados e, em seguida, clique em **resultados** no Olá **campos** painel Olá tooview direita Olá campos que fazem parte deste conjunto de dados.  toocreate utilização de processador linha gráfico que mostra para cada computador, iremos efetuar Olá ações a seguir.

1. Selecione a visualização de gráfico de linha de Olá.
2. Arraste **ObjectName** demasiado**filtro de nível de relatório** e verifique **processador**.
3. Arraste **CounterName** demasiado**filtro de nível de relatório** e verifique **% de tempo do processador**.
4. Arraste **CounterValue** demasiado**valores**.
5. Arraste **computador** demasiado**legenda**.
6. Arraste **TimeGenerated** demasiado**eixo**.

É possível ver o que gráfico de linha resultante esse Olá é apresentado com dados de Olá do nosso conjunto de dados.

![Gráfico de linha do Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Guardar o relatório de Olá
Iremos guardar Olá relatório clicando no Olá botão, Olá parte superior do ecrã de Olá guardar e validar que é agora listada na secção de relatórios de Olá no painel esquerdo Olá.

![Relatórios do Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) toobuild consultas que podem ser exportados tooPower BI.
* Saiba mais sobre [Power BI](http://powerbi.microsoft.com) toobuild visualizações com base na análise de registos exportações.
