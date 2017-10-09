<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>correções toodownload
Efetue Olá os seguintes passos toodownload Olá atualização de software.

1. Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.
    ![Instalar o catálogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload, por exemplo **3063418**e, em seguida, clique em **pesquisa**.
4. Verá Olá **StorSimple atualização 1.2 aplicação atualização** pacote. Clique em **Adicionar**. atualização de Olá será adicionada toohello cesto.
5. Procure as correções adicionais listados na tabela de Olá acima (**3043005** e **3063416**) e adicione cada cesto Olá.
6. Clique em **Ver Cesto**.
   
    ![Ver cesto](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Clique em **Transferir**. Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear. Olá as atualizações são transferidas toohello especificada a localização e colocada numa subpasta com o mesmo nome como atualização Olá de Olá. pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.

> [!NOTE]
> Correções de Olá devem ser acessíveis a ambos os toodetect controladores mensagens de quaisquer potenciais erros de controlador de ponto a ponto Olá.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall e certifique-se correções modo normal
Efetuar Olá tooinstall passos a seguir e certifique-se Olá regular modo correções. Se já instalou utilizando Olá Portal do Azure, avançar diretamente demasiado[instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall Olá de atualização de software, interface do Windows PowerShell de Olá de acesso na consola de série do dispositivo StorSimple. Siga instruções de detalhado Olá [consola de série utilizar o PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Na linha de comandos Olá, prima **Enter**.
2. Selecione **opção 1** toolog no dispositivo toohello com acesso total.
3. tooinstall Olá pacote de atualização, na linha de comandos Olá, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilize o IP, em vez de DNS no caminho de partilha no Olá acima comando. parâmetro de credencial de Olá só é utilizado se aceder a uma partilha autenticada.
   
    Recomendamos que utilize partilhas de tooaccess de parâmetro de credencial de Olá. Mesmo partilhas que estão abertas demasiado "todos os utilizadores" são, normalmente, não abrir toounauthenticated utilizadores.
   
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
5. Monitorizar Olá update utilizando Olá `Get-HcsUpdateStatus` cmdlet.
   
    Olá saída de exemplo seguinte mostra Olá atualização em curso. Olá `RunInprogress` será `True` quando Olá atualização se encontra em curso.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída. Olá `RunInProgress` será `False` quando a atualização de Olá foi concluída.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > Ocasionalmente, Olá cmdlet relatórios `False` quando atualização Olá ainda está em curso. tooensure Olá correção está concluída, aguarde alguns minutos, execute novamente este comando e certifique-se de que Olá `RunInProgress` é `False`. Se estiver, Olá correção foi concluída.
   > 
   > 
6. Após a conclusão da atualização de software Olá, verifique as versões de software do sistema Olá. Escreva Olá os seguintes comandos:
   
    `Get-HcsSystem`
   
    Deverá ver Olá seguintes versões:
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Se os números de versão de Olá não alterar depois de aplicar a atualização de Olá, indica que correção Olá tooapply falhou. Se tal acontecer, entre em contacto com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter assistência.
7. Repita os passos 3 a 5 tooinstall Olá restantes correção de modo de regular (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall e certifique-se correções do modo de manutenção
Utilize as atualizações de firmware do KB3063416 tooinstall disco. Estas atualizações acontece e tome em torno toocomplete 30 45 minutos. Pode escolher tooinstall estes numa janela de manutenção planeada por consola ligação de série do dispositivo toohello.

atualizações de firmware do tooinstall Olá disco, siga as instruções de Olá abaixo.

1. Colocar o dispositivo Olá no modo de manutenção. Tenha em atenção que não deve utilizar a comunicação remota do Windows PowerShell ao ligar o dispositivo de tooa no modo de manutenção. Terá de toorun este cmdlet no controlador de dispositivo Olá quando estiver ligado através da consola de série do dispositivo de Olá. Escreva:
   
    `Enter-HcsMaintenanceMode`
   
    É apresentada abaixo uma saída de exemplo.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitor Olá instalar progresso com `Get-HcsUpdateStatus` comando. Olá atualização estiver concluída quando hello `RunInProgress` alterações demasiado`False`.
4. Depois de concluída a instalação de Olá, será reiniciada controlador Olá em que a correção de modo de manutenção de Olá foi instalada. Inicie sessão como opção 1 com acesso total e verificar a versão de firmware do disco Olá. Escreva:
   
   `Get-HcsFirmwareVersion`
   
   Olá esperado versões de firmware do disco são:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Executar Olá `Get-HcsFirmwareVersion` comando em tooverify controlador segundo Olá que Olá versão do software foi atualizado. Modo de manutenção de Olá, em seguida, pode sair. Escreva o seguinte comando para cada controlador de dispositivo de Olá:
   
   `Exit-HcsMaintenanceMode`
5. os controladores de Olá reinicie quando sair do modo de manutenção. Depois de firmware de disco Olá atualizações são aplicadas com êxito e o dispositivo de Olá saiu do modo de manutenção, toohello retorno portal clássico do Azure. Tenha em atenção que portal Olá poderá não mostrar que instalou as atualizações de modo de manutenção Olá durante 24 horas.

