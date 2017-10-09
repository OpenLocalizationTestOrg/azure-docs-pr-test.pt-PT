<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de Olá tooconfigure e registar

1. Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple. Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**

2. Na sessão de Olá que se abre, prima **Enter** um tempo tooget numa linha de comandos.

3. Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo. Especifique o idioma Olá e, em seguida, prima **Enter**.

4. No menu da consola de série de Olá que é apresentado, selecione a opção 1 demasiado**iniciar sessão com acesso total**.
     Conclua os passos 5 a 12 tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo. **Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá.** menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação. Se não estiver ligado toohello de controlador ativo, desligue e, em seguida, ligar o controlador toohello de Active Directory.

5. Na linha de comandos Olá, escreva a palavra-passe. palavra-passe de dispositivo do Olá predefinida é **Password1**.

6. Olá tipo os seguintes comandos: `Invoke-HcsSetupWizard`.

7. Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá. Fornecer Olá Olá seguintes informações:
   
   * Endereço IP para Olá interface rede DATA 0
   * Máscara de sub-rede
   * Gateway
   * Endereço IP do servidor DNS Primário

   É apresentada uma saída de exemplo abaixo.

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    Olá anterior a saída de exemplo, pode ver que o sistema Olá é validar as definições de rede após cada passo no processo de Olá.

     > [!NOTE]
     > Poderá ter toowait alguns minutos para máscara de sub-rede Olá e as definições de DNS do Olá toobe aplicada. Se receber uma mensagem de erro de "Verificação Olá rede conectividade tooData 0", verifique a ligação de rede física Olá no Olá interface rede DATA 0 do controlador ativo.

8. (Opcional) Configure o servidor proxy Web. Apesar de a configuração do proxy Web ser opcional, **tenha em atenção que se utilizar um proxy Web, só pode configurá-lo aqui**. Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Configure um servidor NTP Primário para o seu dispositivo. Os servidores NTP são obrigatórios, uma vez que o seu dispositivo tem de sincronizar a hora para se poder autenticar junto dos fornecedores de serviços em nuvem. Certifique-se de que a sua rede permite toopass de tráfego NTP do seu centro de dados de toohello Internet. Se esta ação não for possível, especifique um servidor NTP interno.

    É apresentada abaixo uma saída de exemplo.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora. Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo. Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres. Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager do dispositivo. Para tal, terá de chave de registo do serviço Olá que obteve no passo 2. Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.
    
    > [!NOTE]
    > Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá. Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.
    
    É apresentada abaixo uma saída de exemplo.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço. Copie esta chave e guarde-a numa localização segura. **Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager do dispositivo.** Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá. Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto. Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C. Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração. Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.
    
13. Consola de série de Olá saída.
14. Devolver toohello portal do Azure e concluir Olá os seguintes passos:
    
    1. Aceda tooyour do serviço StorSimple Manager de dispositivo.
    2. Clique em **Dispositivos**.
    3. Na tabela de lista de dispositivos de Olá, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá. Estado do dispositivo Olá deve ser **pronto tooset segurança**.
       
        ![Página Dispositivos do StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Poderá ser necessário toowait para alguns minutos para toochange de estado do dispositivo Olá**pronto tooset segurança**.
       
        Se o dispositivo de Olá não for apresentada nesta lista, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação de dispositivo de serviço do Gestor de dispositivos do StorSimple.

