#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO no anfitrião de Olá
1. Abra o Gestor de servidor no anfitrião do Windows Server. Por predefinição, o Gestor de servidor é iniciado quando inicia um membro do grupo de administradores Olá tooa no computador no qual está a executar o Windows Server 2012 R2 ou Windows Server 2012. Se Olá Gestor de servidor já não estiver aberto, clique em **Iniciar > Gestor de servidor**.
   
    ![Gestor de servidor](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. Clique em **Gestor de servidor > Dashboard > Adicionar funções e funcionalidades**. Esta ação inicia Olá **para adicionar funções e funcionalidades** assistente.
   
    ![Assistente para adicionar funções e funcionalidades 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. No Olá **para adicionar funções e funcionalidades** assistente, Olá a seguir:
   
   * No Olá **antes de começar** página, clique em **seguinte**.
   * No Olá **selecionar tipo de instalação** página, aceite a predefinição de Olá de **baseada em funções ou baseada em funcionalidade** instalação. Clique em **Seguinte**.
     
       ![Assistente para adicionar funções e funcionalidades 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * No Olá **servidor de destino selecione** página, escolha **selecione um servidor a partir do agrupamento de servidores de Olá**. O servidor de anfitrião deve ser detetado automaticamente. Clique em **Seguinte**.
   * No Olá **selecionar funções de servidor** página, clique em **seguinte**.
   * No Olá **selecionar funcionalidades** página, selecione **Multipath i / o**e clique em **seguinte**.
     
       ![Assistente para adicionar funções e funcionalidades 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * No Olá **confirmar seleções de instalação** página, confirme a seleção de Olá e, em seguida, selecione **reiniciar o servidor de destino de Olá automaticamente se necessário**, conforme mostrado abaixo. Clique em **Instalar**.
     
       ![Assistente para adicionar funções e funcionalidades 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * Será notificado quando Olá instalação estiver concluída. Clique em **fechar** Assistente de Olá tooclose.
     
       ![Assistente para adicionar funções e funcionalidades 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

