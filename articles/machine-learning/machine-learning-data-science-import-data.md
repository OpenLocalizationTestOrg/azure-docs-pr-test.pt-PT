---
title: dados de aaaImport no Machine Learning Studio | Microsoft Docs
description: "Como tooimport os dados no Azure Machine Learning Studio de várias origens de dados. Saiba que tipos de dados e formatos de dados são suportados."
keywords: "Importar dados, o formato de dados, os tipos de dados, as origens de dados, dados de formação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="e1e43-105">Importar os seus dados de preparação para o Azure Machine Learning Studio a partir de várias origens de dados</span><span class="sxs-lookup"><span data-stu-id="e1e43-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="e1e43-106">toouse os seus próprios dados no Machine Learning Studio toodevelop e formação uma solução de Análise Preditiva, pode:</span><span class="sxs-lookup"><span data-stu-id="e1e43-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="e1e43-107">carregar dados a partir de um **ficheiro local** ahead de tempo da sua toocreate de disco rígido, um módulo de conjunto de dados na sua área de trabalho</span><span class="sxs-lookup"><span data-stu-id="e1e43-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="e1e43-108">aceder a dados a partir de um dos vários **origens de dados online** enquanto está a executar a experimentação utilizando Olá [importar dados] [ import-data] módulo</span><span class="sxs-lookup"><span data-stu-id="e1e43-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="e1e43-109">utilizar dados a partir de outro Azure Machine learning **experimentação** guardada como um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="e1e43-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="e1e43-110">utilizar dados a partir de um local **base de dados do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="e1e43-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="e1e43-111">Cada uma destas opções é descrita dos tópicos de Olá no menu de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="e1e43-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="e1e43-112">Estes tópicos mostram-lhe como tooimport dados a partir destes dados de várias origens toouse no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e1e43-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="e1e43-113">Um número de conjuntos de dados de exemplo estão disponíveis no Machine Learning Studio, pode utilizar para dados de preparação.</span><span class="sxs-lookup"><span data-stu-id="e1e43-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="e1e43-114">Para obter informações acerca deste assunto, consulte [utilizar conjuntos de dados de exemplo de Olá no Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="e1e43-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="e1e43-115">Este tópico introdutórias também descreve como dados tooget prontos a utilizam no Machine Learning Studio e descreve os formatos de dados e os tipos de dados são suportados.</span><span class="sxs-lookup"><span data-stu-id="e1e43-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="e1e43-116">Obter dados pronto a utilizar no Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e1e43-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="e1e43-117">Machine Learning Studio é concebida toowork com dados retangular ou tabela, tais como os dados de texto delimitado por ou estruturados dados a partir de uma base de dados, embora em algumas circunstâncias não retangular dados podem ser utilizados.</span><span class="sxs-lookup"><span data-stu-id="e1e43-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="e1e43-118">É melhor se os seus dados são relativamente limpo.</span><span class="sxs-lookup"><span data-stu-id="e1e43-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="e1e43-119">Ou seja, poderá ser útil tootake care of problemas como cadeias unquoted antes de carregar dados de Olá na sua experiência.</span><span class="sxs-lookup"><span data-stu-id="e1e43-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="e1e43-120">No entanto, existem módulos disponíveis no Machine Learning Studio, que permitem algumas manipulação de dados dentro da sua experimentação.</span><span class="sxs-lookup"><span data-stu-id="e1e43-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="e1e43-121">Dependendo de algoritmos de aprendizagem Olá que irá utilizar, poderá ser necessário toodecide como vai processar problemas estruturais de dados, como os valores em falta e dados dispersos e existem módulos que podem ajudar.</span><span class="sxs-lookup"><span data-stu-id="e1e43-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="e1e43-122">Procure no Olá **transformação de dados** secção da paleta do módulo Olá para módulos que realizam estas funções.</span><span class="sxs-lookup"><span data-stu-id="e1e43-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="e1e43-123">Em qualquer momento na sua experimentação pode ver ou transferir dados Olá que são produzidos por um módulo clicando Olá porta de saída.</span><span class="sxs-lookup"><span data-stu-id="e1e43-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="e1e43-124">Dependendo do módulo Olá, poderá transferir diferentes opções disponíveis ou pode estar toovisualize capaz de dados de Olá dentro do seu browser no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e1e43-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="e1e43-125">Tipos de dados e formatos de dados suportados</span><span class="sxs-lookup"><span data-stu-id="e1e43-125">Data formats and data types supported</span></span>
<span data-ttu-id="e1e43-126">Pode importar um número de tipos de dados para a sua experimentação, consoante o mecanismo de utilizar dados tooimport e onde é proveniente de:</span><span class="sxs-lookup"><span data-stu-id="e1e43-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="e1e43-127">Texto simples (*.txt)</span><span class="sxs-lookup"><span data-stu-id="e1e43-127">Plain text (.txt)</span></span>
* <span data-ttu-id="e1e43-128">Valores separados por vírgulas (CSV) com um cabeçalho (. csv) ou sem (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="e1e43-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="e1e43-129">Separador valores separados por (TSV) com um cabeçalho (.tsv) ou sem (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="e1e43-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="e1e43-130">Ficheiro do Excel</span><span class="sxs-lookup"><span data-stu-id="e1e43-130">Excel file</span></span>
* <span data-ttu-id="e1e43-131">Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="e1e43-131">Azure table</span></span>
* <span data-ttu-id="e1e43-132">Tabela do Hive</span><span class="sxs-lookup"><span data-stu-id="e1e43-132">Hive table</span></span>
* <span data-ttu-id="e1e43-133">Tabela de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e1e43-133">SQL database table</span></span>
* <span data-ttu-id="e1e43-134">Valores de OData</span><span class="sxs-lookup"><span data-stu-id="e1e43-134">OData values</span></span>
* <span data-ttu-id="e1e43-135">Dados SVMLight (.svmlight) (consulte Olá [SVMLight definição](http://svmlight.joachims.org/) para obter informações de formato)</span><span class="sxs-lookup"><span data-stu-id="e1e43-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="e1e43-136">Atributo de dados de formato de ficheiro de relação (ARFF) (.arff) (consulte Olá [definição ARFF](http://weka.wikispaces.com/ARFF) para obter informações de formato)</span><span class="sxs-lookup"><span data-stu-id="e1e43-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="e1e43-137">Ficheiro zip (. zip)</span><span class="sxs-lookup"><span data-stu-id="e1e43-137">Zip file (.zip)</span></span>
* <span data-ttu-id="e1e43-138">Ficheiro de objeto ou a área de trabalho de R (. RData)</span><span class="sxs-lookup"><span data-stu-id="e1e43-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="e1e43-139">Se importar dados num formato como ARFF inclui metadados, o Machine Learning Studio utiliza este cabeçalho de Olá toodefine de metadados e o tipo de dados de cada coluna.</span><span class="sxs-lookup"><span data-stu-id="e1e43-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="e1e43-140">Se importar dados, tais como TSV ou CSV com o formato que não inclua estes metadados, o Machine Learning Studio infere Olá o tipo de dados para cada coluna por dados Olá de amostragem.</span><span class="sxs-lookup"><span data-stu-id="e1e43-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="e1e43-141">Se os dados de Olá também não tem cabeçalhos de coluna, o Machine Learning Studio fornece nomes predefinidos.</span><span class="sxs-lookup"><span data-stu-id="e1e43-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="e1e43-142">Pode especificar explicitamente ou alterar tipos de cabeçalhos e dados de Olá para colunas utilizando Olá [Editar metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="e1e43-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="e1e43-143">seguinte Olá **tipos de dados** são reconhecidos pelo Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="e1e43-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="e1e43-144">Cadeia</span><span class="sxs-lookup"><span data-stu-id="e1e43-144">String</span></span>
* <span data-ttu-id="e1e43-145">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e1e43-145">Integer</span></span>
* <span data-ttu-id="e1e43-146">duplo</span><span class="sxs-lookup"><span data-stu-id="e1e43-146">Double</span></span>
* <span data-ttu-id="e1e43-147">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="e1e43-147">Boolean</span></span>
* <span data-ttu-id="e1e43-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="e1e43-148">DateTime</span></span>
* <span data-ttu-id="e1e43-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1e43-149">TimeSpan</span></span>

<span data-ttu-id="e1e43-150">O Machine Learning Studio utiliza um tipo de dados internos chamado ***dados tabela*** toopass dados entre módulos.</span><span class="sxs-lookup"><span data-stu-id="e1e43-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="e1e43-151">Explicitamente pode converter os dados em formato de tabela de dados utilizando Olá [converter tooDataset] [ convert-to-dataset] módulo.</span><span class="sxs-lookup"><span data-stu-id="e1e43-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="e1e43-152">Qualquer módulo que aceita os formatos que não seja a tabela de dados irá converter Olá dados tooData tabela silenciosamente antes de transmitir módulo seguinte toohello.</span><span class="sxs-lookup"><span data-stu-id="e1e43-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="e1e43-153">Se necessário, pode converter a tabela de dados formato no CSV, TSV, ARFF, ou SVMLight utilizando outros módulos de conversão.</span><span class="sxs-lookup"><span data-stu-id="e1e43-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="e1e43-154">Procure no Olá **conversões de formato de dados** secção da paleta do módulo Olá para módulos que realizam estas funções.</span><span class="sxs-lookup"><span data-stu-id="e1e43-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
