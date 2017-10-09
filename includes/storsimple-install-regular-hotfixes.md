<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="9ccba-101">tooinstall correções regular através do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="9ccba-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="9ccba-102">Ligar a consola de série do dispositivo de toohello.</span><span class="sxs-lookup"><span data-stu-id="9ccba-102">Connect toohello device serial console.</span></span> <span data-ttu-id="9ccba-103">Para obter mais informações, consulte [passo 1: ligar a consola de série toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="9ccba-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="9ccba-104">No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="9ccba-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="9ccba-105">Escrever Olá palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="9ccba-105">Type hello password.</span></span> <span data-ttu-id="9ccba-106">palavra-passe predefinida de Olá é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="9ccba-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="9ccba-107">Na linha de comandos Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="9ccba-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="9ccba-108">Este comando aplica-se apenas tooregular correções.</span><span class="sxs-lookup"><span data-stu-id="9ccba-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="9ccba-109">Execute este comando em apenas um controlador, mas serão atualizados em ambos os controladores.</span><span class="sxs-lookup"><span data-stu-id="9ccba-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="9ccba-110">Poderá notar uma ativação pós-falha controlador durante o processo de atualização de Olá; No entanto, ativação pós-falha de Olá não irá afetar a disponibilidade de sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="9ccba-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="9ccba-111">Quando lhe for pedido, forneça Olá caminho toohello pasta de rede partilhada que contém ficheiros de correções Olá.</span><span class="sxs-lookup"><span data-stu-id="9ccba-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="9ccba-112">Será solicitado para confirmação.</span><span class="sxs-lookup"><span data-stu-id="9ccba-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="9ccba-113">Tipo **Y** tooproceed com a instalação da correção de Olá.</span><span class="sxs-lookup"><span data-stu-id="9ccba-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

