
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="84a0e-101">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/) em http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="84a0e-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="84a0e-102">Na faixa de Olá esquerdo, clique em **Procurar tudo**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="84a0e-103">Olá **procurar** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="84a0e-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="84a0e-104">Desloque-se e clique em **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="84a0e-105">Olá **servidores SQL** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="84a0e-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Localizar o servidor da SQL Database do Azure no portal de Olá][b21-FindServerInPortal]
4. <span data-ttu-id="84a0e-107">Para sua comodidade, clique em Olá minimizar o controlo da Olá anteriormente **procurar** painel.</span><span class="sxs-lookup"><span data-stu-id="84a0e-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="84a0e-108">Na caixa de texto de filtro de Olá, comece a escrever o nome de hello do servidor.</span><span class="sxs-lookup"><span data-stu-id="84a0e-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="84a0e-109">A linha é apresentada.</span><span class="sxs-lookup"><span data-stu-id="84a0e-109">Your row is displayed.</span></span>
6. <span data-ttu-id="84a0e-110">Clique em linha hello do servidor.</span><span class="sxs-lookup"><span data-stu-id="84a0e-110">Click hello row for your server.</span></span> <span data-ttu-id="84a0e-111">É apresentado um painel para o servidor.</span><span class="sxs-lookup"><span data-stu-id="84a0e-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="84a0e-112">No painel do servidor, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="84a0e-113">Olá **definições** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="84a0e-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="84a0e-114">Clique em **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-114">Click **Firewall**.</span></span> <span data-ttu-id="84a0e-115">Olá **as definições da Firewall** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="84a0e-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Clique em Definições > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="84a0e-117">Clique em **Adicionar cliente IP**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-117">Click **Add Client IP**.</span></span> <span data-ttu-id="84a0e-118">Escreva um nome para a nova regra na caixa de texto Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="84a0e-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="84a0e-119">Tipo de Olá baixa e alta os valores de intervalo de Olá pretende de endereços IP tooenable.</span><span class="sxs-lookup"><span data-stu-id="84a0e-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="84a0e-120">Pode ser útil toohave terminar de valor baixo Olá com **.0** e Olá elevada com **.255**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Adicionar um tooallow de intervalo de endereços IP][b41-AddRange]
11. <span data-ttu-id="84a0e-122">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="84a0e-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
