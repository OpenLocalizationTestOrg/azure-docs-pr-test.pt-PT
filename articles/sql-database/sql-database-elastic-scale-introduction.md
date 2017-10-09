---
title: aaaScaling enviados com a SQL Database do Azure | Microsoft Docs
description: "Software como um programadores de serviço (SaaS) pode criar facilmente elástico, bases de dados dimensionáveis Olá utilizar estas ferramentas de nuvem"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Aumentar horizontalmente com a Base de Dados SQL do Azure
Pode ampliar a bases de dados SQL do Azure utilizando Olá facilmente **bases de dados elásticas** ferramentas. Estas ferramentas e funcionalidades permitem-lhe utilizar Olá virtualmente ilimitado base de dados de recursos de **SQL Database do Azure** toocreate soluções para cargas de trabalho transacionais e especialmente Software como aplicações de serviço (SaaS). Funcionalidades de base de dados elásticas são compostas por seguinte Olá:

* [Biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md): biblioteca de clientes Olá é uma funcionalidade que permite-lhe toocreate e manter a bases de dados.  Consulte [começar a utilizar as ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).
* [Ferramenta de intercalação de divisão de bases de dados elástica](sql-database-elastic-scale-overview-split-and-merge.md): move dados entre bases de dados em partição horizontal. Isto é útil para mover dados de um multi-inquilino da base de dados tooa único inquilino da base de dados (ou vice-versa). Consulte [tutorial da ferramenta de intercalação de divisão de base de dados elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [As tarefas de base de dados elásticas](sql-database-elastic-jobs-overview.md) (pré-visualização): utilizar tarefas toomanage grande número de bases de dados SQL do Azure. Facilmente execute operações administrativas como alterações de esquema, gestão de credenciais, as atualizações de dados de referência, recolha de dados de desempenho ou a coleção de telemetria de inquilino (cliente) através de tarefas.
* [Consulta de base de dados elástica](sql-database-elastic-query-overview.md) (pré-visualização): permite-lhe consulta toorun Transact-SQL que abrange várias bases de dados. Isto permite que as ferramentas de tooreporting de ligação, tais como o Excel, PowerBI, Tableau, etc.
* [Transações elásticas](sql-database-elastic-transactions-overview.md): esta funcionalidade permite-lhe toorun transações que abrangem várias bases de dados na base de dados do Azure SQL. Transações da base de dados elásticas estão disponíveis para aplicações de .NET através do ADO .NET e integrar com Olá familiar experiência de programação utilizando Olá [System.Transaction classes](https://msdn.microsoft.com/library/system.transactions.aspx).

gráfico de Olá abaixo mostra uma arquitetura que inclui Olá **funcionalidades da base de dados elástica** na coleção de tooa de relação de bases de dados.

Este gráfico, cores da base de dados de Olá representam o esquemas. Bases de dados com Olá mesma partilha de cor Olá mesmo esquema.

1. Um conjunto de **bases de dados SQL do Azure** estão alojados no Azure através de arquitetura de fragmentação.
2. Olá **biblioteca de clientes de base de dados elástica** está definido toomanage utilizado um ID de partição horizontal.
3. Um subconjunto das bases de dados de Olá são colocados um **conjunto elástico**. (Consulte [o que é um agrupamento?](sql-database-elastic-pool.md)).
4. Um **tarefa da base de dados elástica** executa agendada ou scripts T-SQL de ad-hoc em todas as bases de dados.
5. Olá **ferramenta de intercalação de divisão** toomove utilizados dados de um ID de partição horizontal tooanother.
6. Olá **consulta de base de dados elástica** permite-lhe toowrite uma consulta que abrange todas as bases de dados no conjunto de partições horizontais Olá.
7. **Transações elásticas** permite-lhe toorun transações que abrangem várias bases de dados. 

![Ferramentas de Bases de Dados Elásticas][1]

## <a name="why-use-hello-tools"></a>Porquê utilizar ferramentas de Olá?
Elasticidade alcançar e escala para aplicações em nuvem foi simples para VMs e armazenamento de BLOBs – simplesmente adicionam ou subtrair unidades ou aumentam energia. Mas permaneceu um desafio de monitorização de estado de processamento de dados nas bases de dados relacionais. Desafios emerged nos seguintes cenários:

* A crescer e reduzir a capacidade de parte de base de dados relacional Olá da sua carga de trabalho.
* Gestão de hotspots que podem surgir que afetam um subconjunto específico de dados - por exemplo, um fim-cliente particularmente ocupado (inquilino).

Tradicionalmente, os cenários, como estes tem foi tratados investindo em aplicações de Olá de toosupport de servidores de base de dados de grande escala. No entanto, esta opção é limitada na nuvem de olá onde todo o processamento ocorre no hardware do produto predefinidas. Em vez disso, a distribuição de dados e processamento em muitas bases de dados de forma idêntica estruturada (um padrão de escalamento horizontal conhecido como "fragmentação") fornece uma alternativa tootraditional abordagens de dimensionamento, tanto em termos de custo e a elasticidade.

## <a name="horizontal-and-vertical-scaling"></a>Dimensionamento horizontal e vertical
figura Olá abaixo mostra Olá horizontais e verticais dimensões de dimensionamento, que são formas básico Olá bases de dados elásticas Olá podem ser ampliadas.

![Horizontal versus Vertical Scaleout][2]

Dimensionamento horizontal refere-se tooadding ou remover bases de dados na capacidade de tooadjust ordem ou desempenho global. Isto também é denominado "dimensionamento" out. Fragmentação, na qual os dados estão particionados através de uma coleção de bases de dados de forma idêntica structured, é um tooimplement comuns de forma horizontal dimensionamento.  

Dimensionamento vertical refere tooincreasing ou diminuir o nível de desempenho de Olá de uma base de dados individuais — Isto também é conhecido como "como aumentar verticalmente."

A maioria das aplicações de base de dados de escala da nuvem irão utilizar uma combinação destes dois estratégias. Por exemplo, um Software como uma aplicação de serviço pode utilizar horizontal dimensionamento tooprovision fim-clientes novos e vertical dimensionamento tooallow cada fim-cliente da base de dados toogrow ou operação de encolhimento recursos conforme necessário por carga de trabalho Olá.

* Dimensionamento horizontal gerido utilizando Olá [biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md).
* Dimensionamento vertical é realizada através de camada de serviço do Azure PowerShell cmdlets toochange hello, ou colocando a bases de dados num agrupamento elástico.

## <a name="sharding"></a>Fragmentação
*Fragmentação* é uma técnica toodistribute grandes quantidades de dados de forma idêntica estruturados através de um número de bases de dados independentes. É especialmente popular com os programadores de nuvem criar Software como um ofertas de serviço (SAAS) para clientes finais ou as empresas. Estes clientes finais são frequentemente referidos tooas "inquilinos". Fragmentação poderão ser necessária para diversas razões:  

* quantidade total de Olá de dados é demasiado grande toofit dentro de restrições de Olá de uma base de dados
* débito de transação de Olá de Olá carga de trabalho geral excede as capacidades de Olá de uma base de dados
* Os inquilinos podem requerem isolamento de físico uns dos outros, pelo que são necessários bases de dados separadas para cada inquilino
* Secções diferentes de uma base de dados poderão ter tooreside em diversas localizações geográficas para compatibilidade, desempenho ou motivos geopolíticos.

Outros cenários, como a ingestão de dados dos dispositivos distribuídos, fragmentação pode ser utilizado toofill um conjunto de bases de dados que se encontram organizados temporariamente. Por exemplo, uma base de dados individual pode ser dedicado tooeach dias ou semanas. Nesse caso, a chave de fragmentação do Olá pode ser uma data do Olá de representing número inteiro (presente em todas as linhas das tabelas em partição horizontal Olá) e consultas de obtenção de informações para um intervalo de datas devem ser encaminhadas pelo subconjunto de toohello aplicação Olá das bases de dados que abrangem o intervalo de Olá em pergunta.

Fragmentação funciona melhor quando todas as transações de uma aplicação podem ser restringida tooa único valor de uma chave de fragmentação. Que assegura que todas as transações será local tooa base de dados específica.

## <a name="multi-tenant-and-single-tenant"></a>Multi-inquilino e de inquilino único
Algumas aplicações usam a abordagem mais simples de Olá de criação de uma base de dados separada para cada inquilino. Este é Olá **padrão de fragmentação de inquilino único** que fornece o recurso dimensionamento granularidade Olá do inquilino Olá, capacidade de cópia de segurança/restauro e isolamento. Com a fragmentação de inquilino único, cada base de dados está associado a um valor de ID de inquilino específico (ou valor de chave de cliente), mas essa chave não tem sempre de ser presente em dados de Olá propriamente ditos. É Olá tooroute de responsabilidade da aplicação cada pedido toohello adequada da base de dados - e biblioteca de clientes Olá pode simplificar isto.

![Inquilino único versus multi-inquilino][4]

Outros cenários do pacote de vários inquilinos em conjunto para bases de dados, em vez de isolá-las em bases de dados separadas. Este é típica **padrão de fragmentação do multi-inquilino** - e pode ser controlada pelo facto de Olá que uma aplicação gere grande número de inquilinos muito pequenos. Fragmentação do multi-inquilino, linhas de Olá nas tabelas de base de dados de Olá estão que todos concebido toocarry uma chave de identificar a chave de fragmentação ou o ID do inquilino de Olá. Novamente, a camada da aplicação Olá é responsável por encaminhamento pedido toohello adequada da base de dados um inquilino e isto pode ser suportado pela biblioteca de cliente de base de dados elástica Olá. Além disso, a segurança ao nível da linha pode ser utilizado toofilter que linhas cada inquilino pode aceder ao - para obter mais informações, consulte [aplicações de multi-inquilinos com segurança ao nível da linha e ferramentas de base de dados elástica](sql-database-elastic-tools-multi-tenant-row-level-security.md). Redistribuir dados entre bases de dados pode ser necessária, com o padrão de fragmentação do multi-inquilino de Olá, e este processo é facilitado através da ferramenta de intercalação de divisão de base de dados elástica Olá. toolearn mais informações sobre os padrões de estrutura de aplicações SaaS que utilizam conjuntos elásticos, consulte [padrões de estrutura de aplicações de SaaS multi-inquilino com a SQL Database do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Mover dados de vários inquilinos toosingle as bases de dados
Ao criar uma aplicação SaaS, é normal toooffer potenciais clientes que uma versão de avaliação do Olá software. Neste caso, é económica toouse uma base de dados do multi-inquilino para dados de Olá. No entanto, quando um prospect torna-se um cliente, uma base de dados único inquilino é melhor uma vez que fornece um melhor desempenho. Se o cliente Olá tinha criado dados durante o período de avaliação de Olá, utilize Olá [ferramenta de intercalação de divisão](sql-database-elastic-scale-overview-split-and-merge.md) toomove dados Olá Olá toohello multi-inquilino novo único inquilino da base de dados.

## <a name="next-steps"></a>Passos seguintes
Para uma aplicação de exemplo que demonstra a biblioteca de clientes Olá, consulte [começar com ferramentas elásticas Datababase](sql-database-elastic-scale-get-started.md).

tooconvert existente ferramentas de Olá toouse de bases de dados, consulte [existente a migrar bases de dados de saída tooscale](sql-database-elastic-convert-to-use-elastic-tools.md).

Consulte informações específicas de Olá toosee do conjunto elástico Olá, [considerações sobre preço e desempenho de um conjunto elástico](sql-database-elastic-pool.md), ou criar um novo conjunto com [conjuntos elásticos](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

