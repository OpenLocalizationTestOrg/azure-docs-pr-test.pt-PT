<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall correções regular através do Windows PowerShell para StorSimple
1. Ligar a consola de série do dispositivo de toohello. Para obter mais informações, consulte [passo 1: ligar a consola de série toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**. Escrever Olá palavra-passe. palavra-passe predefinida de Olá é **Password1**.
3. Na linha de comandos Olá, escreva:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Este comando aplica-se apenas tooregular correções. Execute este comando em apenas um controlador, mas serão atualizados em ambos os controladores.
    > Poderá notar uma ativação pós-falha controlador durante o processo de atualização de Olá; No entanto, ativação pós-falha de Olá não irá afetar a disponibilidade de sistema ou a operação.

4. Quando lhe for pedido, forneça Olá caminho toohello pasta de rede partilhada que contém ficheiros de correções Olá.
5. Será solicitado para confirmação. Tipo **Y** tooproceed com a instalação da correção de Olá.

