---
title: "aaaExtend sua experiência com R | Microsoft Docs"
description: "Como a funcionalidade de Olá tooextend do Azure Machine Learning Studio através do idioma Olá R utilizando Olá módulo executar Script do R."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="da550-103">Ampliar a sua experimentação com R</span><span class="sxs-lookup"><span data-stu-id="da550-103">Extend your experiment with R</span></span>
<span data-ttu-id="da550-104">Pode expandir a funcionalidade de Olá do Azure Machine Learning Studio através do idioma Olá R utilizando Olá [executar Script do R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="da550-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="da550-105">Este módulo aceita vários conjuntos de dados de entrada e gera um único conjunto de dados como saída.</span><span class="sxs-lookup"><span data-stu-id="da550-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="da550-106">Pode escrever um script do R para Olá **R Script** parâmetro de Olá [executar Script do R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="da550-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="da550-107">Aceder a cada porta de entrada do módulo Olá através de código semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="da550-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="da550-108">Listar todos os pacotes atualmente instalados</span><span class="sxs-lookup"><span data-stu-id="da550-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="da550-109">Pode alterar a lista de Olá de pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="da550-109">hello list of installed packages can change.</span></span> <span data-ttu-id="da550-110">É possível encontrar uma lista de pacotes atualmente instalados no [R pacotes suportado pelo Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="da550-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="da550-111">Também pode obter a lista completa, atual Olá de pacotes instalados introduzindo Olá seguinte código para Olá [executar Script do R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="da550-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="da550-112">Esta ação envia a lista de Olá de porta de saída de toohello de pacotes do Olá [executar Script do R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="da550-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="da550-113">pacote de Olá tooview lista, ligar um módulo de conversão como [converter tooCSV] [ convert-to-csv] toohello deixado resultado Olá [executar Script do R] [ execute-r-script]módulo, execute a experimentação Olá, em seguida, clique em resultado de Olá do módulo de conversão de Olá e selecione **transferir**.</span><span class="sxs-lookup"><span data-stu-id="da550-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Transferir o resultado do módulo "Converter tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="da550-115">Importar pacotes</span><span class="sxs-lookup"><span data-stu-id="da550-115">Importing packages</span></span>
<span data-ttu-id="da550-116">Pode importar pacotes que já não são instalados utilizando Olá os seguintes comandos no Olá [executar Script do R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="da550-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="da550-117">onde Olá `my_favorite_package.zip` ficheiro contém o pacote.</span><span class="sxs-lookup"><span data-stu-id="da550-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
