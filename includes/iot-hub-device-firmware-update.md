## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada
Nesta secção, pode:

* Criar uma aplicação de consola do Node.js que responde método direto tooa chamado pela nuvem Olá
* Acionar uma atualização de firmware simulada
* Olá de utilização comunicados propriedades tooenable dispositivos duplo consultas tooidentify dispositivos e quando estes pela última vez foi concluída uma atualização de firmware

Passo 1: Criar uma pasta vazia designada **manageddevice**.  No Olá **manageddevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá. Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```

Passo 2: na sua linha de comandos Olá **manageddevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device** e **azure-iot-dispositivo-mqtt** dispositivo Pacotes SDK:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Passo 3: Com um editor de texto, crie um **dmpatterns_fwupdate_device.js** ficheiro Olá **manageddevice** pasta.

Passo 4: Adicione a seguinte Olá 'exigir' instruções início Olá de Olá **dmpatterns_fwupdate_device.js** ficheiro:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Passo 5: Adicionar um **connectionString** variável e utilize-toocreate um **cliente** instância. Substitua Olá `{yourdeviceconnectionstring}` marcador de posição pela cadeia de ligação de Olá feitas anteriormente nota da secção "Criar uma identidade de dispositivo" de Olá anteriormente:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Passo 6: Adicionar seguinte Olá função que é utilizado tooupdate comunicadas propriedades:
   
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

Passo 7: Adicione Olá funções que simulam a transferir e a aplicar imagem de firmware Olá os seguintes:
   
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

Passo 8: Adicionar Olá seguinte função que o estado da atualização de firmware de Olá de atualizações através de Olá reportados propriedades demasiado**a aguardar**. Normalmente, dispositivos são se manter informado sobre uma atualização disponível e um administrador definido política faz com que Olá dispositivo toostart transferir e aplicar a atualização de Olá. Esta função é onde Olá tooenable lógica que política deve ser executada. Para uma simplicidade exemplo Olá aguarda quatro segundos antes de imagem de firmware do continuar toodownload Olá:
   
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

Passo 9: Adicionar Olá seguinte função que o estado da atualização de firmware de Olá de atualizações através de Olá reportados propriedades demasiado**transferir**. Olá função, em seguida, simula uma transferência de firmware e, finalmente, as atualizações Olá tooeither de estado de atualização de firmware **downloadFailed** ou **downloadComplete**:
   
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

Passo 10: Adicionar Olá seguinte função que o estado da atualização de firmware de Olá de atualizações através de Olá reportados propriedades demasiado**aplicar**. Olá função, em seguida, simula aplicar imagem de firmware Olá e, finalmente, as atualizações Olá tooeither de estado de atualização de firmware **applyFailed** ou **applyComplete**:
    
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

Passo 11: Adicionar esse Olá de identificadores de função seguinte Olá **firmwareUpdate** método direto e inicia Olá fase multi firmware processo de atualização:
    
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

Passo 12: Por fim, adicione Olá seguinte código que estabelece ligação tooyour IoT hub:
    
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
> ações de tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 