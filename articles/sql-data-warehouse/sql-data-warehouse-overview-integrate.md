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
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="03483-103">Tirar partido de outros serviços com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="03483-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="03483-104">Além disso tooits principal funcionalidade, o SQL Data Warehouse permite que os utilizadores tooleverage Olá muitos dos outros serviços no Azure em conjunto com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="03483-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="03483-105">Mais concretamente, podemos ter demorado atualmente passos toodeeply integrar com o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="03483-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="03483-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="03483-106">Power BI</span></span>
* <span data-ttu-id="03483-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="03483-107">Azure Data Factory</span></span>
* <span data-ttu-id="03483-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="03483-108">Azure Machine Learning</span></span>
* <span data-ttu-id="03483-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="03483-109">Azure Stream Analytics</span></span>

<span data-ttu-id="03483-110">Estamos a trabalhar tooconnect com mais serviços em Olá ecossistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="03483-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="03483-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="03483-111">Power BI</span></span>
<span data-ttu-id="03483-112">Integração do Power BI permite-lhe capacidade de computação de Olá tooleverage do SQL Data Warehouse com Olá dinâmica reporting e visualização do Power BI.</span><span class="sxs-lookup"><span data-stu-id="03483-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="03483-113">Integração do Power BI atualmente inclui:</span><span class="sxs-lookup"><span data-stu-id="03483-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="03483-114">**Direcionar Connect**: um mais avançadas de ligação com a lógica pushdown no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="03483-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="03483-115">Isto fornece uma análise mais rápido numa escala maior.</span><span class="sxs-lookup"><span data-stu-id="03483-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="03483-116">**Abrir no Power BI**: botão 'Abrir no Power BI' Olá transfere a informação de instância tooPower BI, permitindo uma ligação de mais integrada.</span><span class="sxs-lookup"><span data-stu-id="03483-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="03483-117">Consulte [integrar com o Power BI](sql-data-warehouse-integrate-power-bi.md) ou Olá [documentação do Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="03483-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="03483-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="03483-118">Azure Data Factory</span></span>
<span data-ttu-id="03483-119">O Azure Data Factory fornece aos utilizadores toocreate uma plataforma gerida que pipelines de carga de extrair complexa.</span><span class="sxs-lookup"><span data-stu-id="03483-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="03483-120">Integração do SQL Data Warehouse com o Azure Data Factory inclui seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="03483-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="03483-121">**Procedimentos armazenados**: orquestrar execução Olá de procedimentos armazenados no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="03483-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="03483-122">**Cópia**: dados de toomove ADF de utilização para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="03483-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="03483-123">Esta operação pode utilizar o mecanismo de movimento de dados padrão do ADF ou PolyBase em Olá abrange.</span><span class="sxs-lookup"><span data-stu-id="03483-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="03483-124">Consulte [integrar com o Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou Olá [documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="03483-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="03483-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="03483-125">Azure Machine Learning</span></span>
<span data-ttu-id="03483-126">O Azure Machine Learning é um serviço de análise completamente gerido que permite aos utilizadores modelos intricate toocreate tirar partido de um grande conjunto de ferramentas preditivos.</span><span class="sxs-lookup"><span data-stu-id="03483-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="03483-127">O SQL Data Warehouse é suportado como uma origem e de destino para estes modelos com Olá seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="03483-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="03483-128">**Ler dados:** unidade modelos com dimensionamento, com o T-SQL no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="03483-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="03483-129">**Escrita de dados:** confirmar as alterações de qualquer modelo de cópia tooSQL do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="03483-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="03483-130">Consulte [integrar com o Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) ou Olá [documentação do Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="03483-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="03483-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="03483-131">Azure Stream Analytics</span></span>
<span data-ttu-id="03483-132">O Azure Stream Analytics é uma infraestrutura complexa, completamente gerida para processamento e consumir dados de eventos gerados a partir de Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="03483-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="03483-133">Integração com o SQL Data Warehouse permite para transmissão em fluxo dados toobe efetivamente processada e armazenada em conjunto com a dados relacionais ativar mais aprofundada, mais avançadas de análise.</span><span class="sxs-lookup"><span data-stu-id="03483-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="03483-134">**Resultado da tarefa:** saída de envio do Stream Analytics diretamente tarefas tooSQL do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="03483-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="03483-135">Consulte [integrar com o Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) ou Olá [documentação do Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="03483-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
