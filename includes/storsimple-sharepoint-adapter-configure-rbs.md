<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="fa407-101">Quando efetuar alterações toohello adaptador StorSimple para a configuração do SharePoint RBS, tem de ser sessão iniciada com uma conta de utilizador que pertence toohello grupo Admins do domínio.</span><span class="sxs-lookup"><span data-stu-id="fa407-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="fa407-102">Além disso, tem de aceder a página de configuração de Olá num browser em execução no Olá mesmo anfitrião como Administração Central.</span><span class="sxs-lookup"><span data-stu-id="fa407-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="fa407-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="fa407-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="fa407-104">Abra a página de Administração Central do SharePoint Olá e procurar demasiado**definições do sistema**.</span><span class="sxs-lookup"><span data-stu-id="fa407-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="fa407-105">No Olá **Azure StorSimple** secção, clique em **configurar adaptador do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="fa407-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configurar Olá adaptador do StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="fa407-107">No Olá **configurar adaptador do StorSimple** página:</span><span class="sxs-lookup"><span data-stu-id="fa407-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="fa407-108">Certifique-se de que Olá **ativar caminho edição** caixa de verificação está selecionada.</span><span class="sxs-lookup"><span data-stu-id="fa407-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="fa407-109">Na caixa de texto Olá, escreva o caminho de convenção de Nomenclatura Universal (UNC) Olá do arquivo de BLOB Olá.</span><span class="sxs-lookup"><span data-stu-id="fa407-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="fa407-110">volume de arquivo BLOB Olá tem de estar alojado num volume iSCSI configurado no dispositivo StorSimple de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa407-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="fa407-111">Clique em Olá **ativar** no botão abaixo cada Olá conteúdo bases de dados que pretende que tooconfigure para armazenamento remoto.</span><span class="sxs-lookup"><span data-stu-id="fa407-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="fa407-112">arquivo de BLOB Olá tem de ser partilhados e pode ser acedida por todos os servidores (WFE) front-end web e conta de utilizador de Olá que está configurada para o farm de servidores do SharePoint Olá tem de ter a partilha de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="fa407-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Ativar Olá RBS fornecedor](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="fa407-114">Quando ativar ou desativar RBS, também verá Olá seguir a mensagem.</span><span class="sxs-lookup"><span data-stu-id="fa407-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Configurar StorSimple adaptador Ativar desativar](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="fa407-116">Clique em Olá **atualização** configuração de Olá tooapply do botão.</span><span class="sxs-lookup"><span data-stu-id="fa407-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="fa407-117">Ao clicar em Olá **atualização** botão, Olá estado da configuração RBS será atualizada em todos os servidores WFE, e todo o farm Olá serão RBS-ativado.</span><span class="sxs-lookup"><span data-stu-id="fa407-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="fa407-118">Olá seguir a mensagem é apresentada.</span><span class="sxs-lookup"><span data-stu-id="fa407-118">hello following message appears.</span></span>
      
      ![Mensagem de configuração do adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="fa407-120">Se estiver a configurar RBS para um farm do SharePoint com um número muito elevado de bases de dados (superior a 200), página de web de Administração Central do SharePoint Olá poderá tempo limite. Se isso ocorrer, atualize a página Olá.</span><span class="sxs-lookup"><span data-stu-id="fa407-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="fa407-121">Isto não afeta o processo de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa407-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="fa407-122">Verifique a configuração de Olá:</span><span class="sxs-lookup"><span data-stu-id="fa407-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="fa407-123">Inicie sessão no Web site de Administração Central do SharePoint toohello e procurar toohello **configurar adaptador do StorSimple** página.</span><span class="sxs-lookup"><span data-stu-id="fa407-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="fa407-124">Verifique toomake de detalhes de configuração de Olá certificar-se de que correspondem à definições Olá que introduziu.</span><span class="sxs-lookup"><span data-stu-id="fa407-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="fa407-125">Certifique-se de que RBS funciona corretamente:</span><span class="sxs-lookup"><span data-stu-id="fa407-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="fa407-126">Carregar um tooSharePoint do documento.</span><span class="sxs-lookup"><span data-stu-id="fa407-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="fa407-127">Procure o caminho UNC toohello que configurou.</span><span class="sxs-lookup"><span data-stu-id="fa407-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="fa407-128">Certifique-se de que a estrutura de diretórios do Olá RBS foi criada e que contém o objeto de Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="fa407-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="fa407-129">(Opcional) Pode utilizar Olá Microsoft RBS `Migrate()` cmdlet do PowerShell incluído com o SharePoint toomigrate existente BLOB toohello conteúdo dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fa407-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="fa407-130">Para obter mais informações, consulte [migrar conteúdo ou a sair RBS no SharePoint 2013] [ 6] ou [migrar conteúdo ou a sair RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="fa407-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="fa407-131">(Opcional) Nas instalações de teste, pode verificar que Olá BLOBs foram movidos fora da base de dados conteúdo Olá, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="fa407-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="fa407-132">Inicie o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="fa407-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="fa407-133">Execute consulta ListBlobsInDB_2010.sql ou ListBlobsInDB_2013.sql Olá, da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="fa407-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="fa407-134">Se RBS foi configurada corretamente, deverá aparecer um valor nulo na coluna de SizeOfContentInDB Olá para qualquer objeto que foi carregada e externalized com êxito com RBS.</span><span class="sxs-lookup"><span data-stu-id="fa407-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="fa407-135">(Opcional) Depois de configurar RBS e mover todos os BLOBS conteúdo toohello dispositivo StorSimple, pode mover o dispositivo de toohello Olá conteúdo da base de dados.</span><span class="sxs-lookup"><span data-stu-id="fa407-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="fa407-136">Se escolher toomove Olá conteúdo da base de dados, recomendamos que configurar o armazenamento de base de dados de conteúdo de Olá no dispositivo Olá como um volume primário.</span><span class="sxs-lookup"><span data-stu-id="fa407-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="fa407-137">Em seguida, utilize estabelecida que do SQL Server melhores práticas de dispositivo do StorSimple toohello toomigrate Olá conteúdo da base de dados.</span><span class="sxs-lookup"><span data-stu-id="fa407-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fa407-138">Dispositivo de toohello de base de dados de conteúdo Olá mover só é suportado para a série 8000 do StorSimple de Olá (que não é suportado para a série de Olá 5000 ou 7000).</span><span class="sxs-lookup"><span data-stu-id="fa407-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="fa407-139">Se armazenar os BLOBs e base de dados de conteúdo Olá em volumes separados no dispositivo do StorSimple Olá, recomendamos que configurar no Olá mesmo contentor de volume.</span><span class="sxs-lookup"><span data-stu-id="fa407-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="fa407-140">Isto garante que estes irão ser copiados em segurança em conjunto.</span><span class="sxs-lookup"><span data-stu-id="fa407-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="fa407-141">Se não tiver ativado RBS, não recomendamos mover o dispositivo StorSimple de toohello à base de dados de conteúdo Olá.</span><span class="sxs-lookup"><span data-stu-id="fa407-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="fa407-142">Esta é uma configuração untested.</span><span class="sxs-lookup"><span data-stu-id="fa407-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="fa407-143">Aceda toohello próximo passo: [configurar recolha de lixo](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="fa407-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
