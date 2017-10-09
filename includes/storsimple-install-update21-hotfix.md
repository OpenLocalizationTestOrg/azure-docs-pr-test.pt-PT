<!--author=alkohli last changed: 05/19/16-->

#### <a name="toodownload-hotfixes"></a>correções toodownload
Efetue Olá seguintes passos toodownload Olá atualização de software de Olá catálogo Microsoft Update.

1. Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.
    ![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload, por exemplo **3179904**e, em seguida, clique em **pesquisa**.
   
    Olá listagem de correção é apresentado, por exemplo, **cumulativa 2.2 atualização do pacote de Software para a série de 8000 do StorSimple**.
   
    ![Catálogo de pesquisa](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Clique em **Adicionar**. atualização de Olá está adicionada toohello cesto.
5. Procure as correções adicionais listados na tabela de Olá acima (**3103616**, **3146621**) e adicione cada cesto toohello.
6. Clique em **Ver Cesto**.
7. Clique em **Transferir**. Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear. Olá as atualizações são transferidas toohello especificada a localização e colocada numa pasta com o mesmo nome como atualização Olá de Olá secundárias. pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.

> [!NOTE]
> Correções de Olá devem ser acessíveis a ambos os toodetect controladores mensagens de quaisquer potenciais erros de controlador de ponto a ponto Olá.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall e certifique-se correções modo normal
Efetuar Olá tooinstall passos a seguir e certifique-se correções modo normal. Se já instalou utilizando Olá Portal do Azure, avançar diretamente demasiado[instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall Olá correções, interface do Windows PowerShell de Olá de acesso na consola de série do dispositivo StorSimple. Siga instruções de detalhado Olá [consola de série utilizar o PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Na linha de comandos Olá, prima **Enter**.
2. Selecione **opção 1** toolog no dispositivo toohello com acesso total. Recomendamos que instale a correção de Olá no controlador passivo Olá primeiro.
3. correção de Olá tooinstall, na linha de comandos Olá, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilize o IP, em vez de DNS no caminho de partilha no Olá acima comando. parâmetro de credencial de Olá só é utilizado se aceder a uma partilha autenticada.
   
    Recomendamos que utilize partilhas de tooaccess de parâmetro de credencial de Olá. Mesmo partilhas que estão abertas demasiado "todos os utilizadores" são, normalmente, não abrir toounauthenticated utilizadores.
   
    Forneça a palavra-passe Olá quando lhe for pedido.
   
    É apresentada abaixo uma saída de exemplo.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Tipo **Y** quando o pedido tooconfirm Olá instalação de correção.
   
   > [!IMPORTANT]
   > Se instalar a atualização 2.2, só a instalar o ficheiro binário Olá precedido pela 'all-hcsmdssoftwareudpate'. Não instale Olá Cis e Olá MDS a atualização do agente precedida pela all cismdsagentupdatebundle. Falha toodo, por isso, resultará num erro. 

5. Monitorizar Olá update utilizando Olá `Get-HcsUpdateStatus` cmdlet. atualização Olá primeiro irá concluir num controlador de Olá passiva. Depois do controlador passivo Olá é atualizada, existirá uma ativação pós-falha e atualização Olá, em seguida, irão ser aplicada em Olá outro controlador. atualização de Olá está concluída quando ambos os controladores de Olá são atualizados.
   
    Olá saída de exemplo seguinte mostra Olá atualização em curso. Olá `RunInprogress` será `True` quando Olá atualização se encontra em curso.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída. Olá `RunInProgress` será `False` quando a atualização de Olá foi concluída.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > Ocasionalmente, Olá cmdlet relatórios `False` quando atualização Olá ainda está em curso. tooensure Olá correção está concluída, aguarde alguns minutos, execute novamente este comando e certifique-se de que Olá `RunInProgress` é `False`. Se estiver, Olá correção foi concluída.

1. Após a conclusão da atualização de software Olá, verifique as versões de software do sistema Olá. Escreva:
   
    `Get-HcsSystem`
   
    Deverá ver Olá seguintes versões:
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     Se os números de versão de Olá não alterar depois de aplicar a atualização de Olá, indica que correção Olá tooapply falhou. Se tal acontecer, entre em contacto com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter assistência.
     
     > [!IMPORTANT]
     > Tem de reiniciar o controlador de Active Directory Olá através de Olá `Restart-HcsController` cmdlet antes de aplicar Olá restantes atualizações. 
     > 
     > 
2. Repita os passos 3 a 5 tooinstall Olá restantes correções modo normal.
   
   * atualização de iSCSI Olá KB3146621
   * atualização WMI Olá KB3103616
3. Ignore este passo se estão a atualizar a partir da atualização 2. Se estão a atualizar a partir de um tooUpdate anterior da versão 2, terá também de toodownload:

    - controlador Olá LSI KB3121900

    - atualização de Spaceport Olá KB3090322

    - atualização de Storport Olá KB3080728

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall e certifique-se correções do modo de manutenção
Utilize as atualizações de firmware do KB3121899 tooinstall disco. Estas atualizações acontece e tomar toocomplete cerca de 30 minutos. Pode escolher tooinstall estes numa janela de manutenção planeada por consola ligação de série do dispositivo toohello.

Tenha em atenção que se o firmware do disco já se encontra atualizado, não terá de tooinstall estas atualizações. Executar Olá `Get-HcsUpdateAvailability` cmdlet a partir da consola de série de dispositivo do Olá toocheck se as atualizações estão disponíveis e se Olá atualiza tem acontece (modo de manutenção) ou não acontece (modo normal) atualizações.

atualizações de firmware do tooinstall Olá disco, siga as instruções de Olá abaixo.

1. Colocar o dispositivo de Olá em modo de manutenção de Olá. Tenha em atenção que não deve utilizar a comunicação remota do Windows PowerShell ao ligar o dispositivo de tooa no modo de manutenção. Em vez disso, execute este cmdlet no controlador de dispositivo Olá quando estiver ligado através da consola de série do dispositivo de Olá. Escreva:
   
    `Enter-HcsMaintenanceMode`
   
    É apresentada abaixo uma saída de exemplo.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Em seguida, reinicie os dois controladores de Olá no modo de manutenção.
2. atualização de firmware de disco por Olá tooinstall, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    É apresentada abaixo uma saída de exemplo.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitor Olá instalar progresso com `Get-HcsUpdateStatus` comando. Olá atualização estiver concluída quando hello `RunInProgress` alterações demasiado`False`.
4. Depois de concluída a instalação de Olá, reinicia o controlador de Olá no qual Olá foi instalada a correção de modo de manutenção. Inicie sessão como opção 1 com acesso total e verificar a versão de firmware do disco Olá. Escreva:
   
   `Get-HcsFirmwareVersion`
   
   Olá esperado versões de firmware do disco são:
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   É apresentada abaixo uma saída de exemplo.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    Executar Olá `Get-HcsFirmwareVersion` comando em tooverify controlador segundo Olá que Olá versão do software foi atualizado. Modo de manutenção de Olá, em seguida, pode sair. toodo por isso, escreva Olá seguinte comando para cada controlador de dispositivo:
   
   `Exit-HcsMaintenanceMode`
5. os controladores de Olá reinicie quando sair do modo de manutenção. Depois de firmware de disco Olá atualizações são aplicadas com êxito e o dispositivo de Olá saiu do modo de manutenção, toohello retorno portal clássico do Azure. Tenha em atenção que portal Olá poderá não mostrar que instalou as atualizações de modo de manutenção Olá durante 24 horas.

