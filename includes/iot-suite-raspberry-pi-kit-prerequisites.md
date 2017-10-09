## <a name="prerequisites"></a><span data-ttu-id="4ee31-101">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ee31-101">Prerequisites</span></span>

<span data-ttu-id="4ee31-102">toocomplete neste tutorial, necessita de uma subscrição do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ee31-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4ee31-103">Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="4ee31-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4ee31-104">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="4ee31-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="4ee31-105">Software necessário</span><span class="sxs-lookup"><span data-stu-id="4ee31-105">Required software</span></span>

<span data-ttu-id="4ee31-106">Precisa de cliente SSH no seu tooenable de ambiente de trabalho de máquina tooremotely acesso Olá comando linha no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4ee31-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="4ee31-107">Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="4ee31-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="4ee31-108">Recomendamos que utilize [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="4ee31-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="4ee31-109">A maioria das distribuições de Linux e Mac OS incluem SSH utilitário de linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="4ee31-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="4ee31-110">Para obter mais informações, consulte [SSH utilizando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="4ee31-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="4ee31-111">Hardware necessário</span><span class="sxs-lookup"><span data-stu-id="4ee31-111">Required hardware</span></span>

<span data-ttu-id="4ee31-112">Um computador de secretária tooenable tooconnect remotamente comandos toohello linha no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4ee31-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="4ee31-113">[Microsoft IoT Starter Kit para Raspberry Pi 3] [ lnk-starter-kits] ou componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="4ee31-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="4ee31-114">Este tutorial utiliza Olá seguintes itens do kit de Olá:</span><span class="sxs-lookup"><span data-stu-id="4ee31-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="4ee31-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="4ee31-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="4ee31-116">Cartão MicroSD (com NOOBS)</span><span class="sxs-lookup"><span data-stu-id="4ee31-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="4ee31-117">Um cabo USB Mini</span><span class="sxs-lookup"><span data-stu-id="4ee31-117">A USB Mini cable</span></span>
- <span data-ttu-id="4ee31-118">Um cabo de Ethernet</span><span class="sxs-lookup"><span data-stu-id="4ee31-118">An Ethernet cable</span></span>
- <span data-ttu-id="4ee31-119">Sensor de BME280</span><span class="sxs-lookup"><span data-stu-id="4ee31-119">BME280 sensor</span></span>
- <span data-ttu-id="4ee31-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="4ee31-120">Breadboard</span></span>
- <span data-ttu-id="4ee31-121">Cablagem jumper</span><span class="sxs-lookup"><span data-stu-id="4ee31-121">Jumper wires</span></span>
- <span data-ttu-id="4ee31-122">Resistors</span><span class="sxs-lookup"><span data-stu-id="4ee31-122">Resistors</span></span>
- <span data-ttu-id="4ee31-123">LEDs</span><span class="sxs-lookup"><span data-stu-id="4ee31-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/