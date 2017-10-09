<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="db73b-101">tooconnect através da consola de série de Olá</span><span class="sxs-lookup"><span data-stu-id="db73b-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="db73b-102">Ligar o seu dispositivo de toohello cabo série (diretamente ou através de um adaptador USB de série).</span><span class="sxs-lookup"><span data-stu-id="db73b-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="db73b-103">Abra Olá **painel de controlo**e, em seguida, abra Olá **Gestor de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="db73b-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="db73b-104">Identifique portas Olá COM conforme mostrado na seguinte ilustração de Olá.</span><span class="sxs-lookup"><span data-stu-id="db73b-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Ligar através da consola de série](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="db73b-106">Inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="db73b-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="db73b-107">No painel direito Olá, alterar Olá **tipo de ligação** demasiado**série**.</span><span class="sxs-lookup"><span data-stu-id="db73b-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="db73b-108">No painel direito Olá, escreva a porta COM correta do Olá.</span><span class="sxs-lookup"><span data-stu-id="db73b-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="db73b-109">Certifique-se de que os parâmetros de configuração de série de Olá estão definidos da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="db73b-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="db73b-110">Velocidade: 115.200</span><span class="sxs-lookup"><span data-stu-id="db73b-110">Speed: 115,200</span></span>
   * <span data-ttu-id="db73b-111">Bits de dados: 8</span><span class="sxs-lookup"><span data-stu-id="db73b-111">Data bits: 8</span></span>
   * <span data-ttu-id="db73b-112">Bits de paragem: 1</span><span class="sxs-lookup"><span data-stu-id="db73b-112">Stop bits: 1</span></span>
   * <span data-ttu-id="db73b-113">Paridade: Nenhuma</span><span class="sxs-lookup"><span data-stu-id="db73b-113">Parity: None</span></span>
   * <span data-ttu-id="db73b-114">Fluxo de controlo: Nenhum</span><span class="sxs-lookup"><span data-stu-id="db73b-114">Flow control: None</span></span>
     
     <span data-ttu-id="db73b-115">Estas definições são apresentadas na Olá seguinte ilustração.</span><span class="sxs-lookup"><span data-stu-id="db73b-115">These settings are shown in hello following illustration.</span></span>
     
     ![Definições do PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="db73b-117">Se Olá controlo de fluxo predefinido não funcionar, experimente defini Olá fluxo controlo tooXON/XOFF de entrada.</span><span class="sxs-lookup"><span data-stu-id="db73b-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="db73b-118">Clique em **abra** toostart uma sessão de série.</span><span class="sxs-lookup"><span data-stu-id="db73b-118">Click **Open** toostart a serial session.</span></span>

