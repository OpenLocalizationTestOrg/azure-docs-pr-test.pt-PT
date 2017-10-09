## <a name="traffic-manager-profile"></a><span data-ttu-id="cdac6-101">Perfil do Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="cdac6-101">Traffic Manager Profile</span></span>
<span data-ttu-id="cdac6-102">Gestor de tráfego e o recurso de ponto final de subordinados permitem tooendpoints de encaminhamento de DNS no Azure e fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdac6-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="cdac6-103">Essa distribuição de tráfego é regida pelos métodos de encaminhamento de política.</span><span class="sxs-lookup"><span data-stu-id="cdac6-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="cdac6-104">Gestor de tráfego permite também toobe de estado de funcionamento do ponto final monitorizada e de tráfego diverted adequadamente com base no estado de funcionamento de Olá de um ponto final.</span><span class="sxs-lookup"><span data-stu-id="cdac6-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="cdac6-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdac6-105">Property</span></span> | <span data-ttu-id="cdac6-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdac6-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdac6-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="cdac6-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="cdac6-108">os valores possíveis são *desempenho*, *Weighted*, e *prioridade*</span><span class="sxs-lookup"><span data-stu-id="cdac6-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="cdac6-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="cdac6-109">**dnsConfig**</span></span> |<span data-ttu-id="cdac6-110">FQDN para o perfil de Olá</span><span class="sxs-lookup"><span data-stu-id="cdac6-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="cdac6-111">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="cdac6-111">**Protocol**</span></span> |<span data-ttu-id="cdac6-112">protocolo de monitorização, os valores possíveis são *HTTP* e *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="cdac6-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="cdac6-113">**Porta**</span><span class="sxs-lookup"><span data-stu-id="cdac6-113">**Port**</span></span> |<span data-ttu-id="cdac6-114">monitorização de porta</span><span class="sxs-lookup"><span data-stu-id="cdac6-114">monitoring port</span></span> |
| <span data-ttu-id="cdac6-115">**Caminho**</span><span class="sxs-lookup"><span data-stu-id="cdac6-115">**Path**</span></span> |<span data-ttu-id="cdac6-116">caminho de monitorização</span><span class="sxs-lookup"><span data-stu-id="cdac6-116">monitoring path</span></span> |
| <span data-ttu-id="cdac6-117">**Pontos finais**</span><span class="sxs-lookup"><span data-stu-id="cdac6-117">**Endpoints**</span></span> |<span data-ttu-id="cdac6-118">contentor de recursos de ponto final</span><span class="sxs-lookup"><span data-stu-id="cdac6-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="cdac6-119">Ponto Final</span><span class="sxs-lookup"><span data-stu-id="cdac6-119">Endpoint</span></span>
<span data-ttu-id="cdac6-120">Um ponto final é um recurso de subordinados de um perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="cdac6-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="cdac6-121">Representa um serviço ou web endpoint toowhich utilizador o tráfego é distribuído com base na política de Olá configurado no Olá recursos de perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="cdac6-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="cdac6-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdac6-122">Property</span></span> | <span data-ttu-id="cdac6-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdac6-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdac6-124">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="cdac6-124">**Type**</span></span> |<span data-ttu-id="cdac6-125">Olá, tipo de ponto final de Olá, os valores possíveis são *ponto final do Azure*, *ponto final externo*, e *aninhada ponto final*</span><span class="sxs-lookup"><span data-stu-id="cdac6-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="cdac6-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="cdac6-126">**targetResourceId**</span></span> |<span data-ttu-id="cdac6-127">endereço IP público de um ponto final de serviço ou web.</span><span class="sxs-lookup"><span data-stu-id="cdac6-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="cdac6-128">Isto pode ser um ponto final do Azure ou externo.</span><span class="sxs-lookup"><span data-stu-id="cdac6-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="cdac6-129">**Peso**</span><span class="sxs-lookup"><span data-stu-id="cdac6-129">**Weight**</span></span> |<span data-ttu-id="cdac6-130">peso de ponto final utilizado na gestão de tráfego.</span><span class="sxs-lookup"><span data-stu-id="cdac6-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="cdac6-131">**Prioridade**</span><span class="sxs-lookup"><span data-stu-id="cdac6-131">**Priority**</span></span> |<span data-ttu-id="cdac6-132">prioridade de ponto final de Olá, toodefine utilizado uma ação de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="cdac6-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="cdac6-133">Exemplo de Gestor de tráfego no formato Json:</span><span class="sxs-lookup"><span data-stu-id="cdac6-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="cdac6-134">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cdac6-134">Additional resources</span></span>
<span data-ttu-id="cdac6-135">Leitura [documentação da REST API para o Gestor de tráfego](https://msdn.microsoft.com/library/azure/mt163664.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="cdac6-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

