## <a name="nic"></a><span data-ttu-id="4e06d-101">NIC</span><span class="sxs-lookup"><span data-stu-id="4e06d-101">NIC</span></span>
<span data-ttu-id="4e06d-102">Um recurso de cartão (NIC) de interface de rede fornece uma sub-rede existente do tooan de conectividade de rede num recurso VNet.</span><span class="sxs-lookup"><span data-stu-id="4e06d-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="4e06d-103">Embora possa criar uma NIC como um objeto de autónomo, tem de tooassociate-tooanother objeto tooactually fornecer conectividade.</span><span class="sxs-lookup"><span data-stu-id="4e06d-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="4e06d-104">Uma NIC pode ser utilizado tooconnect uma sub-rede de tooa VM, um endereço IP público ou um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="4e06d-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="4e06d-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="4e06d-105">Property</span></span> | <span data-ttu-id="4e06d-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="4e06d-106">Description</span></span> | <span data-ttu-id="4e06d-107">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="4e06d-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e06d-108">**máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="4e06d-108">**virtualMachine**</span></span> |<span data-ttu-id="4e06d-109">Olá VM NIC está associado.</span><span class="sxs-lookup"><span data-stu-id="4e06d-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="4e06d-110">/subscriptions/{GUID}/../microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="4e06d-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="4e06d-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="4e06d-111">**macAddress**</span></span> |<span data-ttu-id="4e06d-112">Endereço MAC para Olá NIC</span><span class="sxs-lookup"><span data-stu-id="4e06d-112">MAC address for hello NIC</span></span> |<span data-ttu-id="4e06d-113">qualquer valor entre 4 e 30</span><span class="sxs-lookup"><span data-stu-id="4e06d-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="4e06d-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="4e06d-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="4e06d-115">NSG associado toohello NIC</span><span class="sxs-lookup"><span data-stu-id="4e06d-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="4e06d-116">/subscriptions/{GUID}/../microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="4e06d-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="4e06d-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="4e06d-117">**dnsSettings**</span></span> |<span data-ttu-id="4e06d-118">Definições de DNS para Olá NIC</span><span class="sxs-lookup"><span data-stu-id="4e06d-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="4e06d-119">consulte [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="4e06d-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="4e06d-120">Uma placa de Interface de rede ou NIC, representa uma interface de rede que pode ser associado tooa máquina de virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="4e06d-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="4e06d-121">Uma VM pode ter um ou vários NICs.</span><span class="sxs-lookup"><span data-stu-id="4e06d-121">A VM can have one or more NICs.</span></span>

![NIC numa única VM](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="4e06d-123">Configurações de IP</span><span class="sxs-lookup"><span data-stu-id="4e06d-123">IP configurations</span></span>
<span data-ttu-id="4e06d-124">Os NICs que têm um objeto subordinado com o nome **ipConfigurations** contendo Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="4e06d-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="4e06d-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="4e06d-125">Property</span></span> | <span data-ttu-id="4e06d-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="4e06d-126">Description</span></span> | <span data-ttu-id="4e06d-127">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="4e06d-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e06d-128">**sub-rede**</span><span class="sxs-lookup"><span data-stu-id="4e06d-128">**subnet**</span></span> |<span data-ttu-id="4e06d-129">Olá sub-rede NIC é onnected para.</span><span class="sxs-lookup"><span data-stu-id="4e06d-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="4e06d-130">/subscriptions/{GUID}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="4e06d-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="4e06d-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="4e06d-131">**privateIPAddress**</span></span> |<span data-ttu-id="4e06d-132">Endereço IP para Olá NIC na sub-rede Olá</span><span class="sxs-lookup"><span data-stu-id="4e06d-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="4e06d-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="4e06d-133">10.0.0.8</span></span> |
| <span data-ttu-id="4e06d-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="4e06d-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="4e06d-135">Método de alocação de IP</span><span class="sxs-lookup"><span data-stu-id="4e06d-135">IP allocation method</span></span> |<span data-ttu-id="4e06d-136">Dinâmicas ou estáticas</span><span class="sxs-lookup"><span data-stu-id="4e06d-136">Dynamic or Static</span></span> |
| <span data-ttu-id="4e06d-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="4e06d-137">**enableIPForwarding**</span></span> |<span data-ttu-id="4e06d-138">Se Olá NIC pode ser utilizado para o encaminhamento</span><span class="sxs-lookup"><span data-stu-id="4e06d-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="4e06d-139">VERDADEIRO ou FALSO</span><span class="sxs-lookup"><span data-stu-id="4e06d-139">true or false</span></span> |
| <span data-ttu-id="4e06d-140">**primário**</span><span class="sxs-lookup"><span data-stu-id="4e06d-140">**primary**</span></span> |<span data-ttu-id="4e06d-141">Se está Olá NIC Olá NIC primário para Olá VM</span><span class="sxs-lookup"><span data-stu-id="4e06d-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="4e06d-142">VERDADEIRO ou FALSO</span><span class="sxs-lookup"><span data-stu-id="4e06d-142">true or false</span></span> |
| <span data-ttu-id="4e06d-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="4e06d-143">**publicIPAddress**</span></span> |<span data-ttu-id="4e06d-144">PIP associado Olá NIC</span><span class="sxs-lookup"><span data-stu-id="4e06d-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="4e06d-145">consulte [as definições de DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="4e06d-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="4e06d-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="4e06d-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="4e06d-147">Fazer uma cópia Olá de conjuntos de endereços de fim que NIC está associado</span><span class="sxs-lookup"><span data-stu-id="4e06d-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="4e06d-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="4e06d-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="4e06d-149">Entrada NIC está associado a dos Olá de regras NAT para Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="4e06d-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="4e06d-150">Exemplo público endereço IP no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="4e06d-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="4e06d-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4e06d-151">Additional resources</span></span>
* <span data-ttu-id="4e06d-152">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163579.aspx) para NICs.</span><span class="sxs-lookup"><span data-stu-id="4e06d-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

