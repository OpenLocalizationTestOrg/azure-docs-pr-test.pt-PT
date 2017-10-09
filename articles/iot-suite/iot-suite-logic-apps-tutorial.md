---
title: aaaAzure IoT Suite e Logic Apps | Microsoft Docs
description: "Um tutorial sobre como toohook segurança Logic Apps tooAzure IoT Suite para o processo empresarial."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Tutorial: Ligar a solução de monitorização do Azure IoT Suite remota pré-configurada tooyour de aplicação lógica
Olá [Microsoft Azure IoT Suite] [ lnk-internetofthings] solução pré-configurada de monitorização remota é uma excelente forma tooget a trabalhar rapidamente com um conjunto de funcionalidades de ponto-a-ponto que exemplifies uma solução de IoT. Este tutorial orienta como tooadd aplicação lógica tooyour Microsoft Azure IoT Suite remoto solução pré-configurada de monitorização. Estes passos demonstram como pode tirar ainda mais a sua solução de IoT ligando-o processo de negócios tooa.

*Se pretender para instruções sobre como tooprovision uma monitorização remota solução pré-configurada, consulte o artigo [Tutorial: introdução às soluções pré-configuradas de IoT de Olá][lnk-getstarted].*

Antes de começar este tutorial, deve:

* Aprovisionar Olá remoto solução pré-configurada de monitorização na sua subscrição do Azure.
* Criar um tooenable de conta do SendGrid toosend uma mensagem de e-mail que aciona o processo de negócio. Pode inscrever-se para uma conta de avaliação gratuita em [SendGrid](https://sendgrid.com/) clicando **Experimente gratuitamente**. Depois de ter registado para a sua conta de avaliação gratuita, terá de toocreate um [chave de API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) no SendGrid que concede permissões toosend correio. É necessário esta chave de API mais tarde no tutorial Olá.

toocomplete neste tutorial, terá de Visual Studio 2015 ou Visual Studio 2017 toomodify Olá as ações do Olá solução pré-configurada de back-end.

Partindo do princípio de que já tenha sido já aprovisionada monitorização remota solução pré-configurada, navegue toohello o grupo de recursos para essa solução na Olá [portal do Azure][lnk-azureportal]. grupo de recursos de Olá tem Olá mesmo nome como hello solução nome escolheu quando aprovisionou a sua solução de monitorização remota. No grupo de recursos de Olá, pode ver todas as Olá aprovisionado recursos do Azure para a sua solução exceto Olá aplicação Azure Active Directory que pode encontrar no Olá Portal clássico do Azure. Olá seguinte captura de ecrã mostra um exemplo **grupo de recursos** solução pré-configurada do painel para uma monitorização remota:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, configurar toouse de aplicação de lógica de Olá com Olá solução pré-configurada.

## <a name="set-up-hello-logic-app"></a>Configurar Olá aplicação lógica
1. Clique em **adicionar** , Olá parte superior do seu painel do grupo de recursos no Olá portal do Azure.
2. Procurar **aplicação lógica**, selecione-o e, em seguida, clique em **criar**.
3. Preencha Olá **nome** e utilize Olá mesmo **subscrição** e **grupo de recursos** que utilizou quando aprovisionou a sua solução de monitorização remota. Clique em **Criar**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Quando tiver concluído a sua implementação, pode ver Olá que aplicação lógica está listada como um recurso no seu grupo de recursos.
5. Clique em Painel aplicação lógica toonavigate toohello Olá aplicação lógica, selecione de Olá **aplicação lógica em branco** Olá do modelo tooopen **Designer de aplicações lógicas**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Selecione **pedido**. Esta ação Especifica que um pedido HTTP recebido com um JSON específico formatado atos de payload como um acionador.
7. Cole o seguinte código para Olá esquema de JSON de corpo do pedido de Olá:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Pode copiar Olá URL para o post Olá HTTP depois de guardar a aplicação de lógica de Olá, mas primeiro tem de adicionar uma ação.
   > 
   > 
8. Clique em **+ novo passo** sob o acionador manual. Em seguida, clique em **adicionar uma ação**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Procurar **SendGrid - enviar e-mail** e clique no mesmo.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Introduza um nome para a ligação de Olá, tais como **SendGridConnection**, introduza Olá **chave de API do SendGrid** que criou quando configurar a conta do SendGrid e clique em **criar**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Adicionar endereços de e-mail tooboth própria Olá **de** e **para** campos. Adicionar **alerta de monitorização remota [DeviceId]** toohello **requerente** campo. No Olá **corpo da mensagem** campo, adicione **dispositivo [DeviceId] apresentou [measurementName] com o valor [measuredValue].** Pode adicionar **[DeviceId]**, **[measurementName]**, e **[measuredValue]** clicando no Olá **pode inserir dados dos passos anteriores**secção.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Clique em **guardar** no menu superior Olá.
13. Clique em Olá **pedido** Olá acionador e copie **Http Post toothis URL** valor. Este URL é necessário mais tarde no tutorial.

> [!NOTE]
> As Logic Apps permitem-lhe toorun [vários tipos de ação] [ lnk-logic-apps-actions] incluindo ações no Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Configurar Olá EventProcessor Web tarefa
Nesta secção, ligar a solução pré-configurada de toohello aplicação lógica que criou. toocomplete nesta tarefa, adicionar Olá URL tootrigger Olá aplicação lógica toohello ação que é acionado quando um valor de sensor dispositivo excede um limiar.

1. Utilizar o git tooclone Olá mais recente versão de cliente Olá [azure-iot-remote-monitoring repositório do github][lnk-rmgithub]. Por exemplo:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. No Visual Studio, abra Olá **RemoteMonitoring.sln** a partir de cópia de local de Olá do repositório de Olá.
3. Abra Olá **ActionRepository.cs** ficheiro Olá **infraestrutura\\repositório** pasta.
4. Olá atualização **actionIds** dicionário com Olá **Http Post toothis URL** que anotou da sua aplicação lógica da seguinte forma:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Guardar alterações de Olá na solução e sair do Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Implementar a partir da linha de comandos Olá
Nesta secção, implementar a versão atualizada do Olá monitorização solução tooreplace Olá versão remoto atualmente em execução no Azure.

1. Os seguintes Olá [dev configuração] [ lnk-devsetup] instruções tooset configurar o ambiente para implementação.
2. toodeploy localmente, siga Olá [implementação local] [ lnk-localdeploy] instruções.
3. toodeploy toohello na nuvem e atualizar a implementação de nuvem existente, siga Olá [implementação na nuvem] [ lnk-clouddeploy] instruções. Utilize o nome de Olá da implementação original como nome da implementação Olá. Por exemplo, se a implementação original Olá foi chamada **demologicapp**, utilize Olá os seguintes comandos:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Quando Olá compilar o script é executado, não se esqueça de toouse Olá a mesma conta do Azure, subscrição, região e instância do Active Directory que utilizou quando aprovisionou a solução de Olá.

## <a name="see-your-logic-app-in-action"></a>Ver a sua aplicação lógica em ação
Olá solução pré-configurada de monitorização remota tem duas regras configurar por predefinição, quando Aprovisiona uma solução. Ambas as regras são no Olá **SampleDevice001** dispositivo:

* Temperatura > 38.00
* Humidade > 48.00

regra de temperatura Olá aciona Olá **elevar alarme** ação e Olá regra humidade aciona Olá **SendMessage** ação. Partindo do princípio que utilizou Olá mesmo URL para ambos os Olá ações **ActionRepository** classe, os acionadores da aplicação lógica para a regra. Ambas as regras de utilizam SendGrid toosend toohello um e-mail **para** endereço com detalhes de alerta de Olá.

> [!NOTE]
> Olá aplicação lógica continua tootrigger sempre Olá limiar ser cumprido. tooavoid desnecessários mensagens de correio eletrónico, pode desativar ou regras Olá na sua solução portal ou desativar Olá aplicação lógica em Olá [portal do Azure][lnk-azureportal].
> 
> 

Além disso tooreceiving e-mails, também pode ver quando Olá lógica de aplicação é executada no portal de Olá:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Passos seguintes
Agora que utilizou um aplicação lógica tooconnect Olá pré-configurada solução tooa negócio processo, pode saber mais sobre as opções de Olá para personalizar as soluções pré-configuradas de Olá:

* [Utilizar telemetria dinâmica com Olá solução pré-configurada de monitorização remota][lnk-dynamic]
* [Metadados de informações do dispositivo Olá solução pré-configurada de monitorização remota][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
