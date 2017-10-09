
1. <span data-ttu-id="06c60-101">No Olá **ligações híbridas** painel, clique da ligação híbrida Olá que acabou de criar, em seguida, clique em **a configuração do serviço de escuta**.</span><span class="sxs-lookup"><span data-stu-id="06c60-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Clique em configuração do serviço de escuta](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="06c60-103">Olá **propriedades da ligação híbrida** abre o painel.</span><span class="sxs-lookup"><span data-stu-id="06c60-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="06c60-104">Em **Gestor de ligações híbridas no local**, escolha **transferir e configurar manualmente**, guardar Olá transferido HybridConnectionManager.msi pacote e copie a cadeia de ligação de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="06c60-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Clique aqui tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="06c60-106">A partir de uma linha de comandos de administrador, escreva Olá instalador do comando toostart Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="06c60-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="06c60-107">Após Olá executa o programa de instalação, clique em **não agora**, em seguida, procure a pasta de %ProgramFiles%\Microsoft\HybridConnectionManager toohello, execute HCMConfigWizard.exe e clique em **Sim** no Olá **utilizador Controlo de conta** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="06c60-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="06c60-108">Cole Olá híbrida cadeia de ligação que copiou anteriormente e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="06c60-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![A instalar](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="06c60-110">Quando concluída a instalação de Olá, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="06c60-110">When hello install completes, click **Close**.</span></span>
   
    ![Clique em Fechar](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="06c60-112">No Olá **ligações híbridas** painel, Olá **estado** coluna mostra agora **ligado**.</span><span class="sxs-lookup"><span data-stu-id="06c60-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Estado ligado](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

