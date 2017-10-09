<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b8092-101">tooinstall atualizações regulares através do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b8092-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b8092-102">Abra a consola de série do dispositivo de Olá e selecione opção 1, **iniciar sessão com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="b8092-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b8092-103">Escrever Olá palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="b8092-103">Type hello password.</span></span> <span data-ttu-id="b8092-104">palavra-passe predefinida de Olá é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="b8092-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="b8092-105">Na linha de comandos Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="b8092-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="b8092-106">Será notificado se as atualizações estiverem disponíveis e se as atualizações de Olá são acontece ou não acontece.</span><span class="sxs-lookup"><span data-stu-id="b8092-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="b8092-107">Na linha de comandos Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="b8092-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="b8092-108">processo de atualização de Olá será iniciado.</span><span class="sxs-lookup"><span data-stu-id="b8092-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b8092-109">Este comando aplica-se apenas tooregular atualizações.</span><span class="sxs-lookup"><span data-stu-id="b8092-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="b8092-110">Execute este comando em apenas um controlador, mas serão atualizados em ambos os controladores.</span><span class="sxs-lookup"><span data-stu-id="b8092-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="b8092-111">Poderá notar uma ativação pós-falha controlador durante o processo de atualização de Olá; No entanto, ativação pós-falha de Olá não irá afetar a disponibilidade de sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="b8092-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

