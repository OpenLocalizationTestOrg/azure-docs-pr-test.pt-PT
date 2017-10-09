## <a name="public-ip-address"></a><span data-ttu-id="33f13-101">Endereço IP público</span><span class="sxs-lookup"><span data-stu-id="33f13-101">Public IP address</span></span>
<span data-ttu-id="33f13-102">Fornece um recurso de endereço IP público ou uma com acesso à endereço IP de Internet reservado ou dinâmico.</span><span class="sxs-lookup"><span data-stu-id="33f13-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="33f13-103">Apesar de poder criar um endereço IP público como um objeto de autónomo, tem de tooassociate-tooanother objeto tooactually utilizar endereço Olá.</span><span class="sxs-lookup"><span data-stu-id="33f13-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="33f13-104">Pode associar um balanceador de carga do tooa de endereço IP público, gateway de aplicação ou uma NIC tooprovide Internet aceder toothose a recursos.</span><span class="sxs-lookup"><span data-stu-id="33f13-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="33f13-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="33f13-105">Property</span></span> | <span data-ttu-id="33f13-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="33f13-106">Description</span></span> | <span data-ttu-id="33f13-107">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="33f13-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33f13-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="33f13-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="33f13-109">Define se é o endereço IP Olá *estático* ou *dinâmica*.</span><span class="sxs-lookup"><span data-stu-id="33f13-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="33f13-110">estática, dinâmica</span><span class="sxs-lookup"><span data-stu-id="33f13-110">static, dynamic</span></span> |
| <span data-ttu-id="33f13-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="33f13-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="33f13-112">Define Olá inativo tempo limite, com um valor predefinido de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="33f13-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="33f13-113">Se não for recebida nenhuma mais pacotes para uma determinada sessão dentro desta vez, Olá de sessão é terminada.</span><span class="sxs-lookup"><span data-stu-id="33f13-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="33f13-114">qualquer valor entre 4 e 30</span><span class="sxs-lookup"><span data-stu-id="33f13-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="33f13-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="33f13-115">**ipAddress**</span></span> |<span data-ttu-id="33f13-116">Endereço IP atribuído tooobject.</span><span class="sxs-lookup"><span data-stu-id="33f13-116">IP address assigned tooobject.</span></span> <span data-ttu-id="33f13-117">Esta é uma propriedade só de leitura.</span><span class="sxs-lookup"><span data-stu-id="33f13-117">This is a read-only property.</span></span> |<span data-ttu-id="33f13-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="33f13-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="33f13-119">Definições de DNS</span><span class="sxs-lookup"><span data-stu-id="33f13-119">DNS settings</span></span>
<span data-ttu-id="33f13-120">Endereços IP públicos têm um objeto subordinado com o nome **dnsSettings** contendo Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="33f13-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="33f13-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="33f13-121">Property</span></span> | <span data-ttu-id="33f13-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="33f13-122">Description</span></span> | <span data-ttu-id="33f13-123">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="33f13-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33f13-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="33f13-124">**domainNameLabel**</span></span> |<span data-ttu-id="33f13-125">Com o nome do anfitrião utilizado para a resolução do nome.</span><span class="sxs-lookup"><span data-stu-id="33f13-125">Host named used for name resolution.</span></span> |<span data-ttu-id="33f13-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="33f13-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="33f13-127">**FQDN**</span><span class="sxs-lookup"><span data-stu-id="33f13-127">**fqdn**</span></span> |<span data-ttu-id="33f13-128">Nome completamente qualificado para o IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="33f13-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="33f13-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="33f13-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="33f13-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="33f13-130">**reverseFqdn**</span></span> |<span data-ttu-id="33f13-131">Nome de domínio completamente qualificado que resolve toohello endereço IP e está registado no DNS como um registo PTR.</span><span class="sxs-lookup"><span data-stu-id="33f13-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="33f13-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="33f13-132">www.contoso.com.</span></span> |

<span data-ttu-id="33f13-133">Exemplo público endereço IP no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="33f13-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="33f13-134">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="33f13-134">Additional resources</span></span>
* <span data-ttu-id="33f13-135">Obter mais informações [endereços IP públicos](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="33f13-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="33f13-136">Saiba mais sobre [instância nível endereços IP públicos](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="33f13-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="33f13-137">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163638.aspx) para o IP público endereços.</span><span class="sxs-lookup"><span data-stu-id="33f13-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

