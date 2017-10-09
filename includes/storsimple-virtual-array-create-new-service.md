#### <a name="toocreate-a-new-service"></a>toocreate um novo serviço

1.  Utilizar as credenciais da conta Microsoft, inicie sessão no toohello portal do Azure neste URL: <https://portal.azure.com/>. Se implementar o dispositivo de Olá no portal de administração pública, inicie sessão no: <https://portal.azure.us/>

2.  No portal do Azure Olá, clique em **+ novo** &gt; **armazenamento** &gt; **série Virtual StorSimple**.

    ![Criar novo serviço](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  No Olá **Gestor de dispositivos do StorSimple** painel que abre-se, Olá seguintes:

    1.  Forneça um **Nome do recurso** exclusivo para o serviço. Olá recursos é um nome amigável que pode ser utilizado o serviço de Olá tooidentify. nome de Olá pode ter entre 2 e 50 carateres que podem ser letras, números e hífenes. nome de Olá tem de começar e terminar com uma letra ou um número.

    2.  Escolha um **subscrição** de Olá na lista pendente. subscrição de Olá é ligado tooyour conta de faturação. Este campo não estará presente se tiver apenas uma subscrição.

    3.  Para **grupo de recursos**, selecione um existente ou crie um novo grupo. Para obter mais informações, veja [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/) (Grupos de recursos do Azure).

    4.  Forneça uma **Localização** para o serviço. Consulte [regiões do Azure](https://azure.microsoft.com/regions/#services) para obter mais informações sobre os quais os serviços estão disponíveis em cada região. Em geral, escolha um **localização** região geográfica mais próximo do toohello, onde pretende toodeploy seu dispositivo. Também poderá toofactor seguir Olá:

        -   Se tiver cargas de trabalho existentes no Azure que também tenciona toodeploy com o dispositivo StorSimple, recomendamos que utilize esse datacenter.

        -   O armazenamento de Gestor de dispositivos do StorSimple e o Azure pode estar em duas localizações separadas. Nesse caso, é necessário toocreate Olá Gestor de dispositivos do StorSimple e conta do storage do Azure em separado. toocreate uma conta de armazenamento do Azure, aceda toohello o serviço de armazenamento do Azure no Olá portal do Azure e siga os passos de Olá no [criar uma conta de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Depois de criar esta conta, adicioná-lo toohello do serviço StorSimple Manager de dispositivo ao seguir os passos de Olá em [configurar uma nova conta de armazenamento para o serviço de Olá](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Se implementar o dispositivo virtual Olá Olá Government Portal, Olá serviço StorSimple Manager de dispositivo está disponível nas localizações dos EUA Iowa e Virginia-nos.

    5.  Selecione **criar uma nova conta de armazenamento do Azure** tooautomatically criar uma conta de armazenamento com o serviço de Olá. Especifique um **nome da conta de armazenamento**. Se precisar de ter os seus dados numa localização diferente, desmarque esta caixa.

    6.  Verifique **Pin toodashboard** se pretender que um serviço de toothis rápido de ligação no dashboard.

    7.  Clique em **criar** toocreate Olá Gestor de dispositivos do StorSimple.

        ![Criar novo serviço](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

São direcionado toohello **serviço** página de destino. criação do serviço de Olá demora alguns minutos. Depois de serviço Olá é criado com êxito, será notificado adequadamente e estado de Olá do serviço de Olá mudará demasiado**Active Directory**.


