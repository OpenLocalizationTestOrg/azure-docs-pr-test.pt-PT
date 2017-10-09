## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="86b87-101">Preparar o seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="86b87-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="86b87-102">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="86b87-102">Install Raspbian</span></span>

<span data-ttu-id="86b87-103">Se este for Olá pela primeira vez que está a utilizar o seu Raspberry Pi, terá de sistema operativo tooinstall Olá Raspbian utilizando NOOBS no cartão SD de Olá incluído no kit de Olá.</span><span class="sxs-lookup"><span data-stu-id="86b87-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="86b87-104">Olá [Raspberry Pi Software guia] [ lnk-install-raspbian] descreve como tooinstall um sistema operativo no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86b87-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="86b87-105">Este tutorial parte do princípio de que instalou Olá Raspbian sistema no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86b87-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="86b87-106">cartão Olá SD incluído no Olá [Microsoft Azure IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] já NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="86b87-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="86b87-107">Pode efetuar o arranque Olá Raspberry Pi deste Card e escolha tooinstall Olá Raspbian SO.</span><span class="sxs-lookup"><span data-stu-id="86b87-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

<span data-ttu-id="86b87-108">configuração de hardware do toocomplete Olá, tem de:</span><span class="sxs-lookup"><span data-stu-id="86b87-108">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="86b87-109">Ligar o seu Raspberry Pi toohello fonte de alimentação incluído no kit de Olá.</span><span class="sxs-lookup"><span data-stu-id="86b87-109">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="86b87-110">Ligar à rede de tooyour de Raspberry Pi cabo Olá Ethernet incluídos no seu kit.</span><span class="sxs-lookup"><span data-stu-id="86b87-110">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="86b87-111">Em alternativa, pode configurar [sem fios conectividade] [ lnk-pi-wireless] para sua Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86b87-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="86b87-112">Agora concluiu a configuração de hardware Olá do seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86b87-112">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="86b87-113">A iniciar sessão e aceder ao terminal Olá</span><span class="sxs-lookup"><span data-stu-id="86b87-113">Sign in and access hello terminal</span></span>

<span data-ttu-id="86b87-114">Tem duas opções tooaccess num ambiente de terminal no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="86b87-114">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="86b87-115">Se tiver um teclado e monitorizar tooyour ligado Raspberry Pi, pode utilizar Olá Raspbian GUI tooaccess uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="86b87-115">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="86b87-116">Linha de comandos de Olá de acesso na sua Raspberry Pi utilizando SSH a partir do seu computador de secretária.</span><span class="sxs-lookup"><span data-stu-id="86b87-116">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="86b87-117">Utilizar uma janela de terminal no Olá GUI</span><span class="sxs-lookup"><span data-stu-id="86b87-117">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="86b87-118">credenciais predefinidas Olá Raspbian são username **pi** e palavra-passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="86b87-118">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="86b87-119">Na barra de tarefas de Olá no Olá GUI, pode iniciar Olá **Terminal** utilitário com ícone de Olá que se assemelha um monitor.</span><span class="sxs-lookup"><span data-stu-id="86b87-119">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="86b87-120">Inicie sessão com SSH</span><span class="sxs-lookup"><span data-stu-id="86b87-120">Sign in with SSH</span></span>

<span data-ttu-id="86b87-121">Pode utilizar o SSH para acesso da linha de comandos tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86b87-121">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="86b87-122">artigo de Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH no seu Raspberry Pi e como tooconnect de [Windows] [ lnk-ssh-windows] ou [SO Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="86b87-122">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="86b87-123">Inicie sessão com o nome de utilizador **pi** e palavra-passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="86b87-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="86b87-124">Opcional: Partilhar uma pasta no seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="86b87-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="86b87-125">Opcionalmente, poderá ser útil tooshare uma pasta no seu Raspberry Pi com o seu ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="86b87-125">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="86b87-126">Uma pasta de partilha permite toouse seu editor de texto preferido de ambiente de trabalho (tais como [Visual Studio Code](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit ficheiros no seu Raspberry Pi em vez de utilizar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="86b87-126">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="86b87-127">tooshare uma pasta com o Windows, configurar um servidor de Samba em Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86b87-127">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="86b87-128">Em alternativa, utilize incorporado Olá [SFTP](https://www.raspberrypi.org/documentation/remote-access/) servidor com um cliente SFTP no ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="86b87-128">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/