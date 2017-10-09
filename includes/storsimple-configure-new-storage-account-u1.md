<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd uma conta de armazenamento no StorSimple série 8000 atualização 1.0
1. Num serviço do StorSimple Manager Olá página de destino, selecione o seu serviço e faça duplo clique. Esta ação irá demorar toohello **início rápido** página. Selecione Olá **configurar** página.
2. Clique em **Adicionar/editar conta de armazenamento**.
3. No Olá **adicionar/editar conta de armazenamento** caixa de diálogo, clique em **adicionar novo**.
4. No Olá **fornecedor** fornecedor de serviços do campo, selecione Olá nuvem adequada. fornecedores de Olá suportado são Azure, Amazon S3, Amazon S3 com RRS, HP e OpenStack. Especifique as credenciais de Olá e a localização de Olá associado à conta de armazenamento Olá dos seus fornecedores de serviços em nuvem. os campos de Olá apresentados para as credenciais serão diferentes consoante o fornecedor do serviço cloud Olá que especificou. 
   
   * Se tiver selecionado o Azure como o fornecedor de serviço em nuvem, forneça Olá **nome** e Olá primário **chave de acesso** para a sua conta de armazenamento do Microsoft Azure. Para uma conta do Azure, localização Olá será automaticamente preenchida.
     
        ![Adicionar conta de armazenamento do Azure](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Se tiver selecionado Amazon S3 ou Amazon S3 com RRS, forneça um **Nome da Conta de Armazenamento** amigável, **Chave de Acesso** e **Chave Secreta**. Para o Amazon S3 e o Amazon S3 com RRS, é suportada Olá seguintes localizações:
     
     * E.U.A. Standard
     * E.U.A. Oeste (Oregon)
     * E.U.A. Oeste (Norte da Califórnia)
     * UE (Irlanda)
     * Ásia-Pacífico (Singapura)
     * Ásia-Pacífico (Sydney)
     * Ásia-Pacífico (Tóquio)
     * América do Sul (São Paulo)
       
       ![Adicionar conta de armazenamento do Amazon](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Se tiver selecionado HP como o fornecedor de serviços em nuvem, forneça um **Nome da Conta de Armazenamento** amigável, o **ID do Inquilino**, o **Nome de Utilizador** e a **Palavra-passe**. Para HP, é suportada Olá seguintes localizações:
     
     * E.U.A Leste
     * E.U.A. Oeste
       
       ![Adicionar conta de armazenamento de HP](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Se tiver selecionado **Openstack** como o fornecedor de serviços em nuvem, forneça um **Nome do Anfitrião**, a **Chave de Acesso** e a **Chave Secreta**.
     
     > [!NOTE]
     > Para todos os Olá nuvem fornecedores do serviço, excluindo o Azure, é permitido um nome amigável. Pode utilizar diferentes nomes amigáveis e criar mais do que uma conta de armazenamento com Olá mesmo conjunto de credenciais.
     > 
     > 
     
        ![Adicionar conta de armazenamento do Openstack](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Selecione **ativar modo SSL** toocreate um canal seguro para a comunicação de rede entre a nuvem de dispositivo e Olá. Limpar Olá **ativar modo SSL** caixa de verificação apenas se estiver a utilizar uma nuvem privada.
   
   > [!NOTE]
   > Se estiver a utilizar HP como o fornecedor, o modo SSL estará sempre ativado.
   > 
   > 
6. Clique Olá ícone de verificação ![ícone de verificação](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Será notificado depois de conta de armazenamento Olá é criada com êxito.
7. Olá, conta de armazenamento recentemente criada será apresentada no Olá **configurar** página em **contas do Storage**. Clique em **guardar** toosave Olá nova conta do storage. Clique em **OK** quando lhe for pedida a confirmação.

