---
title: "aaaUse análise de registos com uma aplicação de multi-inquilino de base de dados SQL | Microsoft Docs"
description: "Configurar e utilizar a análise de registos (OMS) com a aplicação de Wingtip SaaS de exemplo do Olá SQL Database do Azure"
keywords: tutorial de base de dados sql
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Configurar e utilizar a análise de registos (OMS) com aplicações de Wingtip SaaS Olá

Neste tutorial, configurar e utilizar *Log Analytics ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* para conjuntos elásticos e bases de dados de monitorização. Baseia-se no Olá [tutorial de gestão e monitorização do desempenho](sql-database-saas-tutorial-performance-monitoring.md)e mostra como toouse *Log Analytics* tooaugment Olá monitorização e alertas fornecidas Olá portal do Azure. O Log Analytics é particularmente adequado para a monitorização e os alertas em escala, uma vez que suporta centenas de conjuntos e centenas de milhares de bases de dados. Também fornece uma solução de monitorização única que pode integrar a monitorização de diferentes aplicações e serviços do Azure, em várias subscrições do Azure.

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Instalar e configurar o Log Analytics (OMS)
> * Utilize conjuntos de toomonitor de análise de registos e as bases de dados

toocomplete neste tutorial, Olá se disponibilizar os seguintes pré-requisitos estão concluídas:

* Olá Wingtip SaaS aplicação é implementada. toodeploy em menos de cinco minutos, consulte [implementar e explorar aplicações de Wingtip SaaS Olá](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter mais detalhes, veja [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

Consulte Olá [tutorial de gestão e monitorização do desempenho](sql-database-saas-tutorial-performance-monitoring.md) para um debate de cenários de SaaS Olá padrões, e como estas afetam os requisitos de Olá uma solução de monitorização.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Monitorizar e gerir o desempenho com o Log Analytics (OMS)

Na Base de Dados SQL, a monitorização e os alertas estão disponíveis nas bases de dados e nos conjuntos. Este incorporado monitorização e alertas é específicas do recurso e conveniente para pequenas quantidades de recursos, mas é menos toomonitoring convém grandes instalações ou para fornecer uma vista unificada entre diferentes recursos e as subscrições.

Para cenários de volume elevado, pode ser utilizado o Log Analytics. Este é um serviço Azure separado que fornece análises através de registos de diagnóstico emitidos e telemetria recolhida numa registo análise área de trabalho, que pode recolher a telemetria de muitas serviços e ser utilizado tooquery e definir alertas. O Log Analytics fornece uma linguagem de consulta incorporada e ferramentas de visualização de dados que permitem análises operacionais e visualização de dados. Olá solução de análise do SQL Server fornece vários predefinido conjunto elástico e base de dados de monitorização e alertas, vistas e consultas e permite-lhe adicionar as suas próprias consultas ad-hoc e guardar estas conforme necessário. O OMS também fornece um estruturador de vistas personalizado.

Soluções de áreas de trabalho e a análise de análise do registo podem ser abertas no Olá portal do Azure e no OMS. Olá portal do Azure é Olá mais recente ponto de acesso, mas pode ser por trás do portal do OMS Olá em algumas áreas.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Iniciar Olá carga gerador toocreate dados tooanalyze

1. Abra **demonstração PerformanceMonitoringAndManagement.ps1** no Olá **ISE do PowerShell**. Mantenha este script aberto como poderá ser útil toorun vários dos cenários de geração de carga Olá durante este tutorial.
1. Se tiver menos de cinco inquilinos, aprovisionar um lote de inquilinos tooprovide um contexto de monitorização mais interessante:
   1. Defina **$DemoScenario = 1,** **Aprovisionar um lote de inquilinos**
   1. Prima **F5** script de Olá toorun.

1. Defina **$DemoScenario** = 2, **Gerar carga de intensidade normal (aprox. 40 DTUs)**.
1. Prima **F5** script de Olá toorun.

## <a name="get-hello-wingtip-application-scripts"></a>Obter Olá Wingtip aplicação scripts

Olá scripts Wingtip pedidos de suporte e de código fonte da aplicação estão disponíveis no Olá [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório do github. Ficheiros de script estão localizados na Olá [pasta Learning módulos](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Transferir Olá **Learning módulos** pasta tooyour computador local, mantendo a estrutura de pastas.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Instalar e configurar a análise de registos e Olá solução de análise de SQL do Azure

Análise de registos é um serviço separado que necessita de toobe configurado. O Log Analytics recolhe dados de registo, telemetria e métricas numa área de trabalho do Log Analytics. Uma área de trabalho é um recurso, tal como os outros recursos no Azure, e tem de ser criada. Enquanto a área de trabalho Olá não necessita de toobe criado no Olá mesmo grupo de recursos como Olá aplicação (ões) que está a monitorizar, isto, muitas vezes, faz Olá mais sentido. No caso de Olá da aplicação de Wingtip SaaS Olá, isto permite Olá área de trabalho toobe eliminada facilmente com aplicação Olá, eliminando simplesmente o grupo de recursos de Olá.

1. Abra... \\Learning módulos\\monitorização de desempenho e gestão\\Log Analytics\\*demonstração LogAnalytics.ps1* no Olá **ISE do PowerShell**.
1. Prima **F5** script de Olá toorun.

Neste momento deve ser capaz de análise de registos abertos no Olá portal do Azure (ou no portal do OMS Olá). Irá demorar alguns minutos para toobe telemetria recolhida na área de trabalho de análise de registos de Olá e toobecome visível. será Olá mais que deixar sistema Olá recolha dados Olá experiência de Olá mais interessante. Agora é uma boa altura toograb beverage - basta certificar-se de gerador de carga Olá ainda está em execução!


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Utilize a análise de registos e Olá conjuntos de toomonitor de solução de análise do SQL Server e bases de dados


Neste exercício, abra análise de registos e Olá toolook portal do OMS no telemetria Olá recolhida para bases de dados de Olá e agrupamentos.

1. Procurar toohello [portal do Azure](https://portal.azure.com) e abrir análise de registos, clicando em mais serviços, em seguida, procure a análise de registos:

   ![abrir o Log Analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Selecione a área de trabalho Olá denominada *wtploganalytics -&lt;utilizador&gt;*.

1. Selecione **descrição geral** tooopen Olá solução de análise de registos no Olá portal do Azure.
   ![ligação da descrição geral](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **IMPORTANTE**: poderá demorar alguns minutos antes de solução Olá está ativa. Seja paciente!

1. Clique no Olá tooopen do mosaico de análise de SQL do Azure.

    ![descrição geral](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![análise](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Olá vista Olá solução painel se desloca pela lado, com a suas próprias barra de deslocamento na parte inferior de Olá (atualizar o painel Olá se necessário).

1. Explorar Olá várias vistas ao clicar nos mesmos ou em recursos individuais tooopen Explorador de desagregação, onde pode utilizar Olá tempo-controlo de deslize Olá principais à esquerda ou clique num vertical barra toofocus num setor quanto mais estreitos forem do tempo. Com esta vista, pode selecionar toofocus individuais de bases de dados ou agrupamentos de recursos específico:

    ![gráfico](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Novamente no painel de solução de Olá, se se deslocar para a extremidade direita toohello verá algumas consultas guardadas, que pode clicar em tooopen e explorar. Pode experimentar modificá-las e guardar quaisquer consultas interessantes que produza, as quais pode, em seguida, voltar a abrir e utilizar com outros recursos.

1. Novamente no painel de área de trabalho de análise de registos de Olá, selecione a solução de Portal do OMS tooopen Olá não existe.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. No portal do OMS Olá, pode configurar alertas. Clique na parte de alerta de Olá da base de dados Olá vista DTU.

1. Olá pesquisa de registo de vista que aparece, verá um gráfico de barras de métricas de Olá que está a ser representados.

    ![pesquisa de registos](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Se clicar no alerta na barra de ferramentas Olá será toosee capaz de configuração de alerta de Olá e pode alterá-la.

    ![adicionar regra de alerta](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Olá, monitorização e alertas na análise de registos e OMS baseada em consultas através de dados de Olá na área de trabalho de Olá, ao contrário Olá alertas em cada painel de recursos, o que é específica do recurso. Assim, pode definir um alerta que procura em todas as bases de dados, em vez de definir um por base de dados. Em alternativa, pode também escrever um alerta que utiliza uma consulta composta em vários tipos de recursos. As consultas só são limitadas pelos dados Olá disponíveis na área de trabalho Olá.

Análise de registos da base de dados do SQL Server é cobrada com base no volume de dados de Olá na área de trabalho Olá. Neste tutorial, vai criar uma área de trabalho gratuita, que é limitado too500MB por dia. Assim que esse limite é atingido dados já não são adicionados toohello área de trabalho.


## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Instalar e configurar o Log Analytics (OMS)
> * Utilize conjuntos de toomonitor de análise de registos e as bases de dados

[Tutorial de análise de inquilinos](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Recursos adicionais

* [Tutoriais adicionais que tirar partido de implementação de aplicações de Wingtip SaaS Olá inicial](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Log Analytics do Azure](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
