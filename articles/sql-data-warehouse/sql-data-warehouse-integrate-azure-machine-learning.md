---
title: aaaUse Azure Machine Learning com o SQL Data Warehouse | Microsoft Docs
description: "Tutorial para utilizar o Azure Machine Learning com o Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="02ff8-103">Utilização do Azure Machine Learning com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="02ff8-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="02ff8-104">O Azure Machine Learning é um serviço de Análise Preditiva completamente gerido que pode utilizar modelos preditivos toocreate contra os dados no armazém de dados do SQL Server e, em seguida, publicar como serviços web prontos a consumir.</span><span class="sxs-lookup"><span data-stu-id="02ff8-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="02ff8-105">Pode saber Olá Noções básicas de Análise Preditiva e machine learning ao ler [introdução tooMachine Learning no Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="02ff8-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="02ff8-106">Em seguida, pode saber como toocreate, preparar, Pontuar e testar um modelo de machine learning utilizando Olá [criar experimentação tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="02ff8-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="02ff8-107">Neste artigo, ficará a saber como Olá toodo seguir utilizando Olá [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="02ff8-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="02ff8-108">Ler dados a partir do seu toocreate de base de dados, formação e Pontuar um modelo preditivo</span><span class="sxs-lookup"><span data-stu-id="02ff8-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="02ff8-109">Base de dados de tooyour de dados de escrita</span><span class="sxs-lookup"><span data-stu-id="02ff8-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="02ff8-110">Ler dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="02ff8-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="02ff8-111">Iremos ler dados da tabela do produto na base de dados do Olá AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="02ff8-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="02ff8-112">Passo 1</span><span class="sxs-lookup"><span data-stu-id="02ff8-112">Step 1</span></span>
<span data-ttu-id="02ff8-113">Inicie uma nova experimentação, clicando em + nova em Olá parte inferior da janela Machine Learning Studio, de Olá selecione experimentação e, em seguida, selecione a experimentar em branco.</span><span class="sxs-lookup"><span data-stu-id="02ff8-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="02ff8-114">Predefinição de Olá selecione experimentação nome na Olá parte superior da tela Olá e renomeie-toosomething significativo, por exemplo, predição do preço de bicicletas.</span><span class="sxs-lookup"><span data-stu-id="02ff8-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="02ff8-115">Passo 2</span><span class="sxs-lookup"><span data-stu-id="02ff8-115">Step 2</span></span>
<span data-ttu-id="02ff8-116">Procure o módulo de leitor de Olá na paleta Olá de conjuntos de dados e módulos esquerda Olá da tela de experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="02ff8-117">Arraste a tela de experimentação do Olá módulo toohello.</span><span class="sxs-lookup"><span data-stu-id="02ff8-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="02ff8-118">Passo 3</span><span class="sxs-lookup"><span data-stu-id="02ff8-118">Step 3</span></span>
<span data-ttu-id="02ff8-119">Selecione o módulo de leitor de Olá e preencher o painel de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="02ff8-120">Selecione a SQL Database do Azure como Olá origem de dados.</span><span class="sxs-lookup"><span data-stu-id="02ff8-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="02ff8-121">Nome do servidor de base de dados: nome do servidor de Olá de tipo.</span><span class="sxs-lookup"><span data-stu-id="02ff8-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="02ff8-122">Pode utilizar Olá [portal do Azure] [ Azure portal] toofind isto.</span><span class="sxs-lookup"><span data-stu-id="02ff8-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="02ff8-123">Nome da base de dados: nome do tipo hello do servidor de Olá que acabou de especificar uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="02ff8-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="02ff8-124">Nome de conta de utilizador do servidor: nome de utilizador de Olá de tipo de uma conta que tenha permissões de acesso para a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="02ff8-125">Palavra-passe de conta de utilizador do: forneça Olá palavra-passe para Olá especificar conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="02ff8-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="02ff8-126">Aceitar qualquer certificado de servidor: Utilize esta opção (menos segura), se quiser tooskip rever o certificado de site Olá antes de ler os dados.</span><span class="sxs-lookup"><span data-stu-id="02ff8-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="02ff8-127">Consulta de base de dados: introduza uma instrução de SQL que descreve os dados de Olá pretende tooread.</span><span class="sxs-lookup"><span data-stu-id="02ff8-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="02ff8-128">Neste caso, iremos irá ler os dados da tabela de produto Olá seguinte consulta a utilizar.</span><span class="sxs-lookup"><span data-stu-id="02ff8-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="02ff8-129">Passo 4</span><span class="sxs-lookup"><span data-stu-id="02ff8-129">Step 4</span></span>
1. <span data-ttu-id="02ff8-130">Execute Olá experimentação ao clicar em execução na tela de experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="02ff8-131">Quando Olá da experimentação ser concluída, o módulo leitor de Olá terá uma marca de verificação verde tooindicate que foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="02ff8-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="02ff8-132">Repare também Olá terminado com o estado no canto superior direito de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="02ff8-133">toosee Olá dados importados, clique Olá porta de saída na parte inferior de Olá de conjunto de dados para automóveis Olá e selecione o visualizar.</span><span class="sxs-lookup"><span data-stu-id="02ff8-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="02ff8-134">Criar, dar formação e um modelo de pontuação</span><span class="sxs-lookup"><span data-stu-id="02ff8-134">Create, train and score a model</span></span>
<span data-ttu-id="02ff8-135">Agora pode utilizar este conjunto de dados:</span><span class="sxs-lookup"><span data-stu-id="02ff8-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="02ff8-136">Criar um modelo: processar os dados e definir funcionalidades</span><span class="sxs-lookup"><span data-stu-id="02ff8-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="02ff8-137">Preparar o modelo de Olá: escolher e aplicar um algoritmo de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="02ff8-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="02ff8-138">Classificação e teste Olá modelo: prever novos preços de bicicletas</span><span class="sxs-lookup"><span data-stu-id="02ff8-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="02ff8-139">mais informações sobre como toocreate, preparar, Pontuar e testar um machine learning Olá de utilização do modelo de toolearn [criar experimentação tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="02ff8-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="02ff8-140">Escrever tooAzure de dados do armazém de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="02ff8-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="02ff8-141">Iremos escrever Olá resultado conjunto tooProductPriceForecast tabela na base de dados do Olá AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="02ff8-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="02ff8-142">Passo 1</span><span class="sxs-lookup"><span data-stu-id="02ff8-142">Step 1</span></span>
<span data-ttu-id="02ff8-143">Procure o módulo de escritor Olá na paleta Olá de conjuntos de dados e módulos esquerda Olá da tela de experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="02ff8-144">Arraste a tela de experimentação do Olá módulo toohello.</span><span class="sxs-lookup"><span data-stu-id="02ff8-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="02ff8-145">Passo 2</span><span class="sxs-lookup"><span data-stu-id="02ff8-145">Step 2</span></span>
<span data-ttu-id="02ff8-146">Selecione o módulo de escritor Olá e preencher o painel de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="02ff8-147">Selecione a SQL Database do Azure como Olá dados de destino.</span><span class="sxs-lookup"><span data-stu-id="02ff8-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="02ff8-148">Nome do servidor de base de dados: nome do servidor de Olá de tipo.</span><span class="sxs-lookup"><span data-stu-id="02ff8-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="02ff8-149">Pode utilizar Olá [portal do Azure] [ Azure portal] toofind isto.</span><span class="sxs-lookup"><span data-stu-id="02ff8-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="02ff8-150">Nome da base de dados: nome do tipo hello do servidor de Olá que acabou de especificar uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="02ff8-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="02ff8-151">Nome de conta de utilizador do servidor: nome de utilizador de Olá de tipo de uma conta que tenha permissões de escrita da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="02ff8-152">Palavra-passe de conta de utilizador do: forneça Olá palavra-passe para Olá especificar conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="02ff8-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="02ff8-153">Aceitar qualquer certificado de servidor (inseguras): selecione esta opção se não quiser que o certificado de Olá tooview.</span><span class="sxs-lookup"><span data-stu-id="02ff8-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="02ff8-154">Lista separada por vírgulas de toobe colunas guardado: forneça uma lista de colunas de conjunto de dados ou o resultado de Olá que pretende que o toooutput.</span><span class="sxs-lookup"><span data-stu-id="02ff8-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="02ff8-155">Nome da tabela de dados: Especifique Olá nome da tabela de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="02ff8-156">Lista separada por vírgulas de colunas de datatable: especificar toouse de nomes de coluna Olá numa tabela nova Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="02ff8-157">Olá nomes de coluna podem ser diferentes do Olá aqueles no conjunto de dados de origem de Olá, mas tem de listar Olá o mesmo número de colunas aqui por si para a tabela de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="02ff8-158">Número de linhas escrito por operação de SQL Azure: pode configurar Olá número de linhas que são escritos tooa SQL da base de dados numa única operação.</span><span class="sxs-lookup"><span data-stu-id="02ff8-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="02ff8-159">Passo 3</span><span class="sxs-lookup"><span data-stu-id="02ff8-159">Step 3</span></span>
1. <span data-ttu-id="02ff8-160">Execute Olá experimentação ao clicar em execução na tela de experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="02ff8-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="02ff8-161">Quando Olá da experimentação ser concluída, todos os módulos terá um tooindicate de marca de verificação verde foi concluídas com êxito.</span><span class="sxs-lookup"><span data-stu-id="02ff8-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02ff8-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="02ff8-162">Next steps</span></span>
<span data-ttu-id="02ff8-163">Para obter mais sugestões de desenvolvimento, veja [SQL Data Warehouse development overview (Descrição geral do desenvolvimento no SQL Data Warehouse)][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="02ff8-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
