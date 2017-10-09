<!--author=SharS last changed: 06/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de Olá tooconfigure e registar
1. Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple. Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**
2. Na sessão de Olá que se abre, prima **Enter** um tempo tooget numa linha de comandos.
3. Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo. Especifique o idioma Olá e, em seguida, prima **Enter**.
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. No menu da consola de série de Olá que é apresentado, escolha a opção 1 toolog com acesso total.
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Efetue Olá os seguintes passos tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo.
   
   > [!IMPORTANT]
   > Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá. menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação. Se não são ligar toohello de controlador ativo, desligue e, em seguida, ligar o controlador de Active Directory toohello.
   
   1. Na linha de comandos Olá, escreva a palavra-passe. palavra-passe de dispositivo do Olá predefinida é **Password1**.
   2. Escreva Olá os seguintes comandos:
      
        `Invoke-HcsSetupWizard`
   3. Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá. Fornecer Olá seguintes informações:
      
      * Endereço de IP da interface rede DATA 0
      * Máscara de sub-rede
      * Gateway
      * Endereço IP do servidor DNS Primário
      * Endereço IP do servidor NTP Primário
      
      > [!NOTE]
      > Poderá ter toowait alguns minutos para máscara de sub-rede Olá e toobe de definições de DNS aplicada.
    
   4. Opcionalmente, configure o servidor proxy web.
      
      > [!IMPORTANT]
      > Apesar da configuração de proxy web é opcional, lembre-se de que se utilizar um proxy web, só pode configurá-lo aqui. Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
     
6. Prima Ctrl + C Assistente de configuração de Olá tooexit.
8. Execute Olá seguir o portal do Microsoft Azure Government de cmdlet toopoint Olá dispositivos toohello (porque aponta portal clássico do Azure público toohello por predefinição). Esta ação irá reiniciar tanto os controladores. Recomendamos que utilize sessões PuTTY dois toosimultaneously ligar tooboth controladores para que possa ver quando cada controlador é reiniciado.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Verá uma mensagem de confirmação. Aceite a predefinição de Olá (**Y**).
9. Execute Olá cmdlet tooresume configuração os seguintes:
   
    `Invoke-HcsSetupWizard`
   
    ![Assistente de configuração de retomar](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
10. Aceite as definições de rede Olá. Verá uma mensagem de validação após a aceitação de cada definição.
11. Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora. Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo. Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres. Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.
    
    <br/>![Registar o dispositivo 5 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager do dispositivo. Para tal, será necessário Olá, chave de registo do serviço que obteve no [passo 2: chave de registo do serviço de Olá Get](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.
    
    > [!NOTE]
    > Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá. Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.
    
    ![Progresso de registo do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço. Copie esta chave e guarde-a numa localização segura. **Esta chave é necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager do dispositivo.** Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-8000-security.md) para obter mais informações sobre esta chave.
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)
    > [!IMPORTANT]
    > texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá. Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto.
    > 
    > Não utilize **Ctrl + C** chave de encriptação de dados de serviço Olá toocopy. Utilizar **Ctrl + C** fará com que o Assistente de configuração do Olá tooexit. Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.
    
14. Consola de série de Olá saída.
15. Devolver toohello Portal do Azure Government e concluir Olá os seguintes passos:
    
    1. Aceda tooyour do serviço StorSimple Manager de dispositivo.
    2. Clique em **Dispositivos**. Na lista de Olá dos dispositivos, identifica o dispositivo de Olá que são ddeploying. Certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá. Estado do dispositivo Olá deve ser **Online**.
            
        Se o estado do dispositivo Olá for **Offline**, aguarde alguns minutos para Olá toocome de dispositivo online.
       
        Se o dispositivo de Olá é continuar offline mesmo após alguns minutos, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).
       
        Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação do Gestor de dispositivos do StorSimple serviço para o dispositivo.

