<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate um novo serviço

1. Utilizar o seu toolog de credenciais de conta Microsoft no toohello [portal do Azure](https://portal.azure.com/).

2. No portal do Azure Olá, clique em  **+**  e, em seguida, no marketplace Olá, clique em **ver todos os**.

    ![Crie o Gestor de Dispositivos do StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Procure o _StorSimple Físico_. Selecione e clique em **Série do Dispositivo Físico do StorSimple** e, em seguida, clique em **Criar**. Em alternativa, no portal do Azure de Olá clicar  **+**  e, em **armazenamento**, clique em **série de dispositivo físico StorSimple**.

    ![Crie o Gestor de Dispositivos do StorSimple](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. No Olá **Gestor de dispositivos do StorSimple** painel, Olá os seguintes passos:
   
   1. Forneça um **Nome do recurso** exclusivo para o serviço. Este é um nome amigável que pode ser utilizado o serviço de Olá tooidentify. nome de Olá pode ter entre 2 e 50 carateres que podem ser letras, números e hífenes. nome de Olá tem de começar e terminar com uma letra ou um número.

   2. Escolha um **subscrição** de Olá na lista pendente. subscrição de Olá é ligado tooyour conta de faturação. Este campo não estará presente se tiver apenas uma subscrição.

   3. Para **Grupo de recursos**, **Utilizar existente** ou **Criar novo**. Para obter mais informações, veja [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/) (Grupos de recursos do Azure).
   
   4. Forneça uma **Localização** para o serviço. Em geral, escolha uma localização mais próxima toohello região geográfica onde pretende toodeploy seu dispositivo. Também poderá toofactor no Olá seguintes considerações: 
      
      * Se tiver cargas de trabalho existentes no Azure que também tenciona toodeploy com o dispositivo StorSimple, deve utilizar esse datacenter.
      * O serviço Gestor de Dispositivos do StorSimple e o armazenamento do Azure podem estar em duas localizações diferentes. Nesse caso, é necessário toocreate Olá Gestor de dispositivos do StorSimple e conta do storage do Azure em separado. toocreate uma conta de armazenamento do Azure, aceda toohello o serviço de armazenamento do Azure no Olá portal do Azure e siga os passos de Olá no [criar uma conta de armazenamento do Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Depois de criar esta conta, adicioná-lo toohello do serviço StorSimple Manager de dispositivo ao seguir os passos de Olá em [configurar uma nova conta de armazenamento para o serviço de Olá](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Selecione **criar uma nova conta de armazenamento** tooautomatically criar uma conta de armazenamento com o serviço de Olá. Especifique um nome para esta conta de armazenamento. Se precisar de ter os seus dados numa localização diferente, desmarque esta caixa.

   6. Verifique **Pin toodashboard** se pretender que um serviço de toothis rápido de ligação no dashboard.
      
   7. Clique em **criar** toocreate Olá Gestor de dispositivos do StorSimple.

       ![Crie o Gestor de Dispositivos do StorSimple](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
criação do serviço de Olá demora alguns minutos. Depois do serviço de Olá foi criado com êxito, verá uma notificação e painel de serviço novo Olá abre-se.
   
![Crie o Gestor de Dispositivos do StorSimple](./media/storsimple-8000-create-new-service/createssdevman5.png)


