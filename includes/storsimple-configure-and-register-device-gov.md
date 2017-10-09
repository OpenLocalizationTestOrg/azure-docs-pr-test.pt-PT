<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de Olá tooconfigure e registar
1. Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple. Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**
2. Na sessão de Olá que se abre, prima Enter uma vez tooget numa linha de comandos. 
3. Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo. Especifique idiomas Olá e, em seguida, prima Enter. 
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. No menu da consola de série de Olá que é apresentado, escolha a opção 1 toolog com acesso total. 
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. Efetue Olá os seguintes passos tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo.
   
   > [!IMPORTANT]
   > Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá. menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação. Se não são ligar toohello de controlador ativo, desligue e, em seguida, ligar o controlador de Active Directory toohello.
   > 
   > 
   
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
      > 
      > 
   4. Opcionalmente, configure o servidor proxy web.
      
      > [!IMPORTANT]
      > Apesar da configuração de proxy web é opcional, lembre-se de que se utilizar um proxy web, só pode configurá-lo aqui. Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). 
      > 
      > 
6. Prima Ctrl + C Assistente de configuração de Olá tooexit.
7. Instale atualizações de Olá da seguinte forma:
   
   1. Utilize Olá os seguintes cmdlet tooset IPs em ambos os controladores de Olá:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. Na linha de comandos Olá, execute `Get-HcsUpdateAvailability`. Devem ser notificados que atualizações estão disponíveis.
   3. Execute `Start-HcsUpdate`. Pode executar este comando em qualquer nó. Actualizações serão aplicadas no primeiro controlador de Olá, controlador Olá irá efetuar a ativação pós-falha e, em seguida, Olá actualizações serão aplicadas no Olá outro controlador.
      
      Poderá monitorizar Olá progresso da atualização de Olá executando `Get-HcsUpdateStatus`.    
      
      Olá saída de exemplo seguinte mostra Olá atualização em curso.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída.
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      Esta operação pode demorar horas too11 tooapply Olá todas as atualizações, incluindo Olá atualizações do Windows.

8. Após todos os hello atualizações são instaladas com êxito, hello execute seguintes cmdlet tooconfirm que Olá foram corretamente aplicadas as atualizações de software:
   
     `Get-HcsSystem`
   
    Deverá ver Olá seguintes versões:
   
   * HcsSoftwareVersion: 6.3.9600.17491
   * CisAgentVersion: 1.0.9037.0
   * MdsAgentVersion: 26.0.4696.1433
9. Olá execute os seguintes cmdlet tooconfirm que Olá atualização de firmware foi aplicado corretamente:
   
    `Start-HcsFirmwareCheck`.
   
     Estado do firmware Olá deve ser **UpToDate**.
10. Execute Olá seguir o portal do Microsoft Azure Government de cmdlet toopoint Olá dispositivos toohello (porque aponta portal clássico do Azure público toohello por predefinição). Esta ação irá reiniciar tanto os controladores. Recomendamos que utilize sessões PuTTY dois toosimultaneously ligar tooboth controladores para que possa ver quando cada controlador é reiniciado.
    
     `Set-CloudPlatform -AzureGovt_US`
    
    Verá uma mensagem de confirmação. Aceite a predefinição de Olá (**Y**).
11. Execute Olá cmdlet tooresume configuração os seguintes:
    
     `Invoke-HcsSetupWizard`
    
     ![Assistente de configuração de retomar](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    Quando retomar a configuração, o Assistente de Olá será versão Olá atualização 1 (o que corresponde tooversion 17469). 
12. Aceite as definições de rede Olá. Verá uma mensagem de validação após a aceitação de cada definição.
13. Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora. Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo. Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres. Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.
    
    <br/>![Registar o dispositivo 5 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager. Para tal, será necessário Olá, chave de registo do serviço que obteve no [passo 2: chave de registo do serviço de Olá Get](#step-2-get-the-service-registration-key). Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.
    
    > [!NOTE]
    > Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá. Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.
    > 
    > 
    
    ![Progresso de registo do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço. Copie esta chave e guarde-a numa localização segura. **Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager.** Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá. Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto. 
    > 
    > Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C. Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração. Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.
    > 
    > 
16. Consola de série de Olá saída.
17. Devolver toohello Portal do Azure Government e concluir Olá os seguintes passos:
    
    1. Faça duplo clique em seu Olá de tooaccess do serviço StorSimple Manager **início rápido** página.
    2. Clique em **Ver dispositivos ligados**.
    3. No Olá **dispositivos** página, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá. Estado do dispositivo Olá deve ser **Online**.
       
        ![Página Dispositivos do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        Se o estado do dispositivo Olá for **Offline**, aguarde alguns minutos para Olá toocome de dispositivo online. 
       
        Se o dispositivo de Olá é continuar offline mesmo após alguns minutos, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação de serviço para o dispositivo StorSimple Manager.

