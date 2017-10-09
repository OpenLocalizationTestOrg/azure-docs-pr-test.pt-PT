> [!div class="op_single_selector"]
> * [C em Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C em Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

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

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/