<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de Olá tooconfigure e registar
1. Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple. Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**
2. Na sessão de Olá que se abre, prima Enter uma vez tooget numa linha de comandos. 
3. Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo. Especifique idiomas Olá e, em seguida, prima Enter. 
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. No menu da consola de série de Olá que é apresentado, escolha a opção 1 toolog com acesso total. 
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Conclua os passos 5 a 12 tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo. **Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá.** menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação. Se não estiver ligado toohello de controlador ativo, desligue e, em seguida, ligar o controlador toohello de Active Directory.
5. Na linha de comandos Olá, escreva a palavra-passe. palavra-passe de dispositivo do Olá predefinida é **Password1**.
6. Escreva Olá os seguintes comandos:
   
     `Invoke-HcsSetupWizard` 
7. Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá. Fornecer Olá Olá seguintes informações: 
   
   * Endereço IP para Olá interface rede DATA 0
   * Máscara de sub-rede
   * Gateway
   * Endereço IP do servidor DNS Primário
   * Endereço IP do servidor NTP Primário
     
     > [!NOTE]
     > Poderá ter toowait alguns minutos para máscara de sub-rede Olá e as definições de DNS do Olá toobe aplicada. Se obtiver um "Olá dispositivo não está pronto." mensagem de erro, de ligação de rede física de Olá do verificação no Olá interface rede DATA 0 do controlador ativo.
     > 
     > 
8. (Opcional) Configure o servidor proxy Web. Apesar de a configuração do proxy Web ser opcional, **tenha em atenção que se utilizar um proxy Web, só pode configurá-lo aqui**. Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). Caso se depare com problemas durante este passo, consulte a documentação de orientação tootroubleshooting para [erros durante a configuração do proxy web](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá. As definições que aplicou antes de emitir este comando serão mantidas.

1. Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange-la nas sessões subsequentes. Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo. Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres. palavra-passe de Olá tem de conter uma combinação de carateres minúsculos, carateres em maiúsculas, números e carateres especiais.
2. palavra-passe do Olá Snapshot Manager do StorSimple também é definida aqui. Utilize esta palavra-passe quando autenticar um dispositivo com o anfitrião do Windows a executar o Snapshot Manager do StorSimple. Quando solicitado, forneça uma palavra-passe do 14 too15 caráter. Olá palavra-passe tem de conter uma combinação de três das seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais. 
   
   ![Registar o dispositivo 4 do StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Só pode repor a palavra-passe de Olá Snapshot Manager do StorSimple da interface de serviço do StorSimple Manager Olá. Para obter passos detalhados, consulte demasiado[alterar Olá StorSimple as palavras-passe utilizando Olá do serviço StorSimple Manager](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot quaisquer problemas durante este passo, consulte tootroubleshooting orientações para [erros relacionados com toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager. Para tal, terá de chave de registo do serviço Olá que obteve no passo 2. Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.
   
   tootroubleshoot eventuais falhas de registo do dispositivo possíveis, consulte demasiado[erros durante o registo de dispositivo](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Para resolução de problemas detalhada, também pode consultar demasiado[exemplo passo a passo de resolução de problemas](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço. Copie esta chave e guarde-a numa localização segura.
   
   > [!WARNING]
   > Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager. Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.
   > 
   > 
   
    ![Registar o dispositivo 6 do StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá. Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto. Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C. Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração. Como resultado, palavra-passe de administrador de dispositivo Olá e a palavra-passe do Olá Snapshot Manager do StorSimple não serão alteradas e dispositivo Olá irá reverter as de palavras-passe toohello predefinido.
5. Consola de série de Olá saída.
6. Devolver toohello portal clássico do Azure e concluir Olá os seguintes passos:
   
   1. Faça duplo clique em seu Olá de tooaccess do serviço StorSimple Manager **início rápido** página.
   2. Clique em **Ver dispositivos ligados**.
   3. No Olá **dispositivos** página, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá. Estado do dispositivo Olá deve ser **Online**. Se o estado do dispositivo Olá for **Offline**, aguarde alguns minutos para Olá toocome de dispositivo online.
   
   ![Página Dispositivos do StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Depois do dispositivo de Olá estiver online, ligue os cabos de rede de Olá que tinha desligado no início Olá deste passo.
   > 
   > 

Depois do dispositivo de Olá for registado com êxito e não ficar online, pode executar Olá `Test-HcsmConnection -Verbose` tooensure Olá conectividade de rede está em bom estado. Para Olá utilização detalhada deste cmdlet, visite demasiado[referência de cmdlets para Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Vídeo disponível](./media/storsimple-configure-and-register-device/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como tooconfigure e registar o dispositivo através do Windows PowerShell para StorSimple, clique em [aqui](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

