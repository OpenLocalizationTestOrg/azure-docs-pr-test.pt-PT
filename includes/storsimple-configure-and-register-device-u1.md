<!--author=alkohli last changed: 02/22/2016-->


### <a name="to-configure-and-register-the-device"></a>Para configurar e registar o dispositivo
1. Aceda à interface do Windows PowerShell na consola de série do dispositivo StorSimple. Para obter as instruções, veja [Utilizar o PuTTY para ligar à consola de série do dispositivo](#use-putty-to-connect-to-the-device-serial-console). **Confirme que está a seguir o procedimento rigorosamente. Caso contrário, não conseguirá aceder à consola.**
2. Na sessão apresentada, prima Enter uma vez para obter uma linha de comandos. 
3. Ser-lhe-á solicitado que escolha o idioma que pretende configurar para o dispositivo. Especifique o idioma e prima Enter. 
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. No menu da consola de série apresentado, selecione a opção 1 para iniciar sessão com acesso total. 
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Execute os passos 5 a 12 para configurar as definições de rede mínimas necessárias para o dispositivo. **Estes passos de configuração têm de ser executados no controlador ativo do dispositivo.** O menu da consola de série indica o estado do controlador na mensagem de faixa. Se não estiver ligado ao controlador ativo, desligue e volte a ligar ao controlador ativo.
5. Na linha de comandos, escreva a sua palavra-passe. A palavra-passe predefinida do dispositivo é **Password1**.
6. Escreva o seguinte comando: `Invoke-HcsSetupWizard`. 
7. Será apresentado um assistente de configuração para o ajudar a configurar as definições de rede do dispositivo. Forneça as seguintes informações: 
   
   * Endereço IP da interface de rede DATA 0
   * Máscara de sub-rede
   * Gateway
   * Endereço IP do servidor DNS Primário
     
        Tenha em atenção que o sistema está a validar as definições de rede após cada passo no processo.
     
     > [!NOTE]
     > Poderá ter de aguardar alguns minutos para que sejam aplicadas as definições de DNS e de máscara de sub-rede. Se obtiver uma mensagem de erro “Verifique a conetividade de rede a DATA 0”, verifique a ligação de rede física na interface da rede DATA 0 do controlador ativo.
     > 
     > 
8. (Opcional) Configure o servidor proxy Web. Apesar de a configuração do proxy Web ser opcional, **tenha em atenção que se utilizar um proxy Web, só pode configurá-lo aqui**. Para obter mais informações, veja [Configure web proxy for your device (Configurar o proxy Web para o seu dispositivo)](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Configure um servidor NTP Primário para o seu dispositivo. Os servidores NTP são obrigatórios, uma vez que o seu dispositivo tem de sincronizar a hora para se poder autenticar junto dos fornecedores de serviços em nuvem. Verifique se a sua rede permite que o tráfego NTP passe do datacenter para a Internet. Se esta ação não for possível, especifique um servidor NTP interno. 
10. Por motivos de segurança, a palavra-passe de administrador do dispositivo expira após a primeira sessão e terá de a alterar agora. Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo. Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres. A palavra-passe tem de conter três dos seguintes: minúsculas, maiúsculas, números e carateres especiais.
    
    <br/>![Registar o dispositivo 5 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. O último passo do assistente de configuração regista o dispositivo com o serviço StorSimple Manager. Para o poder fazer, precisa da chave de registo do serviço obtida no passo 2. Depois de fornecer a chave de registo, poderá ter de aguardar 2 a 3 minutos até o dispositivo ficar registado.
    
    > [!NOTE]
    > Pode premir Ctrl + C em qualquer momento para sair do assistente de configuração. Se tiver introduzido todas as definições de rede (Endereço IP para Data 0, Máscara de sub-rede e Gateway), as entradas serão mantidas.
    > 
    > 
    
    ![Registar o dispositivo 6 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Uma vez registado o dispositivo, aparecerá uma chave de Encriptação de Dados do Serviço. Copie esta chave e guarde-a numa localização segura. **Esta chave será necessária com a chave de registo do serviço para registar dispositivos adicionais com o serviço StorSimple Manager.** Veja [Segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > Para copiar o texto da janela da consola de série, basta selecioná-lo. Em seguida, poderá colá-lo na área de transferência ou num editor de texto. NÃO utilize Ctrl + C para copiar a chave de encriptação de dados do serviço. A utilização de Ctrl + C fecha o assistente de configuração. Como resultado, a palavra-passe de administrador do dispositivo não será alterada e o dispositivo irá reverter para a palavra-passe predefinida.
    > 
    > 
13. Feche a consola de série.
14. Regresse ao Portal Clássico do Azure e execute os seguintes passos:
    
    1. Faça duplo clique no serviço StorSimple Manager para aceder à página **Início Rápido**.
    2. Clique em **Ver dispositivos ligados**.
    3. Na página **Dispositivos**, verifique se o dispositivo foi ligado com êxito ao serviço, vendo o seu estado. O estado do dispositivo deve ser **Online**.
       
        ![Página Dispositivos do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Se o estado do dispositivo for **Offline**, aguarde alguns minutos para que o dispositivo fique online. 
       
        Se o dispositivo continuar offline mesmo após alguns minutos, terá então de verificar se a sua rede de firewall foi configurada do modo descrito em [Requisitos de rede para o seu dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Verifique se a porta 9354 está aberta para comunicação de saída, uma vez que é utilizada pelo barramento de serviço para a comunicação Serviço a dispositivo do StorSimple Manager.

