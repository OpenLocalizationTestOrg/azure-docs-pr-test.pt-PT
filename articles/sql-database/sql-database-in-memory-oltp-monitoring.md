---
title: "armazenamento de dentro da memória XTP aaaMonitor | Microsoft Docs"
description: "Monitor de armazenamento de dentro da memória XTP e estimativa utilizam, capacidade; Resolva o erro de capacidade 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Monitorizar o Armazenamento OLTP Dentro da Memória
Quando utilizar [OLTP na memória](sql-database-in-memory.md), dados em tabelas com otimização de memória e variáveis de tabela residem no armazenamento do OLTP dentro da memória. Cada escalão de serviço Premium tem um tamanho de armazenamento de OLTP na memória máximo, o que é descrito da Olá [artigo escalões de serviço de base de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Depois deste limite for excedido, insira e atualizar operações poderão começam a falhar (com o erro 41823). Nesse momento será necessário tooeither eliminar dados tooreclaim de memória ou atualizar o escalão de desempenho de Olá da base de dados.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Determinar se a dados se encaixa na extremidade de armazenamento em memória Olá
Determinar a extremidade de armazenamento Olá: consulte Olá [artigo escalões de serviço de base de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para caps de armazenamento Olá das camadas de serviços de Premium Olá diferentes.

Estimar os requisitos para uma tabela com otimização de memória funciona Olá mesmo de memória de uma forma para o SQL Server faz na SQL Database do Azure. Demorar alguns minutos tooreview nesse tópico [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Tenha em atenção que a tabela de Olá e linhas de variável de tabela, bem como índices, contam para o tamanho de dados de utilizador máximo Olá. Além disso, ALTER TABLE tem suficiente toocreate sala de uma nova versão da tabela inteira Olá e seus índices.

## <a name="monitoring-and-alerting"></a>Monitorização e alertas
Pode monitorizar a utilização de memória de armazenamento como uma percentagem do Olá [extremidade de armazenamento para o escalão de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) no Olá Azure [portal](https://portal.azure.com/): 

* No painel da base de dados de Olá, localize a caixa de utilização de recursos de Olá e clique em Editar.
* Em seguida, selecione a métrica de Olá `In-Memory OLTP Storage percentage`.
* tooadd um alerta, clique em Olá utilização de recursos caixa tooopen Olá métrica painel, em seguida, clique em Adicionar alerta.

Ou utilize a seguinte consulta tooshow Olá de memória a utilização do armazenamento de Olá:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Corrija situações de memória esgotada - erro 41823
Resultados de execução-memória esgotada em operações de inserção, ATUALIZAÇÃO e criar a falhar com a mensagem de erro 41823.

Mensagem de erro 41823 indica que as tabelas com otimização de memória de Olá e variáveis de tabela excedeu o tamanho máximo Olá.

tooresolve este erro é:

* Eliminar dados de tabelas com otimização de memória de Olá, potencialmente descarregar tootraditional de dados de Olá, com base em disco tabelas; ou,
* Atualizar tooone de camada de serviço Olá com armazenamento suficiente na memória para os dados de Olá terá tookeep em tabelas com otimização de memória.

## <a name="next-steps"></a>Passos seguintes
Para monitorizar orientações, consulte [monitorização SQL Database do Azure utilizar as vistas de gestão dinâmica](sql-database-monitoring-with-dmvs.md).
