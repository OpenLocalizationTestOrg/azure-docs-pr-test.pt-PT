---
title: bases de dados de nuvem de escalamento horizontal de aaaManaging | Microsoft Docs
description: "Ilustra o serviço de tarefas de bases de dados elásticas Olá"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Gerir bases de dados de nuvem de escalamento horizontal
Olá toomanage expandidos a bases de dados, **tarefas de bases de dados elásticas** funcionalidade ativa (pré-visualização) tooreliably executar um script de Transact-SQL (T-SQL) entre um grupo de bases de dados, incluindo:

* uma coleção personalizado de bases de dados (explicado abaixo)
* todas as bases de dados num [conjunto elástico](sql-database-elastic-pool.md)
* um conjunto de partições horizontais (criado utilizando [biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md)). 

## <a name="documentation"></a>Documentação
* [Instalar componentes de tarefa de base de dados elástica Olá](sql-database-elastic-jobs-service-installation.md). 
* [Começar a utilizar com as tarefas de bases de dados elásticas](sql-database-elastic-jobs-getting-started.md).
* [Criar e gerir tarefas através do PowerShell](sql-database-elastic-jobs-powershell.md).
* [Criar e gerir expandido terminar bases de dados do Azure SQL](sql-database-elastic-jobs-getting-started.md)

**As tarefas de base de dados elásticas** é atualmente um cliente alojado do Azure serviço em nuvem que permite a execução de Olá de ad-hoc e agendadas tarefas administrativas, que são chamadas **tarefas**. Com tarefas, pode facilmente e fiável gerir grandes grupos de bases de dados do Azure SQL ao executar operações administrativas do Transact-SQL scripts tooperform. 

![Serviço de tarefas de base de dados elástica][1]

## <a name="why-use-jobs"></a>Porquê utilizar tarefas?
**Gerir**

Facilmente Efetue alterações de esquema, gestão de credenciais, as atualizações de dados de referência, recolha de dados de desempenho ou a coleção de telemetria do inquilino (cliente).

**Relatórios**

Dados agregados de uma coleção de bases de dados do Azure SQL Server para uma tabela de destino única.

**Reduzir a sobrecarga**

Normalmente, tem de ligar a base de dados de tooeach independentemente nas instruções de Transact-SQL de toorun de ordem ou efetuar outras tarefas administrativas. Uma tarefa processa as tarefas de Olá de início de sessão na base de dados de tooeach no grupo de destino Olá. Pode também define, manter e manter o Transact-SQL toobe de scripts executado entre um grupo de bases de dados do Azure SQL.

**Gestão de contas**

As tarefas executadas Olá script e registo Olá o estado de execução para cada base de dados. Também obter a repetição automática quando ocorrem falhas.

**Flexibilidade**

Definir grupos personalizados de bases de dados do Azure SQL e definir agendas para executar uma tarefa.

> [!NOTE]
> No portal do Azure Olá, só um conjunto de funções reduzido limitada tooSQL Azure elástico agrupamentos está disponível. Utilize Olá conjunto completo de APIs de PowerShell tooaccess Olá de funcionalidade atual.
> 
> 

## <a name="applications"></a>Aplicações
* Execute tarefas administrativas, tal como implementar um novo esquema.
* Atualize informações de produto de dados de referência comuns em todas as bases de dados. Ou agendas automático atualiza cada dia da semana, após horas.
* Reconstrua o desempenho das consultas tooimprove índices. Olá reconstruir pode ser configurado tooexecute através de uma coleção de bases de dados numa base periódica, tal como durante as horas de ponta.
* Recolha os resultados da consulta de um conjunto de bases de dados numa tabela central numa base em curso. As consultas de desempenho podem ser executadas continuamente e configurado tootrigger tarefas adicionais toobe executado.
* Executar consultas mais de processamento de dados em execução num grande conjunto de bases de dados, por exemplo Olá coleção de telemetria de cliente. Os resultados são recolhidos para uma tabela de destino única para análise adicional.

## <a name="elastic-database-jobs-end-to-end"></a>As tarefas de base de dados elásticas: ponto a ponto
1. Instalar Olá **tarefas de bases de dados elásticas** componentes. Para obter mais informações, consulte [tarefas de instalação de base de dados elástica](sql-database-elastic-jobs-service-installation.md). Se a instalação de Olá falhar, consulte [como toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Utilize Olá das APIs do PowerShell tooaccess mais funcionalidade, por exemplo, criar coleções de base de dados personalizado, adicionar as agendas de e/ou a recolha de conjuntos de resultados. Portal de Olá de utilização para a criação/monitorização de tarefas e de instalação simple limitada tooexecution contra um **conjunto elástico**. 
3. Criar credenciais encriptado para execução da tarefa e [adicionar Olá utilizador (ou função) tooeach da base de dados no grupo de Olá](sql-database-security-overview.md).
4. Crie um script T-SQL que pode ser executado relativamente a cada base de dados no grupo de Olá de idempotent. 
5. Siga estes passos toocreate os trabalhos utilizam Olá portal do Azure: [criar e gerir tarefas de bases de dados elásticas](sql-database-elastic-jobs-create-and-manage.md). 
6. Ou utilizar scripts do PowerShell: [criar e gerir tarefas de bases de dados elásticas uma base de dados SQL através do PowerShell (pré-visualização)](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Scripts de Idempotent
scripts de Olá tem de ser [idempotent](https://en.wikipedia.org/wiki/Idempotence). Em termos simples, "idempotent" significa que se o script de Olá com êxito e for executada novamente, hello mesmo resultado ocorre. Um script pode falhar devido a problemas de rede tootransient. Nesse caso, a tarefa Olá automaticamente tentará executar script de Olá um número de vezes antes de desisting predefinido. Um script de idempotent tem Olá mesmo resultar, mesmo que tenha sido executada com êxito duas vezes. 

Uma tática simple é tootest quanto à existência de Olá de um objeto antes de criar.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

Da mesma forma, um script tem de ser capaz de tooexecute com êxito por logicamente testar e countering quaisquer condições que encontra.

## <a name="failures-and-logs"></a>Falhas e os registos
Se um script falhar após várias tentativas, tarefa Olá registará Olá erro e continua. Após termina uma tarefa (isto é, uma execução em todas as bases de dados no grupo de Olá), pode verificar a respetiva lista de tentativas falhadas. registos de Olá fornecem detalhes scripts defeituoso toodebug. 

## <a name="group-types-and-creation"></a>Tipos de grupo e criação
Existem dois tipos de grupos: 

1. Conjuntos de partições horizontais
2. Grupos personalizados

Grupos de conjunto de partições horizontais são criados utilizando Olá [ferramentas de base de dados elástica](sql-database-elastic-scale-introduction.md). Quando cria um grupo de conjunto de partições horizontais, bases de dados são adicionados ou removidos do grupo de Olá automaticamente. Por exemplo, um ID de partição horizontal novo será automaticamente no grupo de Olá quando adicionar toohello mapa de partições horizontais. Em seguida, pode ser executada uma tarefa em relação a grupo Olá.

Grupos personalizados, no Olá por outro lado, rigidly são definidos. Explicitamente tem de adicionar ou remover bases de dados de grupos personalizados. Se uma base de dados no grupo de Olá for removido, a tarefa de Olá tentará script de Olá toorun na base de dados de Olá resultavam uma eventual falha. Os grupos criados utilizando Olá portal do Azure atualmente são grupos personalizados. 

## <a name="components-and-pricing"></a>Os componentes e preços
Olá seguintes componentes funcionam em conjunto toocreate um serviço de nuvem do Azure que permite a execução do ad-hoc das tarefas administrativas. componentes de Olá estão instalados e configurados automaticamente durante a configuração, na sua subscrição. Pode identificar serviços Olá como todos eles ter Olá mesmo gerado automaticamente nome. o nome de Olá é exclusivo e consiste em Olá. o prefixo "edj" seguido de 21 carateres gerados aleatoriamente.

* **Serviço Cloud do Azure**: tarefas de bases de dados elásticas (pré-visualização) é entregue como uma nuvem do Azure alojada de cliente pedida de execução de tooperform do serviço de Olá tarefas. No portal de Olá, serviço Olá é implementado e alojado na sua subscrição do Microsoft Azure. serviço de predefinição implementado de Olá é executado com o mínimo de Olá de funções de trabalho dois para elevada disponibilidade. tamanho predefinido de Olá de cada função de trabalho (ElasticDatabaseJobWorker) é executado numa instância A0. Para os preços, consulte [preços de serviços de Cloud](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Base de dados SQL do Azure**: serviço Olá utiliza uma base de dados de SQL do Azure conhecido como Olá **base de dados de controlo** toostore todos os metadados de tarefa Olá. camada de serviço predefinido Olá é um S0. Para os preços, consulte [preços da SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).
* **Service Bus do Azure**: um Azure Service Bus destina-se coordenação de trabalho de Olá dentro Olá o serviço em nuvem do Azure. Consulte [preços de barramento de serviço](https://azure.microsoft.com/pricing/details/service-bus/).
* **Armazenamento do Azure**: uma conta do Storage Azure é utilizada no evento Olá que um problema requer uma depuração ainda mais o registo de saída de diagnóstico toostore (consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](../cloud-services/cloud-services-dotnet-diagnostics.md)). Para os preços, consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Como funcionam as tarefas de base de dados elástica
1. Uma base de dados do SQL do Azure é designado uma **base de dados de controlo** que armazena todos os dados e estado de dados de metadados.
2. base de dados de controlo de Olá é acedida pela Olá **tarefa serviço** toolaunch e controlar tooexecute de tarefas.
3. Duas funções diferentes comunicam com a base de dados de controlo de Olá: 
   * Controlador: Determina quais as tarefas requerem Olá de tooperform tarefas pedidas tarefa e tarefas falhadas tentativas através da criação de novas tarefas.
   * Tarefa a execução da tarefa: Tarefas de Olá ativada.

### <a name="job-task-types"></a>Tipos de tarefas da tarefa
Existem vários tipos de tarefas que realizar a execução de tarefas:

* ShardMapRefresh: Consultas Olá toodetermine de mapa de partições horizontais todas as bases de dados de Olá utilizados como shards
* ScriptSplit: Script de Olá divisões nas instruções 'ACEDA' em lotes
* ExpandJob: Cria subordinado tarefas para cada base de dados de uma tarefa que tenha como destino um grupo de bases de dados
* ScriptExecution: Executa um script em relação a uma determinada base de dados utilizando as credenciais definidas
* Dacpac: Aplica-se DACPAC tooa determinada base de dados utilizando as credenciais específicas

## <a name="end-to-end-job-execution-work-flow"></a>Fluxo de trabalho do execução tarefa de ponto a ponto
1. Utilizar Olá Portal ou Olá API do PowerShell, uma tarefa é inserida Olá **base de dados de controlo**. tarefa de Olá solicita a execução de um script de Transact-SQL em relação a um grupo de bases de dados utilizando credenciais específicas.
2. controlador Olá identifica nova tarefa de Olá. As tarefas da tarefa são criadas e executar o script de Olá toosplit e bases de dados do grupo de Olá toorefresh. Por último, uma nova tarefa é criada e executar a tarefa de Olá tooexpand e criar novo subordinado tarefas onde cada tarefa subordinada é especificado tooexecute Olá script Transact-SQL em relação a uma base de dados individual num grupo de Olá.
3. controlador Olá identifica Olá criado tarefas subordinadas. Para cada tarefa, o controlador de Olá cria e aciona um tarefa tooexecute Olá script de tarefa de uma base de dados. 
4. Depois de concluir todas as tarefas da tarefa, controlador Olá atualiza o estado do Olá tarefas tooa foi concluída. 
   Em qualquer momento durante a execução da tarefa, Olá API do PowerShell pode ser utilizado tooview Olá estado atual da execução da tarefa. Todas as horas devolvido por Olá das APIs do PowerShell são representados em UTC. Se assim o desejar, um pedido de cancelamento pode ser toostop iniciada uma tarefa. 

## <a name="next-steps"></a>Passos seguintes
[Instalar componentes de Olá](sql-database-elastic-jobs-service-installation.md), em seguida, [criar e adicionar um registo na base de dados de tooeach no grupo de Olá das bases de dados](sql-database-manage-logins.md). toofurther compreender a tarefa de criação e gestão, consulte [criar e gerir tarefas de bases de dados elásticas](sql-database-elastic-jobs-create-and-manage.md). Consulte também [introdução às tarefas de bases de dados elásticas](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


