---
title: "gestão aaaAlert no Microsoft monitorização produtos | Microsoft Docs"
description: "Um alerta indica algum problema que necessita de atenção a partir de um administrador.  Este artigo descreve as diferenças de Olá em como os alertas são criados e geridos no System Center Operations Manager (SCOM) e análise de registos e apresenta as melhores práticas no tirar partido dos dois produtos de Olá para uma estratégia de gestão de alertas híbrida."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Gerir alertas com a monitorização da Microsoft
Um alerta indica algum problema que necessita de atenção a partir de um administrador.  Existem diferenças distintas entre o System Center Operations Manager (SCOM) e análise de registos no Operations Management Suite (OMS) em termos de como os alertas são criados, como são geridos e analisados e como são notificados que foi um problema crítico detetada.

## <a name="alerts-in-operations-manager"></a>Alertas no Operations Manager
Os alertas no SCOM são gerados por regras individuais ou monitores tooindicate um problema específico.  Um monitor pode gerar um alerta quando os mesmos entrarão num Estado de erro enquanto uma regra pode gerar um alerta tooindicate algum problema crítico que não é toohello diretamente relacionado com estado de funcionamento de um objeto gerido.  Pacotes de gestão incluem uma variedade de fluxos de trabalho que criam alertas para a aplicação Olá ou serviço que eles geridos.  Parte do processo de Olá de configuração de um novo pacote de gestão é de otimização-tooensure que não recebe alertas excessivos para problemas que não considerar críticos.

![Vista de alerta do SCOM](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM fornece gestão de alertas completa com alertas de estado que pode ser alterado por administradores, à medida que trabalham problema de Olá tooresolve.  Quando o problema de Olá foi resolvido, o administrador de Olá define tooclosed alerta Olá em que momento já não será apresentada nas vistas a apresentar os alertas ativos.  Alertas que são gerados a partir de monitores podem ser resolvidos automaticamente quando o monitor de Olá devolve tooa bom estado.

![Estado do alerta](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Alertas na análise de registos
É criado um alerta na análise de registos por uma consulta de registo que é executada automaticamente em intervalos regulares.  Pode criar uma regra de alerta a partir de qualquer consulta de registo.  Se a consulta de Olá devolve resultados correspondentes aos critérios de Olá que especificar, em seguida, é criado um alerta.  Isto pode ser uma consulta específica que cria um alerta se for detetado um evento específico, ou pode utilizar uma consulta mais geral que se parece qualquer evento de erro relacionados com tooa determinada aplicação.

Alertas de análise do registo são escritos no repositório do OMS toohello como um evento e podem ser obtidas com uma consulta de registo.  Não têm um Estado como eventos do SCOM para que pode indicar quando o problema de Olá foi resolvido.

![Alerta do OMS](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Quando o SCOM é utilizado como uma origem de dados para análise de registos, alertas do SCOM são escritas repositório do OMS toohello são criadas e modificadas.  

![Alerta do SCOM](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Olá [solução de gestão de alertas](http://technet.microsoft.com/library/mt484092.aspx) fornece um resumo dos alertas ativos e várias consultas comuns tooretrieve diferentes conjuntos de alertas.  Este procedimento fornece uma análise mais eficaz dos alertas que um relatório no SCOM.  Pode desagregar a partir dos dados de toodetailed Olá resumos e criar consultas ad hoc tooretrieve diferentes conjuntos de alertas.

![Solução de gestão de alertas](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Notificações
Notificações no SCOM enviam-lhe um e-mail ou texto em resposta tooalerts que correspondem aos critérios específicos.  Pode criar subscrições de notificação diferentes que tenham diferentes pessoas notificadas consoante esses critérios como objeto de Olá a ser monitorizado, Olá gravidade do alerta Olá, tipo de Olá problema detetado ou Olá hora do dia.

Algumas subscrições podem ser utilizado tooimplement uma estratégia completa de notificação para um grande número de pacotes de gestão.

![Alertas do SCOM](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Análise de registos pode notificá-lo através de correio que foi criado um alerta, definindo uma ação de notificação de e-mail em cada [regra de alerta](http://technet.microsoft.com/library/mt614775.aspx).  Não tem capacidade de Olá de Olá SCOM subscrever toomultiple alertas com uma única regra.  Também precisa de toocreate as suas próprias regras de alerta, uma vez que OMS não fornece quaisquer pré-configurada.

![Alertas do Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

Não é possível completamente gerir alertas do SCOM na análise de registos entanto, uma vez que apenas pode modificá-las na consola de operações de Olá.  Análise de registos é útil como parte de uma gestão de alertas apesar processar para fornecer ferramentas de análise que SCOM individualmente não tem.

## <a name="alert-remediation"></a>Remediação de alerta
[Remediação](http://technet.microsoft.com/library/mt614775.aspx) refere-se o problema Olá correto tooan tentativa tooautomatically identificado por um alerta.

SCOM permite-lhe toorun diagnósticos e recuperações no monitor de tooa de resposta de introduzir um mau estado de funcionamento.  Isto acontece criação Olá alerta de monitor de toohello em simultâneo.  Os diagnósticos e recuperações, normalmente, são implementadas como um script que é executado num agente Olá.  Um toogather de tentativas de diagnóstico mais informações sobre Olá detetado problema a uma recuperação tenta problema de Olá toocorrect.

Análise de registos permite-lhe toostart um [runbook de automatização do Azure](https://azure.microsoft.com/documentation/services/automation/) ou chamar um webhook no alerta de análise de registos de tooa de resposta.  Os Runbooks podem conter lógica complexa implementada no PowerShell.  script de Olá é executada no Azure e pode aceder a quaisquer recursos do Azure ou recursos externos disponíveis da nuvem Olá.  A automatização do Azure têm Olá capacidade tooexecute runbooks num servidor no seu datacenter local, mas esta funcionalidade não está atualmente disponível a partir do runbook Olá alertas de análise de tooLog de resposta.

Tanto as recuperações no SCOM e runbooks no OMS pode conter scripts do PowerShell, mas as recuperações são mais difíceis toocreate e gerir porque tem de estar contidas dentro de um pacote de gestão.  Os Runbooks são armazenados na automatização do Azure que fornece funcionalidades para a criação, teste e gerir runbooks.

Se utilizar o SCOM como uma origem de dados para análise de registos, pode criar um alerta de análise de registos com um tooretrieve de consulta do registo SCOM alertas armazenados no Olá repositório do OMS.  Isto permitiria que lhe toorun um runbook de automatização do Azure no alerta SCOM tooa de resposta.  Obviamente, uma vez que o runbook Olá será executada no Azure, este não seria uma estratégia viável para recuperações de problemas no local.

## <a name="next-steps"></a>Passos seguintes
* Saiba os detalhes de Olá de [alertas no System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

