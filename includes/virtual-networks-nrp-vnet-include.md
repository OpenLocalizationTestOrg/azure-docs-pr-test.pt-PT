## <a name="virtual-network"></a><span data-ttu-id="c0be1-101">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="c0be1-101">Virtual Network</span></span>
<span data-ttu-id="c0be1-102">Recursos de redes (VNET) e sub-redes virtuais ajudam a definir um limite de segurança para cargas de trabalho em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be1-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="c0be1-103">Uma VNet é caracterizada por uma coleção de espaços de endereços, definida como blocos CIDR.</span><span class="sxs-lookup"><span data-stu-id="c0be1-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0be1-104">Os administradores de rede estiver familiarizados com notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="c0be1-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="c0be1-105">Se não estiver familiarizado com CIDR, [saber mais acerca do mesmo](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="c0be1-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![VNet com várias sub-redes](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="c0be1-107">As VNets conter Olá seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="c0be1-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="c0be1-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c0be1-108">Property</span></span> | <span data-ttu-id="c0be1-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="c0be1-109">Description</span></span> | <span data-ttu-id="c0be1-110">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="c0be1-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0be1-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="c0be1-111">**addressSpace**</span></span> |<span data-ttu-id="c0be1-112">Coleção de prefixos de endereços que compõem Olá VNet em notação CIDR</span><span class="sxs-lookup"><span data-stu-id="c0be1-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="c0be1-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c0be1-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="c0be1-114">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="c0be1-114">**subnets**</span></span> |<span data-ttu-id="c0be1-115">Coleção de sub-redes que compõem Olá VNet</span><span class="sxs-lookup"><span data-stu-id="c0be1-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="c0be1-116">consulte [sub-redes](#Subnets) abaixo.</span><span class="sxs-lookup"><span data-stu-id="c0be1-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="c0be1-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="c0be1-117">**ipAddress**</span></span> |<span data-ttu-id="c0be1-118">Endereço IP atribuído tooobject.</span><span class="sxs-lookup"><span data-stu-id="c0be1-118">IP address assigned tooobject.</span></span> <span data-ttu-id="c0be1-119">Esta é uma propriedade só de leitura.</span><span class="sxs-lookup"><span data-stu-id="c0be1-119">This is a read-only property.</span></span> |<span data-ttu-id="c0be1-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="c0be1-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="c0be1-121">Sub-redes</span><span class="sxs-lookup"><span data-stu-id="c0be1-121">Subnets</span></span>
<span data-ttu-id="c0be1-122">Uma sub-rede é um recurso de subordinados de uma VNet e ajuda a definir segmentos dos espaços de endereços dentro de um bloco CIDR utilizar prefixos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="c0be1-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="c0be1-123">NICs podem ser adicionados toosubnets e tooVMs ligado, fornecer conectividade de várias cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c0be1-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="c0be1-124">Sub-redes contenham Olá seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="c0be1-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="c0be1-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c0be1-125">Property</span></span> | <span data-ttu-id="c0be1-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="c0be1-126">Description</span></span> | <span data-ttu-id="c0be1-127">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="c0be1-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0be1-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="c0be1-128">**addressPrefix**</span></span> |<span data-ttu-id="c0be1-129">Prefixo de endereço único que compõem a sub-rede de Olá em notação CIDR</span><span class="sxs-lookup"><span data-stu-id="c0be1-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="c0be1-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="c0be1-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="c0be1-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="c0be1-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="c0be1-132">NSG aplicado toohello sub-rede</span><span class="sxs-lookup"><span data-stu-id="c0be1-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="c0be1-133">consulte [NSGs](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="c0be1-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="c0be1-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="c0be1-134">**routeTable**</span></span> |<span data-ttu-id="c0be1-135">Tabela de rotas aplicadas toohello sub-rede</span><span class="sxs-lookup"><span data-stu-id="c0be1-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="c0be1-136">consulte [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="c0be1-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="c0be1-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="c0be1-137">**ipConfigurations**</span></span> |<span data-ttu-id="c0be1-138">Coleção de objetos de configruation IP utilizados por NICs toohello ligado sub-rede</span><span class="sxs-lookup"><span data-stu-id="c0be1-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="c0be1-139">consulte [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="c0be1-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="c0be1-140">Exemplo VNet no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="c0be1-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="c0be1-141">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c0be1-141">Additional resources</span></span>
* <span data-ttu-id="c0be1-142">Obter mais informações [VNet](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0be1-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="c0be1-143">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163650.aspx) para VNets.</span><span class="sxs-lookup"><span data-stu-id="c0be1-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="c0be1-144">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163618.aspx) das sub-redes.</span><span class="sxs-lookup"><span data-stu-id="c0be1-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

