<span data-ttu-id="0ed00-101">Siga estes passos tooinstall e execute o MongoDB numa máquina virtual com o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0ed00-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ed00-102">Funcionalidades de segurança do MongoDB, como a autenticação e o enlace de endereço IP, não estão ativadas por predefinição.</span><span class="sxs-lookup"><span data-stu-id="0ed00-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="0ed00-103">Funcionalidades de segurança devem ser ativadas antes de implementar o ambiente de produção do MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="0ed00-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="0ed00-104">Para obter mais informações, consulte [segurança e autenticação](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="0ed00-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="0ed00-105">Depois de se ligar máquinas toohello utilizando o ambiente de trabalho remoto, abra o Internet Explorer de Olá **iniciar** menu na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ed00-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="0ed00-106">Selecione Olá **ferramentas** botão no canto superior direito Olá.</span><span class="sxs-lookup"><span data-stu-id="0ed00-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="0ed00-107">No **opções da Internet**, selecione Olá **segurança** separador e, em seguida, selecione Olá **Sites fidedignos** ícone e, finalmente, clique em Olá **Sites** botão.</span><span class="sxs-lookup"><span data-stu-id="0ed00-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="0ed00-108">Adicionar *https://\*. mongodb.org* toohello lista de sites fidedignos.</span><span class="sxs-lookup"><span data-stu-id="0ed00-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="0ed00-109">Aceda demasiado[transfere - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="0ed00-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="0ed00-110">Determinar Olá **atual versão estável** de **Comunidade servidor**, selecione hello mais recente **64-bit** versão na coluna de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0ed00-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="0ed00-111">Transferir e, em seguida, execute o instalador do MSI Olá.</span><span class="sxs-lookup"><span data-stu-id="0ed00-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="0ed00-112">MongoDB é normalmente instalado na c:\Programas\Microsoft Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ed00-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="0ed00-113">Procure as variáveis de ambiente no ambiente de trabalho Olá e adicione a variável de caminho de toohello binários caminho Olá MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ed00-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="0ed00-114">Por exemplo, poderá determinar os binários de Olá em c:\Programas\Microsoft Files\MongoDB\Server\3.4\bin no seu computador.</span><span class="sxs-lookup"><span data-stu-id="0ed00-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="0ed00-115">Criar os diretórios de dados e de registo do MongoDB no disco de dados de Olá (tais como unidade **f:**) que criou no Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="0ed00-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="0ed00-116">De **iniciar**, selecione **linha de comandos** tooopen uma janela de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="0ed00-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="0ed00-117">Escreva:</span><span class="sxs-lookup"><span data-stu-id="0ed00-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="0ed00-118">toorun Olá base de dados, execute:</span><span class="sxs-lookup"><span data-stu-id="0ed00-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="0ed00-119">Todas as mensagens de registo são direcionado toohello *F:\MongoLogs\mongolog.log* de ficheiros mongod.exe servidor é iniciado e preallocates ficheiros do diário.</span><span class="sxs-lookup"><span data-stu-id="0ed00-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="0ed00-120">Pode demorar alguns minutos para MongoDB toopreallocate ficheiros do diário Olá e começar a escutar ligações.</span><span class="sxs-lookup"><span data-stu-id="0ed00-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="0ed00-121">linha de comandos Olá permanece direcionada para esta tarefa enquanto a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="0ed00-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="0ed00-122">Olá toostart shell administrativa do MongoDB, abrir outra janela de comando de **iniciar** e Olá tipo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0ed00-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="0ed00-123">base de dados de Olá é criado pelo Olá insert.</span><span class="sxs-lookup"><span data-stu-id="0ed00-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="0ed00-124">Em alternativa, pode instalar mongod.exe como um serviço:</span><span class="sxs-lookup"><span data-stu-id="0ed00-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="0ed00-125">Um serviço é instalado com o nome MongoDB com uma descrição do "BD de Mongo".</span><span class="sxs-lookup"><span data-stu-id="0ed00-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="0ed00-126">Olá `--logpath` opção tem de ser toospecify utilizado um ficheiro de registo, desde Olá a executar o serviço não tem uma saída de toodisplay de janela de comando.</span><span class="sxs-lookup"><span data-stu-id="0ed00-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="0ed00-127">Olá `--logappend` opção especifica que um reinício do serviço de Olá provoca o ficheiro de registo saída tooappend toohello existente.</span><span class="sxs-lookup"><span data-stu-id="0ed00-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="0ed00-128">Olá `--dbpath` opção especifica a localização de Olá do diretório de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ed00-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="0ed00-129">Para mais relacionados com o serviço opções da linha de comandos, consulte [relacionados com o serviço opções da linha de comandos][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="0ed00-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="0ed00-130">no serviço de Olá toostart, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="0ed00-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="0ed00-131">Agora que MongoDB está instalado e em execução, terá de tooopen uma porta na Firewall do Windows para que as possa remotamente ligar tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ed00-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="0ed00-132">De Olá **iniciar** menu, selecione **ferramentas administrativas** e, em seguida, **Firewall do Windows com segurança avançada**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="0ed00-133">a) no painel esquerdo Olá, selecione **regras de entrada**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="0ed00-134">No Olá **ações** painel Olá direito, selecione **nova regra...** .</span><span class="sxs-lookup"><span data-stu-id="0ed00-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Firewall do Windows][Image1]

    <span data-ttu-id="0ed00-136">b) na Olá **novo Assistente de regras de entrada**, selecione **porta** e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Firewall do Windows][Image2]

    <span data-ttu-id="0ed00-138">c) selecione **TCP** e, em seguida, **portas locais específicas**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="0ed00-139">Especifique uma porta de "27017" (porta de predefinição Olá MongoDB escuta) e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Firewall do Windows][Image3]

    <span data-ttu-id="0ed00-141">d) selecione **permitir ligação Olá** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Firewall do Windows][Image4]

    <span data-ttu-id="0ed00-143">i) clique em **seguinte** novamente.</span><span class="sxs-lookup"><span data-stu-id="0ed00-143">e) Click **Next** again.</span></span>

    ![Firewall do Windows][Image5]

    <span data-ttu-id="0ed00-145">f) Especifique um nome para a regra de Olá, tal como "MongoPort" e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Firewall do Windows][Image6]

12. <span data-ttu-id="0ed00-147">Se não configurar um ponto final para o MongoDB quando criou a máquina virtual de Olá, pode fazê-lo agora.</span><span class="sxs-lookup"><span data-stu-id="0ed00-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="0ed00-148">Terá de regra de firewall de Olá e Olá endpoint toobe tooconnect capaz de tooMongoDB remotamente.</span><span class="sxs-lookup"><span data-stu-id="0ed00-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="0ed00-149">No portal do Azure Olá, clique em **máquinas virtuais (clássicas)**, clique no nome de Olá da nova máquina virtual e, em seguida, clique em **pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Pontos Finais][Image7]

13. <span data-ttu-id="0ed00-151">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0ed00-151">Click **Add**.</span></span>

14. <span data-ttu-id="0ed00-152">Adicionar um ponto final com o nome "Mongo" protocolo **TCP**e ambos **pública** e **privada** portas definido demasiado "27017".</span><span class="sxs-lookup"><span data-stu-id="0ed00-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="0ed00-153">Abrir esta porta permite toobe MongoDB acedida remotamente.</span><span class="sxs-lookup"><span data-stu-id="0ed00-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Pontos Finais][Image9]

> [!NOTE]
> <span data-ttu-id="0ed00-155">porta Olá 27017 é Olá predefinido porta é utilizada por MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ed00-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="0ed00-156">Pode alterar esta porta predefinida, especificando Olá `--port` parâmetro ao iniciar o servidor de mongod.exe Olá.</span><span class="sxs-lookup"><span data-stu-id="0ed00-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="0ed00-157">Certifique-se de que toogive Olá o mesmo número de porta na firewall de Olá e Olá "Mongo" ponto final no Olá precedente instruções.</span><span class="sxs-lookup"><span data-stu-id="0ed00-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
