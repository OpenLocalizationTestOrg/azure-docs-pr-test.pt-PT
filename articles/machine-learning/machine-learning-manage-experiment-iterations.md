---
title: "aaaManage experimentação iterações no Machine Learning Studio | Microsoft Docs"
description: "Como toomanage experimentação iterações no Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Gerir iterações da experimentação no Azure Machine Learning Studio
Desenvolver um modelo de Análise Preditiva é um processo iterativo - à medida que modifica Olá várias funções e os parâmetros da sua experimentação, os seus resultados convergem até achar que tem um modelo preparado e eficaz. Processo de toothis da chave é Olá de controlo de várias iterações da sua experimentação parâmetros e configurações.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Pode rever execuções anteriores das suas experimentações em qualquer altura na ordem toochallenge revê e, em última análise confirmar ou refinar pressupostos anteriores. Quando executa uma experimentação, o Machine Learning Studio mantém um histórico de Olá executar, incluindo o conjunto de dados, módulo e ligações de porta e os parâmetros. Este histórico também captura resultados, informações de tempo de execução, tais como iniciar e parar vezes, as mensagens do registo e estado de execução. Pode ser novamente em qualquer um destes é executado em qualquer chronology de Olá tooreview de tempo da sua experimentação e resultados intermédios. Mesmo pode utilizar uma execução anterior toolaunch sua experimentação para uma nova fase de consulta e de deteção no seu caminho toocreating simples, complexos ou até mesmo ensemble modelação soluções.

> [!NOTE]
> Quando visualiza uma execução anterior de uma experimentação, o que a versão da experimentação Olá está bloqueada e não pode ser editada. No entanto, pode, guarde uma cópia do mesmo ao clicar em **guardar como** e fornecer um novo nome para a cópia de Olá. O Machine Learning Studio abre Olá nova cópia, que pode, em seguida, editar e executar. Esta cópia da sua experimentação está disponível no Olá **EXPERIMENTAÇÕES** lista juntamente com todos os seus outras experimentações.
> 
> 

## <a name="viewing-hello-prior-run"></a>Olá de visualização de executar o anterior
Quando tiver de abrir uma experimentação que executou, pelo menos, uma vez, pode ver Olá anterior a execução da experimentação Olá clicando **executar o anterior** no painel de propriedades de Olá.

Por exemplo, suponha que criar uma experimentação e executam versões do mesmo às 11:23, 11:42 e 11:55. Se abrir a última execução de Olá da experimentação Olá (11:55) e clique em **executar o anterior**, versão Olá executou às 11:42 é aberto.

## <a name="viewing-hello-run-history"></a>Olá visualizar o histórico de execução
Pode ver todas as Olá anterior é executado de uma experimentação, clicando em **ver histórico de execuções** numa experiência aberta.

Por exemplo, suponha que criar uma experimentação com Olá [regressão Linear] [ linear-regression] módulo e pretender que efeito de Olá tooobserve da alteração do valor Olá **ritmo de aprendizagem** no resultados da sua experimentação. Executar a experimentação de Olá várias vezes com valores diferentes para este parâmetro, da seguinte forma:

| Valor de velocidade de aprendizagem | Hora de início de execução |
| --- | --- |
| 0.1 |9/11/2014 4:18:58 pm |
| 0.2 |9/11/2014 4:24:33 pm |
| 0.4 |9/11/2014 4:28:36 pm |
| 0.5 |9/11/2014 4:33:31 pm |

Se clicar em **ver histórico de EXECUÇÕES**, é apresentada uma lista de todas as execuções destas:

![Histórico de execução de exemplo][runhistory]

Clique em qualquer uma destas tooview executa um instantâneo de Olá experimentação momento Olá que foi executada. Olá configuração, os valores de parâmetros, comentários e os resultados são preservado todos os toogive que um registo de concluir essa execução da sua experimentação.

> [!TIP]
> toodocument as iterações de experimentação Olá, pode modificar título Olá sempre a executá-lo, pode atualizar Olá **resumo** de Olá experimentação no painel de propriedades de Olá, e pode adicionar ou atualizar comentários sobre o módulos individuais toorecord as suas alterações. comentários de Olá título, o resumo e módulo são guardados com cada execução da experimentação Olá.
> 
> 

lista de Olá de experimentações no Olá **EXPERIMENTAÇÕES** separador no Machine Learning Studio apresenta sempre a versão mais recente do Olá de uma experimentação. Se abrir uma execução anterior da experimentação Olá (utilizando **executar o anterior** ou **ver histórico de EXECUÇÕES**), pode voltar a versão de rascunho toohello clicando **ver histórico de EXECUÇÕES** e selecionar Olá iteração que tenha um **estado** de **Editable**.

## <a name="iterating-on-a-previous-run"></a>Iterating numa execução anterior
Ao clicar em **executar o anterior** ou **ver histórico de EXECUÇÕES** e abrir uma execução anterior, pode ver uma experimentação concluída no modo só de leitura.

Se quiser toobegin uma iteração da sua experimentação começadas forma Olá esteja configurado para uma execução anterior, pode fazê-abrir Olá, executar e clicando em **guardar como**. Esta ação cria uma nova experimentação, com um título de novo, um histórico de execução vazio e todos os componentes de Olá e os valores dos parâmetros de Olá anterior executar. Esta nova experiência está listada no Olá **EXPERIMENTAÇÕES** separador home page do Machine Learning Studio Olá e pode modificar e executá-la, iniciar uma nova histórico de execução para esta iteração da sua experimentação. 

Por exemplo, suponha que tem experimentação Olá mostrado na secção anterior Olá do histórico de execução. Pretende tooobserve o que acontece quando definir Olá **ritmo de aprendizagem** too0.4 de parâmetro e tente valores diferentes para Olá **diversas epochs formação** parâmetro.

1. Clique em **ver histórico de EXECUÇÕES** e abra iteração Olá da experimentação Olá que tenha sido executada em 4:28:36 pm (na qual configurou too0.4 de valor de parâmetro de Olá).
2. Clique em **guardar como**.
3. Introduza um título nova e clique em Olá **OK** marca de verificação. É criada uma nova cópia da experimentação Olá.
4. Modificar Olá **diversas epochs formação** parâmetro.
5. Clique em **executar**.

Agora pode continuar toomodify e executar esta versão da sua experimentação, criar um novo toorecord de histórico de execução do trabalho.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
