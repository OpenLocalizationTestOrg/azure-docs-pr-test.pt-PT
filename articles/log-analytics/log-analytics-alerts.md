---
title: alertas de aaaUnderstanding no Log Analytics do Azure | Microsoft Docs
description: "Alertas na análise de registos identificar informações importantes no seu repositório do OMS e podem proativamente notificá-lo de problemas ou da invocação ações tooattempt toocorrect-los.  Este artigo descreve os diferentes tipos de Olá de regras de alertas e como são definidos."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Alertas de compreender na análise de registos

Alertas na análise de registos identificam informações importantes no seu repositório de análise de registos.  Este artigo fornece detalhes de regras de alerta como em projetos de análise de registos e descreve Olá as diferenças entre os diferentes tipos de regras de alertas.

Para o processo de Olá de criação de regras de alertas, consulte Olá seguintes artigos:

- Criar regras de alertas utilizando [portal do Azure](log-analytics-alerts-creating.md)
- Criar regras de alertas utilizando [modelo do Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Criar regras de alertas utilizando [REST API](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Regras de alertas

Os alertas são criados pelas regras de alerta que execute automaticamente pesquisas de registo em intervalos regulares.  Se Olá os resultados da pesquisa de registo Olá correspondem aos critérios de específicos, em seguida, é criado um registo de alerta.  regra de Olá, em seguida, pode executar automaticamente um ou mais ações tooproactively notificá-lo de alerta de Olá ou da invocação do outro processo.  Diferentes tipos de regras de alerta utilizam diferentes lógica tooperform nesta análise.

![Alertas do Log Analytics](media/log-analytics-alerts/overview.png)

Regras de alerta são definidas pelo Olá os detalhes:

- **Pesquisa de registo**.  consulta de Olá que é executada sempre que a regra de alerta Olá é acionado.  registos de Olá devolvidos por esta consulta é utilizada toodetermine se é criado um alerta.
- **Janela de tempo**.  Especifica o intervalo de tempo de Olá para consulta Olá.  consulta de Olá devolve apenas os registos que foram criados dentro deste intervalo de Olá hora atual.  Isto pode ser qualquer valor entre 5 minutos e 24 horas. Por exemplo, se hello hora janela é definida too60 minutos e Olá consulta é executada em 1:15 PM, é devolvido apenas os registos criados entre 12:15 PM e 1:15 PM.
- **Frequência**.  Especifica a frequência hello consulta deve ser executada. Pode ser qualquer valor entre 5 minutos e 24 horas. Deve ser igual tooor inferior a janela de tempo de Olá.  Se o valor de Olá for superior à janela de tempo de Olá, em seguida, o risco de registos que está a ser omitidos.<br>Por exemplo, considere uma janela de tempo de 30 minutos e uma frequência de 60 minutos.  Se a consulta de Olá é executada em 1:00, devolve registos entre 12:30 e 1:00 PM.  Olá próxima vez que pretende executar a consulta de Olá é 2:00 quando devolvam registos entre 1:30 e 2:00.  Nunca deverá ser avaliados de quaisquer registos criados entre 1:00 e 1:30.
- **Limiar**.  Olá os resultados da pesquisa de registo Olá são avaliada toodetermine se deve ser criado um alerta.  limiar de Olá é diferente para diferentes tipos de Olá de regras de alertas.

Cada regra de alerta no Log Analytics é um dos dois tipos.  Cada um destes tipos é descrita detalhadamente nas secções Olá que se seguem.

- **[Número de resultados](#number-of-results-alert-rules)**. Único alerta criada quando regista número Olá devolvido pela pesquisa de registo Olá exceder um número especificado.
- **[Medida de métrica](#metric-measurement-alert-rules)**.  Alerta criada para cada objeto no Olá os resultados da pesquisa de Olá de registo com valores que excedem o limiar especificado.

Olá as diferenças entre os tipos de regra de alerta são os seguintes.

- **Número de resultados** regra de alerta sempre criará um tempo de alerta único **medida métrica** regra de alerta cria um alerta para cada objeto que excede o limiar de Olá.
- **Número de resultados** regras de alerta criar um alerta quando o limiar de Olá for excedido uma única vez. **Medida de métrica** regras de alertas podem criar um alerta quando for excedido o limiar de Olá um determinado número de vezes ao longo de um intervalo de tempo específico.

## <a name="number-of-results-alert-rules"></a>Número de regras de alerta de resultados
**Número de resultados** regras de alerta criar um único alerta quando o número de Olá de registos devolvidos pela consulta de pesquisa de Olá exceder o limiar especificado Olá.

### <a name="threshold"></a>Limiar
limiar de Olá para um **número de resultados** regra de alerta é simplesmente maior ou menor do que um valor específico.  Se o número de Olá de registos devolvidos pela pesquisa de registo Olá corresponde a este critério, é criado um alerta.

### <a name="scenarios"></a>Cenários

#### <a name="events"></a>Eventos
Este tipo de regra de alerta é ideal para trabalhar com eventos, tais como registos de eventos do Windows, Syslog, e os registos personalizados.  Poderá pretender toocreate um alerta quando um evento de erro específico é criado ou quando são criados vários eventos de erro dentro de uma janela de tempo específico.

tooalert num evento único, número de Olá do conjunto de resultados toogreater que 0 e frequência de Olá e minutos de too5 de janela de tempo.  Consulta de Olá que executa cada 5 minutos e verifique a existência de ocorrência de Olá de um único evento que foi criada uma vez que foi executada a consulta do Olá último tempo Olá.  Uma frequência de tempo pode atrasar o tempo de Olá entre Olá ter de eventos recolhidos e alerta Olá a ser criada.

Algumas aplicações podem iniciar um erro de ocasional necessariamente não deve emitir um alerta.  Por exemplo, a aplicação Olá poderá Repita o processo de Olá que criou o evento de erro Olá e, em seguida, terá êxito Olá próxima vez.  Neste caso, poderá não pretende que toocreate Olá alerta, a menos que são criados vários eventos dentro de uma janela de tempo específico.  

Em alguns casos, poderá ser útil toocreate um alerta na ausência de Olá de um evento.  Por exemplo, um processo pode iniciar eventos regular tooindicate que está a funcionar corretamente.  Se não registar um estes eventos dentro de uma janela de tempo específico, deverá ser criado um alerta.  Neste caso, deverá definir o limiar de Olá demasiado**inferior a 1**.

#### <a name="performance-alerts"></a>Alertas de desempenho
[Dados de desempenho](log-analytics-data-sources-performance-counters.md) são armazenadas como registos na Olá tooevents semelhante do OMS repositório.  Se pretender tooalert quando um contador de desempenho excede um limiar específico, esse limiar deve ser incluído numa consulta Olá.

Por exemplo, se pretendesse tooalert quando hello processador é executada através de 90%, teria de utilizar uma consulta como Olá seguir com o limiar de Olá para a regra de alerta Olá **maior que 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Se quisesse tooalert quando processador Olá apresentou uma média de mais de 90% de uma janela de tempo específico, teria de utilizar uma consulta com Olá [medir comando](log-analytics-search-reference.md#commands) com Olá seguinte com o limiar de Olá para a regra de alerta Olá **maior que 0** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consultas alteraria toohello seguinte:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Regras de alerta de métrica de medida

>[!NOTE]
> Regras de alerta de medida métrica estão atualmente em pré-visualização pública.

**Medida de métrica** regras de alerta criar um alerta para cada objeto numa consulta com um valor que excede um limiar especificado.  Têm Olá seguintes diferenças distintas de **número de resultados** regras de alertas.

#### <a name="log-search"></a>Pesquisas de registos
Apesar de poder utilizar qualquer consulta para um **número de resultados** regra de alerta, existem consulta de Olá requisitos específicos para uma regra de alerta de métrica de medida.  Tem de incluir um [medir comando](log-analytics-search-reference.md#commands) resultados de Olá toogroup num campo específico. Este comando tem de incluir Olá seguintes elementos.

- **A função de agregação**.  Determina o cálculo de Olá que é executado e potencialmente tooaggregate um campo numérico.  Por exemplo, **existente** irá devolver o número de registos Olá consulta Olá, **avg(CounterValue)** irá devolver a média de Olá do campo de CounterValue Olá ao longo do intervalo de Olá.
- **Campo de grupo**.  É criado um registo com um valor de agregados para cada instância deste campo e pode ser gerado um alerta para cada.  Por exemplo, se pretendesse toogenerate um alerta para cada computador, teria de utilizar **por computador**.   
- **Intervalo**.  Define o intervalo de tempo de Olá durante o qual os dados de Olá são agregados.  Por exemplo, se tiver especificado **5minutes**, seria possível criar um registo para cada instância do campo de grupo Olá agregado em intervalos de 5 minutos ao longo de janela de tempo de Olá especificada para o alerta de Olá.

#### <a name="threshold"></a>Limiar
limiar de Olá para regras de alerta de métrica de medida é definido por um valor de agregação e um número de violações.  Se qualquer ponto de dados na pesquisa de registo Olá exceder este valor, tem considerado uma violação.  Se exceder o número de Olá de falhas para qualquer objeto nos resultados de Olá Olá valor especificado, em seguida, é criado um alerta para esse objeto.

#### <a name="example"></a>Exemplo
Considere um cenário em que pretendia um alerta se a qualquer computador excedeu a utilização do processador de 90% três vezes mais de 30 minutos.  Poderá criar uma regra de alerta com Olá os detalhes.  

**Consulta:** tipo = desempenho ObjectName = processador CounterName = "% de tempo do processador" | medir avg(CounterValue) por computador intervalo de 5 minutos<br>
**Janela de tempo:** 30 minutos<br>
**Frequência de alerta:** 5 minutos<br>
**Valor de agregação:** excelente a 90<br>
**Alerta de Acionador com base na:** Total de falhas maior 5<br>

consulta de Olá criaria um valor médio para cada computador em intervalos de 5 minutos.  Esta consulta iria ser executada a cada 5 minutos para os dados recolhidos através de Olá anteriores 30 minutos.  Dados de exemplo são mostrados abaixo para três computadores.

![Resultados da consulta de exemplo](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

Neste exemplo, seriam possível criar alertas separadas para srv02 e srv03, uma vez que estes infringido limiar de 90% Olá 3 vezes durante a janela de tempo de Olá.  Se hello **alerta acionador com base na:** foram alteradas demasiado**Consecutive** , em seguida, seria possível criar um alerta apenas para srv03, uma vez que o se infringido limiar Olá para 3 amostras consecutivas.

## <a name="alert-records"></a>Registos de alerta
Alerta registos criados pelas regras de alerta na análise de registos tem um **tipo** de **alerta** e um **SourceSystem** de **OMS**.  Têm propriedades Olá no Olá a tabela seguinte.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*OMS* |
| *Objeto*  | [Alertas de medida métrica](#metric-measurement-alert-rules) terá uma propriedade para o campo de grupo Olá.  Por exemplo, se a pesquisa de registo Olá grupos no computador, Olá alerta de registo com tem um campo de computador com o nome de Olá do computador de Olá como valor de Olá.
| AlertName |Nome do alerta Olá. |
| AlertSeverity |Nível de gravidade do alerta Olá. |
| LinkToSearchResults |Ligação tooLog análise registo pesquisa que devolva os registos de Olá da consulta de Olá que criou o alerta de Olá. |
| Consulta |Texto da consulta de Olá que foi executada. |
| QueryExecutionEndTime |Fim do intervalo de tempo de Olá para consulta Olá. |
| QueryExecutionStartTime |Início do intervalo de tempo de Olá para consulta Olá. |
| ThresholdOperator | Operador que foi utilizado pela regra de alerta de Olá. |
| ThresholdValue | Valor que foi utilizado pela regra de alerta de Olá. |
| TimeGenerated |Alerta de Olá data e hora foi criada. |

Existem outros tipos de alerta registos criados pela Olá [solução de gestão de alerta](log-analytics-solution-alert-management.md) e [exporta do Power BI](log-analytics-powerbi.md).  Estes têm um **tipo** de **alerta** , mas são distinguidos pelo respetivo **SourceSystem**.


## <a name="next-steps"></a>Passos seguintes
* Instalar Olá [solução de gestão de alertas](log-analytics-solution-alert-management.md) alertas tooanalyze criadas na análise de registos com alertas recolhidos a partir de System Center Operations Manager.
* Leia mais sobre [pesquisas de registo](log-analytics-log-searches.md) que pode gerar alertas.
* Conclua uma explicação passo a passo para [configurar um webook](log-analytics-alerts-webhooks.md) com uma regra de alerta.  
* Saiba como toowrite [runbooks na automatização do Azure](https://azure.microsoft.com/documentation/services/automation) problemas de tooremediate identificados através de alertas.
