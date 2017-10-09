---
title: aaaAzure dos limites de recursos de base de dados SQL | Microsoft Docs
description: "Esta página descreve alguns limites de recursos comuns para a SQL Database do Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limites de recursos de base de dados SQL do Azure
## <a name="overview"></a>Descrição geral
Base de dados SQL do Azure gere Olá recursos disponíveis tooa base de dados utilizando dois mecanismos diferentes: **governação de recursos** e **imposição dos limites**. Este tópico explica estas duas áreas principais de gestão de recursos.

## <a name="resource-governance"></a>Governação de recursos
Um dos objetivos de estrutura de Olá dos escalões de serviço básico, Standard, Premium e Premium RS Olá para toobehave da SQL Database do Azure como se a base de dados de Olá se encontra em execução na sua própria máquina, isolada de outras bases de dados. Governação de recursos emula este comportamento. Se Olá agregados a utilização de recursos atingir Olá máxima disponível da CPU, memória, e/s de registo e base de dados do toohello atribuído do recursos de e/s de dados, recurso governação consultas de filas em execução e atribuir recursos toohello colocados em fila à medida que as consultas liberte.

Como num computador dedicado, a utilização de todos os resultados de recursos disponíveis numa execução mais atualmente executar consultas, que pode resultar em tempos limite de comandos no cliente Olá. Aplicações com a lógica de repetição agressiva e aplicações que executar consultas na base de dados de Olá com uma frequência alta podem encontrar as mensagens de erros quando tenta consultas novas tooexecute quando foi atingido o limite de Olá de pedidos em simultâneo.

### <a name="recommendations"></a>Recomendações:
Monitorizar a utilização de recursos de Olá e tempos de resposta médio de Olá de consultas quando prestes a máxima utilização de Olá de uma base de dados. Quando encontrar latências de consulta, geralmente, tem três opções:

1. Reduza o número de Olá de receber pedidos toohello da base de dados tooprevent tempo limite e Olá pile cópias de segurança de pedidos.
2. Atribua uma base de dados de toohello nível de desempenho superior.
3. Otimize a utilização de recursos de consultas tooreduce Olá cada consulta. Para obter mais informações, consulte Olá consulta Tuning/Hinting secção no artigo do Olá guia de desempenho de base de dados de SQL do Azure.

## <a name="enforcement-of-limits"></a>Imposição de limites
Recursos que não sejam da CPU, memória, e/s de registo e e/s de dados são impostos pelo negar novos pedidos de quando os limites são atingidos. Quando uma base de dados atinge o limite de tamanho máximo de Olá configurado, inserções e as atualizações que aumentam o tamanho de dados falhar, enquanto seleciona e eliminações continuarem toowork. Os clientes recebem um [mensagem de erro](sql-database-develop-error-messages.md) consoante o limite de Olá que foi atingido.

Por exemplo, número de Olá de ligações tooa SQL da base de dados e o número de Olá de pedidos em simultâneo que podem ser processados são restritos. Base de dados SQL permite-número de Olá de ligações toohello da base de dados toobe superior ao número de Olá de agrupamento de ligações de toosupport de pedidos em simultâneo. Enquanto o número de Olá de ligações que estão disponíveis pode facilmente ser controlado através da aplicação Olá, número de Olá de pedidos paralelos é frequentemente tooestimate mais difícil vezes e toocontrol. Especialmente durante cargas de pico quando a aplicação Olá envia ou demasiados pedidos ou base de dados de Olá atinge os limites de recursos e iniciado o piling cópias de segurança de threads de trabalho devido a consultas em execução toolonger, podem ser encontrados erros.

## <a name="service-tiers-and-performance-levels"></a>Escalões de serviço e níveis de desempenho
Existem camadas de serviços e níveis de desempenho de bases de dados individuais e conjuntos elásticos.

### <a name="single-databases"></a>Bases de dados individuais
Para uma base de dados, os limites de Olá de uma base de dados são definidos por Olá da base de dados e o desempenho do escalão de nível de serviço. Olá, a tabela seguinte descreve as características de Olá das bases de dados básicas, Standard, Premium e Premium RS em vários níveis de desempenho.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Clientes que utilizam os níveis de desempenho P11 e P15 pode utilizar a cópia de segurança too4 TB de armazenamento incluído sem encargos adicionais. Esta opção de 4 TB está atualmente disponível na Olá seguintes regiões: East2 nos, EUA oeste, Virginia us dos EUA, Europa Ocidental, Alemanha Central, Sul Oriental, leste do Japão, leste da Austrália, Canadá Central e Canadá Leste.
>

### <a name="elastic-pools"></a>Conjuntos elásticos
[Conjuntos elásticos](sql-database-elastic-pool.md) partilhar recursos em bases de dados no agrupamento de Olá. Olá, a tabela seguinte descreve as características de Olá dos conjuntos elásticos básicas, Standard, Premium e Premium RS.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Para uma definição expandida de cada recurso listado nas tabelas anteriores Olá, consulte as descrições de Olá no [capacidades de camadas e limites de serviço](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Para obter uma descrição geral dos escalões de serviço, consulte [escalões de serviço de base de dados de SQL do Azure e níveis de desempenho](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Outros limites de base de dados SQL
| Área | Limite | Descrição |
| --- | --- | --- |
| Bases de dados utilizando a exportação automática por subscrição |10 |A exportação automática permite-lhe toocreate uma agenda personalizada para cópias de segurança das bases de dados do SQL Server. pré-visualização de Olá desta funcionalidade irá terminar em 1 de Março de 2017.  |
| Bases de dados por servidor |Cópia de segurança too5000 |Cópia de segurança too5000 bases de dados são permitidas por servidor. |
| DTUs por servidor |45000 |Para o aprovisionamento de bases de dados autónomo e conjuntos elásticos, 45000 DTUs são permitidas por servidor. número total de Olá de bases de dados autónomo e agrupamentos permitidos por servidor só está limitado pelo número de hello do servidor DTUs.  

> [!IMPORTANT]
> Azure SQL da base de dados automática de exportar está agora em pré-visualização e irá ser reformada no dia 1 de Março de 2017. A partir de 1 de Dezembro de 2016, já não será capaz de tooconfigure automatizada exportação em qualquer base de dados do SQL Server. Todas as suas tarefas de exportação automática existente irão continuar toowork até 1 de Março de 2017. Depois de 1 de Dezembro de 2016, pode utilizar [retenção de cópias de segurança de longa duração](sql-database-long-term-retention.md) ou [da automatização do Azure](../automation/automation-intro.md) bases de dados do SQL tooarchive periodicamente através do PowerShell periodicamente de acordo com a agenda de tooa à sua escolha. Para obter um script de exemplo, pode transferir Olá [script a partir do GitHub de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Recursos
[Subscrição do Azure e limites de serviço, Quotas e restrições](../azure-subscription-service-limits.md)

[Escalões de serviço de base de dados SQL do Azure e níveis de desempenho](sql-database-service-tiers.md)

[Mensagens de erro para os programas de clientes da Base de Dados SQL (Error messages for SQL Database client programs)](sql-database-develop-error-messages.md)
