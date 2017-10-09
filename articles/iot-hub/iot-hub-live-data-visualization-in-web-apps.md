---
title: "visualização de dados de aaaReal tempo dos dados de sensores do seu hub IoT do Azure – Web Apps | Microsoft Docs"
description: "Utilize a funcionalidade de aplicações Web de Olá do App Service do Microsoft Azure toovisualize relativos à temperatura e humidade dados que são recolhidas a partir do sensor Olá e enviados tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualização de dados em tempo real, visualização de dados em direto, visualização de dados de sensor"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Visualizar dados de sensores em tempo real do seu hub IoT do Azure utilizando a funcionalidade de aplicações Web Olá do App Service do Azure

![Diagrama de ponto a ponto](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>O que irá aprender

Neste tutorial, saiba como os dados de sensores em tempo real de toovisualize que o seu IoT hub recebe ao executar uma aplicação web que estão alojados numa aplicação web. Se pretende que os tootry toovisualize Olá dados no seu IoT hub, utilizando o Power BI, consulte o artigo [dados de sensores em tempo real de toovisualize utilize Power BI do IoT Hub do Azure](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>O que fazer

- Crie uma aplicação web no Olá portal do Azure.
- Prepare o seu IoT hub para acesso a dados através da adição de um grupo de consumidores.
- Configure dados de sensores do Olá web app tooread do seu IoT hub.
- Carregar um toobe de aplicações web alojada pelo Olá web app.
- Abrir Olá web toosee em tempo real relativos à temperatura e humidade dados da aplicação a partir do seu IoT hub.

## <a name="what-you-need"></a>Do que precisa

- [Configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), que abrange Olá os seguintes requisitos:
  - Uma subscrição do Azure Active Directory
  - Um Iot hub na sua subscrição
  - Uma aplicação cliente que envia o Iot hub tooyour mensagens
- [Transferir o Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Criar uma aplicação Web

1. No Olá [portal do Azure](https://ms.portal.azure.com/), clique em **novo** > **Web + móvel** > **aplicação Web**.
2. Introduza um nome de tarefa exclusivo, certifique-se de subscrição de Olá, especifique um grupo de recursos e uma localização, selecione **Pin toodashboard**e, em seguida, clique em **criar**.

   Recomendamos que selecione Olá mesma localização que o grupo de recursos. Se o fizer, auxilia com velocidade de processamento e reduz o custo de Olá de transferência de dados.

   ![Criar uma aplicação Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Configurar Olá web tooread os dados da aplicação do seu IoT hub

1. Abra a aplicação de web de Olá que apenas tiver sido aprovisionados.
2. Clique em **definições da aplicação**e, em **as definições de aplicação**, adicionar Olá pares chave/valor a seguir:

   | Chave                                   | Valor                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Obtidos a partir do Explorador do iothub                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | nome de Olá do grupo de consumidores Olá que adicione tooyour IoT hub  |

   ![Adicionar a aplicação de web de tooyour definições com pares chave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Clique em **definições da aplicação**, em **definições gerais**, Olá alternar **Web sockets** opção e, em seguida, clique em **guardar**.

   ![Ative a opção de sockets Olá Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Carregar um toobe de aplicações web alojada pelo Olá web app

No GitHub, fizemos disponível uma aplicação web que apresenta dados de sensores em tempo real a partir do seu IoT hub. Tudo o que precisa toodo é configurar toowork de aplicação web de Olá com um repositório de Git, transfira a aplicação web de Olá a partir do GitHub e, em seguida, carregue-o tooAzure para Olá web app toohost.

1. Na aplicação web de Olá, clique em **opções de implementação** > **Escolher origem** > **repositório de Git Local**e, em seguida, clique em **OK**.

   ![Configurar o web app implementação toouse Olá repositório de Git local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Clique em **as credenciais de implementação**, criar um utilizador nome e palavra-passe toouse tooconnect toohello repositório de Git no Azure e, em seguida, clique em **guardar**.

3. Clique em **descrição geral**e anote o valor Olá **url de clone de Git**.

   ![Obter o URL do clone de Git Olá da sua aplicação web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Abra uma janela de terminal no seu computador local ou um comando.

5. Transferir a aplicação web de Olá a partir do GitHub e carregá-la tooAzure para Olá web app toohost. toodo por isso, execute Olá os seguintes comandos:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<URL de clone de Git\> é Olá URL do repositório de Git Olá encontrado no Olá **descrição geral** página da aplicação web de Olá.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Abrir Olá web toosee em tempo real relativos à temperatura e humidade dados da aplicação a partir do seu IoT hub

No Olá **descrição geral** página da sua aplicação web, clique em Olá URL tooopen Olá web app.

![Obter URL Olá da sua aplicação web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Deverá ver a temperatura em tempo real Olá e os dados de humidade do seu IoT hub.

![Página da aplicação Web em tempo real temperatura e humidade a mostrar](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Certifique-se a aplicação de exemplo de Olá está em execução no seu dispositivo. Se não, obterá um gráfico em branco, pode consultar toohello tutoriais em [configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Passos seguintes
Utilizou com êxito os dados de sensores em tempo real de toovisualize de aplicação web do seu IoT hub.

Para um maneira toovisualize de dados do IoT Hub do Azure, consulte [dados de sensores em tempo real de toovisualize Power BI da utilização do seu IoT hub](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
