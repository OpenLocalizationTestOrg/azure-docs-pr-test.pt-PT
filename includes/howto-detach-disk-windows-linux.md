<span data-ttu-id="1d48e-101">Quando já não necessita de um disco de dados que esteja anexado tooa máquina, pode facilmente desanexá-lo.</span><span class="sxs-lookup"><span data-stu-id="1d48e-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="1d48e-102">Desanexar um disco remove o disco de Olá da máquina virtual de Olá, mas não elimina disco Olá do Olá conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d48e-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="1d48e-103">Se pretende que os toouse Olá existente dados no disco Olá novamente, pode reattach-toohello mesma máquina virtual ou outro.</span><span class="sxs-lookup"><span data-stu-id="1d48e-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="1d48e-104">toodetach um disco de sistema operativo, terá primeiro toodelete Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="1d48e-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="1d48e-105">Localizar o disco de Olá</span><span class="sxs-lookup"><span data-stu-id="1d48e-105">Find hello disk</span></span>
<span data-ttu-id="1d48e-106">Se não souber o nome de Olá de Olá disco ou quiser tooverify-lo antes de desanexá-lo, siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="1d48e-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="1d48e-107">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d48e-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="1d48e-108">Clique em **máquinas virtuais**, e, em seguida, selecione Olá VM adequado.</span><span class="sxs-lookup"><span data-stu-id="1d48e-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="1d48e-109">Clique em **discos** ao longo de Olá deixado edge do dashboard de máquina virtual de Olá, em **definições**.</span><span class="sxs-lookup"><span data-stu-id="1d48e-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="1d48e-110">dashboard de máquina virtual de Olá lista Olá nome e o tipo de todos os discos ligados.</span><span class="sxs-lookup"><span data-stu-id="1d48e-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="1d48e-111">Por exemplo, este ecrã mostra uma máquina virtual com um disco de sistema operativo (SO) e um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="1d48e-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Localizar o disco de dados](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="1d48e-113">Exposição do disco de Olá</span><span class="sxs-lookup"><span data-stu-id="1d48e-113">Detach hello disk</span></span>
1. <span data-ttu-id="1d48e-114">No portal do Azure Olá, clique em **máquinas virtuais**e, em seguida, clique no nome de Olá da máquina virtual Olá que tem o disco de dados de Olá pretende toodetach.</span><span class="sxs-lookup"><span data-stu-id="1d48e-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="1d48e-115">Clique em **discos** ao longo de Olá deixado edge do dashboard de máquina virtual de Olá, em **definições**.</span><span class="sxs-lookup"><span data-stu-id="1d48e-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="1d48e-116">Clique em disco Olá pretende toodetach.</span><span class="sxs-lookup"><span data-stu-id="1d48e-116">Click hello disk you want toodetach.</span></span>

  ![Identificar Olá disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="1d48e-118">A partir da barra de comando Olá, clique em **anulação de exposições**.</span><span class="sxs-lookup"><span data-stu-id="1d48e-118">From hello command bar, click **Detach**.</span></span>

  ![Localizar Olá desanexar comando](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="1d48e-120">Na janela de confirmação de Olá, clique em **Sim** disco de Olá toodetach.</span><span class="sxs-lookup"><span data-stu-id="1d48e-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Confirme o disco de Olá anular a exposição](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="1d48e-122">disco Olá permanece no armazenamento, mas já não máquina virtual de tooa anexado.</span><span class="sxs-lookup"><span data-stu-id="1d48e-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
