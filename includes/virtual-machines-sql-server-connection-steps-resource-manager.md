### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="2b9af-101">Configurar uma etiqueta de DNS para endereço IP público Olá</span><span class="sxs-lookup"><span data-stu-id="2b9af-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="2b9af-102">tooconnect toohello motor de base de dados do SQL Server de Olá Internet, considere criar uma etiqueta de DNS para o seu endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="2b9af-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="2b9af-103">Pode ligar ao endereço IP, mas Olá etiqueta de DNS cria um registo que seja mais fácil tooidentify e abstracts Olá subjacente endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="2b9af-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="2b9af-104">As etiquetas de DNS não são necessárias se a instância de plano tooonly ligar toohello do SQL Server dentro Olá mesma rede Virtual ou apenas localmente.</span><span class="sxs-lookup"><span data-stu-id="2b9af-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="2b9af-105">toocreate uma etiqueta de DNS, comece por selecionar **máquinas virtuais** no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="2b9af-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="2b9af-106">Selecione o seu toobring VM do SQL Server, as respetivas propriedades.</span><span class="sxs-lookup"><span data-stu-id="2b9af-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="2b9af-107">Na descrição geral de máquina virtual de Olá, selecione o **endereço IP público**.</span><span class="sxs-lookup"><span data-stu-id="2b9af-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![endereço IP público.](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="2b9af-109">Nas propriedades de Olá do endereço IP público, expanda **configuração**.</span><span class="sxs-lookup"><span data-stu-id="2b9af-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="2b9af-110">Introduza um nome para a Etiqueta de DNS.</span><span class="sxs-lookup"><span data-stu-id="2b9af-110">Enter a DNS Label name.</span></span> <span data-ttu-id="2b9af-111">Este nome é um registo que podem ser utilizados tooconnect tooyour VM do SQL Server por nome em vez de por endereço IP diretamente.</span><span class="sxs-lookup"><span data-stu-id="2b9af-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="2b9af-112">Clique em Olá **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="2b9af-112">Click hello **Save** button.</span></span>

    ![etiqueta de DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="2b9af-114">Ligar toohello motor de base de dados a partir de outro computador</span><span class="sxs-lookup"><span data-stu-id="2b9af-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="2b9af-115">Num computador ligado toohello internet, abra SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2b9af-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="2b9af-116">Se não tiver o SQL Server Management Studio, poderá transferi-lo [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="2b9af-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="2b9af-117">No Olá **ligar tooServer** ou **ligar tooDatabase motor** caixa de diálogo, editar Olá **nome do servidor** valor.</span><span class="sxs-lookup"><span data-stu-id="2b9af-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="2b9af-118">Introduza o endereço IP Olá ou nome DNS completo da máquina virtual de Olá (determinado na tarefa anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="2b9af-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="2b9af-119">Também pode adicionar uma vírgula e fornecer a porta TCP do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2b9af-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="2b9af-120">Por exemplo, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="2b9af-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="2b9af-121">No Olá **autenticação** caixa, selecione **autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2b9af-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="2b9af-122">No Olá **início de sessão** caixa, nome do tipo Olá de um início de sessão SQL válido.</span><span class="sxs-lookup"><span data-stu-id="2b9af-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="2b9af-123">No Olá **palavra-passe** caixa, a palavra-passe Olá de tipo de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="2b9af-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="2b9af-124">Clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="2b9af-124">Click **Connect**.</span></span>

    ![ligação SSMS](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)