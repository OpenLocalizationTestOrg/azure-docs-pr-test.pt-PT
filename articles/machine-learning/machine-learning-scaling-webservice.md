---
title: "aaaHow tooincrease simultaneidade de um serviço web Azure Machine Learning | Microsoft Docs"
description: "Saiba como tooincrease simultaneidade de um Azure Machine Learning serviço web adicionando os pontos finais adicionais."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "do Azure machine learning, serviços web, operationalization, dimensionamento, ponto final, concorrência"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Dimensionar um serviço web Azure Machine Learning adicionando os pontos finais adicionais
> [!NOTE]
> Este tópico descreve tooa aplicável técnicas **clássico** serviço Web do Machine Learning. 
> 
> 

Por predefinição, cada serviço Web publicado é configurado toosupport 20 pedidos em simultâneo e pode ser tão elevado como 200 pedidos em simultâneo. Enquanto Olá portal clássico do Azure fornece uma forma tooset este valor, do Azure Machine Learning automaticamente otimiza Olá definição tooprovide Olá melhor desempenho para o seu serviço web e valor portal Olá é ignorado. 

Se planear toocall Olá API com uma carga maior do que um valor de número máximo de chamadas em simultâneo de 200 irá suportar, deve criar vários pontos finais no Olá mesmo serviço Web. Em seguida, pode distribuir aleatoriamente a carga em todos eles.

Olá dimensionamento de um serviço Web é uma tarefa comuns. Algumas razões tooscale são toosupport mais de 200 pedidos em simultâneo, aumentar a disponibilidade através de vários pontos finais ou forneça pontos finais separados para o serviço web de Olá. Pode aumentar a escala de Olá adicionando os pontos finais adicionais para Olá mesmo serviço Web através de [portal clássico do Azure](https://manage.windowsazure.com/) ou Olá [serviço Web do Azure Machine Learning](https://services.azureml.net/) portal.

Para obter mais informações sobre como adicionar novos pontos finais, consulte [criação de pontos finais](machine-learning-create-endpoint.md).

Tenha em atenção que o com uma contagem de concorrência elevado pode ser detrimental se não estiver a chamar Olá API com uma taxa elevada de proporcionalmente. Poderá ver esporádicas tempos limite e/ou picos de latência de Olá se colocar uma carga relativamente baixa numa API configurada para elevada carga.

Olá que APIs síncronas são normalmente utilizadas em situações em que uma baixa latência for pretendida. Latência aqui implica tempo Olá Olá API toocomplete um pedido leva e não uma conta para qualquer atrasos de rede. Imaginemos que tem uma API com uma latência de 50-ms. toofully consumir capacidade disponível do Olá com um nível elevado de limitação e máx. de chamadas em simultâneo = 20, terá de toocall esta API 20 * 1000 / 50 = 400 vezes por segundo. Expandir ainda mais este, um máximo de chamadas em simultâneo de 200 permite-lhe toocall Olá API 4000 vezes por segundo, partindo do princípio de uma latência de 50-ms.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
