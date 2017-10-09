* No **adicionar vCenter**, especifique um nome amigável para o servidor de anfitrião ou o vCenter da vSphere Olá e, em seguida, especifique o endereço IP Olá ou FQDN do servidor de Olá. Deixe porta Olá como 443, a menos que os servidores do VMware são toolisten configurada para pedidos numa porta diferente. Selecione Olá conta que seja tooconnect toohello VMware vCenter ou vSphere ESXi servidor. Clique em **OK**.

    ![VMware](./media/site-recovery-add-vcenter/vmware-server.png)

   > [!NOTE]
   > Se estiver a adicionar Olá do VMware vCenter server ou o anfitrião do VMware vSphere com uma conta que não tem privilégios de administrador no servidor de anfitrião do vCenter ou Olá, certifique-se de que a conta de Olá tem esses privilégios ativados: Centro de dados, o arquivo de dados, pasta, anfitrião, rede , Recursos, a Máquina Virtual e vSphere distribuídas comutador. Além disso, Olá do VMware vCenter server tem as vistas de armazenamento de Olá privilégio ativadas.
