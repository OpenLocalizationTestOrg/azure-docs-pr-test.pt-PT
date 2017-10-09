Quando já não necessita de um disco de dados que esteja anexado tooa máquina, pode facilmente desanexá-lo. Desanexar um disco remove o disco de Olá da máquina virtual de Olá, mas não elimina disco Olá do Olá conta do storage do Azure.

Se pretende que os toouse Olá existente dados no disco Olá novamente, pode reattach-toohello mesma máquina virtual ou outro.  

> [!NOTE]
> toodetach um disco de sistema operativo, terá primeiro toodelete Olá máquina.
>

## <a name="find-hello-disk"></a>Localizar o disco de Olá
Se não souber o nome de Olá de Olá disco ou quiser tooverify-lo antes de desanexá-lo, siga estes passos.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).

2. Clique em **máquinas virtuais**, e, em seguida, selecione Olá VM adequado.

3. Clique em **discos** ao longo de Olá deixado edge do dashboard de máquina virtual de Olá, em **definições**.

 dashboard de máquina virtual de Olá lista Olá nome e o tipo de todos os discos ligados. Por exemplo, este ecrã mostra uma máquina virtual com um disco de sistema operativo (SO) e um disco de dados:

    ![Localizar o disco de dados](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Exposição do disco de Olá
1. No portal do Azure Olá, clique em **máquinas virtuais**e, em seguida, clique no nome de Olá da máquina virtual Olá que tem o disco de dados de Olá pretende toodetach.

2. Clique em **discos** ao longo de Olá deixado edge do dashboard de máquina virtual de Olá, em **definições**.

3. Clique em disco Olá pretende toodetach.

  ![Identificar Olá disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. A partir da barra de comando Olá, clique em **anulação de exposições**.

  ![Localizar Olá desanexar comando](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. Na janela de confirmação de Olá, clique em **Sim** disco de Olá toodetach.

  ![Confirme o disco de Olá anular a exposição](./media/howto-detach-disk-windows-linux/confirmdetach.png)

disco Olá permanece no armazenamento, mas já não máquina virtual de tooa anexado.
