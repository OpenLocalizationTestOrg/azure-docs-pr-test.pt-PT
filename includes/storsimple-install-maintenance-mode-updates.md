<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>atualizações de modo de manutenção tooinstall através do Windows PowerShell para StorSimple
1. Se não tiver o feito, aceder à consola de série do dispositivo de Olá e selecione opção 1, **iniciar sessão com acesso total**. 
2. Escrever Olá palavra-passe. palavra-passe predefinida de Olá é **Password1**.
3. Na linha de comandos Olá, escreva:
   
     `Get-HcsUpdateAvailability` 
4. Será notificado se as atualizações estiverem disponíveis e se as atualizações de Olá são acontece ou não acontece. as atualizações acontece tooapply, terá de dispositivo de Olá tooput no modo de manutenção. Consulte [passo 2: modo de manutenção introduza](../articles/storsimple/storsimple-update-device.md#step2) para obter instruções.
5. Quando o dispositivo está no modo de manutenção, Olá linha de comandos, escreva:`Start-HcsUpdate`
6. Será solicitado para confirmação. Depois de confirmar atualizações Olá, irá ser instalados num controlador de Olá que atualmente estão a aceder. Depois de instalar as atualizações de Olá, controlador Olá será reiniciado. 
7. Monitorizar o estado de Olá das atualizações. Escreva:
   
    `Get-HcsUpdateStatus`
   
    Se hello `RunInProgress` é `True`, atualização Olá ainda está em curso. Se `RunInProgress` é `False`, ele indica que a atualização Olá foi concluída.  
8. Quando a atualização Olá está instalada num controlador de Olá atual e foi reiniciado, ligue toohello outro controlador e efetuar os passos 1 a 6.
9. Depois de ambos os controladores foram atualizados, saia do modo de manutenção. Consulte [passo 4: modo de manutenção de saída](../articles/storsimple/storsimple-update-device.md#step4) para obter instruções.

