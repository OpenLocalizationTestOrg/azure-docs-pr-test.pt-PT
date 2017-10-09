<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a>toocreate um contentor de volume
1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**. A partir de Olá tabela lista de dispositivos de Olá, selecione e clique no dispositivo. 

    ![Painel Contentor de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. No dashboard de dispositivo Olá, clique em **+ adicionar contentor de volume**

    ![Painel Contentor de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. No Olá **contentor de volume adicionar** painel:
   
   1. dispositivo Olá é selecionado automaticamente.
   2. Forneça um **Nome** para o contentor do volume. nome de Olá tem de ser 3 too32 carateres. Não pode mudar o nome de um contentor de volumes depois de o mesmo ter sido criado.
   3. Selecione **ativar a encriptação de armazenamento de nuvem** tooenable encriptação de dados de Olá enviados a partir de Olá dispositivo toohello nuvem.
   4. Forneça e confirme uma **chave de encriptação de armazenamento na nuvem** que 8 too32 carateres de comprimento. Esta chave é utilizada por Olá dispositivo tooaccess encriptados de dados.
   5. Selecione um **conta de armazenamento** tooassociate com este contentor de volume. Pode escolher uma conta do storage existente ou a conta predefinida Olá que é gerada no momento de Olá da criação do serviço. Também pode utilizar Olá **adicionar novo** opção toospecify uma conta de armazenamento que não se encontra ligado toothis a subscrição do serviço.
   6. Selecione **ilimitada** no Olá **Especificar largura de banda** na lista pendente se desejar tooconsume largura de banda disponível Olá todos os. Também pode definir esta opção demasiado**personalizada** tooemploy controlos de largura de banda e especifique um valor entre 1 e 1000 Mbps.
      Se tiver as informações de utilização de largura de banda disponíveis, poderá ser tooallocate capaz de largura de banda com base num agendamento, especificando **selecionar um modelo de largura de banda**. Para um procedimento passo a passo, consulte demasiado[adicionar um modelo de largura de banda](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).

      ![Painel Contentor de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. Clique em **Criar**.

        ![Painel Contentor de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       Será notificado quando o contentor de volume Olá é criado com êxito.

       ![Notificação de criação do contentor de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   Olá recém-criado contentor de volume é listado na lista de Olá de contentores de volume para o seu dispositivo.

   ![Painel Adicionar contentor de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


