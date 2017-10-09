---
title: "esquema de base de dados do Azure SQL aaaManage numa aplicação multi-inquilino | Microsoft Docs"
description: "Gerir o Esquema para vários inquilinos numa aplicação multi-inquilino que utiliza a Base de Dados SQL do Azure"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Gerir o esquema para vários inquilinos no Olá aplicação Wingtip SaaS

Olá [primeiro tutorial de Wingtip SaaS](sql-database-saas-tutorial.md) mostra como aplicação Olá pode aprovisionar uma base de dados do inquilino e registá-lo no catálogo de Olá. Como qualquer aplicação Olá aplicação Wingtip SaaS será evoluir ao longo do tempo e, por vezes irá necessitar de base de dados de toohello de alterações. As alterações podem incluir o esquema nova ou alterada, os dados de referência de novas ou alteradas e desempenho de aplicações ideal de tooensure de tarefas de manutenção de rotina da base de dados. Com uma aplicação SaaS, estas alterações necessitam de toobe implementado de forma coordenada através de uma frota potencialmente grande de bases de dados do inquilino. Para estes toobe de alterações de inquilino no futuro bases de dados, que precisam toobe incorporada no processo de aprovisionamento de Olá.

Este tutorial explicar dois cenários - implementação de atualizações de dados de referência para todos os inquilinos, e retuning um índice numa Olá tabela que contém dados de referência de Olá. Olá [as tarefas elásticas](sql-database-elastic-jobs-overview.md) funcionalidade é utilizada tooexecute estas operações em todos os inquilinos e Olá *dourada* base de dados do inquilino que é utilizado como um modelo para novas bases de dados.

Neste tutorial, ficará a saber como:

> [!div class="checklist"]

> * Criar uma conta de tarefa
> * Consulta em vários inquilinos
> * Atualizar dados em todas as bases de dados de inquilinos
> * Criar um índice numa tabela em todas as bases de dados de inquilinos


toocomplete neste tutorial, Olá se disponibilizar os seguintes pré-requisitos são cumpridos:

* Olá Wingtip SaaS aplicação é implementada. toodeploy em menos de cinco minutos, consulte [implementar e explorar aplicações de Wingtip SaaS Olá](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter mais detalhes, veja [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* Olá mais recente versão do SQL Server Management Studio (SSMS) está instalada. [Transferir e instalar o SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Este tutorial utiliza funcionalidades do Olá serviço base de dados do SQL Server que estão numa (tarefas de bases de dados elásticas) de pré-visualização limitada. Se desejar toodo neste tutorial, forneça o id de subscrição tooSaaSFeedback@microsoft.com com o requerente = elástico de tarefas de pré-visualização. Depois de receber a confirmação de que a sua subscrição tiver sido ativada, [transferir e instalar os cmdlets de tarefas de pré-versão mais recentes Olá](https://github.com/jaredmoo/azure-powershell/releases). Esta pré-visualização é limitada, por isso, contacte SaaSFeedback@microsoft.com para suporte ou questões relacionados.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Introdução tooSaaS padrões de gestão de esquema

Olá único inquilino por base de dados SaaS padrão benefícios em muitos aspetos do isolamento de dados de Olá resulta, mas em Olá simultâneo apresenta a complexidade adicional de Olá da manutenção e gestão de muitas bases de dados. [As tarefas elásticas](sql-database-elastic-jobs-overview.md) facilita a administração e gestão de camada de dados do SQL Server Olá. As tarefas permitem-lhe toosecurely e fiável, executam tarefas (scripts T-SQL) independentes da interação do utilizador ou de entrada, um grupo de bases de dados. Este método pode ser utilizado toodeploy esquema e alterações de dados de referência comuns em todos os inquilinos numa aplicação. As tarefas elásticas também podem ser utilizado toomaintain um *dourada* cópia da base de dados de Olá utilizado toocreate novos inquilinos, assegurando que tem dados de esquema e de referência mais recentes no Olá sempre.

![ecrã](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Pré-visualização limitada das Tarefas Elásticas

Existe uma nova versão das Tarefas Elásticas, que agora é uma funcionalidade integrada da Base de Dados SQL do Azure (não requer nenhum componente ou serviço adicional). Esta nova versão das Tarefas Elásticas está atualmente em pré-visualização limitada. Esta pré-visualização limitada atualmente suporta contas de trabalho do PowerShell toocreate e toocreate T-SQL e gerir tarefas.

> [!NOTE]
> *Este tutorial utiliza funcionalidades do Olá serviço base de dados do SQL Server que estão numa (tarefas de bases de dados elásticas) de pré-visualização limitada. Se desejar toodo neste tutorial, forneça o id de subscrição tooSaaSFeedback@microsoft.com com o requerente = elástico de tarefas de pré-visualização. Depois de receber a confirmação de que a sua subscrição tiver sido ativada, [transferir e instalar os cmdlets de tarefas de pré-versão mais recentes Olá](https://github.com/jaredmoo/azure-powershell/releases). Esta pré-visualização é limitada, por isso, contacte SaaSFeedback@microsoft.com para suporte ou questões relacionados.*

## <a name="get-hello-wingtip-application-scripts"></a>Obter Olá Wingtip aplicação scripts

Olá Wingtip SaaS scripts e código fonte da aplicação estão disponíveis no Olá [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório do github. [Os passos scripts de Wingtip SaaS toodownload Olá](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Criar uma base de dados das contas de tarefa e uma nova conta de tarefa

Este tutorial requer PowerShell toocreate Olá tarefa da base de dados e a tarefa de conta. Tal como MSDB e SQL Server Agent, utiliza as tarefas elásticas um Azure SQL da base de dados toostore definições de tarefas, o estado de tarefa e o histórico. Depois de Olá tarefa conta estiver criada, pode criar e monitorizar tarefas imediatamente.

1. Abra... \\Learning módulos\\esquema gestão\\*demonstração SchemaManagement.ps1* no Olá **ISE do PowerShell**.
1. Prima **F5** script de Olá toorun.

Olá *demonstração SchemaManagement.ps1* script chamadas Olá *implementar SchemaManagement.ps1* script toocreate um *S2* com o nome da base de dados **jobaccount** num servidor de catálogo Olá. Em seguida, cria conta de tarefa Olá, passando a base de dados do Olá jobaccount como uma chamada de criação de conta do parâmetro toohello tarefa.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Criar uma tarefa toodeploy novos referência dados tooall inquilinos

Cada base de dados do inquilino inclui um conjunto de tipos de venue que definem o tipo de Olá dos eventos que estão alojados num venue. Neste exercício, implementar um tipos de venue adicionais do atualização tooall Olá inquilino bases de dados tooadd dois: *da sua motocicleta Racing* e *Swimming Club*. Estes tipos de venue correspondem a imagem de fundo de toohello que vê na aplicação de eventos do Olá inquilino.

Clique em Olá Venue tipo menu pendente e validar que estão disponíveis apenas 10 opções de tipo venue e, especificamente esse 'Da sua motocicleta Racing' e 'Swimming Club' não estão incluídos na lista de Olá.

Agora vamos criar um Olá de tooupdate tarefa *VenueTypes* uma tabela em todas as bases de dados de inquilino de Olá e adicionar novos tipos de venue Olá.

uma nova tarefa toocreate, podemos utilizar um conjunto de tarefas de sistema armazenados procedimentos criados na base de dados do Olá jobaccount quando Olá tarefa conta foi criada.

1. Abra o SSMS e ligar o servidor de catálogo toohello: catálogo -\<utilizador\>. database.windows.net servidor
1. Também ligar o servidor de inquilino toohello: tenants1 -\<utilizador\>. database.windows.net
1. Procurar toohello *contosoconcerthall* base de dados no Olá *tenants1* hello do servidor e a consulta *VenueTypes* tooconfirm de tabela que *da sua motocicleta Racing*  e *Swimming Club* **não são** na lista de resultados de Olá.
1. Ficheiro aberto Olá... \\Learning módulos\\esquema gestão\\DeployReferenceData.sql
1. Modificar a instrução de Olá: definir @wtpUser = &lt;utilizador&gt; e substitua o valor de utilizador de Olá utilizado quando implementou a aplicação de Wingtip Olá
1. Certifique-se de que a base de dados de jobaccount toohello ligado e prima **F5** para executar o script de Olá

* **SP\_adicionar\_destino\_grupo** cria o nome do grupo de destino da Olá DemoServerGroup, agora é preciso tooadd membros de destino.
* **SP\_adicionar\_destino\_grupo\_membro** adiciona um *servidor* tipo de membro, considere todas as bases de dados dentro desse (tenha em atenção é Olá tenants1-doservidordedestino&lt; Utilizador&gt; server com bases de dados de inquilino de Olá) no momento da tarefa de execução deve ser incluída na tarefa de Olá, Olá segundo é adicionar uma *base de dados* como alvo o tipo de membro, especificamente Olá ('dourada' da base de dados basetenantdb) que reside no catálogo -&lt;utilizador&gt; servidor e por último outro *base de dados* destino grupo membro tipo tooinclude Olá adhocanalytics base de dados que é utilizado um tutorial posterior.
* **sp\_add\_job** cria uma tarefa denominada “Implementação de Dados de Referência”
* **SP\_adicionar\_passo** cria o passo da tarefa Olá que contém o T-SQL comando texto tooupdate Olá tabela de referência, VenueTypes
* vistas de restantes Olá no script de Olá apresentam existência Olá de objetos de Olá e execução da tarefa de monitorização. Utilize o valor do Estado tooreview Olá estas consultas Olá **ciclo de vida** toodetermine de coluna quando a tarefa de Olá foi concluída com êxito em todas as bases de dados do inquilino e Olá duas bases de dados adicionais que contém a tabela de referência de Olá.

1. No SSMS, navegue toohello *contosoconcerthall* base de dados no Olá *tenants1* hello do servidor e a consulta *VenueTypes* tooconfirm de tabela que *Motorcycle Racing* e *Swimming Club* **são** agora na lista de resultados de Olá.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Criar um índice de tabela de referência do tarefa toomanage Olá

Exercício anterior toohello semelhante, este exercício cria um índice de Olá tarefa toorebuild na chave primária da tabela referência Olá, uma operação de gestão de base de dados típicas um administrador pode executar após um carregamento de dados de grandes dimensões para uma tabela.

Criar uma tarefa utilizando Olá mesmo tarefas 'system' procedimentos armazenados.

1. Abra o SSMS e ligue toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor
1. Ficheiro aberto Olá... \\Learning módulos\\esquema gestão\\OnlineReindex.sql
1. Clique com o botão direito, selecione a ligação e ligar toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor, se ainda não estiver ligado
1. Certifique-se a base de dados do toohello ligado jobaccount e prima script de Olá F5 toorun

* sp\_add\_job cria uma nova tarefa denominada “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”
* SP\_adicionar\_passo cria o passo da tarefa Olá que contém o índice de Olá de tooupdate de texto de comando de T-SQL




## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]

> * Criar um tooquery de conta de trabalho em vários inquilinos
> * Atualizar dados em todas as bases de dados de inquilinos
> * Criar um índice numa tabela em todas as bases de dados de inquilinos

[Tutorial de análises ad hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Recursos adicionais

* [Tutoriais adicionais que se baseiam Olá implementação de aplicação Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Managing scaled-out cloud databases (Gerir bases de dados de escalamento horizontal na cloud)](sql-database-elastic-jobs-overview.md)
* [Create and manage scaled-out cloud databases (Criar e gerir bases de dados de escalamento horizontal na cloud)](sql-database-elastic-jobs-create-and-manage.md)
