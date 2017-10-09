<span data-ttu-id="aeb3e-101">Está agora disponível o suporte de duas funcionalidades de depuração no Azure: Saída da Consola e Captura de Ecrã para o modelo de implementação das Máquinas Virtuais do Azure (Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="aeb3e-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="aeb3e-102">Quando o seus próprios tooAzure de imagem ou mesmo arrancar uma das imagens da plataforma de Olá, pode ser muitos motivos por que motivo uma Máquina Virtual obtém num Estado não arranque.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="aeb3e-103">Ativar estas funcionalidades tooeasily diagnosticar e recuperar máquinas virtuais de falhas de arranque.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="aeb3e-104">Para máquinas de virtuais do Linux, pode visualizar facilmente resultado Olá o início de sessão de consola do Olá Portal:</span><span class="sxs-lookup"><span data-stu-id="aeb3e-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portal do Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="aeb3e-106">No entanto, para o Windows e máquinas virtuais do Linux, Azure também permite toosee uma captura de ecrã de Olá VM de hipervisor Olá:</span><span class="sxs-lookup"><span data-stu-id="aeb3e-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Erro](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="aeb3e-108">Estas duas funcionalidades são suportadas para Máquinas Virtuais do Azure em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="aeb3e-109">Tenha em atenção, capturas de ecrã e de saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="aeb3e-110">Erros de arranque comuns</span><span class="sxs-lookup"><span data-stu-id="aeb3e-110">Common boot errors</span></span>

- [<span data-ttu-id="aeb3e-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="aeb3e-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="aeb3e-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="aeb3e-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="aeb3e-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="aeb3e-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="aeb3e-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="aeb3e-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="aeb3e-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="aeb3e-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="aeb3e-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="aeb3e-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="aeb3e-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="aeb3e-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="aeb3e-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="aeb3e-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="aeb3e-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="aeb3e-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="aeb3e-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="aeb3e-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="aeb3e-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="aeb3e-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="aeb3e-122">Não foi encontrado nenhum sistema operativo</span><span class="sxs-lookup"><span data-stu-id="aeb3e-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="aeb3e-123">Falha de arranque ou INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="aeb3e-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="aeb3e-124">Ativar o diagnóstico numa máquina virtual nova</span><span class="sxs-lookup"><span data-stu-id="aeb3e-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="aeb3e-125">Quando criar uma nova máquina Virtual do Portal de pré-visualização de Olá, selecione Olá **do Azure Resource Manager** da lista pendente de modelo de implementação Olá:</span><span class="sxs-lookup"><span data-stu-id="aeb3e-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="aeb3e-127">Configure Olá monitorização opção tooselect Olá conta do storage onde pretende que tooplace estes ficheiros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Criar VM](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="aeb3e-129">Se estiver a implementar a partir de um modelo Azure Resource Manager, navegue até tooyour recurso de Máquina Virtual e de acréscimo secção de perfil de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="aeb3e-130">Lembre-se o cabeçalho de versão de API do toouse Olá "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="aeb3e-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="aeb3e-131">perfil de diagnóstico de Olá permite-lhe conta do storage tooselect olá onde pretende tooput estes registos.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="aeb3e-132">toodeploy uma amostra de Máquina Virtual com o diagnóstico de arranque ativado, modificação do nosso repositório aqui.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="aeb3e-133">Atualizar uma máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="aeb3e-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="aeb3e-134">diagnóstico de arranque tooenable através do Portal de Olá, também pode atualizar uma Máquina Virtual através de Olá Portal.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="aeb3e-135">Selecione Olá opção de diagnóstico de arranque e de guardar.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="aeb3e-136">Reinicie o efeito de tootake Olá VM.</span><span class="sxs-lookup"><span data-stu-id="aeb3e-136">Restart hello VM tootake effect.</span></span>

![Atualizar VM Existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

