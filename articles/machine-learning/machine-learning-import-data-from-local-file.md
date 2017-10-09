---
title: aaaImport dados de um ficheiro para o Azure Machine Learning Studio | Microsoft Docs
description: "Saiba como tooupload dados de formação do ficheiro do seu disco rígido de tooAzure Machine Learning Studio. Esta ação cria um módulo de conjunto de dados na área de trabalho Olá."
keywords: "Importar dados, o formato de dados, os tipos de dados, as origens de dados, dados de formação"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Importar dados de formação de um ficheiro no disco rígido no Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Saiba como tooupload dados de ficheiro do seu disco rígido toouse como dados de formação no Azure Machine Learning Studio. Ao importar o ficheiro de dados de Olá, tem um módulo de conjunto de dados pronto para ser utilizada em sua área de trabalho.

## <a name="steps-tooimport-data-from-a-local-file"></a>Dados de tooimport passos de um ficheiro local
tooimport dados a partir de um disco rígido local, Olá seguintes:

1. Clique em **+ novo** em Olá parte inferior da janela de Machine Learning Studio Olá.
2. Selecione **DATASET** e **partir do ficheiro LOCAL**.
3. No Olá **carregue um novo conjunto de dados** caixa de diálogo, procurar toohello ficheiro pretende tooupload
4. Introduza um nome, identifique o tipo de dados de Olá e, opcionalmente, introduza uma descrição. Recomenda-se uma descrição - permite-lhe toorecord qualquer caraterísticas sobre dados Olá que pretende que tooremember quando dados Olá Olá futuro.
5. caixa de verificação de Olá **esta é a versão nova do Olá de um conjunto de dados existente** permite-lhe tooupdate um conjunto de dados existente com novos dados. Clique nesta caixa de verificação e, em seguida, introduza o nome de Olá de um conjunto de dados existente.

![Carregue um novo conjunto de dados](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Durante o carregamento, verá uma mensagem que o ficheiro está a ser carregado. Carregar tempo depende do tamanho de Olá dos seus dados e Olá velocidade do seu serviço de toohello de ligação. Se souber o ficheiro de Olá irá demorar muito tempo, pode efetuar outras ações no interior do Machine Learning Studio enquanto aguarde. No entanto, a fechar o browser Olá provoca toofail de carregamento de dados de Olá.

## <a name="dataset-module-is-ready-for-use"></a>Módulo de conjunto de dados está pronto a utilizar
Depois dos dados são carregados, é armazenado num módulo conjunto de dados e está disponível tooany experimentação na sua área de trabalho.

Quando estiver a editar uma experimentação, pode encontrar Olá conjuntos de dados que criou no Olá **conjuntos de dados os meus** lista em Olá **conjuntos de dados guardado** lista na paleta do módulo Olá. Pode arrastar e largar Olá conjunto de dados para a tela de experimentação do Olá quando pretender que o conjunto de dados do toouse Olá para análise adicional e a aprendizagem.
