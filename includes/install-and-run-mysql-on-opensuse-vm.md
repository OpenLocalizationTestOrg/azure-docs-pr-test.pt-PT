
1. <span data-ttu-id="76283-101">privilégios tooescalate, tipo:</span><span class="sxs-lookup"><span data-stu-id="76283-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="76283-102">Introduza a sua palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="76283-102">Enter your password.</span></span>
2. <span data-ttu-id="76283-103">tooinstall edição de servidor de Comunidade do MySQL, escreva:</span><span class="sxs-lookup"><span data-stu-id="76283-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="76283-104">Aguarde enquanto o MySQL transfere e instala.</span><span class="sxs-lookup"><span data-stu-id="76283-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="76283-105">tooset MySQL toostart quando inicia o sistema de Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="76283-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="76283-106">Inicie manualmente o daemon de MySQL Olá (mysqld) com este comando:</span><span class="sxs-lookup"><span data-stu-id="76283-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="76283-107">Estado de Olá toocheck de Olá MySQL daemon, escreva:</span><span class="sxs-lookup"><span data-stu-id="76283-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="76283-108">Olá toostop MySQL daemon, escreva:</span><span class="sxs-lookup"><span data-stu-id="76283-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="76283-109">Após a instalação, a palavra-passe de raiz do Olá MySQL está vazio por predefinição.</span><span class="sxs-lookup"><span data-stu-id="76283-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="76283-110">Recomendamos que execute **mysql\_segura\_instalação**, um script que ajuda a proteger MySQL.</span><span class="sxs-lookup"><span data-stu-id="76283-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="76283-111">script de Olá solicita a sua palavra-passe de raiz de toochange Olá MySQL, remova contas de utilizador anónimo, desativar inícios de sessão remoto raiz, remover bases de dados de teste e recarregar a tabela de privilégios Olá.</span><span class="sxs-lookup"><span data-stu-id="76283-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="76283-112">Recomendamos que responder Sim tooall destas opções e altere a palavra-passe de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="76283-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="76283-113">Escreva este script de Olá toorun MySQL script de instalação:</span><span class="sxs-lookup"><span data-stu-id="76283-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="76283-114">Inicie sessão no tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="76283-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="76283-115">Introduza Olá MySQL palavra-passe raiz (o que mudou no passo anterior Olá) e irá ser apresentado numa linha de onde pode emitir toointeract de declarações do SQL Server com a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="76283-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="76283-116">toocreate um novo utilizador MySQL, executar Olá seguinte Olá **mysql >** linha:</span><span class="sxs-lookup"><span data-stu-id="76283-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="76283-117">Tenha em atenção, ponto e vírgula do Olá (;) no fim de Olá do Olá linhas são cruciais para comandos Olá a terminar.</span><span class="sxs-lookup"><span data-stu-id="76283-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="76283-118">toocreate Olá uma base de dados e conceder `mysqluser` permissões de utilizador no mesmo, Olá problema os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="76283-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="76283-119">Tenha em atenção que os nomes de utilizador de base de dados e as palavras-passe só são utilizadas pelos scripts ligar toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="76283-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="76283-120">Os nomes das contas de utilizador de base de dados não representa necessariamente contas de utilizador real no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="76283-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="76283-121">toolog na partir de outro computador, tipo:</span><span class="sxs-lookup"><span data-stu-id="76283-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="76283-122">onde `ip-address` é Olá o endereço IP do computador Olá partir do qual irá ligar tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="76283-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="76283-123">Olá tooexit utilitário de administração de base de dados MySQL, escreva:</span><span class="sxs-lookup"><span data-stu-id="76283-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="76283-124">Adicionar um ponto final</span><span class="sxs-lookup"><span data-stu-id="76283-124">Add an endpoint</span></span>
1. <span data-ttu-id="76283-125">Depois de instalado o MySQL, terá de remotamente tooconfigure tooaccess um ponto final MySQL.</span><span class="sxs-lookup"><span data-stu-id="76283-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="76283-126">Inicie sessão no toohello [portal clássico do Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="76283-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="76283-127">Clique em **máquinas virtuais**, clique no nome de Olá da nova máquina virtual e, em seguida, clique em **pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="76283-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="76283-128">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="76283-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="76283-129">Adicionar um ponto final com o nome "MySQL" com o protocolo **TCP**, e **pública** e **privada** portas definido demasiado "3306".</span><span class="sxs-lookup"><span data-stu-id="76283-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="76283-130">tooremotely ligar a máquina virtual de toohello do seu computador, o tipo:</span><span class="sxs-lookup"><span data-stu-id="76283-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="76283-131">Por exemplo, se utilizar Olá virual máquina que foi criada neste tutorial, escreva este comando:</span><span class="sxs-lookup"><span data-stu-id="76283-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
