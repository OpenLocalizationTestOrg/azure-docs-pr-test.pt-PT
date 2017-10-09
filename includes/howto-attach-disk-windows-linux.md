


## <a name="attach-an-empty-disk"></a>Anexar um disco vazio
Anexar um disco vazio é tooadd uma forma simples dados de disco, porque o Azure cria o ficheiro. vhd Olá para si e armazena-os na conta do storage Olá.

1. Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá VM adequado.

2. No menu de definições de Olá, clique em **discos**.

   ![Anexar um disco novo vazio](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Na barra de comando Olá, clique em **anexar novo**.  
    Olá **anexar novo disco** é apresentada a caixa de diálogo.

    ![Anexe um novo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Preencha Olá seguintes informações:
    - No **nome de ficheiro**, aceite o nome predefinido de Olá ou escreva outro para o ficheiro. vhd Olá. o disco de dados de Olá utiliza um nome gerado automaticamente, mesmo que escreva outro nome para o ficheiro. vhd Olá.
    - Selecione Olá **tipo** do disco de dados de Olá. Todas as máquinas virtuais suportam discos padrão. Número de máquinas virtuais também suporta discos premium.
    - Selecione Olá **tamanho (GB)** do disco de dados de Olá.
    - Para **alojar a colocação em cache**, escolha none ou só de leitura.
    - Clique em OK toofinish.

4. Depois de disco de dados de Olá é criado e ligado, este está listado na secção discos Olá Olá VM.

   ![Disco de dados nova e vazio anexado com êxito](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Depois de adicionar um disco de dados, tem de toolog no toohello VM e inicializar disco Olá, para que possa ser utilizado.

## <a name="how-to-attach-an-existing-disk"></a>Como: anexar um disco existente
Para anexar um disco existente, tem de ter um .vhd disponível numa conta de armazenamento. Olá utilize [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload Olá. vhd ficheiro toohello conta do storage. Depois de ter criado e carregado o ficheiro. vhd Olá, poderá anexar-tooa VM.

1. Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá máquina virtual adequado.

2. No menu de definições de Olá, clique em **discos**.

3. Na barra de comando Olá, clique em **anexar existente**.

    ![Anexar disco de dados](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Clique em **localização**. contas de armazenamento disponível Olá apresentam. Em seguida, selecione uma conta de armazenamento adequado aos listados.

    ![Forneça a conta de armazenamento do disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. A **conta de armazenamento** contém um ou mais contentores que contêm as unidades de disco (vhds). Selecione o contentor adequado Olá das listados.

    ![Forneça o contentor do windows de máquinas virtuais](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Olá **vhds** painel apresenta uma lista de unidades de disco Olá contidas no contentor de Olá. Clique dos discos de Olá e, em seguida, clique em selecionar.

    ![Forneça a imagem de disco para o windows de máquinas virtuais](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Olá **anexar o disco existente** painel apresenta novamente, com a localização de Olá que contém a conta de armazenamento Olá, contentor e máquina virtual do disco rígido (vhd) selecionado tooadd toohello.

  Definir **alojar a colocação em cache** toonone ou leitura apenas, em seguida, clique em OK.

    ![Disco de dados foi exposto com êxito](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
