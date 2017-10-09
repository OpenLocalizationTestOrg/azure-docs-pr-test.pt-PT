## <a name="route-tables"></a><span data-ttu-id="e008c-101">Tabelas de rotas</span><span class="sxs-lookup"><span data-stu-id="e008c-101">Route tables</span></span>
<span data-ttu-id="e008c-102">Recursos de tabela de rota contém toodefine rotas utilizadas como o tráfego flui dentro da sua infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e008c-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="e008c-103">Pode utilizar definidas pelo utilizador (UDR) de rotas toosend todo o tráfego de uma determinada sub-rede tooa aplicação virtual, tais como um sistema de deteção intrusões ou uma firewall (IDS).</span><span class="sxs-lookup"><span data-stu-id="e008c-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="e008c-104">Pode associar um toosubnets da tabela de rota.</span><span class="sxs-lookup"><span data-stu-id="e008c-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="e008c-105">As tabelas de rotas contenham Olá seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="e008c-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="e008c-106">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e008c-106">Property</span></span> | <span data-ttu-id="e008c-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="e008c-107">Description</span></span> | <span data-ttu-id="e008c-108">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="e008c-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e008c-109">**rotas**</span><span class="sxs-lookup"><span data-stu-id="e008c-109">**routes**</span></span> |<span data-ttu-id="e008c-110">Coleção de utilizador rotas definidas na tabela de rota Olá</span><span class="sxs-lookup"><span data-stu-id="e008c-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="e008c-111">consulte [rotas definidas pelo utilizador](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="e008c-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="e008c-112">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="e008c-112">**subnets**</span></span> |<span data-ttu-id="e008c-113">Coleção de tabela de rotas de Olá sub-redes é demasiado aplicada</span><span class="sxs-lookup"><span data-stu-id="e008c-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="e008c-114">consulte [sub-redes](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="e008c-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="e008c-115">Rotas definidas pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="e008c-115">User defined routes</span></span>
<span data-ttu-id="e008c-116">Pode criar toospecify UDRs onde o tráfego deve ser enviado, com base no respetivo endereço de destino.</span><span class="sxs-lookup"><span data-stu-id="e008c-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="e008c-117">Pode considerar uma rota como definição de gateway predefinido do Olá com base no endereço de destino Olá de um pacote de rede.</span><span class="sxs-lookup"><span data-stu-id="e008c-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="e008c-118">UDRs contenham Olá seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="e008c-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="e008c-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e008c-119">Property</span></span> | <span data-ttu-id="e008c-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="e008c-120">Description</span></span> | <span data-ttu-id="e008c-121">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="e008c-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e008c-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="e008c-122">**addressPrefix**</span></span> |<span data-ttu-id="e008c-123">Prefixo do endereço ou o endereço IP completo para o destino de Olá</span><span class="sxs-lookup"><span data-stu-id="e008c-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="e008c-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="e008c-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="e008c-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="e008c-125">**nextHopType**</span></span> |<span data-ttu-id="e008c-126">Tipo de dispositivo Olá tráfego será enviado</span><span class="sxs-lookup"><span data-stu-id="e008c-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="e008c-127">Internet VirtualAppliance, Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="e008c-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="e008c-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="e008c-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="e008c-129">Endereço IP do próximo salto de Olá</span><span class="sxs-lookup"><span data-stu-id="e008c-129">IP address for hello next hop</span></span> |<span data-ttu-id="e008c-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="e008c-130">192.168.1.4</span></span> |

<span data-ttu-id="e008c-131">Tabela de rota de exemplo no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="e008c-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="e008c-132">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e008c-132">Additional resources</span></span>
* <span data-ttu-id="e008c-133">Obter mais informações [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e008c-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="e008c-134">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt502549.aspx) para tabelas de rota.</span><span class="sxs-lookup"><span data-stu-id="e008c-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="e008c-135">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt502539.aspx) do utilizador definida rotas (UDRs).</span><span class="sxs-lookup"><span data-stu-id="e008c-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

