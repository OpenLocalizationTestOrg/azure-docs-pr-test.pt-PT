Se a máquina virtual (VM) no Azure encontra um erro de arranque ou de disco, poderá ser necessário tooperform passos no disco rígido virtual Olá próprio de resolução de problemas. Um exemplo comum seria uma atualização da aplicação com falhas que impede que Olá VM arrancar com êxito. Este artigo descreve como toouse tooconnect portal do Azure a toofix VM do disco rígido virtual tooanother quaisquer erros e, em seguida, voltar a criar a VM original.

## <a name="recovery-process-overview"></a>Descrição geral do processo de recuperação
Olá, processo de resolução de problemas é o seguinte:

1. Eliminar Olá VM que está a encontrar problemas, mas manter Olá os discos rígidos virtuais.
2. Anexe e montar o disco rígido virtual de Olá tooanother VM para resolução de problemas.
3. Ligar toohello VM de resolução de problemas. Editar ficheiros ou executar ferramentas toofix erros no Olá original disco virtual.
4. Desmonte e desanexar o disco rígido virtual Olá de Olá VM de resolução de problemas.
5. Crie uma VM utilizando Olá original disco virtual.

## <a name="delete-hello-original-vm"></a>Eliminar Olá original VM
Os discos rígidos virtuais e as VMs são dois recursos diferentes do Azure. Um disco rígido virtual é onde o sistema de operativo Olá, aplicações e configurações são armazenadas. Olá VM é apenas metadados, que define o tamanho de Olá ou localização e o que faz referência a recursos, tais como um disco rígido virtual ou o cartão de interface de rede virtual (NIC). Cada disco rígido virtual obtém uma concessão atribuída quando esse disco é anexado tooa VM. Embora os discos de dados podem ser ligados e anular a exposição mesmo enquanto Olá VM está em execução, o disco do SO Olá não pode ser desligado, a menos que Olá recurso VM é eliminado. concessão de Olá continua tooassociate Olá SO disco tooa VM mesmo quando se encontra num estado parado e desalocado essa VM.

Olá primeiro passo toorecovering a VM é o recurso VM de Olá toodelete próprio. A eliminar Olá VM deixa Olá os discos rígidos virtuais na sua conta de armazenamento. Depois de Olá que VM é eliminada, pode anexar o disco rígido virtual de Olá tooanother tootroubleshoot VM e resolva os erros de Olá. 

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com). 
2. Olá menu no lado esquerdo Olá, clique em **máquinas virtuais (clássicas)**.
3. Selecione Olá VM que tenha o problema de Olá, clique **discos**e, em seguida, identificar o nome de Olá do disco de rígido virtual Olá. 
4. Selecione o disco de rígido virtual Olá SO e verifique Olá **localização** conta de armazenamento de Olá tooidentify que contém esse disco rígido virtual. No seguinte exemplo de Olá, Olá imediatamente antes cadeia ". w" é o nome de conta do storage Olá.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![imagem de Olá sobre a localização da VM](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Faça duplo clique Olá VM e, em seguida, selecione **eliminar**. Certifique-se de que os discos de Olá não forem seleccionados quando eliminar Olá VM.
6. Crie uma VM de recuperação nova. Este VM tem de constar Olá mesmo região grupo de recursos e (serviço de nuvem) como problema Olá VM.
7. Selecione a VM de recuperação de Olá e, em seguida, selecione **discos** > **anexar existente**.
8. tooselect o disco rígido virtual existente, clique em **ficheiro VHD**:

    ![Procurar o VHD existente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Selecione a conta de armazenamento Olá > contentor VHD > olá disco rígido virtual, clique em Olá **selecione** botão tooconfirm à sua escolha.

    ![Selecionar o seu VHD existente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Com o VHD selecionado agora, selecione **OK** tooattach Olá disco rígido virtual existente.
11. Após alguns segundos, Olá **discos** painel para a VM irá apresentar o disco rígido virtual ligado como um disco de dados:

    ![Disco rígido virtual já existente anexado como disco de dados](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Resolva os problemas no Olá original disco virtual
Quando está montado Olá existente disco virtual, agora pode efetuar qualquer manutenção e passos de resolução de problemas, conforme necessário. Assim que tiver resolvido problemas Olá, continue com Olá os seguintes passos.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Desmonte e desanexar Olá original disco virtual
Depois dos erros são resolvidos, desmontar e exposição do disco rígido virtual existente por Olá da sua VM de resolução de problemas. Não é possível utilizar o disco rígido virtual, juntamente com quaisquer outro VM até que a concessão de Olá que anexa toohello de disco rígido virtual Olá VM de resolução de problemas é libertado.  

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com). 
2. No menu de Olá no lado esquerdo Olá, selecione **máquinas virtuais (clássicas)**.
3. Localize a VM de recuperação de Olá. Selecione discos, disco de Olá de contexto e, em seguida, selecione **anulação de exposições**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Criar uma VM a partir do disco de rígido Olá original

toocreate uma VM a partir do seu disco rígido virtual original, utilize [portal clássico do Azure](https://manage.windowsazure.com).

1. Inicie sessão no [portal clássico do Azure](https://manage.windowsazure.com).
2. Na parte inferior de Olá do portal de Olá, selecione **novo** > **computação** > **Máquina Virtual** > **da Galeria** .
3. No Olá **escolhe uma imagem** secção, selecione **meu discos**, e, em seguida, selecione Olá disco rígido virtual original. Verifique as informações de localização de Olá. Esta é a região de olá onde Olá VM tem de ser implementada. Selecione o botão seguinte Olá.
4. No Olá **configuração da Máquina Virtual** secção, escreva o nome da VM Olá e selecionar um tamanho para Olá VM.
