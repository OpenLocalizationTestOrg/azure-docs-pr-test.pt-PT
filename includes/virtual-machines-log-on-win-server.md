1. Clicar em **Ligar** cria e transfere um ficheiro do protocolo RDP (ficheiro .rdp). Clique em **abra** toouse este ficheiro.
2. Irá receber um aviso que Olá RDP é de um publicador desconhecido. É uma situação normal. Na janela de ambiente de trabalho remoto Olá, clique em **Connect** toocontinue.
   
    ![Captura de ecrã de um aviso sobre um publicador desconhecido.](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. No Olá **segurança do Windows** janela, escreva Olá as credenciais para uma conta de máquina virtual de Olá e, em seguida, clique em **OK**.
   
     **Conta local** -trata-se normalmente conta local Olá nome de utilizador e palavra-passe que especificou quando criou Olá máquina virtual. Neste caso, o domínio de Olá é o nome de Olá da máquina virtual de Olá e é introduzido como *vmname*&#92; *nome de utilizador*.  
   
    **VM associada ao domínio** - se Olá VM pertence tooa domínio, introduza o nome de utilizador Olá no formato de Olá *domínio*&#92; *Nome de utilizador*. Olá conta também tem de tooeither ser na Olá administradores grupo ou terem sido concedido privilégios de acesso remoto toohello VM.
   
    **Controlador de domínio** - se Olá VM for um controlador de domínio, o nome de utilizador do tipo Olá e a palavra-passe de uma conta de administrador de domínio desse domínio.
4. Clique em **Sim** tooverify Olá identidade da máquina virtual de Olá e concluir o início de sessão.
   
   ![Captura de ecrã que mostra uma mensagem sobre a confirmação identidade Olá Olá VM.](./media/virtual-machines-log-on-win-server/cert-warning.png)

