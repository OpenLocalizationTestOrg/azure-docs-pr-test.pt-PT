## <a name="overview"></a>Descrição geral

Neste tutorial, conclua Olá os seguintes passos:

- Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure. Este passo automaticamente implementa e configura vários serviços do Azure.
- Configure a sua toocommunicate de dispositivo com o seu computador e a solução de monitorização remota Olá.
- Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar a telemetria simulada que pode ver no dashboard da solução Olá.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, necessita de uma subscrição do Azure Active Directory.

> [!NOTE]
> Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].

### <a name="required-software"></a>Software necessário

Precisa de cliente SSH no seu tooenable de ambiente de trabalho de máquina tooremotely acesso Olá comando linha no Olá Raspberry Pi.

- Windows não inclui um cliente SSH. Recomendamos que utilize [PuTTY](http://www.putty.org/).
- A maioria das distribuições de Linux e Mac OS incluem SSH utilitário de linha de comandos Olá. Para obter mais informações, consulte [SSH utilizando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

### <a name="required-hardware"></a>Hardware necessário

Um computador de secretária tooenable tooconnect remotamente comandos toohello linha no Olá Raspberry Pi.

[Microsoft IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] ou componentes equivalentes. Este tutorial utiliza Olá seguintes itens do kit de Olá:

- Raspberry Pi 3
- Cartão MicroSD (com NOOBS)
- Um cabo USB Mini
- Um cabo de Ethernet

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/