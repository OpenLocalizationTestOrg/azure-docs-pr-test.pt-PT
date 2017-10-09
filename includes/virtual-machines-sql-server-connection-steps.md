### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Portas TCP abertas na firewall do Windows hello para a instância predefinida de Olá de Olá motor de base de dados
1. Ligar a máquina virtual de toohello com o ambiente de trabalho remoto. Para obter instruções detalhadas sobre a ligação toohello VM, consulte [abrir uma VM do SQL com o ambiente de trabalho remoto](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Depois de a sessão, no ecrã de início de Olá, escreva **WF.msc**e, em seguida, prima ENTER.
   
    ![Iniciar Olá programa de Firewall](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. No Olá **Firewall do Windows com segurança avançada**, no Olá painel esquerdo, faça duplo clique **regras de entrada**e, em seguida, clique em **nova regra** no painel de ações de Olá.
   
    ![Nova Regra](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. No Olá **novo Assistente de regras de entrada** caixa de diálogo em **tipo de regra**, selecione **porta**e, em seguida, clique em **seguinte**.
5. No Olá **protocolo e portas** caixa de diálogo, utilizar a predefinição de Olá **TCP**. No Olá **portas locais específicas** caixa, em seguida, Olá do tipo número de porta do instância Olá Olá motor de base de dados (**1433** para a instância predefinida de Olá ou à sua escolha para uma porta privada Olá no passo de ponto final de Olá).
   
    ![Porta TCP 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Clique em **Seguinte**.
7. No Olá **ação** caixa de diálogo, selecione **permitir ligação Olá**e, em seguida, clique em **seguinte**.
   
    **Nota de segurança:** selecionar **permitir a ligação de Olá se é seguro** pode proporcionar segurança adicional. Selecione esta opção se pretender que as opções de segurança adicional tooconfigure no seu ambiente.
   
    ![Permitir Ligações](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. No Olá **perfil** caixa de diálogo, selecione **pública**, **privada**, e **domínio**. Clique depois em **Seguinte**.
   
    **Nota de segurança:** selecionar **pública** permite o acesso através de Olá internet. Sempre que for possível, selecione um perfil mais restritivo.
   
    ![Perfil Público](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. No Olá **nome** , escreva um nome e descrição para esta regra e, em seguida, clique em **concluir**.
   
    ![Nome da Regra](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Abra portas adicionais para outros componentes conforme necessário. Para obter mais informações, consulte [configurar tooAllow de Firewall do Windows hello acesso ao servidor de SQL](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Configurar o SQL Server toolisten no Olá protocolo TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Configurar o SQL Server para autenticação em modo misto
Olá motor de base de dados do SQL Server não é possível utilizar a autenticação do Windows sem o ambiente de domínio. tooconnect toohello motor de base de dados de outro computador, configurar o SQL Server para a autenticação de modo misto. A autenticação em modo misto permite a Autenticação do SQL Server e a Autenticação do Windows.

> [!NOTE]
> Configurar a autenticação em modo misto poderá não ser necessário se tiver configurado uma Rede Virtual do Azure com um ambiente de domínio configurado.
> 
> 

1. Enquanto a máquina virtual de toohello ligado, na página de início de Olá, escreva **SQL Server Management Studio** e clique no ícone Olá selecionado.
   
    Olá pela primeira vez, que abra o Management Studio tem de criar ambiente do Olá utilizadores Management Studio. Esta operação poderá demorar alguns tempo.
2. Gestão Studio apresenta Olá **ligar tooServer** caixa de diálogo. No Olá **nome do servidor** caixa, tipo Olá nome Olá máquina virtual tooconnect toohello motor de base de dados com Olá Object Explorer (em vez do nome de máquina virtual de Olá também pode utilizar **(local)** ou um único período como Olá **nome do servidor**). Selecione **autenticação do Windows**e deixe  ***your_VM_name*\your_local_administrator** no Olá **nome de utilizador** caixa. Clique em **Ligar**.
   
    ![Ligar tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. No SQL Server Management Studio Object Explorer, clique no nome de Olá da instância de Olá do SQL Server (nome da máquina virtual Olá) e, em seguida, clique em **propriedades**.
   
    ![Propriedades do Servidor](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. No Olá **segurança** página **autenticação de servidor**, selecione **modo do SQL Server e a autenticação do Windows**e, em seguida, clique em **OK** .
   
    ![Selecionar Modo de Autenticação](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Na caixa de diálogo de SQL Server Management Studio Olá, clique em **OK** tooacknowledge Olá requisito toorestart do SQL Server.
6. No Object Explorer, clique com o botão direito do rato no seu servidor e, em seguida, clique em **Reiniciar** (se o SQL Server Agent estiver em execução, também terá de o reiniciar).
   
    ![Reiniciar](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Na caixa de diálogo de SQL Server Management Studio Olá, clique em **Sim** tooagree que pretende que o toorestart do SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Criar inícios de sessão de autenticação do SQL Server
tooconnect toohello motor de base de dados de outro computador, tem de criar pelo menos um início de sessão de autenticação de SQL Server.

1. No SQL Server Management Studio Object Explorer, expanda a pasta de Olá da instância de servidor Olá do qual pretende que o novo início de sessão do toocreate Olá.
2. Contexto Olá **segurança** pasta, ponto demasiado**novo**e selecione **início de sessão...** .
   
    ![Novo Início de Sessão](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. No Olá **início de sessão - novo** caixa de diálogo Olá **geral** página, introduza o nome de Olá do novo utilizador de Olá no Olá **nome de início de sessão** caixa.
4. Selecione **Autenticação do SQL Server**.
5. No Olá **palavra-passe** box, introduza uma palavra-passe para o utilizador novo Olá. Introduzir essa palavra-passe novamente na Olá **Confirmar palavra-passe** caixa.
6. Selecione as opções de imposição de palavras-passe de Olá necessárias (**impor a política de palavra-passe**, **impor a expiração de palavra-passe**, e **o utilizador deve alterar a palavra-passe no próximo início de sessão**). Se estiver a utilizar este início de sessão para si, não terá toorequire alterar uma palavra-passe no próximo início de sessão Olá.
7. De Olá **base de dados predefinida** lista, selecione uma base de dados predefinida do início de sessão Olá. **mestre** Olá predefinido para esta opção. Se ainda não criou uma base de dados do utilizador, deixe definido demasiado**mestre**.
   
    ![Propriedades do Início de Sessão](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Se este for Olá primeiro início de sessão que está a criar, poderá ser útil toodesignate este início de sessão como um administrador do SQL Server. Se assim for, em Olá **funções de servidor** página, verificação **sysadmin**.
   
   > [!NOTE]
   > Os membros Olá função servidor fixa sysadmin têm controlo total do Olá motor de base de dados. Deve restringir cuidadosamente os membros desta função.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Clique em OK.

Para obter mais informações sobre os inícios de sessão do SQL Server, veja [Criar um Início de Sessão](http://msdn.microsoft.com/library/aa337562.aspx).

