
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="57d43-101">Criar uma regra de firewall ao nível do servidor no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="57d43-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="57d43-102">No painel de servidor SQL Olá, em definições, clique em **Firewall** o painel do SQL Server de Olá do tooopen Olá Firewall.</span><span class="sxs-lookup"><span data-stu-id="57d43-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="57d43-103">Reveja o endereço IP de cliente de Olá apresentado e validar que este é o endereço IP no Olá Internet utilizando um browser da sua preferência (peça "o que é o meu endereço IP).</span><span class="sxs-lookup"><span data-stu-id="57d43-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="57d43-104">Ocasionalmente, os endereços IP não correspondem devido a vários motivos.</span><span class="sxs-lookup"><span data-stu-id="57d43-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="57d43-105">Partindo do princípio que correspondem aos endereços IP Olá, clique em **Adicionar IP do cliente** na barra de ferramentas Olá.</span><span class="sxs-lookup"><span data-stu-id="57d43-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![adicionar IP de cliente](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="57d43-107">Pode abrir um intervalo de endereços completo ou uma firewall de base de dados SQL Olá no Olá tooa único endereço IP do servidor.</span><span class="sxs-lookup"><span data-stu-id="57d43-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="57d43-108">Abrir Olá firewall permite aos administradores do SQL Server e base de dados do utilizadores toologin tooany no Olá toowhich de servidor têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="57d43-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="57d43-109">Clique em **guardar** no Olá toosave da barra de ferramentas esta regra de firewall ao nível do servidor e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="57d43-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![adicionar IP de cliente](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="57d43-111">Para obter um tutorial, veja o artigo [Tutorial da Base de Dados SQL: Criar um servidor, uma regra de firewall ao nível do servidor, uma base de dados de exemplo, uma regra de firewall ao nível da base de dados e ligar com o SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="57d43-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
