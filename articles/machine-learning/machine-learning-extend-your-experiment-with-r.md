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
# <a name="extend-your-experiment-with-r"></a>Ampliar a sua experimentação com R
Pode expandir a funcionalidade de Olá do Azure Machine Learning Studio através do idioma Olá R utilizando Olá [executar Script do R] [ execute-r-script] módulo.

Este módulo aceita vários conjuntos de dados de entrada e gera um único conjunto de dados como saída. Pode escrever um script do R para Olá **R Script** parâmetro de Olá [executar Script do R] [ execute-r-script] módulo.

Aceder a cada porta de entrada do módulo Olá através de código semelhante toohello seguinte:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Listar todos os pacotes atualmente instalados
Pode alterar a lista de Olá de pacotes instalados. É possível encontrar uma lista de pacotes atualmente instalados no [R pacotes suportado pelo Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).

Também pode obter a lista completa, atual Olá de pacotes instalados introduzindo Olá seguinte código para Olá [executar Script do R] [ execute-r-script] módulo:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Esta ação envia a lista de Olá de porta de saída de toohello de pacotes do Olá [executar Script do R] [ execute-r-script] módulo.
pacote de Olá tooview lista, ligar um módulo de conversão como [converter tooCSV] [ convert-to-csv] toohello deixado resultado Olá [executar Script do R] [ execute-r-script]módulo, execute a experimentação Olá, em seguida, clique em resultado de Olá do módulo de conversão de Olá e selecione **transferir**. 

![Transferir o resultado do módulo "Converter tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importar pacotes
Pode importar pacotes que já não são instalados utilizando Olá os seguintes comandos no Olá [executar Script do R] [ execute-r-script] módulo:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

onde Olá `my_favorite_package.zip` ficheiro contém o pacote.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
