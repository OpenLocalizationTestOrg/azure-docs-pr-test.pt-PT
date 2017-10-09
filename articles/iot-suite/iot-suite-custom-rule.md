---
title: aaaCreate uma regra personalizada no Azure IoT Suite | Microsoft Docs
description: "Como toocreate uma regra personalizada num IoT Suite solução pré-configurada."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Criar uma regra personalizada no Olá solução pré-configurada de monitorização remota

## <a name="introduction"></a>Introdução

Em soluções de Olá pré-configurada, pode configurar [regras que é acionam quando uma telemetria valor para um dispositivo atinge um limiar específico][lnk-builtin-rule]. [Utilizar telemetria dinâmica com Olá solução pré-configurada de monitorização remota] [ lnk-dynamic-telemetry] descreve como adicionar valores de telemetria personalizada, tal como *ExternalTemperature* tooyour solução. Este artigo mostra como tipos de regra personalizada de toocreate para telemetria dinâmica na sua solução.

Este tutorial utiliza um simple Node.js dispositivo simulado toogenerate telemetria dinâmica toosend toohello solução pré-configurada de back-end. Em seguida, adicione regras personalizadas no Olá **RemoteMonitoring** solução do Visual Studio e implementar este tooyour de back-end personalizado subscrição do Azure.

toocomplete neste tutorial, precisa de:

* Uma subscrição ativa do Azure. Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk_free_trial].
* [NODE.js] [ lnk-node] versão 0.12 ou posterior toocreate um dispositivo simulado.
* Visual Studio 2015 ou Visual Studio 2017 toomodify Olá pré-configurada solução de back-end com as regras de novo.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Tome nota do nome da solução Olá que escolheu para a sua implementação. Terá este nome de solução mais tarde no tutorial.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Pode parar a aplicação de consola do Node.js Olá quando tiver verificado que está a enviar **ExternalTemperature** telemetria toohello solução pré-configurada. Janela de consola Olá manter abertas porque executar esta aplicação de consola do Node.js novamente depois de adicionar a solução de toohello Olá regra personalizada.

## <a name="rule-storage-locations"></a>Localizações de armazenamento de regra

Informações sobre regras é persistente em duas localizações:

* **DeviceRulesNormalizedTable** tabela – esta tabela armazena um normalizado regras toohello definidas pelo portal de solução Olá de referência. Quando o portal de solução Olá apresenta as regras de dispositivos, consulta esta tabela para definições de regras de Olá.
* **DeviceRules** blob – este blob armazena todas as regras de Olá definidas para todos os registado dispositivos e estão definidos como uma entrada toohello de referência do Azure Stream Analytics as tarefas.
 
Quando atualizar uma regra existente ou definir uma nova regra no portal de solução Olá, tabela Olá e BLOBs são atualizados tooreflect Olá alterações. regra de Olá definição apresentado no portal de Olá provém de arquivo de tabela Olá e regra Olá definição referenciada pelas tarefas do Stream Analytics Olá provém do blob Olá. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Atualizar a solução do Olá RemoteMonitoring Visual Studio

Olá passos seguintes mostram como toomodify Olá RemoteMonitoring Visual Studio solução tooinclude uma nova regra que utiliza Olá **ExternalTemperature** telemetria enviada do dispositivo simulado Olá:

1. Se que ainda não tiver feito, Olá clone **azure-iot-remote-monitoring** localização de adequado tooa repositório no seu computador local utilizando Olá os seguintes comandos de Git:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. No Visual Studio, abra o ficheiro de RemoteMonitoring.sln de Olá da sua cópia local do Olá **azure-iot-remote-monitoring** repositório.

3. Abra o ficheiro de Olá Infrastructure\Models\DeviceRuleBlobEntity.cs e adicione um **ExternalTemperature** propriedade da seguinte forma:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. No mesmo ficheiro de Olá, adicione um **ExternalTemperatureRuleOutput** propriedade da seguinte forma:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Abra o ficheiro de Olá Infrastructure\Models\DeviceRuleDataFields.cs e adicione o seguinte Olá **ExternalTemperature** propriedade depois Olá existente **humidade** propriedade:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. No mesmo ficheiro de Olá, atualize Olá **_availableDataFields** método tooinclude **ExternalTemperature** da seguinte forma:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Abra o ficheiro de Olá Infrastructure\Repository\DeviceRulesRepository.cs e modificar Olá **BuildBlobEntityListFromTableRows** método da seguinte forma:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Reconstruir e voltar a implementar a solução de Olá.

Agora pode implementar Olá atualizado solução tooyour subscrição do Azure.

1. Abra uma linha de comandos elevada e navegue toohello raiz da sua cópia local do repositório azure-iot-remote-monitoring de Olá.

2. toodeploy solução atualizada, execute Olá os seguintes comandos substituindo **{nome da implementação}** com o nome de Olá da implementação da solução pré-configurada que apontou anteriormente:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Actualizar a tarefa de Stream Analytics Olá

Quando a implementação de Olá estiver concluída, pode atualizar Olá Stream Analytics tarefa toouse Olá novas definições de regras.

1. No portal do Azure Olá, navegue até toohello grupo de recursos que contém recursos da sua solução pré-configurada. Este grupo de recursos tem Olá mesmo nome que especificou para Olá solução durante a implementação de Olá.

2. Navegue toohello {nome da implementação}-tarefa do Stream Analytics de regras. 

3. Clique em **parar** tarefa de Stream Analytics Olá toostop a execução. (Tem de aguardar Olá de transmissão em fluxo toostop tarefa antes de poder editar consulta Olá).

4. Clique em **consulta**. Editar Olá do Olá consulta tooinclude **SELECIONE** instrução para **ExternalTemperature**. Olá exemplo seguinte mostra Olá concluída consulta com Olá novo **SELECIONE** instrução:

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Clique em **guardar** toochange Olá atualizado consulta de regra.

6. Clique em **iniciar** tarefa de Stream Analytics toostart Olá executar de novo.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Adicionar a nova regra no dashboard de Olá

Agora pode adicionar Olá **ExternalTemperature** dispositivo tooa de regra no dashboard de solução Olá.

1. Navegue toohello portal de solução.

2. Navegue toohello **dispositivos** painel.

3. Localizar Olá personalizadas do dispositivo que criou que envia **ExternalTemperature** telemetria e no Olá **detalhes do dispositivo** painel, clique em **Adicionar regra**.

4. Selecione **ExternalTemperature** no **campo de dados**.

5. Definir **limiar** too56. Em seguida, clique em **guardar e ver regras**.

6. Devolva o histórico de alarme toohello dashboard tooview Olá.

7. Na janela de consola Olá que deixadas abertas, começar a enviar do Olá Node.js consola aplicação toobegin **ExternalTemperature** dados de telemetria.

8. Tenha em atenção que Olá **histórico de alarme** tabela mostra alarmes novo quando nova regra de Olá é activada.
 
## <a name="additional-information"></a>Informações adicionais

Operador de Olá alteração  **>**  for mais complexo e vai mais além Olá passos descritos neste tutorial. Enquanto pode alterar toouse de tarefa do Stream Analytics Olá qualquer operador pretender, ao refletir que operador no portal de solução Olá é uma tarefa de mais complexa. 

## <a name="next-steps"></a>Passos seguintes
Agora que viu como regras personalizadas toocreate, pode saber mais sobre soluções de Olá pré-configurada:

- [Ligar a aplicação lógica tooyour Azure IoT Suite monitorização remota pré-configurada solução][lnk-logic-app]
- [Solução pré-configurada de metadados de informações do dispositivo na monitorização remota do Olá][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md