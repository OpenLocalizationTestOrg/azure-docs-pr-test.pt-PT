---
title: "aaaLogging para serviços web do Machine Learning | Microsoft Docs"
description: "Saiba como os serviços web tooenable registo para o Machine Learning. O registo fornece informações adicionais toohelp Olá APIs de resolução de problemas."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Ativar o registo para os serviços Web do Machine Learning
Este documento fornece informações sobre Olá registo a capacidade de serviços web do Machine Learning. O registo fornece informações adicionais, para além de apenas um número de erro e uma mensagem, que pode ajudar a resolver o toohello chamadas APIs do Machine Learning.  

## <a name="how-tooenable-logging-for-a-web-service"></a>Como tooenable o registo para um serviço Web

Ativar o registo de Olá [serviços Web do Azure Machine Learning](https://services.azureml.net) portal. 

1. Inicie sessão no portal de serviços Web do Azure Machine Learning toohello em [https://services.azureml.net](https://services.azureml.net). Para um serviço web clássico, também pode obter toohello portal clicando **nova experiência de serviços Web** na página de serviços Web Machine Learning Olá no Machine Learning Studio.

   ![Nova ligação de experiência de serviços Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Na barra de menu superior Olá, clique em **serviços Web** para um novo serviço web, ou clique em **serviços Web clássicos** para um clássico de serviço web.

   ![Selecione o novo ou clássico serviços web](media/machine-learning-web-services-logging/select-web-service.png)

3. Para um novo serviço web, clique em nome do serviço web Olá. Para um serviço web clássico, clique em nome do serviço web Olá e, em seguida, na página seguinte Olá, clique em ponto final adequado de Olá.

4. Na barra de menu superior Olá, clique em **configurar**.

5. Conjunto Olá **ativar registo** opção demasiado*erro* (toolog apenas erros) ou *todos os* (para o registo completo).

   ![Selecione o nível de registo](media/machine-learning-web-services-logging/enable-logging.png)

6. Clique em **Guardar**.

7. Para os serviços web clássico, crie Olá **ml diagnóstico** contentor.

   Todos os registos do serviço web são mantidos num contentor do blob denominado **ml diagnóstico** na conta do storage Olá associada ao serviço web de Olá. Para novos serviços web, este contentor é criado Olá pela primeira vez, aceder ao serviço web Olá. Para os serviços web clássico, terá de contentor de Olá toocreate se ainda não existir. 

   1. No Olá [portal do Azure](https://portal.azure.com), aceda a conta de armazenamento de toohello associada ao serviço web de Olá.

   2. Em **serviço Blob**, clique em **contentores**.

   3. Se contentor Olá **ml diagnóstico** não existe, clique em **+ contentor**, dê Olá contentor Olá nome "ml-diagnóstico" e selecione Olá **aceder tipo** como "Blob". Clique em **OK**.

      ![Selecione o nível de registo](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Para um serviço web clássico, Olá Dashboard de serviços Web do Machine Learning Studio também tem um registo de tooenable comutador. No entanto, porque o registo está agora gerido através do portal de serviços Web Olá, terá de tooenable registo através do portal de Olá, tal como descrito neste artigo. Se já tiver ativado o registo no Studio, em seguida, no Portal de serviços Web Olá, desative o registo e volte a ativar.


## <a name="hello-effects-of-enabling-logging"></a>efeitos de Olá de ativar o registo
Quando o registo está ativado, Olá diagnóstico e de erros de ponto final de serviço do Olá web são registados no Olá **ml diagnóstico** contentor do blob no Olá conta do Storage do Azure ligado com área de trabalho do utilizador Olá. Este contentor contém todas as informações de diagnóstico de Olá para todos os Olá web pontos finais de serviço para todas as áreas de trabalho Olá associados a esta conta de armazenamento.

Olá registos podem ser vistos utilizando qualquer um dos Olá tooexplore disponíveis várias ferramentas uma conta de armazenamento do Azure. Olá mais fácil poderá ser a conta de armazenamento de toohello toonavigate no Olá portal do Azure, clique em **contentores**e, em seguida, clique em contentor Olá **ml diagnóstico**.  

## <a name="log-blob-detail-information"></a>Informações de detalhe do registo blob
Cada blob no contentor de Olá contém informações de diagnóstico de Olá para exactamente um Olá seguintes ações:

* Uma execução do método de Olá execução de lote  
* Uma execução do método de Olá resposta-pedido  
* Inicialização de um contentor de resposta-pedido

nome de Olá de cada blob tem um prefixo de Olá seguinte formato: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Onde _tipo de registo_ é um dos seguintes valores de Olá:  

* Batch  
* pontuação/pedidos  
* pontuação/init  

