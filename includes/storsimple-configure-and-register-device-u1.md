<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de Olá tooconfigure e registar
1. Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple. Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**
2. Na sessão de Olá que se abre, prima Enter uma vez tooget numa linha de comandos. 
3. Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo. Especifique idiomas Olá e, em seguida, prima Enter. 
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. No menu da consola de série de Olá que é apresentado, escolha a opção 1 toolog com acesso total. 
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Conclua os passos 5 a 12 tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo. **Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá.** menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação. Se não estiver ligado toohello de controlador ativo, desligue e, em seguida, ligar o controlador toohello de Active Directory.
5. Na linha de comandos Olá, escreva a palavra-passe. palavra-passe de dispositivo do Olá predefinida é **Password1**.
6. Olá tipo os seguintes comandos: `Invoke-HcsSetupWizard`. 
7. Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá. Fornecer Olá Olá seguintes informações: 
   
   * Endereço IP para Olá interface rede DATA 0
   * Máscara de sub-rede
   * Gateway
   * Endereço IP do servidor DNS Primário
     
        Tenha em atenção que o sistema Olá é validar as definições de rede após cada passo no processo de Olá.
     
     > [!NOTE]
     > Poderá ter toowait alguns minutos para máscara de sub-rede Olá e as definições de DNS do Olá toobe aplicada. Se receber uma mensagem de erro de "Verificação Olá rede conectividade tooData 0", verifique a ligação de rede física Olá no Olá interface rede DATA 0 do controlador ativo.
     > 
     > 
8. (Opcional) Configure o servidor proxy Web. Apesar de a configuração do proxy Web ser opcional, **tenha em atenção que se utilizar um proxy Web, só pode configurá-lo aqui**. Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Configure um servidor NTP Primário para o seu dispositivo. Os servidores NTP são obrigatórios, uma vez que o seu dispositivo tem de sincronizar a hora para se poder autenticar junto dos fornecedores de serviços em nuvem. Certifique-se de que a sua rede permite toopass de tráfego NTP do seu centro de dados de toohello Internet. Se esta ação não for possível, especifique um servidor NTP interno. 
10. Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora. Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo. Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres. Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.
    
    <br/>![Registar o dispositivo 5 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager. Para tal, terá de chave de registo do serviço Olá que obteve no passo 2. Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.
    
    > [!NOTE]
    > Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá. Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.
    > 
    > 
    
    ![Registar o dispositivo 6 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço. Copie esta chave e guarde-a numa localização segura. **Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager.** Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá. Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto. Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C. Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração. Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.
    > 
    > 
13. Consola de série de Olá saída.
14. Devolver toohello portal clássico do Azure e concluir Olá os seguintes passos:
    
    1. Faça duplo clique em seu Olá de tooaccess do serviço StorSimple Manager **início rápido** página.
    2. Clique em **Ver dispositivos ligados**.
    3. No Olá **dispositivos** página, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá. Estado do dispositivo Olá deve ser **Online**.
       
        ![Página Dispositivos do StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Se o estado do dispositivo Olá for **Offline**, aguarde alguns minutos para Olá toocome de dispositivo online. 
       
        Se o dispositivo de Olá é continuar offline mesmo após alguns minutos, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação do StorSimple Manager serviço para o dispositivo.

