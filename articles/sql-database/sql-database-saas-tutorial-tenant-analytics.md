---
title: "as consultas de análises de aaaRun contra várias bases de dados SQL do Azure | Microsoft Docs"
description: "Extrair dados de bases de dados do inquilino para uma base de dados de análise para a análise offline"
keywords: tutorial de base de dados sql
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Extrair dados de bases de dados do inquilino para uma base de dados de análise para a análise offline

Neste tutorial, utilize uma tarefa elástico toorun consultas cada base de dados do inquilino. tarefa de Olá extrai dados de vendas de permissão e carrega-o para uma base de dados de análise (ou do armazém de dados) para análise. Olá base de dados de análise em seguida, é consultado tooextract conhecimentos aprofundados sobre estes dados operacionais diárias de todos os inquilinos.


Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar base de dados de análise de inquilino de Olá
> * Criar dados de tooretrieve uma tarefa agendada e preencher a base de dados de análise de Olá

toocomplete neste tutorial, Olá se disponibilizar os seguintes pré-requisitos são cumpridos:

* Olá Wingtip SaaS aplicação é implementada. toodeploy em menos de cinco minutos, consulte [implementar e explorar aplicações de Wingtip SaaS Olá](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter mais detalhes, veja [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* Olá mais recente versão do SQL Server Management Studio (SSMS) está instalada. [Transferir e instalar o SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Padrão de Análise Operacional de Inquilinos

Uma das oportunidades de excelente Olá com aplicações de SaaS é toouse Olá inquilino avançado dados que são armazenados na nuvem de Olá. Utilize este dados toogain aprofundadas operação Olá e a utilização da sua aplicação e inquilinos. Estes dados podem ajudá desenvolvimento da funcionalidade, melhoramentos de Facilidade de utilização e outros investimentos na aplicação Olá e plataforma. O acesso a estes dados é fácil quando existir uma única base de dados multi-inquilino, mas não será tão fácil quando existir uma distribuição à escala através de potencialmente milhares de bases de dados. Uma abordagem tooaccessing estes dados são toouse as tarefas elásticas, que permitem o resultado a devolver resultados da consulta da tarefa execução toobe capturada numa base de dados de saída e a tabela.

## <a name="get-hello-wingtip-application-scripts"></a>Obter Olá Wingtip aplicação scripts

Olá Wingtip SaaS scripts e código fonte da aplicação estão disponíveis no Olá [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório do github. [Os passos scripts de Wingtip SaaS toodownload Olá](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Implementar uma base de dados dos resultados da análise de inquilinos

Este tutorial requer toohave que Olá de toocapture implementada uma base de dados resultante da execução da tarefa de scripts, que contêm a devolver resultados de consultas. Vamos criar uma base de dados chamada tenantanalytics para esta finalidade.

1. Abra... \\Learning módulos\\análise operacional\\inquilino análise\\*demonstração TenantAnalyticsDB.ps1* no Olá *ISE do PowerShell* e defina Olá seguinte valor:
   * **$DemoScenario** = **2** *Implementar a base de dados da análise operacional*
1. Prima **F5** script de demonstração de Olá toorun (que Olá chamadas *implementar TenantAnalyticsDB.ps1* script) que cria Olá inquilino análise da base de dados.

## <a name="create-some-data-for-hello-demo"></a>Criar alguns dados de demonstração de Olá

1. Abra... \\Learning módulos\\análise operacional\\inquilino análise\\*demonstração TenantAnalyticsDB.ps1* no Olá *ISE do PowerShell* e defina Olá seguinte valor:
   * **$DemoScenario** = **1** *Comprar bilhetes para eventos em todos os locais*
1. Prima **F5** toorun Olá script e criar pedido de compra de histórico.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Criar uma análise de inquilino de tooretrieve tarefa agendada sobre compras de permissão

Este script cria uma tooretrieve permissão compra as informações da tarefa a partir de todos os inquilinos. Depois agregado numa única tabela, pode obter métricas insightful avançadas sobre a aquisição padrões entre inquilinos Olá de pedido de suporte.

1. Abra o SSMS e ligue toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor
1. Abra ...\\Módulos de Aprendizagem\\Análise Operacional\\Análise de Inquilinos\\*TicketPurchasesfromAllTenants.sql*
1. Modificar &lt;utilizador&gt;, nome de utilizador de Olá de utilização utilizado quando implementou a aplicação de Wingtip SaaS Olá, Olá parte superior do script Olá, **sp\_adicionar\_destino\_grupo\_membro** e **sp\_adicionar\_passo de tarefa**
1. Clique com o botão direito, selecione **ligação**e ligar toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor, se ainda não estiver ligado
1. Certifique-se de que estão ligado toohello **jobaccount** base de dados e prima **F5** para executar o script de Olá

* **SP\_adicionar\_destino\_grupo** cria o nome do grupo de destino Olá *TenantGroup*, agora é preciso tooadd membros de destino.
* **SP\_adicionar\_destino\_grupo\_membro** adiciona um *servidor* tipo de membro, considere todas as bases de dados dentro do que (tenha em atenção é Olá customer1 - o servidor de destino &lt;Utilizador&gt; server com bases de dados de inquilino de Olá) no momento da tarefa de execução deve ser incluída na tarefa de Olá.
* **sp\_add\_job** cria uma nova tarefa semanal agendada denominada “Compras de Bilhetes de Todos os Inquilinos”
* **SP\_adicionar\_passo** cria o passo da tarefa Olá contendo tooretrieve de texto de comando T-SQL todas as informações de compra de permissão de Olá de todos os inquilinos e Olá cópia devolver resultados para uma tabela chamada  *AllTicketsPurchasesfromAllTenants*
* vistas de restantes Olá no script de Olá apresentam existência Olá de objetos de Olá e execução da tarefa de monitorização. Reveja o valor de estado de Olá de Olá **ciclo de vida** estado de Olá toomonitor de coluna. Uma vez, foi concluída com êxito, a tarefa de Olá foi concluída com êxito em todas as bases de dados do inquilino e de Olá duas bases de dados adicionais, que contém Olá referenciam tabela.

Com êxito a executar o script de Olá deve resultar em resultados semelhantes:

![resultados](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Criar um tooretrieve tarefa adquire uma contagem de resumo de permissão de todos os inquilinos

Este script cria uma soma de tooretrieve de tarefa de todas as compras de permissão de todos os inquilinos.

1. Abra o SSMS e ligue toohello *catálogo -&lt;utilizador&gt;. database.windows.net* servidor
1. Ficheiro aberto Olá... \\Learning módulos\\aprovisionar e catálogo\\análise operacional\\inquilino análise\\*TicketPurchasesfromAllTenants.sql resultados*
1. Modificar &lt;utilizador&gt;, nome de utilizador de Olá de utilização utilizado quando implementou a aplicação de Wingtip SaaS Olá no script de Olá, no Olá **sp\_adicionar\_passo** procedimento armazenado
1. Clique com o botão direito, selecione **ligação**e ligar toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor, se ainda não estiver ligado
1. Certifique-se de que estão ligado toohello **tenantanalytics** base de dados e prima **F5** para executar o script de Olá

Com êxito a executar o script de Olá deve resultar em resultados semelhantes:

![resultados](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** cria uma nova tarefa agendada semanal denominada “ResultsTicketsOrders”

* **SP\_adicionar\_passo** cria o passo da tarefa Olá contendo tooretrieve de texto de comando T-SQL todas as informações de compra de permissão de Olá de todos os inquilinos e Olá cópia devolver resultados para uma tabela chamada CountofTicketOrders

* vistas de restantes Olá no script de Olá apresentam existência Olá de objetos de Olá e execução da tarefa de monitorização. Reveja o valor de estado de Olá de Olá **ciclo de vida** estado de Olá toomonitor de coluna. Uma vez, foi concluída com êxito, a tarefa de Olá foi concluída com êxito em todas as bases de dados do inquilino e de Olá duas bases de dados adicionais, que contém Olá referenciam tabela.


## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Implementar a base de dados de análise de inquilinos
> * Criar uma tarefa agendada tooretrieve analítico de dados entre inquilinos

Parabéns!

## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais baseiam Olá aplicação Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Tarefas elásticas](sql-database-elastic-jobs-overview.md)
