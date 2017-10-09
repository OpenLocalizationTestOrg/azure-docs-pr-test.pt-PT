#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="8de37-101">toostop e iniciar um dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="8de37-101">toostop and start a virtual device</span></span>
<span data-ttu-id="8de37-102">toostop um dispositivo virtual, clique no respetivo nome e, em seguida, clique em **encerramento**.</span><span class="sxs-lookup"><span data-stu-id="8de37-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="8de37-103">Enquanto o dispositivo virtual Olá está a encerrar, o respetivo estado é **parar**.</span><span class="sxs-lookup"><span data-stu-id="8de37-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="8de37-104">Após a paragem do dispositivo virtual Olá, o respetivo estado é **parado**.</span><span class="sxs-lookup"><span data-stu-id="8de37-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="8de37-105">Utilize Olá os seguintes cmdlets toostop e iniciar um dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="8de37-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="8de37-106">toorestart um dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="8de37-106">toorestart a virtual device</span></span>
<span data-ttu-id="8de37-107">Quando um dispositivo virtual está em execução e pretender toorestart, clique no respetivo nome e, em seguida, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="8de37-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="8de37-108">Enquanto o dispositivo virtual Olá está a reiniciar, o respetivo estado é **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="8de37-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="8de37-109">Quando o dispositivo virtual Olá estiver pronto para lhe toouse, o respetivo estado é **executar**.</span><span class="sxs-lookup"><span data-stu-id="8de37-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="8de37-110">Utilize Olá seguintes cmdlet toorestart um dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="8de37-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

