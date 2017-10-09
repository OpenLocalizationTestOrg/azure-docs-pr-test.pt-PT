## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="b18c4-101">Preparar o seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b18c4-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="b18c4-102">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="b18c4-102">Install Raspbian</span></span>

<span data-ttu-id="b18c4-103">Se este for Olá pela primeira vez que está a utilizar o seu Raspberry Pi, terá de sistema operativo tooinstall Olá Raspbian utilizando NOOBS no cartão SD de Olá incluído no kit de Olá.</span><span class="sxs-lookup"><span data-stu-id="b18c4-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="b18c4-104">Olá [Raspberry Pi Software guia] [ lnk-install-raspbian] descreve como tooinstall um sistema operativo no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="b18c4-105">Este tutorial parte do princípio de que instalou Olá Raspbian sistema no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="b18c4-106">cartão Olá SD incluído no Olá [Microsoft Azure IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] já NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="b18c4-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="b18c4-107">Pode efetuar o arranque Olá Raspberry Pi deste Card e escolha tooinstall Olá Raspbian SO.</span><span class="sxs-lookup"><span data-stu-id="b18c4-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="b18c4-108">Configurar o hardware de Olá</span><span class="sxs-lookup"><span data-stu-id="b18c4-108">Set up hello hardware</span></span>

<span data-ttu-id="b18c4-109">Este tutorial utiliza o sensor Olá BME280 incluído no Olá [Microsoft Azure IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] toogenerate dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="b18c4-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="b18c4-110">Utiliza um tooindicate LED quando Olá Raspberry Pi processa um método de invocação a partir do dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="b18c4-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="b18c4-111">componentes de Olá no quadro de bread Olá são:</span><span class="sxs-lookup"><span data-stu-id="b18c4-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="b18c4-112">LED vermelho</span><span class="sxs-lookup"><span data-stu-id="b18c4-112">Red LED</span></span>
- <span data-ttu-id="b18c4-113">220 Ohm resistor (vermelho, vermelho, castanha)</span><span class="sxs-lookup"><span data-stu-id="b18c4-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="b18c4-114">Sensor de BME280</span><span class="sxs-lookup"><span data-stu-id="b18c4-114">BME280 sensor</span></span>

<span data-ttu-id="b18c4-115">Olá diagrama que se segue mostra como tooconnect seu hardware:</span><span class="sxs-lookup"><span data-stu-id="b18c4-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Configuração de hardware para Raspberry Pi][img-connection-diagram]

<span data-ttu-id="b18c4-117">Olá tabela seguinte resume as ligações de Olá de Olá Raspberry Pi toohello componentes breadboard Olá:</span><span class="sxs-lookup"><span data-stu-id="b18c4-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="b18c4-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b18c4-118">Raspberry Pi</span></span>            | <span data-ttu-id="b18c4-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="b18c4-119">Breadboard</span></span>             |<span data-ttu-id="b18c4-120">Cor</span><span class="sxs-lookup"><span data-stu-id="b18c4-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="b18c4-121">GND (Pin 14)</span><span class="sxs-lookup"><span data-stu-id="b18c4-121">GND (Pin 14)</span></span>            | <span data-ttu-id="b18c4-122">Pin de - Provider LED (18A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="b18c4-123">Roxo</span><span class="sxs-lookup"><span data-stu-id="b18c4-123">Purple</span></span>          |
| <span data-ttu-id="b18c4-124">GPCLK0 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="b18c4-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="b18c4-125">Resistor (25A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-125">Resistor (25A)</span></span>         | <span data-ttu-id="b18c4-126">Orange</span><span class="sxs-lookup"><span data-stu-id="b18c4-126">Orange</span></span>          |
| <span data-ttu-id="b18c4-127">SPI_CE0 (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="b18c4-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="b18c4-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-128">CS (39A)</span></span>               | <span data-ttu-id="b18c4-129">Azul</span><span class="sxs-lookup"><span data-stu-id="b18c4-129">Blue</span></span>          |
| <span data-ttu-id="b18c4-130">SPI_SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="b18c4-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="b18c4-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-131">SCK (36A)</span></span>              | <span data-ttu-id="b18c4-132">Amarelo</span><span class="sxs-lookup"><span data-stu-id="b18c4-132">Yellow</span></span>        |
| <span data-ttu-id="b18c4-133">SPI_MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="b18c4-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="b18c4-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-134">SDO (37A)</span></span>              | <span data-ttu-id="b18c4-135">Branco</span><span class="sxs-lookup"><span data-stu-id="b18c4-135">White</span></span>         |
| <span data-ttu-id="b18c4-136">SPI_MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="b18c4-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="b18c4-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-137">SDI (38A)</span></span>              | <span data-ttu-id="b18c4-138">Verde</span><span class="sxs-lookup"><span data-stu-id="b18c4-138">Green</span></span>         |
| <span data-ttu-id="b18c4-139">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="b18c4-139">GND (Pin 6)</span></span>             | <span data-ttu-id="b18c4-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-140">GND (35A)</span></span>              | <span data-ttu-id="b18c4-141">Preto</span><span class="sxs-lookup"><span data-stu-id="b18c4-141">Black</span></span>         |
| <span data-ttu-id="b18c4-142">3.3 V (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="b18c4-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="b18c4-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="b18c4-143">3Vo (34A)</span></span>              | <span data-ttu-id="b18c4-144">Vermelho</span><span class="sxs-lookup"><span data-stu-id="b18c4-144">Red</span></span>           |

<span data-ttu-id="b18c4-145">configuração de hardware do toocomplete Olá, tem de:</span><span class="sxs-lookup"><span data-stu-id="b18c4-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="b18c4-146">Ligar o seu Raspberry Pi toohello fonte de alimentação incluído no kit de Olá.</span><span class="sxs-lookup"><span data-stu-id="b18c4-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="b18c4-147">Ligar à rede de tooyour de Raspberry Pi cabo Olá Ethernet incluídos no seu kit.</span><span class="sxs-lookup"><span data-stu-id="b18c4-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="b18c4-148">Em alternativa, pode configurar [sem fios conectividade] [ lnk-pi-wireless] para sua Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="b18c4-149">Agora concluiu a configuração de hardware Olá do seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="b18c4-150">A iniciar sessão e aceder ao terminal Olá</span><span class="sxs-lookup"><span data-stu-id="b18c4-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="b18c4-151">Tem duas opções tooaccess num ambiente de terminal no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="b18c4-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="b18c4-152">Se tiver um teclado e monitorizar tooyour ligado Raspberry Pi, pode utilizar Olá Raspbian GUI tooaccess uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="b18c4-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="b18c4-153">Linha de comandos de Olá de acesso na sua Raspberry Pi utilizando SSH a partir do seu computador de secretária.</span><span class="sxs-lookup"><span data-stu-id="b18c4-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="b18c4-154">Utilizar uma janela de terminal no Olá GUI</span><span class="sxs-lookup"><span data-stu-id="b18c4-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="b18c4-155">credenciais predefinidas Olá Raspbian são username **pi** e palavra-passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="b18c4-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="b18c4-156">Na barra de tarefas de Olá no Olá GUI, pode iniciar Olá **Terminal** utilitário com ícone de Olá que se assemelha um monitor.</span><span class="sxs-lookup"><span data-stu-id="b18c4-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="b18c4-157">Inicie sessão com SSH</span><span class="sxs-lookup"><span data-stu-id="b18c4-157">Sign in with SSH</span></span>

<span data-ttu-id="b18c4-158">Pode utilizar o SSH para acesso da linha de comandos tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="b18c4-159">artigo de Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH no seu Raspberry Pi e como tooconnect de [Windows] [ lnk-ssh-windows] ou [SO Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="b18c4-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="b18c4-160">Inicie sessão com o nome de utilizador **pi** e palavra-passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="b18c4-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="b18c4-161">Opcional: Partilhar uma pasta no seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b18c4-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="b18c4-162">Opcionalmente, poderá ser útil tooshare uma pasta no seu Raspberry Pi com o seu ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b18c4-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="b18c4-163">Uma pasta de partilha permite toouse seu editor de texto preferido de ambiente de trabalho (tais como [Visual Studio Code](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit ficheiros no seu Raspberry Pi em vez de utilizar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="b18c4-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="b18c4-164">tooshare uma pasta com o Windows, configurar um servidor de Samba em Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="b18c4-165">Em alternativa, utilize incorporado Olá [SFTP](https://www.raspberrypi.org/documentation/remote-access/) servidor com um cliente SFTP no ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b18c4-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="b18c4-166">Ativar SPI</span><span class="sxs-lookup"><span data-stu-id="b18c4-166">Enable SPI</span></span>

<span data-ttu-id="b18c4-167">Antes de poder executar a aplicação de exemplo de Olá, tem de ativar o barramento de série periféricos Interface (SPI) Olá Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="b18c4-168">Olá Raspberry Pi comunica com dispositivos de sensor Olá BME280 através de Olá SPI bus.</span><span class="sxs-lookup"><span data-stu-id="b18c4-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="b18c4-169">Utilize Olá seguinte ficheiro de configuração do comando tooedit Olá:</span><span class="sxs-lookup"><span data-stu-id="b18c4-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="b18c4-170">Localize a linha de Olá:</span><span class="sxs-lookup"><span data-stu-id="b18c4-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="b18c4-171">linha de Olá toouncomment, eliminar Olá `#` início Olá.</span><span class="sxs-lookup"><span data-stu-id="b18c4-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="b18c4-172">Guardar as alterações (**Ctrl-O**, **Enter**) e saída Olá editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="b18c4-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="b18c4-173">tooenable SPI, reiniciar Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b18c4-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="b18c4-174">Reiniciando desliga terminal Olá, tem de toosign no novamente quando Olá Raspberry Pi reinicia:</span><span class="sxs-lookup"><span data-stu-id="b18c4-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/