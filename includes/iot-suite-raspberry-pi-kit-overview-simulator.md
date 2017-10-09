## <a name="overview"></a><span data-ttu-id="9a828-101">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="9a828-101">Overview</span></span>

<span data-ttu-id="9a828-102">Neste tutorial, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9a828-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="9a828-103">Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a828-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="9a828-104">Este passo automaticamente implementa e configura vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a828-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="9a828-105">Configure a sua toocommunicate de dispositivo com o seu computador e a solução de monitorização remota Olá.</span><span class="sxs-lookup"><span data-stu-id="9a828-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="9a828-106">Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar a telemetria simulada que pode ver no dashboard da solução Olá.</span><span class="sxs-lookup"><span data-stu-id="9a828-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a828-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9a828-107">Prerequisites</span></span>

<span data-ttu-id="9a828-108">toocomplete neste tutorial, necessita de uma subscrição do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a828-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9a828-109">Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9a828-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9a828-110">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="9a828-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="9a828-111">Software necessário</span><span class="sxs-lookup"><span data-stu-id="9a828-111">Required software</span></span>

<span data-ttu-id="9a828-112">Precisa de cliente SSH no seu tooenable de ambiente de trabalho de máquina tooremotely acesso Olá comando linha no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9a828-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="9a828-113">Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="9a828-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="9a828-114">Recomendamos que utilize [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="9a828-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="9a828-115">A maioria das distribuições de Linux e Mac OS incluem SSH utilitário de linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="9a828-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="9a828-116">Para obter mais informações, consulte [SSH utilizando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="9a828-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="9a828-117">Hardware necessário</span><span class="sxs-lookup"><span data-stu-id="9a828-117">Required hardware</span></span>

<span data-ttu-id="9a828-118">Um computador de secretária tooenable tooconnect remotamente comandos toohello linha no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9a828-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="9a828-119">[Microsoft IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] ou componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="9a828-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="9a828-120">Este tutorial utiliza Olá seguintes itens do kit de Olá:</span><span class="sxs-lookup"><span data-stu-id="9a828-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="9a828-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="9a828-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="9a828-122">Cartão MicroSD (com NOOBS)</span><span class="sxs-lookup"><span data-stu-id="9a828-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="9a828-123">Um cabo USB Mini</span><span class="sxs-lookup"><span data-stu-id="9a828-123">A USB Mini cable</span></span>
- <span data-ttu-id="9a828-124">Um cabo de Ethernet</span><span class="sxs-lookup"><span data-stu-id="9a828-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/