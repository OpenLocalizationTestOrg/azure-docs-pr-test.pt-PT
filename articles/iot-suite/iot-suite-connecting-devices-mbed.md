---
title: aaaConnect um dispositivo utilizando C no mbed | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurada solução de monitorização remota, utilizando uma aplicação de escrita no C executadas em dispositivos mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Ligar o seu toohello de dispositivo (mbed) de solução pré-configurada de monitorização remota

## <a name="scenario-overview"></a>Descrição geral do cenário
Neste cenário, vai criar um dispositivo que envia Olá seguir monitorização remota do telemetria toohello [solução pré-configurada][lnk-what-are-preconfig-solutions]:

* Temperatura externa
* Temperatura interna
* Humidade

Para uma simplicidade código Olá no dispositivo Olá gera valores de exemplo, mas Aconselhamo-tooextend Olá exemplo por ligar sensores real tooyour dispositivo e envia a telemetria real.

Olá é dispositivo também toomethods toorespond capaz de invocado a partir do dashboard de solução Olá e valores de propriedade definidos no dashboard de solução Olá assim o desejar.

toocomplete neste tutorial, precisa de uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].

## <a name="before-you-start"></a>Antes de começar
Antes de escrever qualquer código para o seu dispositivo, terá de aprovisionar a sua solução pré-configurada de monitorização remota e aprovisionar um novo dispositivo personalizado nessa solução.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprovisionar a solução pré-configurada de monitorização remota
dispositivo de Olá criar neste tutorial envia a instância de tooan de dados do Olá [monitorização remota] [ lnk-remote-monitoring] solução pré-configurada. Se não tiver sido já aprovisionada Olá solução pré-configurada na sua conta do Azure de monitorização remota, utilize Olá os seguintes passos:

1. No Olá <https://www.azureiotsuite.com/> página, clique em  **+**  toocreate uma solução.
2. Clique em **selecione** no Olá **monitorização remota** painel toocreate sua solução.
3. No Olá **criar solução de monitorização remota** página, introduza um **nome da solução** à sua escolha, selecione Olá **região** pretende toodeploy para e selecione Olá do Azure subscrição toowant toouse. Em seguida, clique em **Criar solução**.
4. Aguarde pela conclusão do processo de aprovisionamento de Olá.

> [!WARNING]
> soluções de Olá pré-configuradas utilizam facturável serviços do Azure. Certifique-se de tooremove Olá solução pré-configurada da sua subscrição quando tiver terminado com o mesmo tooavoid quaisquer custos desnecessários. Pode remover por completo uma solução pré-configurada da sua subscrição, visitando Olá <https://www.azureiotsuite.com/> página.
> 
> 

Quando terminar, Olá processo para Olá solução de monitorização remota de aprovisionamento, clique em **iniciar** dashboard da solução Olá tooopen no seu browser.

![Dashboard de soluções][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Aprovisionar o seu dispositivo no Olá solução de monitorização remota
> [!NOTE]
> Se já tiver aprovisionado um dispositivo na sua solução, pode ignorar este passo. Precisa de credenciais de dispositivo tooknow Olá quando cria a aplicação de cliente Olá.
> 
> 

Para uma solução de toohello pré-configurada tooconnect do dispositivo, tem de identificar próprio tooIoT Hub utilizando as credenciais válidas. Pode obter credenciais de dispositivo Olá a partir do dashboard de solução Olá. Incluir as credenciais de dispositivo Olá na sua aplicação de cliente mais tarde no tutorial.

uma solução de monitorização remota do dispositivo tooyour tooadd, Olá concluir os seguintes passos no dashboard de solução Olá:

1. No Olá esquerda canto inferior do dashboard de Olá, clique em **adicionar um dispositivo**.
   
   ![Adicionar um dispositivo][1]
2. No Olá **dispositivo personalizado** painel, clique em **adicionar novo**.
   
   ![Adicionar um dispositivo personalizado][2]
3. Escolha **Definir o meu próprio ID do Dispositivo**. Introduza um ID de dispositivo como **mydevice**, clique em **verifique ID** tooverify esse nome não está já em utilização e, em seguida, clique em **criar** dispositivo de Olá tooprovision.
   
   ![Adicionar ID do dispositivo][3]
4. Se um dispositivo de Olá nota credenciais (ID de dispositivo, o nome de anfitrião do IoT Hub e a chave de dispositivo). A aplicação cliente tem toohello de tooconnect estes valores de solução de monitorização remota. Em seguida, clique em **Guardar**.
   
    ![Ver as credenciais do dispositivo][4]
5. Selecione o seu dispositivo na lista de dispositivos de Olá no dashboard de solução Olá. Em seguida, no Olá **detalhes do dispositivo** painel, clique em **ativar dispositivos**. Estado de Olá do seu dispositivo está agora **executar**. solução de monitorização remota Olá pode agora receber telemetria a partir do dispositivo e invocar métodos num dispositivo Olá.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Compilar e executar a solução de exemplo de Olá C

Olá instruções que se seguem descrevem Olá os passos para ligar um [preparados mbed K64F-FRDM Freescale] [ lnk-mbed-home] dispositivo toohello solução de monitorização remota.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Ligar a rede de tooyour Olá mbed dispositivo e a máquina de ambiente de trabalho

1. Ligar a rede tooyour Olá mbed dispositivo com um cabo de Ethernet. Este passo é necessário porque a aplicação de exemplo de Olá requer acesso à internet.

1. Consulte [introdução mbed] [ lnk-mbed-getstarted] tooconnect o mbed dispositivo tooyour ambiente de trabalho PC.

1. Se o seu PC de secretária com o Windows, consulte o artigo [PC configuração] [ lnk-mbed-pcconnect] tooyour mbed dispositivo do tooconfigure porta série acesso.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Criar um projeto de mbed e importar o código de exemplo de Olá

Siga estes passos tooadd algumas projeto de mbed de tooan de código de exemplo. Importar projeto de arranque de monitorização remota de Olá e, em seguida, altere Olá de toouse Olá projeto protocolo MQTT em vez de Olá protocolo AMQP. Atualmente, terá de toouse Olá MQTT protocolo toouse Olá funcionalidades gestão de dispositivos do IoT Hub.

1. No seu browser, aceda toohello mbed.org [site programador](https://developer.mbed.org/). Se ainda não inscrito, verá uma opção toocreate uma conta (é gratuito). Caso contrário, inicie sessão com as credenciais da conta. Em seguida, clique em **compilador** no canto direito superior da página Olá Olá. Esta ação coloca toohello *área de trabalho* interface.

1. Certifique-se a plataforma de hardware de Olá estiver a utilizar é apresentado no canto direito superior da janela de Olá hello, ou clique em ícone Olá Olá canto direito tooselect sua plataforma de hardware.

1. Clique em **importação** no menu principal Olá. Em seguida, clique em **clique aqui tooimport a partir do URL**.
   
    ![Área de trabalho de toombed de importação de início][6]

1. Na janela de pop-up Olá, introduza a ligação de Olá para Olá exemplo código https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, em seguida, clique em **importação**.
   
    ![Importar a área de trabalho de toombed de código de exemplo][7]

1. Pode ver na janela de compilador Olá mbed que também importar este projeto importa vários bibliotecas. Algumas são fornecidas e mantidas pela equipa do Azure IoT Olá ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), enquanto outros estão disponíveis no catálogo de bibliotecas de mbed Olá de bibliotecas de terceiros.
   
    ![Projeto de mbed de vista][8]

1. No Olá **área de trabalho do programa**, contexto Olá **iothub\_amqp\_transporte** biblioteca, clique em **eliminar**e, em seguida, clique em **OK** tooconfirm.

1. No Olá **área de trabalho do programa**, contexto Olá **azure\_amqp\_c** biblioteca, clique em **eliminar**e, em seguida, clique em **OK**  tooconfirm.

1. Contexto Olá **remote_monitoring** projeto no Olá **área de trabalho do programa**, selecione **importação biblioteca**, em seguida, selecione **de URL**.
   
    ![Iniciar a área de trabalho de toombed de importação de biblioteca][6]

1. Na janela de pop-up Olá, introduza a ligação de Olá para Olá MQTT transporte biblioteca https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transporte /, em seguida, clique em **importação**.
   
    ![Importar a área de trabalho biblioteca toombed][12]

1. Olá repetida passo tooadd Olá MQTT biblioteca anterior do https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. A área de trabalho aspeto agora Olá seguinte:

    ![Área de trabalho do Vista mbed][13]

1. Abra Olá remoto\_monitoring\remote_monitoring.c ficheiro e substituir Olá existente `#include` instruções com Olá seguinte código:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Eliminar Olá todos os restantes código Olá remoto\_monitoring\remote\_monitoring.c ficheiro.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilar e executar o exemplo de Olá

Adicionar Olá do código tooinvoke **remoto\_monitorização\_executar** funcionar e, em seguida, criar e executar a aplicação de dispositivo Olá.

1. Adicionar um **principal** função com o seguinte código no fim de Olá do Olá remoto\_Olá do monitoring.c ficheiro tooinvoke **remoto\_monitorização\_executar** função:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Clique em **compilar** programa de Olá toobuild. Em segurança pode ignorar quaisquer avisos, mas se a compilação de Olá gerar erros, corrija-os antes de continuar.

1. Se a compilação de Olá for bem-sucedida, o Web site de compilador do Olá mbed gera um ficheiro. bin com o nome de Olá do seu projeto e transfere-tooyour de computador local. Dispositivo de cópia Olá. bin ficheiro toohello. Guardar o dispositivo de toohello Olá. bin ficheiro faz com que Olá dispositivo toorestart e executar programa Olá contido num ficheiro. bin de Olá. Pode reiniciar manualmente o programa de Olá em qualquer altura, premindo o botão de reposição de Olá no dispositivo de mbed Olá.

1. Liga dispositivo toohello a utilizar uma aplicação de cliente SSH, como o PuTTY. Pode determinar a porta série Olá que utiliza o seu dispositivo, verificando o Gestor de dispositivos do Windows.
   
    ![][11]

1. No PuTTY, clique em Olá **série** tipo de ligação. dispositivo Olá liga-se normalmente na transmissão 9600, por isso, introduza 9600 no Olá **velocidade** caixa. Em seguida, clique em **abra**.

1. programa de Olá começa a ser executada. Poderá ter quadro de Olá tooreset (prima CTRL + Break ou no botão de reposição do painel de Olá prima) se o programa de Olá não for iniciado automaticamente quando liga.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
