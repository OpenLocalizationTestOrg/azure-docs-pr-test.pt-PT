---
title: "telemetria dinâmica aaaUse | Microsoft Docs"
description: "Siga este tutorial toolearn toouse telemetria dinâmica com Olá Azure IoT Suite monitorização remota como solução pré-configurada."
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
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Utilizar telemetria dinâmica com Olá solução pré-configurada de monitorização remota

Telemetria dinâmica permite toovisualize toohello qualquer telemetria enviada solução pré-configurada de monitorização remota. dispositivos de Olá simulado que implementar com a solução pré-configurada de Olá enviam telemetria de temperatura e humidade, que pode visualizar no dashboard de Olá. Se personalizar dispositivos simulados existentes, criar novos dispositivos simulados ou ligar a dispositivos físicos toohello pré-configurada solução pode enviar outros valores de telemetria, tais como a temperatura externa Olá, RPM ou windspeed. Em seguida, pode visualizar esta telemetria adicional no dashboard de Olá.

Este tutorial utiliza um dispositivo simulado Node.js simple que pode modificar facilmente tooexperiment com a telemetria dinâmica.

toocomplete neste tutorial, irá precisar de:

* Uma subscrição ativa do Azure. Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk_free_trial].
* [NODE.js] [ lnk-node] versão 0.12 ou posterior.

Pode concluir este tutorial em qualquer sistema operativo, tais como o Windows ou Linux, onde pode instalar o Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Adicionar um tipo de telemetria

Olá passo seguinte consiste em telemetria de Olá tooreplace gerada pelo dispositivo simulado de Node.js Olá com um novo conjunto de valores:

1. Parar Olá Node.js dispositivo simulado, escrevendo **Ctrl + C** na sua linha de comandos ou a shell.
2. No ficheiro de remote_monitoring.js Olá, pode ver os valores de base de dados de Olá de temperatura existente Olá, a humidade e a telemetria de temperatura externa. Adicione um valor de base de dados para **rpm** da seguinte forma:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. dispositivo simulado do Node.js Olá utiliza Olá **generateRandomIncrement** funcionar Olá remote_monitoring.js ficheiro tooadd toohello um incremento aleatório valores de base de dados. Utilize uma ordem aleatória Olá **rpm** valor através da adição de uma linha de código após randomizations existente Olá da seguinte forma:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Adicione Olá novo rpm valor toohello JSON payload Olá dispositivo envia tooIoT Hub:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Execute o dispositivo do Node.js de Olá simulado utilizando Olá os seguintes comandos:

    `node remote_monitoring.js`

6. Observe Olá novo RPM tipo de telemetria apresentadas no gráfico de Olá no dashboard de Olá:

![Adicionar RPM toohello dashboard][image3]

> [!NOTE]
> Pode ter toodisable e, em seguida, ativar o dispositivo de Node.js Olá Olá **dispositivos** página Olá dashboard toosee Olá de alterações do imediatamente.

## <a name="customize-hello-dashboard-display"></a>Personalizar a apresentação de dashboard Olá

Olá **Device-Info** mensagem pode incluir metadados sobre a telemetria de Olá dispositivo Olá pode enviar tooIoT Hub. Estes metadados podem especificar os tipos de telemetria Olá Olá dispositivo envia. Modificar Olá **deviceMetaData** valor Olá remote_monitoring.js ficheiro tooinclude um **telemetria** definição seguir Olá **comandos** definição. Olá seguinte fragmento de código mostra Olá **comandos** definição (ser tooadd se um `,` após Olá **comandos** definição):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> solução de monitorização remota Olá utiliza uma definição de metadados do correspondência sensível toocompare Olá com dados no fluxo de telemetria de Olá.


Adicionar um **telemetria** definição conforme mostrado no Olá anterior fragmento de código não alterar o comportamento de Olá do dashboard de Olá. No entanto, os metadados de Olá também podem incluir um **DisplayName** toocustomize Olá apresentação no dashboard de Olá de atributos. Olá atualização **telemetria** definição de metadados, conforme mostrado no Olá seguinte fragmento:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

Olá seguinte captura de ecrã mostra como esta alteração modifica a legenda do gráfico Olá no dashboard de Olá:

![Personalizar a legenda do gráfico Olá][image4]

> [!NOTE]
> Pode ter toodisable e, em seguida, ativar o dispositivo de Node.js Olá Olá **dispositivos** página Olá dashboard toosee Olá de alterações do imediatamente.

## <a name="filter-hello-telemetry-types"></a>Filtrar os tipos de telemetria de Olá

Por predefinição, o gráfico de Olá no dashboard de Olá mostra todas as séries de dados num fluxo de telemetria de Olá. Pode utilizar Olá **Device-Info** metadados toosuppress Olá apresentação dos tipos de telemetria específico no gráfico de Olá. 

gráfico de Olá toomake Mostrar apenas as relativos à temperatura e humidade telemetria, omita **ExternalTemperature** de Olá **Device-Info** **telemetria** metadados da seguinte forma:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

Olá **temperatura Outdoor** já não é apresentado no gráfico de Olá:

![Filtro Olá telemetria no dashboard de Olá][image5]

Esta alteração afeta apenas a visualização de gráfico de Olá. Olá **ExternalTemperature** valores de dados ainda são armazenados e disponibilizados para qualquer processamento de back-end.

> [!NOTE]
> Pode ter toodisable e, em seguida, ativar o dispositivo de Node.js Olá Olá **dispositivos** página Olá dashboard toosee Olá de alterações do imediatamente.

## <a name="handle-errors"></a>Processar erros

Para um toodisplay de fluxo de dados no gráfico de Olá, respetivo **tipo** no Olá **Device-Info** metadados tem de corresponder ao tipo de dados de Olá dos valores de telemetria de Olá. Por exemplo, se hello metadados Especifica que Olá **tipo** humidade dados são **int** e um **duplo** se encontra no fluxo de telemetria de Olá, em seguida, a telemetria de humidade Olá não apresente no gráfico de Olá. No entanto, Olá **humidade** valores ainda são armazenados e disponibilizados para qualquer processamento de back-end.

## <a name="next-steps"></a>Passos seguintes

Agora que viu como toouse de telemetria dinâmico, pode saber mais sobre como Olá soluções pré-configuradas utilizam as informações do dispositivo: [solução pré-configurada de metadados de informações do dispositivo na monitorização remota do Olá] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
