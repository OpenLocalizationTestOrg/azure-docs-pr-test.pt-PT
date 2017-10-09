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
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="d9ecd-103">Utilizar telemetria dinâmica com Olá solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="d9ecd-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="d9ecd-104">Telemetria dinâmica permite toovisualize toohello qualquer telemetria enviada solução pré-configurada de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="d9ecd-105">dispositivos de Olá simulado que implementar com a solução pré-configurada de Olá enviam telemetria de temperatura e humidade, que pode visualizar no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="d9ecd-106">Se personalizar dispositivos simulados existentes, criar novos dispositivos simulados ou ligar a dispositivos físicos toohello pré-configurada solução pode enviar outros valores de telemetria, tais como a temperatura externa Olá, RPM ou windspeed.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="d9ecd-107">Em seguida, pode visualizar esta telemetria adicional no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="d9ecd-108">Este tutorial utiliza um dispositivo simulado Node.js simple que pode modificar facilmente tooexperiment com a telemetria dinâmica.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="d9ecd-109">toocomplete neste tutorial, irá precisar de:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="d9ecd-110">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-110">An active Azure subscription.</span></span> <span data-ttu-id="d9ecd-111">Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d9ecd-112">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="d9ecd-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="d9ecd-113">[NODE.js] [ lnk-node] versão 0.12 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="d9ecd-114">Pode concluir este tutorial em qualquer sistema operativo, tais como o Windows ou Linux, onde pode instalar o Node.js.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="d9ecd-115">Adicionar um tipo de telemetria</span><span class="sxs-lookup"><span data-stu-id="d9ecd-115">Add a telemetry type</span></span>

<span data-ttu-id="d9ecd-116">Olá passo seguinte consiste em telemetria de Olá tooreplace gerada pelo dispositivo simulado de Node.js Olá com um novo conjunto de valores:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="d9ecd-117">Parar Olá Node.js dispositivo simulado, escrevendo **Ctrl + C** na sua linha de comandos ou a shell.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="d9ecd-118">No ficheiro de remote_monitoring.js Olá, pode ver os valores de base de dados de Olá de temperatura existente Olá, a humidade e a telemetria de temperatura externa.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="d9ecd-119">Adicione um valor de base de dados para **rpm** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="d9ecd-120">dispositivo simulado do Node.js Olá utiliza Olá **generateRandomIncrement** funcionar Olá remote_monitoring.js ficheiro tooadd toohello um incremento aleatório valores de base de dados.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="d9ecd-121">Utilize uma ordem aleatória Olá **rpm** valor através da adição de uma linha de código após randomizations existente Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="d9ecd-122">Adicione Olá novo rpm valor toohello JSON payload Olá dispositivo envia tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="d9ecd-123">Execute o dispositivo do Node.js de Olá simulado utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="d9ecd-124">Observe Olá novo RPM tipo de telemetria apresentadas no gráfico de Olá no dashboard de Olá:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Adicionar RPM toohello dashboard][image3]

> [!NOTE]
> <span data-ttu-id="d9ecd-126">Pode ter toodisable e, em seguida, ativar o dispositivo de Node.js Olá Olá **dispositivos** página Olá dashboard toosee Olá de alterações do imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="d9ecd-127">Personalizar a apresentação de dashboard Olá</span><span class="sxs-lookup"><span data-stu-id="d9ecd-127">Customize hello dashboard display</span></span>

<span data-ttu-id="d9ecd-128">Olá **Device-Info** mensagem pode incluir metadados sobre a telemetria de Olá dispositivo Olá pode enviar tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="d9ecd-129">Estes metadados podem especificar os tipos de telemetria Olá Olá dispositivo envia.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="d9ecd-130">Modificar Olá **deviceMetaData** valor Olá remote_monitoring.js ficheiro tooinclude um **telemetria** definição seguir Olá **comandos** definição.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="d9ecd-131">Olá seguinte fragmento de código mostra Olá **comandos** definição (ser tooadd se um `,` após Olá **comandos** definição):</span><span class="sxs-lookup"><span data-stu-id="d9ecd-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

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
> <span data-ttu-id="d9ecd-132">solução de monitorização remota Olá utiliza uma definição de metadados do correspondência sensível toocompare Olá com dados no fluxo de telemetria de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="d9ecd-133">Adicionar um **telemetria** definição conforme mostrado no Olá anterior fragmento de código não alterar o comportamento de Olá do dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="d9ecd-134">No entanto, os metadados de Olá também podem incluir um **DisplayName** toocustomize Olá apresentação no dashboard de Olá de atributos.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="d9ecd-135">Olá atualização **telemetria** definição de metadados, conforme mostrado no Olá seguinte fragmento:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

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

<span data-ttu-id="d9ecd-136">Olá seguinte captura de ecrã mostra como esta alteração modifica a legenda do gráfico Olá no dashboard de Olá:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Personalizar a legenda do gráfico Olá][image4]

> [!NOTE]
> <span data-ttu-id="d9ecd-138">Pode ter toodisable e, em seguida, ativar o dispositivo de Node.js Olá Olá **dispositivos** página Olá dashboard toosee Olá de alterações do imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="d9ecd-139">Filtrar os tipos de telemetria de Olá</span><span class="sxs-lookup"><span data-stu-id="d9ecd-139">Filter hello telemetry types</span></span>

<span data-ttu-id="d9ecd-140">Por predefinição, o gráfico de Olá no dashboard de Olá mostra todas as séries de dados num fluxo de telemetria de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="d9ecd-141">Pode utilizar Olá **Device-Info** metadados toosuppress Olá apresentação dos tipos de telemetria específico no gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="d9ecd-142">gráfico de Olá toomake Mostrar apenas as relativos à temperatura e humidade telemetria, omita **ExternalTemperature** de Olá **Device-Info** **telemetria** metadados da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="d9ecd-143">Olá **temperatura Outdoor** já não é apresentado no gráfico de Olá:</span><span class="sxs-lookup"><span data-stu-id="d9ecd-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filtro Olá telemetria no dashboard de Olá][image5]

<span data-ttu-id="d9ecd-145">Esta alteração afeta apenas a visualização de gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-145">This change only affects hello chart display.</span></span> <span data-ttu-id="d9ecd-146">Olá **ExternalTemperature** valores de dados ainda são armazenados e disponibilizados para qualquer processamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="d9ecd-147">Pode ter toodisable e, em seguida, ativar o dispositivo de Node.js Olá Olá **dispositivos** página Olá dashboard toosee Olá de alterações do imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="d9ecd-148">Processar erros</span><span class="sxs-lookup"><span data-stu-id="d9ecd-148">Handle errors</span></span>

<span data-ttu-id="d9ecd-149">Para um toodisplay de fluxo de dados no gráfico de Olá, respetivo **tipo** no Olá **Device-Info** metadados tem de corresponder ao tipo de dados de Olá dos valores de telemetria de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="d9ecd-150">Por exemplo, se hello metadados Especifica que Olá **tipo** humidade dados são **int** e um **duplo** se encontra no fluxo de telemetria de Olá, em seguida, a telemetria de humidade Olá não apresente no gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="d9ecd-151">No entanto, Olá **humidade** valores ainda são armazenados e disponibilizados para qualquer processamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="d9ecd-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9ecd-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d9ecd-152">Next steps</span></span>

<span data-ttu-id="d9ecd-153">Agora que viu como toouse de telemetria dinâmico, pode saber mais sobre como Olá soluções pré-configuradas utilizam as informações do dispositivo: [solução pré-configurada de metadados de informações do dispositivo na monitorização remota do Olá] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="d9ecd-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
