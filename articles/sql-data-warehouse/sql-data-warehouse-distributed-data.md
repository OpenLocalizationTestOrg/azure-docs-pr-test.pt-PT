---
title: "aaaHow distribuída funciona de dados no Azure SQL Data Warehouse | Microsoft Docs"
description: "Saiba como os dados são distribuídos para em massa paralelas processamento (MPP) e Olá opções de distribuição de tabelas do Azure SQL Data Warehouse e Parallel Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Dados distribuídos e tabelas distribuídas para em massa paralelas processamento (MPP)
Saiba como os dados de utilizador são distribuídos no Azure SQL Data Warehouse e Parallel Data Warehouse, que são os sistemas de em massa paralelas processamento (MPP) da Microsoft. Conceber a sua toouse do armazém de dados dados distribuídos eficazmente ajuda-o a tooachieve Olá processamento de consultas vantagens de Olá arquitetura MPP. Algumas opções de design de base de dados podem ter um impacto significativo em melhorar o desempenho das consultas.  

> [!NOTE]
> O Azure SQL Data Warehouse e Olá de utilização de Parallel Data Warehouse mesmo processamento paralelo em grande escala (MPP) design, mas têm algumas diferenças devido a Olá subjacente plataforma. O SQL Data Warehouse é uma plataforma como serviço (PaaS) que é executado no Azure. Parallel Data Warehouse é executado no sistema de plataforma de análise (APS) que é uma aplicação no local que é executado no Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>O que é distribuídos dados?
No SQL Data Warehouse e Parallel Data Warehouse, dados distribuídos refere-se dados toouser que são armazenados em várias localizações em Olá sistema MPP. Cada uma dessas localizações funciona como um armazenamento independente e a unidade de processamento que executa as consultas no respetivo parte dos dados de Olá. Dados distribuídos são fundamental toorunning consultas no desempenho de consulta elevado tooachieve paralela.

toodistribute dados, o armazém de dados de Olá atribui cada linha de uma tabela tooone distribuída da localização do utilizador.  Pode distribuir tabelas com um método de distribuição hash nem um método de round robin. método de distribuição Olá é especificado em Olá instrução CREATE TABLE. 

## <a name="hash-distributed-tables"></a>Tabelas hash distribuída
Olá seguinte diagrama ilustra como um completo (tabela não distribuído) obtém armazenado como uma tabela hash distribuída. Uma função determinista atribui a distribuição de tooone de toobelong cada linha. Na definição da tabela Olá, uma das colunas de Olá está designada como coluna de distribuição Olá. função de hash de Olá utiliza o valor de Olá no Olá distribuição coluna tooassign distribuição de tooa cada linha.

Existem considerações de desempenho para a seleção de Olá de uma coluna de distribuição, como distinctness, desfasamento de dados e tipos de Olá de consultas executadas num sistema Olá.

![Tabela de distribuídas](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "tabela distribuídas")  

* Cada linha pertence tooone distribuição.  
* Um algoritmo de hash determinista atribui a distribuição de tooone cada linha.  
* número de Olá de linhas de tabela por distribuição varia conforme exibido tamanhos diferentes de Olá de tabelas.

## <a name="round-robin-distributed-tables"></a>Tabelas distribuídas round robin
Uma tabela distribuída round robin distribui linhas Olá atribuindo a distribuição de tooa cada linha de uma forma sequencial. É dados tooload rápido numa tabela round robin, mas o desempenho de consulta pode ser mais lento.  Associar uma tabela de round robin, normalmente, requer reshuffling Olá linhas tooenable Olá consulta tooproduce um resultado preciso, que demora tempo.

## <a name="distributed-storage-locations-are-called-distributions"></a>Localizações de armazenamento distribuído são denominadas distribuições
Cada localização distribuída é designada uma distribuição. Quando executa uma consulta em paralelo, cada distribuição executa uma consulta SQL na sua parte dos dados de Olá. SQL Data Warehouse utiliza a consulta de Olá toorun de base de dados SQL. Parallel Data Warehouse utiliza a consulta do SQL Server toorun Olá. Esta estrutura de arquitetura de nada partilhado é fundamental tooachieving Escalamento horizontal computação paralela.

### <a name="can-i-view-hello-distributions"></a>Pode ver as distribuições de Olá?
Cada distribuição tem um ID de distribuição e fica visível em vistas de sistema que dizem respeito tooSQL do armazém de dados e Parallel Data Warehouse. Pode utilizar o desempenho das consultas tootroubleshoot Olá distribuição ID e outros problemas. Para obter uma lista de vistas de sistema Olá, consulte Olá [vista de sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Diferença entre uma distribuição e um nó de computação
Uma distribuição é a unidade básica de Olá para armazenar dados distribuídos e processamento de consultas paralelas. Distribuições estão agrupadas em nós de computação. Cada nó de computação controla as distribuições de um ou mais.  

* Analytics Platform System usa nós de computação como um componente central das capacidades de arquitetura e escalável de hardware de Olá. Utiliza sempre oito distribuições por nó de computação, conforme mostrado no diagrama de Olá para tabelas hash distribuída. Olá, número de nós de computação e Olá, por conseguinte, o número de distribuições, é determinado pelo número de Olá de nós de computação que comprar para aplicação Olá. Por exemplo, se comprar oito nós de computação, obter 64 distribuições (8 nós x 8 distribuições/nó de computação). 
* Armazém de dados do SQL Server tem um número fixo de 60 Distribuições e um número de nós de computação flexível. nós de computação Olá são implementados com recursos de computação e armazenamento do Azure. Pode alterar o número de Olá de nós de computação de acordo com toohello back-end serviço carga de trabalho e a capacidade de computação de Olá (DWUs) Especifique Olá do armazém de dados. Quando altera o número de Olá de nós de computação, número de Olá de distribuições por nó de computação também é alterado. 

### <a name="can-i-view-hello-compute-nodes"></a>Pode ver nós de computação de Olá?
Cada nó de computação tem um ID de nó e fica visível em vistas de sistema que dizem respeito tooSQL do armazém de dados e Parallel Data Warehouse.  Pode ver o nó de computação Olá ao procurar pela coluna de node_id Olá nas vistas de sistema cujos nomes começam por sys.pdw_nodes. Para obter uma lista de vistas de sistema Olá, consulte Olá [vista de sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Tabelas replicadas
Uma tabela que é replicada tem um totalmente cópia da tabela de Olá armazenados em cada nó de computação. Uma tabela a ser replicada remove os dados de tootransfer de necessidade de Olá entre nós de computação antes de uma associação ou agregação. As tabelas replicadas não são apenas exequível com tabelas pequenas devido a Olá tabela completa do armazenamento adicional necessário toostore Olá em cada nó de computação.  

Olá diagrama seguinte mostra uma tabela não replicada que está armazenada em cada nó de computação. Para o SQL Data Warehouse, tabela replicada Olá é totalmente copiados tooa a base de dados de distribuição em cada nó de computação. Para Parallel Data Warehouse, tabela replicada Olá é armazenada em todos os discos atribuídos nó de computação toohello.  Esta estratégia de disco é implementada através da utilização de grupos de ficheiros do SQL Server.  

![Tabela de replicados](media/sql-data-warehouse-distributed-data/replicated-table.png "replicados tabela") 

## <a name="next-steps"></a>Passos seguintes
tabelas de toouse distribuído de forma eficaz, consulte [distribuir tabelas no armazém de dados do SQL Server](sql-data-warehouse-tables-distribute.md)  

