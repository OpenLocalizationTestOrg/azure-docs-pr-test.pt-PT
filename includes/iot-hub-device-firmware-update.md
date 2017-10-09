## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b5220-101">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="b5220-101">Create a simulated device app</span></span>
<span data-ttu-id="b5220-102">Nesta secção, pode:</span><span class="sxs-lookup"><span data-stu-id="b5220-102">In this section, you:</span></span>

* <span data-ttu-id="b5220-103">Criar uma aplicação de consola do Node.js que responde método direto tooa chamado pela nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="b5220-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="b5220-104">Acionar uma atualização de firmware simulada</span><span class="sxs-lookup"><span data-stu-id="b5220-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="b5220-105">Olá de utilização comunicados propriedades tooenable dispositivos duplo consultas tooidentify dispositivos e quando estes pela última vez foi concluída uma atualização de firmware</span><span class="sxs-lookup"><span data-stu-id="b5220-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="b5220-106">Passo 1: Criar uma pasta vazia designada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="b5220-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="b5220-107">No Olá **manageddevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5220-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b5220-108">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="b5220-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="b5220-109">Passo 2: na sua linha de comandos Olá **manageddevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device** e **azure-iot-dispositivo-mqtt** dispositivo Pacotes SDK:</span><span class="sxs-lookup"><span data-stu-id="b5220-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="b5220-110">Passo 3: Com um editor de texto, crie um **dmpatterns_fwupdate_device.js** ficheiro Olá **manageddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="b5220-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="b5220-111">Passo 4: Adicione a seguinte Olá 'exigir' instruções início Olá de Olá **dmpatterns_fwupdate_device.js** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="b5220-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="b5220-112">Passo 5: Adicionar um **connectionString** variável e utilize-toocreate um **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="b5220-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="b5220-113">Substitua Olá `{yourdeviceconnectionstring}` marcador de posição pela cadeia de ligação de Olá feitas anteriormente nota da secção "Criar uma identidade de dispositivo" de Olá anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b5220-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="b5220-114">Passo 6: Adicionar seguinte Olá função que é utilizado tooupdate comunicadas propriedades:</span><span class="sxs-lookup"><span data-stu-id="b5220-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

<span data-ttu-id="b5220-115">Passo 7: Adicione Olá funções que simulam a transferir e a aplicar imagem de firmware Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b5220-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

<span data-ttu-id="b5220-116">Passo 8: Adicionar Olá seguinte função que o estado da atualização de firmware de Olá de atualizações através de Olá reportados propriedades demasiado**a aguardar**.</span><span class="sxs-lookup"><span data-stu-id="b5220-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="b5220-117">Normalmente, dispositivos são se manter informado sobre uma atualização disponível e um administrador definido política faz com que Olá dispositivo toostart transferir e aplicar a atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5220-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="b5220-118">Esta função é onde Olá tooenable lógica que política deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="b5220-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="b5220-119">Para uma simplicidade exemplo Olá aguarda quatro segundos antes de imagem de firmware do continuar toodownload Olá:</span><span class="sxs-lookup"><span data-stu-id="b5220-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

<span data-ttu-id="b5220-120">Passo 9: Adicionar Olá seguinte função que o estado da atualização de firmware de Olá de atualizações através de Olá reportados propriedades demasiado**transferir**.</span><span class="sxs-lookup"><span data-stu-id="b5220-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="b5220-121">Olá função, em seguida, simula uma transferência de firmware e, finalmente, as atualizações Olá tooeither de estado de atualização de firmware **downloadFailed** ou **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="b5220-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

<span data-ttu-id="b5220-122">Passo 10: Adicionar Olá seguinte função que o estado da atualização de firmware de Olá de atualizações através de Olá reportados propriedades demasiado**aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b5220-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="b5220-123">Olá função, em seguida, simula aplicar imagem de firmware Olá e, finalmente, as atualizações Olá tooeither de estado de atualização de firmware **applyFailed** ou **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="b5220-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

<span data-ttu-id="b5220-124">Passo 11: Adicionar esse Olá de identificadores de função seguinte Olá **firmwareUpdate** método direto e inicia Olá fase multi firmware processo de atualização:</span><span class="sxs-lookup"><span data-stu-id="b5220-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="b5220-125">Passo 12: Por fim, adicione Olá seguinte código que estabelece ligação tooyour IoT hub:</span><span class="sxs-lookup"><span data-stu-id="b5220-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="b5220-126">ações de tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="b5220-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b5220-127">No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5220-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 