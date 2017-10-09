---
title: "aaaBuild integrado soluções do SQL Data Warehouse | Microsoft Docs"
description: "Ferramentas e parceiros com soluções que se integram com o SQL Data Warehouse. "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Tirar partido de outros serviços com o SQL Data Warehouse
Além disso tooits principal funcionalidade, o SQL Data Warehouse permite que os utilizadores tooleverage Olá muitos dos outros serviços no Azure em conjunto com o mesmo.  Mais concretamente, podemos ter demorado atualmente passos toodeeply integrar com o seguinte Olá:

* Power BI
* Azure Data Factory
* Azure Machine Learning
* Azure Stream Analytics

Estamos a trabalhar tooconnect com mais serviços em Olá ecossistema do Azure.

## <a name="power-bi"></a>Power BI
Integração do Power BI permite-lhe capacidade de computação de Olá tooleverage do SQL Data Warehouse com Olá dinâmica reporting e visualização do Power BI. Integração do Power BI atualmente inclui:

* **Direcionar Connect**: um mais avançadas de ligação com a lógica pushdown no armazém de dados do SQL Server.  Isto fornece uma análise mais rápido numa escala maior.
* **Abrir no Power BI**: botão 'Abrir no Power BI' Olá transfere a informação de instância tooPower BI, permitindo uma ligação de mais integrada.

Consulte [integrar com o Power BI](sql-data-warehouse-integrate-power-bi.md) ou Olá [documentação do Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obter mais informações.

## <a name="azure-data-factory"></a>Azure Data Factory
O Azure Data Factory fornece aos utilizadores toocreate uma plataforma gerida que pipelines de carga de extrair complexa.  Integração do SQL Data Warehouse com o Azure Data Factory inclui seguinte Olá:

* **Procedimentos armazenados**: orquestrar execução Olá de procedimentos armazenados no armazém de dados do SQL Server.
* **Cópia**: dados de toomove ADF de utilização para o SQL Data Warehouse.  Esta operação pode utilizar o mecanismo de movimento de dados padrão do ADF ou PolyBase em Olá abrange. 

Consulte [integrar com o Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou Olá [documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) para obter mais informações.

## <a name="azure-machine-learning"></a>Azure Machine Learning
O Azure Machine Learning é um serviço de análise completamente gerido que permite aos utilizadores modelos intricate toocreate tirar partido de um grande conjunto de ferramentas preditivos.  O SQL Data Warehouse é suportado como uma origem e de destino para estes modelos com Olá seguintes funcionalidades:

* **Ler dados:** unidade modelos com dimensionamento, com o T-SQL no armazém de dados do SQL Server.
* **Escrita de dados:** confirmar as alterações de qualquer modelo de cópia tooSQL do armazém de dados.

Consulte [integrar com o Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) ou Olá [documentação do Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) para obter mais informações.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics
O Azure Stream Analytics é uma infraestrutura complexa, completamente gerida para processamento e consumir dados de eventos gerados a partir de Hub de eventos do Azure.  Integração com o SQL Data Warehouse permite para transmissão em fluxo dados toobe efetivamente processada e armazenada em conjunto com a dados relacionais ativar mais aprofundada, mais avançadas de análise.  

* **Resultado da tarefa:** saída de envio do Stream Analytics diretamente tarefas tooSQL do armazém de dados.

Consulte [integrar com o Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) ou Olá [documentação do Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) para obter mais informações.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
