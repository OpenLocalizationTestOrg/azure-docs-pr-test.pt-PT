<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="b2677-101">Neste procedimento, irá:</span><span class="sxs-lookup"><span data-stu-id="b2677-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="b2677-102">[Preparar o executável do toorun Olá responsável pela manutenção](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="b2677-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="b2677-103">[Preparar a base de dados de conteúdo Olá e a Reciclagem para eliminação imediata de BLOBs órfãos](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="b2677-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="b2677-104">[Executar Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="b2677-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="b2677-105">[Reverter a base de dados de conteúdo de Olá e definições de reciclagem](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="b2677-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="b2677-106">tooprepare toorun Olá responsável pela manutenção</span><span class="sxs-lookup"><span data-stu-id="b2677-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="b2677-107">No servidor de front-end Web Olá, abra Olá Shell de gestão do SharePoint 2013 como administrador.</span><span class="sxs-lookup"><span data-stu-id="b2677-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="b2677-108">Navegue toohello pasta *unidade de arranque*: \Programas\Microsoft SQL remoto Blob Storage 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="b2677-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="b2677-109">Mudar o nome **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** demasiado**Web. config**.</span><span class="sxs-lookup"><span data-stu-id="b2677-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="b2677-110">Utilize `aspnet_regiis -pdf connectionStrings` ficheiro do toodecrypt Olá Web. config.</span><span class="sxs-lookup"><span data-stu-id="b2677-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="b2677-111">No ficheiro Web. config desencriptada de Olá, em Olá `connectionStrings` nós, adicionar Olá a cadeia de ligação para a instância do SQL server e Olá nome de base de dados de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b2677-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="b2677-112">Consulte o seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="b2677-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="b2677-113">Utilize `aspnet_regiis –pef connectionStrings` toore-encriptar o ficheiro Web. config de Olá.</span><span class="sxs-lookup"><span data-stu-id="b2677-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="b2677-114">Mudar o nome tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config Web. config.</span><span class="sxs-lookup"><span data-stu-id="b2677-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="b2677-115">tooprepare Olá conteúdo da base de dados e reciclagem tooimmediately eliminar BLOBs órfãos</span><span class="sxs-lookup"><span data-stu-id="b2677-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="b2677-116">No Olá do SQL Server, no SQL Server Management Studio, execute Olá seguintes consultas de atualização de base de dados conteúdo Olá destino:</span><span class="sxs-lookup"><span data-stu-id="b2677-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="b2677-117">No Olá front-end servidor web, em **Administração Central**, editar Olá **definições gerais de aplicação Web** para Olá pretendido Olá de desativação do conteúdo da base de dados tootemporarily Reciclagem.</span><span class="sxs-lookup"><span data-stu-id="b2677-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="b2677-118">Esta ação irá também vazio Olá Reciclagem qualquer relacionados para coleções de sites.</span><span class="sxs-lookup"><span data-stu-id="b2677-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="b2677-119">toodo, clique em **Administração Central** -> **gestão de aplicações** -> **aplicações Web (gerir web Apps)**  ->  **SharePoint - 80** -> **definições de aplicações gerais**.</span><span class="sxs-lookup"><span data-stu-id="b2677-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="b2677-120">Conjunto Olá **reciclar o estado de reciclagem** demasiado**OFF**.</span><span class="sxs-lookup"><span data-stu-id="b2677-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Definições gerais de aplicação Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="b2677-122">Olá toorun responsável pela manutenção</span><span class="sxs-lookup"><span data-stu-id="b2677-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="b2677-123">No servidor de front-end web Olá, na Olá Shell de gestão do SharePoint 2013, execute Olá responsável pela manutenção da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="b2677-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="b2677-124">Apenas Olá `GarbageCollection` operação é suportada para StorSimple neste momento.</span><span class="sxs-lookup"><span data-stu-id="b2677-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="b2677-125">Note também que os parâmetros de Olá emitidos para Microsoft.Data.SqlRemoteBlobs.Maintainer.exe são sensíveis a maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b2677-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="b2677-126">toorevert Olá conteúdo da base de dados e definições de reciclagem</span><span class="sxs-lookup"><span data-stu-id="b2677-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="b2677-127">No Olá do SQL Server, no SQL Server Management Studio, execute Olá seguintes consultas de atualização de base de dados conteúdo Olá destino:</span><span class="sxs-lookup"><span data-stu-id="b2677-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="b2677-128">No servidor de front-end web Olá, no **Administração Central**, editar Olá **definições gerais de aplicação Web** para Olá pretendido Olá toore ativar do conteúdo da base de dados da Reciclagem.</span><span class="sxs-lookup"><span data-stu-id="b2677-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="b2677-129">toodo, clique em **Administração Central** -> **gestão de aplicações** -> **aplicações Web (gerir web Apps)**  ->  **SharePoint - 80** -> **definições de aplicações gerais**.</span><span class="sxs-lookup"><span data-stu-id="b2677-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="b2677-130">Definir Olá reciclar o estado de reciclagem demasiado**ON**.</span><span class="sxs-lookup"><span data-stu-id="b2677-130">Set hello Recycle Bin Status too**ON**.</span></span>

