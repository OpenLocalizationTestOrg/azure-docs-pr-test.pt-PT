<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>tooinstall atualizações regulares através do Windows PowerShell para StorSimple
1. Abra a consola de série do dispositivo de Olá e selecione opção 1, **iniciar sessão com acesso total**. Escrever Olá palavra-passe. palavra-passe predefinida de Olá é *Password1*. 
2. Na linha de comandos Olá, escreva:
   
     `Get-HcsUpdateAvailability`
   
    Será notificado se as atualizações estiverem disponíveis e se as atualizações de Olá são acontece ou não acontece.
3. Na linha de comandos Olá, escreva:
   
     `Start-HcsUpdate`
   
    processo de atualização de Olá será iniciado.

> [!IMPORTANT]
> * Este comando aplica-se apenas tooregular atualizações. Execute este comando em apenas um controlador, mas serão atualizados em ambos os controladores. 
> * Poderá notar uma ativação pós-falha controlador durante o processo de atualização de Olá; No entanto, ativação pós-falha de Olá não irá afetar a disponibilidade de sistema ou a operação.
> 
> 

