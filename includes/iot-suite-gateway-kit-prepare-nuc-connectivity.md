## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="b3765-101">Preparar o Intel NUC</span><span class="sxs-lookup"><span data-stu-id="b3765-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="b3765-102">configuração de hardware do toocomplete Olá, tem de:</span><span class="sxs-lookup"><span data-stu-id="b3765-102">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="b3765-103">Ligar o Intel NUC toohello fonte de alimentação incluído no kit de Olá.</span><span class="sxs-lookup"><span data-stu-id="b3765-103">Connect your Intel NUC toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="b3765-104">Ligar à rede de tooyour do Intel NUC com um cabo de Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b3765-104">Connect your Intel NUC tooyour network using an Ethernet cable.</span></span>

<span data-ttu-id="b3765-105">Agora concluiu a configuração de hardware de Olá do seu dispositivo de gateway Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="b3765-105">You have now completed hello hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="b3765-106">A iniciar sessão e aceder ao terminal Olá</span><span class="sxs-lookup"><span data-stu-id="b3765-106">Sign in and access hello terminal</span></span>

<span data-ttu-id="b3765-107">Tem duas opções tooaccess num ambiente de terminal no seu NUC Intel:</span><span class="sxs-lookup"><span data-stu-id="b3765-107">You have two options tooaccess a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="b3765-108">Se tiver um teclado e monitorizar tooyour ligado Intel NUC, pode aceder diretamente a shell de Olá.</span><span class="sxs-lookup"><span data-stu-id="b3765-108">If you have a keyboard and monitor connected tooyour Intel NUC, you can access hello shell directly.</span></span> <span data-ttu-id="b3765-109">as credenciais predefinidas de Olá são username **raiz** e palavra-passe **raiz**.</span><span class="sxs-lookup"><span data-stu-id="b3765-109">hello default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="b3765-110">Shell de Olá de acesso na sua NUC Intel utilizando SSH a partir do seu computador de secretária.</span><span class="sxs-lookup"><span data-stu-id="b3765-110">Access hello shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="b3765-111">Inicie sessão com SSH</span><span class="sxs-lookup"><span data-stu-id="b3765-111">Sign in with SSH</span></span>

<span data-ttu-id="b3765-112">toosign com SSH, terá de endereço IP de Olá do seu NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="b3765-112">toosign in with SSH, you need hello IP address of your Intel NUC.</span></span> <span data-ttu-id="b3765-113">Se tiver um teclado e monitorizar tooyour ligado Intel NUC, utilize Olá `ifconfig` endereço IP de Olá toofind de comandos.</span><span class="sxs-lookup"><span data-stu-id="b3765-113">If you have a keyboard and monitor connected tooyour Intel NUC, use hello `ifconfig` command toofind hello IP address.</span></span> <span data-ttu-id="b3765-114">Em alternativa, ligar tooyour router toolist Olá endereços dispositivos na sua rede.</span><span class="sxs-lookup"><span data-stu-id="b3765-114">Alternatively, connect tooyour router toolist hello addresses of devices on your network.</span></span>

<span data-ttu-id="b3765-115">Inicie sessão com o nome de utilizador **raiz** e palavra-passe **raiz**.</span><span class="sxs-lookup"><span data-stu-id="b3765-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="b3765-116">Opcional: Partilhar uma pasta no seu NUC Intel</span><span class="sxs-lookup"><span data-stu-id="b3765-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="b3765-117">Opcionalmente, poderá ser útil tooshare uma pasta no seu NUC Intel com o seu ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b3765-117">Optionally, you may want tooshare a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="b3765-118">Uma pasta de partilha permite toouse seu editor de texto preferido de ambiente de trabalho (tais como [Visual Studio Code](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit ficheiros no seu NUC Intel em vez de utilizar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="b3765-118">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="b3765-119">tooshare uma pasta com o Windows, configurar um servidor de Samba em Olá Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="b3765-119">tooshare a folder with Windows, configure a Samba server on hello Intel NUC.</span></span> <span data-ttu-id="b3765-120">Em alternativa, utilize o servidor SFTP Olá no Olá Intel NUC com um cliente SFTP no seu computador de secretária.</span><span class="sxs-lookup"><span data-stu-id="b3765-120">Alternatively, use hello SFTP server on hello Intel NUC with an SFTP client on your desktop machine.</span></span>
