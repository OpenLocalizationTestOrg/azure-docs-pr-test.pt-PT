## <a name="prepare-your-raspberry-pi"></a>Preparar o seu Raspberry Pi

### <a name="install-raspbian"></a>Instalar Raspbian

Se este for Olá pela primeira vez que está a utilizar o seu Raspberry Pi, terá de sistema operativo tooinstall Olá Raspbian utilizando NOOBS no cartão SD de Olá incluído no kit de Olá. Olá [Raspberry Pi Software guia] [ lnk-install-raspbian] descreve como tooinstall um sistema operativo no seu Raspberry Pi. Este tutorial parte do princípio de que instalou Olá Raspbian sistema no seu Raspberry Pi.

> [!NOTE]
> cartão Olá SD incluído no Olá [Microsoft Azure IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] já NOOBS instalado. Pode efetuar o arranque Olá Raspberry Pi deste Card e escolha tooinstall Olá Raspbian SO.

configuração de hardware do toocomplete Olá, tem de:

- Ligar o seu Raspberry Pi toohello fonte de alimentação incluído no kit de Olá.
- Ligar à rede de tooyour de Raspberry Pi cabo Olá Ethernet incluídos no seu kit. Em alternativa, pode configurar [sem fios conectividade] [ lnk-pi-wireless] para sua Raspberry Pi.

Agora concluiu a configuração de hardware Olá do seu Raspberry Pi.

### <a name="sign-in-and-access-hello-terminal"></a>A iniciar sessão e aceder ao terminal Olá

Tem duas opções tooaccess num ambiente de terminal no seu Raspberry Pi:

- Se tiver um teclado e monitorizar tooyour ligado Raspberry Pi, pode utilizar Olá Raspbian GUI tooaccess uma janela de terminal.

- Linha de comandos de Olá de acesso na sua Raspberry Pi utilizando SSH a partir do seu computador de secretária.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Utilizar uma janela de terminal no Olá GUI

credenciais predefinidas Olá Raspbian são username **pi** e palavra-passe **raspberry**. Na barra de tarefas de Olá no Olá GUI, pode iniciar Olá **Terminal** utilitário com ícone de Olá que se assemelha um monitor.

#### <a name="sign-in-with-ssh"></a>Inicie sessão com SSH

Pode utilizar o SSH para acesso da linha de comandos tooyour Raspberry Pi. artigo de Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH no seu Raspberry Pi e como tooconnect de [Windows] [ lnk-ssh-windows] ou [SO Linux & Mac][lnk-ssh-linux].

Inicie sessão com o nome de utilizador **pi** e palavra-passe **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Opcional: Partilhar uma pasta no seu Raspberry Pi

Opcionalmente, poderá ser útil tooshare uma pasta no seu Raspberry Pi com o seu ambiente de trabalho. Uma pasta de partilha permite toouse seu editor de texto preferido de ambiente de trabalho (tais como [Visual Studio Code](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit ficheiros no seu Raspberry Pi em vez de utilizar `nano` ou `vi`.

tooshare uma pasta com o Windows, configurar um servidor de Samba em Olá Raspberry Pi. Em alternativa, utilize incorporado Olá [SFTP](https://www.raspberrypi.org/documentation/remote-access/) servidor com um cliente SFTP no ambiente de trabalho.

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/