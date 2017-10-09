## <a name="scenario"></a><span data-ttu-id="2fbcd-101">Cenário</span><span class="sxs-lookup"><span data-stu-id="2fbcd-101">Scenario</span></span>
<span data-ttu-id="2fbcd-102">toobetter ilustrar como toocreate uma VNet e sub-redes, este documento irá utilizar o cenário de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="2fbcd-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![Cenário de VNet](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="2fbcd-104">Neste cenário, vai criar uma VNet com o nome **TestVNet** com um bloco CIDR reservado de **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="2fbcd-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="2fbcd-105">A VNet irá conter Olá seguintes sub-redes:</span><span class="sxs-lookup"><span data-stu-id="2fbcd-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="2fbcd-106">**Front-end**, utilizando **192.168.1.0/24** como bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="2fbcd-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="2fbcd-107">**Back-end**, utilizando **192.168.2.0/24** como bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="2fbcd-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

