
<br>

> [!NOTE]
> <span data-ttu-id="0e64a-101">Se lhe foi fornecido um nome de utilizador e palavra-passe por um administrador, há a possibilidade de boa que já tem um trabalho ou escola ID (também por vezes denominado um *ID organizacional*).</span><span class="sxs-lookup"><span data-stu-id="0e64a-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="0e64a-102">Se Sim, pode imediatamente começar toouse tooaccess sua conta do Azure recursos do Azure que necessitam de um.</span><span class="sxs-lookup"><span data-stu-id="0e64a-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="0e64a-103">Se achar que não é possível utilizar esses recursos, poderá ter tooreturn toothis artigo para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="0e64a-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="0e64a-104">Para obter mais informações, consulte [contas que pode utilizar para iniciar sessão](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [subscrição como um Azure é tooAzure relacionado AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="0e64a-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="0e64a-105">passos de Olá são simples.</span><span class="sxs-lookup"><span data-stu-id="0e64a-105">hello steps are simple.</span></span> <span data-ttu-id="0e64a-106">Terá de toolocate sua assinada na identidade no portal clássico do Azure de Olá, detetar o seu domínio do Azure Active Directory predefinido e adicionar um novo tooit de utilizador como um coadministrador do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e64a-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="0e64a-107">Localizar o diretório predefinido no Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="0e64a-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="0e64a-108">Iniciar sessão em toohello [portal clássico do Azure](https://manage.windowsazure.com) com a sua identidade da conta Microsoft pessoal.</span><span class="sxs-lookup"><span data-stu-id="0e64a-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="0e64a-109">Depois de iniciarem sessão, desloque para baixo do painel de Olá azul do Olá deixado lado e clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="0e64a-111">Vamos começar por ao localizar algumas informações sobre a sua identidade no Azure.</span><span class="sxs-lookup"><span data-stu-id="0e64a-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="0e64a-112">Deverá ver algo semelhante Olá seguintes no painel principal Olá, que mostra que tem um diretório predefinido.</span><span class="sxs-lookup"><span data-stu-id="0e64a-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="0e64a-113">Vamos descobrir mais informações acerca do mesmo.</span><span class="sxs-lookup"><span data-stu-id="0e64a-113">Let's find out some more information about it.</span></span> <span data-ttu-id="0e64a-114">Clique em linha de diretório predefinido de Olá, que proporciona em Propriedades de diretório Olá predefinidas.</span><span class="sxs-lookup"><span data-stu-id="0e64a-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="0e64a-115">nome de domínio do tooview Olá predefinido, clique em **domínios**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="0e64a-116">Aqui, deve ser capaz de toosee quando foi criado Olá conta do Azure, Azure Active Directory criado um domínio de pessoais predefinido que é um valor de hash (um número gerado a partir de uma cadeia de texto) do seu ID pessoal utilizado como um subdomínio onmicrosoft.com. É Olá domínio toowhich agora, irá adicionar um novo utilizador.</span><span class="sxs-lookup"><span data-stu-id="0e64a-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="0e64a-117">Criar um novo utilizador no domínio predefinido de Olá</span><span class="sxs-lookup"><span data-stu-id="0e64a-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="0e64a-118">Clique em **utilizadores** e procure a sua conta pessoal único.</span><span class="sxs-lookup"><span data-stu-id="0e64a-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="0e64a-119">Deverá ver no Olá **origem** coluna que é um **conta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="0e64a-120">Queremos toocreate um utilizador na sua predefinição. domínio do Azure Active Directory onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="0e64a-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="0e64a-121">Vamos toofollow [estas instruções](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) no Olá próximos passos, mas utilize um exemplo específico.</span><span class="sxs-lookup"><span data-stu-id="0e64a-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="0e64a-122">Na Olá parte inferior da página Olá, clique em **+ adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="0e64a-123">Na página Olá que aparece, escreva o novo nome de utilizador Olá e torne Olá **tipo de utilizador** um **novo utilizador na sua organização**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="0e64a-124">Neste exemplo, o novo nome de utilizador Olá é `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="0e64a-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="0e64a-125">Selecione o domínio predefinido Olá que é detetado anteriormente como domínio Olá para endereço de correio eletrónico do ahmet.</span><span class="sxs-lookup"><span data-stu-id="0e64a-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="0e64a-126">Clique Olá seta seguinte quando terminar.</span><span class="sxs-lookup"><span data-stu-id="0e64a-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="0e64a-127">Adicionar mais detalhes para Ahmet, mas certifique-se de que tooselect Olá adequado **função** valor.</span><span class="sxs-lookup"><span data-stu-id="0e64a-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="0e64a-128">É fácil toouse **Administrador Global** toomake sure coisas estão a funcionar, mas se utilizar uma função de menor, que é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="0e64a-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="0e64a-129">Este exemplo utiliza Olá **utilizador** função.</span><span class="sxs-lookup"><span data-stu-id="0e64a-129">This example uses hello **User** role.</span></span> <span data-ttu-id="0e64a-130">(Saber mais em [permissões de administrador pela função](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Não ative a autenticação multifator, a menos que queira toouse a autenticação multifator para cada operação de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="0e64a-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="0e64a-131">Quando tiver terminado, clique em seta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0e64a-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="0e64a-132">Clique em Olá **criar** botão toogenerate e apresentar uma palavra-passe temporária de Ahmet.</span><span class="sxs-lookup"><span data-stu-id="0e64a-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="0e64a-133">Copie o endereço de e-mail de nome de utilizador hello, ou utilize **enviar correio ELETRÓNICO em palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="0e64a-134">Terá de Olá informações toolog em breve.</span><span class="sxs-lookup"><span data-stu-id="0e64a-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="0e64a-135">Agora deverá ver o novo utilizador Olá, **Ahmet Olá programador**, tenham origem a partir do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e64a-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="0e64a-136">Criou trabalho novo Olá ou identidade da escola com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e64a-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="0e64a-137">No entanto, esta identidade ainda não tem permissões toouse Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="0e64a-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="0e64a-138">Se utilizar **enviar correio ELETRÓNICO em palavra-passe**, Olá seguinte tipo de correio eletrónico é enviada.</span><span class="sxs-lookup"><span data-stu-id="0e64a-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="0e64a-139">Adição de direitos de coadministrador do Azure para subscrições</span><span class="sxs-lookup"><span data-stu-id="0e64a-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="0e64a-140">Agora é preciso novo utilizador do tooadd Olá como coadministrador da sua subscrição para que o utilizador novo Olá pode iniciar sessão toohello Portal de gestão.</span><span class="sxs-lookup"><span data-stu-id="0e64a-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="0e64a-141">toodo, no painel inferior esquerda de Olá clique **definições**.</span><span class="sxs-lookup"><span data-stu-id="0e64a-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="0e64a-142">Na área de definições principal Olá, clique em **administradores** em Olá superior e deverá ver apenas a identidade da conta de Microsoft pessoal.</span><span class="sxs-lookup"><span data-stu-id="0e64a-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="0e64a-143">Na Olá parte inferior da página Olá, clique em **+ adicionar** toospecify coadministrador.</span><span class="sxs-lookup"><span data-stu-id="0e64a-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="0e64a-144">Aqui, introduza o endereço de correio eletrónico Olá do novo utilizador de Olá que criou, incluindo o domínio predefinido.</span><span class="sxs-lookup"><span data-stu-id="0e64a-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="0e64a-145">Conforme mostrado na captura de ecrã seguinte Olá, uma marca de verificação verde é apresentada a seguinte toohello utilizador do diretório do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="0e64a-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="0e64a-146">Lembre-se tooselect todas as subscrições Olá que pretende que este tooadminister capaz de toobe de utilizador.</span><span class="sxs-lookup"><span data-stu-id="0e64a-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="0e64a-147">Quando tiver terminado, deverá ver dois utilizadores, incluindo a sua identidade coadministrador novo.</span><span class="sxs-lookup"><span data-stu-id="0e64a-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="0e64a-148">Termine sessão no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e64a-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="0e64a-149">Iniciar sessão e a alteração de palavra-passe do utilizador novo Olá</span><span class="sxs-lookup"><span data-stu-id="0e64a-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="0e64a-150">Inicie sessão como utilizador novo Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="0e64a-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="0e64a-151">Será imediatamente toocreate que lhes é pedida uma palavra-passe nova.</span><span class="sxs-lookup"><span data-stu-id="0e64a-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="0e64a-152">Deve de ser recompensado com êxito que se assemelha Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="0e64a-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="0e64a-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0e64a-153">Next steps</span></span>
<span data-ttu-id="0e64a-154">Agora, pode utilizar o novo toouse de identidade do Azure Active Directory [os modelos de grupo de recursos do Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0e64a-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
