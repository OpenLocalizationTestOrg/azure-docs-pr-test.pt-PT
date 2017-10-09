<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall correções do modo de manutenção através do Windows PowerShell para StorSimple
> [!IMPORTANT]
> No modo de manutenção, precisa tooapply Olá correção pela primeira vez num controlador e, em seguida, no Olá outro controlador.
> 
> 

1. Coloque o dispositivo de Olá no modo de manutenção. Consulte [passo 2: modo de manutenção introduza](../articles/storsimple/storsimple-update-device.md#step2) para obter instruções sobre como tooenter modo de manutenção.
2. correção do Olá tooapply, tipo:
   
     `Start-HcsHotfix` 
3. Quando lhe for pedido, forneça Olá caminho toohello pasta de rede partilhada que contém ficheiros de correções Olá.
4. Será solicitado para confirmação. Tipo **Y** tooproceed com a instalação da correção de Olá.
5. Após aplicou Olá correção num controlador, de início de sessão toohello outro controlador. Aplica a correção de Olá como fez para o controlador de Olá anterior.
6. Depois de Olá correções são aplicadas, saia do modo de manutenção. Consulte [passo 4: modo de manutenção de saída](../articles/storsimple/storsimple-update-device.md#step4) para obter instruções.

