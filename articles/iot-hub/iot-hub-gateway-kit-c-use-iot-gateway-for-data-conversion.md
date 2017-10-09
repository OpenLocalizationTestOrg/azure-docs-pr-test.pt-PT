---
title: "conversão de aaaData no gateway de IoT com limite de IoT do Azure | Microsoft Docs"
description: "Utilize o IoT gateway tooconvert Olá formato de dados de sensor através de um módulo personalizado a partir do Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversão de dados de gateway do IOT, transformação de dados do gateway de iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="407ca-104">Utilize o gateway de IoT para transformação de dados de sensor com limite de IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="407ca-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="407ca-105">Antes de começar este tutorial, certifique-se que tiver concluído Olá seguir lições na sequência:</span><span class="sxs-lookup"><span data-stu-id="407ca-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="407ca-106">Configurar o Intel NUC como um gateway do IoT</span><span class="sxs-lookup"><span data-stu-id="407ca-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="407ca-107">Utilize o IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="407ca-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="407ca-108">Um objetivo de um gateway de Iot é tooprocess recolhidos dados antes de a enviar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="407ca-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="407ca-109">Limite de IoT do Azure introduz módulos que podem ser criados e assembled tooform fluxo de trabalho de processamento de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="407ca-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="407ca-110">Um módulo recebe uma mensagem, efetua algumas ações no mesmo e, em seguida, mova-para outros tooprocess de módulos.</span><span class="sxs-lookup"><span data-stu-id="407ca-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="407ca-111">O que irá aprender</span><span class="sxs-lookup"><span data-stu-id="407ca-111">What you learn</span></span>

<span data-ttu-id="407ca-112">Pode saber como toocreate tooconvert um módulo mensagens de Olá SensorTag num formato diferente.</span><span class="sxs-lookup"><span data-stu-id="407ca-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="407ca-113">O que fazer</span><span class="sxs-lookup"><span data-stu-id="407ca-113">What you do</span></span>

* <span data-ttu-id="407ca-114">Crie um módulo tooconvert uma mensagem recebida num ficheiro em formato Olá. JSON.</span><span class="sxs-lookup"><span data-stu-id="407ca-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="407ca-115">Compile o módulo Olá.</span><span class="sxs-lookup"><span data-stu-id="407ca-115">Compile hello module.</span></span>
* <span data-ttu-id="407ca-116">Adicione aplicação de exemplo Olá módulo toohello var de limite de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="407ca-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="407ca-117">Execute a aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="407ca-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="407ca-118">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="407ca-118">What you need</span></span>

* <span data-ttu-id="407ca-119">Olá seguintes tutoriais foi concluídas em sequência:</span><span class="sxs-lookup"><span data-stu-id="407ca-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="407ca-120">Configurar o Intel NUC como um gateway do IoT</span><span class="sxs-lookup"><span data-stu-id="407ca-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="407ca-121">Utilize o IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="407ca-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="407ca-122">Um cliente SSH que é executado no computador anfitrião.</span><span class="sxs-lookup"><span data-stu-id="407ca-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="407ca-123">PuTTY recomenda-se no Windows.</span><span class="sxs-lookup"><span data-stu-id="407ca-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="407ca-124">Linux e macOS já vêm com um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="407ca-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="407ca-125">endereço IP Olá e Olá nome de utilizador e palavra-passe tooaccess Olá gateway a partir do cliente SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="407ca-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="407ca-126">Uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="407ca-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="407ca-127">Criar um módulo</span><span class="sxs-lookup"><span data-stu-id="407ca-127">Create a module</span></span>

1. <span data-ttu-id="407ca-128">No computador do anfitrião de Olá, execute o cliente SSH Olá e ligar o gateway de IoT toohello.</span><span class="sxs-lookup"><span data-stu-id="407ca-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="407ca-129">Clone o ficheiros de origem Olá do módulo de conversão de Olá do GitHub toohello diretório raiz do gateway de IoT Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="407ca-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="407ca-130">Este é um módulo nativo do limite do Azure, escrito no Olá linguagem de programação de C.</span><span class="sxs-lookup"><span data-stu-id="407ca-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="407ca-131">módulo Olá converte formato Olá de mensagens recebidas Olá seguir uma:</span><span class="sxs-lookup"><span data-stu-id="407ca-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="407ca-132">Compilar o módulo Olá</span><span class="sxs-lookup"><span data-stu-id="407ca-132">Compile hello module</span></span>

<span data-ttu-id="407ca-133">no módulo de Olá toocompile, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="407ca-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="407ca-134">Obtém um `libmy_module.so` depois de concluída a compilação de Olá de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="407ca-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="407ca-135">Tome nota do caminho absoluto do Olá deste ficheiro.</span><span class="sxs-lookup"><span data-stu-id="407ca-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="407ca-136">Adicionar a aplicação de exemplo Olá módulo toohello var</span><span class="sxs-lookup"><span data-stu-id="407ca-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="407ca-137">Aceda a pasta de amostras toohello executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="407ca-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="407ca-138">Abra o ficheiro de configuração de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="407ca-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="407ca-139">Adicionar um módulo através da inserção Olá seguinte código toohello `modules` secção.</span><span class="sxs-lookup"><span data-stu-id="407ca-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="407ca-140">Substitua `[Your libmy_module.so path]` no código Olá com o caminho absoluto do Olá de Olá libmy_module.so' ficheiros.</span><span class="sxs-lookup"><span data-stu-id="407ca-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="407ca-141">Substitua o código de Olá no Olá `links` secção com Olá seguir uma:</span><span class="sxs-lookup"><span data-stu-id="407ca-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="407ca-142">Prima `ESC`e, em seguida, escreva `:wq` ficheiros de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="407ca-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="407ca-143">Executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="407ca-143">Run hello sample application</span></span>

1. <span data-ttu-id="407ca-144">Ligar Olá SensorTag.</span><span class="sxs-lookup"><span data-stu-id="407ca-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="407ca-145">Definir variável de ambiente de SSL_CERT_FILE Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="407ca-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="407ca-146">Aplicação de exemplo de Olá execução com Olá adicionadas módulo executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="407ca-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="407ca-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="407ca-147">Next steps</span></span>

<span data-ttu-id="407ca-148">Com êxito já utilizar IoT gateway tooconvert Olá mensagem de saudação do SensorTag num ficheiro em formato Olá. JSON.</span><span class="sxs-lookup"><span data-stu-id="407ca-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
