#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="3c59f-101">toocreate pontos finais públicos no dispositivo de Olá de nuvem</span><span class="sxs-lookup"><span data-stu-id="3c59f-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="3c59f-102">Inicie sessão no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c59f-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="3c59f-103">Aceda demasiado**máquinas virtuais**e, em seguida, selecione e clique em máquina virtual Olá que está a ser utilizada como a aplicação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3c59f-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="3c59f-104">É necessário toocreate rede segurança grupo (NSG) regra toocontrol Olá fluxo de tráfego de e para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3c59f-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="3c59f-105">Efetue Olá os seguintes passos toocreate uma regra NSG.</span><span class="sxs-lookup"><span data-stu-id="3c59f-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="3c59f-106">Selecione **Grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="3c59f-107">Clique em Olá rede grupo de segurança predefinido que é apresentado.</span><span class="sxs-lookup"><span data-stu-id="3c59f-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="3c59f-108">Selecione **Regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="3c59f-109">Clique em **+ adicionar** toocreate uma regra de segurança de entrada.</span><span class="sxs-lookup"><span data-stu-id="3c59f-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="3c59f-110">No painel de regra de segurança de entrada de adicionar Olá:</span><span class="sxs-lookup"><span data-stu-id="3c59f-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="3c59f-111">Para Olá **nome**, seguinte do tipo Olá nome para o ponto final de Olá: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="3c59f-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="3c59f-112">Para Olá **prioridade**, selecione um número menor de 1000 (que é a prioridade de Olá para a regra predefinida de Olá).</span><span class="sxs-lookup"><span data-stu-id="3c59f-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="3c59f-113">Valor mais alto de Olá, prioridade Olá inferior.</span><span class="sxs-lookup"><span data-stu-id="3c59f-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="3c59f-114">Conjunto Olá **origem** demasiado**qualquer**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="3c59f-115">Para Olá **serviço**, selecione **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="3c59f-116">Olá **protocolo** é automaticamente definido demasiado**TCP** e Olá **intervalo de porta** estiver definido demasiado**5986**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="3c59f-117">Clique em **OK** regra de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c59f-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="3c59f-118">O passo final é tooassociate grupo de segurança de rede com uma sub-rede ou de uma interface de rede específicas.</span><span class="sxs-lookup"><span data-stu-id="3c59f-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="3c59f-119">Efetue Olá tooassociate passos a seguir o grupo de segurança de rede com uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="3c59f-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="3c59f-120">Aceda demasiado**sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="3c59f-121">Clique em **+ Associar**.</span><span class="sxs-lookup"><span data-stu-id="3c59f-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="3c59f-122">Selecione a rede virtual e, em seguida, selecione a sub-rede adequada Olá.</span><span class="sxs-lookup"><span data-stu-id="3c59f-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="3c59f-123">Clique em **OK** regra de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c59f-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="3c59f-124">Depois de criar a regra de Olá, pode ver o respetivo endereço de IP Virtual público (VIP) do detalhes toodetermine Olá.</span><span class="sxs-lookup"><span data-stu-id="3c59f-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="3c59f-125">Registe esse endereço.</span><span class="sxs-lookup"><span data-stu-id="3c59f-125">Record this address.</span></span>


