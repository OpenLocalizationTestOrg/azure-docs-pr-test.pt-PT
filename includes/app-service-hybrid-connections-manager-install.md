
1. No Olá **ligações híbridas** painel, clique da ligação híbrida Olá que acabou de criar, em seguida, clique em **a configuração do serviço de escuta**.
   
    ![Clique em configuração do serviço de escuta](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Olá **propriedades da ligação híbrida** abre o painel. Em **Gestor de ligações híbridas no local**, escolha **transferir e configurar manualmente**, guardar Olá transferido HybridConnectionManager.msi pacote e copie a cadeia de ligação de gateway Olá.
   
    ![Clique aqui tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. A partir de uma linha de comandos de administrador, escreva Olá instalador do comando toostart Olá os seguintes:
   
        start HybridConnectionManager.msi
4. Após Olá executa o programa de instalação, clique em **não agora**, em seguida, procure a pasta de %ProgramFiles%\Microsoft\HybridConnectionManager toohello, execute HCMConfigWizard.exe e clique em **Sim** no Olá **utilizador Controlo de conta** caixa de diálogo.
5. Cole Olá híbrida cadeia de ligação que copiou anteriormente e clique em **OK**. 
   
    ![A instalar](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Quando concluída a instalação de Olá, clique em **fechar**.
   
    ![Clique em Fechar](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    No Olá **ligações híbridas** painel, Olá **estado** coluna mostra agora **ligado**. 
   
    ![Estado ligado](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

