---
title: "aaaMigrate tooSQL sua solução do armazém de dados | Microsoft Docs"
description: "Orientações de migração para colocar a sua plataforma a solução tooAzure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Migrar o tooAzure solução SQL Data Warehouse
Ver o que está envolvido num tooAzure de solução de base de dados do armazém de dados do SQL Server existente a migrar. 

## <a name="profile-your-workload"></a>A carga de trabalho de perfil
Antes de migrar, quer toobe determinada que do armazém de dados do SQL Server é a solução certa do Olá para a carga de trabalho. SQL Data Warehouse é uma análise de tooperform sistema distribuída concebido dados de grandes dimensões.  Migrar tooSQL do armazém de dados requer algumas alterações de estrutura que não são demasiado difícil toounderstand mas poderão demorar algum tempo tooimplement. Se a sua empresa precisar de um armazém de dados de classe empresarial, os benefícios de Olá merecem esforço Olá. No entanto, se não precisa de energia Olá do SQL Data Warehouse, é mais económico toouse do SQL Server ou SQL Database do Azure.

Considere utilizar o SQL Data Warehouse quando tiver:
- Ter um ou mais Terabytes de dados
- Planear a análise de toorun em grandes quantidades de dados
- Tem de Olá capacidade tooscale computação e armazenamento 
- Pretende que os custos de toosave por colocar em pausa recursos de computação quando não precisar deles.

Não utilize o SQL Data Warehouse para cargas de trabalho (OLTP) operacionais que tem:
- Frequência alta lê e escreve
- Grande número de singleton seleciona
- Volumes elevados de inserções de linha única
- Linha por linha tem de processar
- Formatos incompatíveis (JSON, XML)


## <a name="plan-hello-migration"></a>Migração do plano de Olá

Depois de decidir toomigrate um tooSQL de solução do armazém de dados existente, é importante tooplan migração de Olá antes da introdução. 

Um objetivo de planeamento é tooensure os dados, esquemas de tabela, e código são compatíveis com o SQL Data Warehouse. Existem algumas diferenças de compatibilidade toowork à volta entre o sistema atual e o SQL Data Warehouse. Plus, a migrar grandes quantidades de dados tooAzure demora tempo. Um planeamento cuidado expedites ao obter o tooAzure de dados. 

Outro objetivo do planeamento é design toomake tooensure ajustes que a solução tira partido do desempenho de consulta elevado Olá que SQL Data Warehouse é concebido tooprovide. Conceber armazéns de dados para a escala apresenta padrões de conceção diferentes e abordagens tradicionais, por isso, não são sempre Olá melhor. Embora pode efetuar alguns ajustes de design após a migração, efetuar as alterações mais cedo no processo de Olá irá poupar tempo posteriormente.

tooperform uma migração com êxito, terá de toomigrate as esquemas de tabela, o seu código e os dados. Para obter orientações sobre estes tópicos de migração, consulte:

-  [Migrar as esquemas](sql-data-warehouse-migrate-schema.md)
-  [Migrar o seu código](sql-data-warehouse-migrate-code.md)
-  [Migrar os dados](sql-data-warehouse-migrate-data.md). 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Passos seguintes
Olá CAT (equipa de Consultadora dos clientes) também tem algumas excelente documentação de orientação do armazém de dados do SQL Server, que publicam através de blogues.  Observe respetivo artigo, [tooAzure de dados de migração do armazém de dados do SQL Server na prática] [ Migrating data tooAzure SQL Data Warehouse in practice] para orientações adicionais sobre a migração.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
