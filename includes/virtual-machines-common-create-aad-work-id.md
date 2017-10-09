
<br>

> [!NOTE]
> Se lhe foi fornecido um nome de utilizador e palavra-passe por um administrador, há a possibilidade de boa que já tem um trabalho ou escola ID (também por vezes denominado um *ID organizacional*). Se Sim, pode imediatamente começar toouse tooaccess sua conta do Azure recursos do Azure que necessitam de um. Se achar que não é possível utilizar esses recursos, poderá ter tooreturn toothis artigo para obter ajuda. Para obter mais informações, consulte [contas que pode utilizar para iniciar sessão](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [subscrição como um Azure é tooAzure relacionado AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

passos de Olá são simples. Terá de toolocate sua assinada na identidade no portal clássico do Azure de Olá, detetar o seu domínio do Azure Active Directory predefinido e adicionar um novo tooit de utilizador como um coadministrador do Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Localizar o diretório predefinido no Olá portal clássico do Azure
Iniciar sessão em toohello [portal clássico do Azure](https://manage.windowsazure.com) com a sua identidade da conta Microsoft pessoal. Depois de iniciarem sessão, desloque para baixo do painel de Olá azul do Olá deixado lado e clique em **do Active Directory**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Vamos começar por ao localizar algumas informações sobre a sua identidade no Azure. Deverá ver algo semelhante Olá seguintes no painel principal Olá, que mostra que tem um diretório predefinido.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Vamos descobrir mais informações acerca do mesmo. Clique em linha de diretório predefinido de Olá, que proporciona em Propriedades de diretório Olá predefinidas.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

nome de domínio do tooview Olá predefinido, clique em **domínios**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Aqui, deve ser capaz de toosee quando foi criado Olá conta do Azure, Azure Active Directory criado um domínio de pessoais predefinido que é um valor de hash (um número gerado a partir de uma cadeia de texto) do seu ID pessoal utilizado como um subdomínio onmicrosoft.com. É Olá domínio toowhich agora, irá adicionar um novo utilizador.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Criar um novo utilizador no domínio predefinido de Olá
Clique em **utilizadores** e procure a sua conta pessoal único. Deverá ver no Olá **origem** coluna que é um **conta Microsoft**. Queremos toocreate um utilizador na sua predefinição. domínio do Azure Active Directory onmicrosoft.com.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Vamos toofollow [estas instruções](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) no Olá próximos passos, mas utilize um exemplo específico.

Na Olá parte inferior da página Olá, clique em **+ adicionar utilizador**. Na página Olá que aparece, escreva o novo nome de utilizador Olá e torne Olá **tipo de utilizador** um **novo utilizador na sua organização**. Neste exemplo, o novo nome de utilizador Olá é `ahmet`. Selecione o domínio predefinido Olá que é detetado anteriormente como domínio Olá para endereço de correio eletrónico do ahmet. Clique Olá seta seguinte quando terminar.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Adicionar mais detalhes para Ahmet, mas certifique-se de que tooselect Olá adequado **função** valor. É fácil toouse **Administrador Global** toomake sure coisas estão a funcionar, mas se utilizar uma função de menor, que é uma boa ideia. Este exemplo utiliza Olá **utilizador** função. (Saber mais em [permissões de administrador pela função](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Não ative a autenticação multifator, a menos que queira toouse a autenticação multifator para cada operação de início de sessão. Quando tiver terminado, clique em seta seguinte Olá.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Clique em Olá **criar** botão toogenerate e apresentar uma palavra-passe temporária de Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Copie o endereço de e-mail de nome de utilizador hello, ou utilize **enviar correio ELETRÓNICO em palavra-passe**. Terá de Olá informações toolog em breve.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Agora deverá ver o novo utilizador Olá, **Ahmet Olá programador**, tenham origem a partir do Azure Active Directory. Criou trabalho novo Olá ou identidade da escola com o Azure Active Directory. No entanto, esta identidade ainda não tem permissões toouse Azure recursos.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Se utilizar **enviar correio ELETRÓNICO em palavra-passe**, Olá seguinte tipo de correio eletrónico é enviada.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Adição de direitos de coadministrador do Azure para subscrições
Agora é preciso novo utilizador do tooadd Olá como coadministrador da sua subscrição para que o utilizador novo Olá pode iniciar sessão toohello Portal de gestão. toodo, no painel inferior esquerda de Olá clique **definições**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Na área de definições principal Olá, clique em **administradores** em Olá superior e deverá ver apenas a identidade da conta de Microsoft pessoal. Na Olá parte inferior da página Olá, clique em **+ adicionar** toospecify coadministrador. Aqui, introduza o endereço de correio eletrónico Olá do novo utilizador de Olá que criou, incluindo o domínio predefinido. Conforme mostrado na captura de ecrã seguinte Olá, uma marca de verificação verde é apresentada a seguinte toohello utilizador do diretório do Olá predefinido. Lembre-se tooselect todas as subscrições Olá que pretende que este tooadminister capaz de toobe de utilizador.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Quando tiver terminado, deverá ver dois utilizadores, incluindo a sua identidade coadministrador novo. Termine sessão no portal de Olá.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Iniciar sessão e a alteração de palavra-passe do utilizador novo Olá
Inicie sessão como utilizador novo Olá que criou.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Será imediatamente toocreate que lhes é pedida uma palavra-passe nova.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Deve de ser recompensado com êxito que se assemelha Olá seguinte.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Passos seguintes
Agora, pode utilizar o novo toouse de identidade do Azure Active Directory [os modelos de grupo de recursos do Azure](../articles/xplat-cli-azure-resource-manager.md).

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
