---
title: aaaReset uma Windows palavra-passe local sem agente do Azure | Microsoft Docs
description: "Como tooreset Olá palavra-passe de uma conta de utilizador do Windows local quando o agente convidado do Azure de Olá não está instalado nem funcionar numa VM"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="1d473-103">Como tooreset Windows palavra-passe local para a VM do Azure</span><span class="sxs-lookup"><span data-stu-id="1d473-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="1d473-104">Pode repor Olá Windows palavra-passe local de uma VM no Azure utilizando o Olá [portal do Azure ou do Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fornecido Olá convidado do Azure está instalado.</span><span class="sxs-lookup"><span data-stu-id="1d473-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="1d473-105">Este método é Olá forma primário tooreset uma palavra-passe para uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d473-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="1d473-106">Se ocorrerem problemas com o agente convidado do Azure de Olá não responde ou falhar tooinstall depois de carregar uma imagem personalizada, pode repor manualmente uma palavra-passe do Windows.</span><span class="sxs-lookup"><span data-stu-id="1d473-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="1d473-107">Este artigo descreve em detalhe como tooreset uma palavra-passe de conta local ligando Olá tooanother de disco virtual de origem SO VM.</span><span class="sxs-lookup"><span data-stu-id="1d473-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="1d473-108">Só utilize este processo como último recurso.</span><span class="sxs-lookup"><span data-stu-id="1d473-108">Only use this process as a last resort.</span></span> <span data-ttu-id="1d473-109">Tente sempre uma palavra-passe utilizando Olá tooreset [portal do Azure ou do Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primeiro.</span><span class="sxs-lookup"><span data-stu-id="1d473-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="1d473-110">Descrição geral do processo de Olá</span><span class="sxs-lookup"><span data-stu-id="1d473-110">Overview of hello process</span></span>
<span data-ttu-id="1d473-111">passos de núcleos de Olá para efetuar uma palavra-passe local reposta para uma VM do Windows no Azure, quando não existe nenhum agente de convidados do Azure do acesso toohello é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1d473-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="1d473-112">Elimine Olá de VM de origem.</span><span class="sxs-lookup"><span data-stu-id="1d473-112">Delete hello source VM.</span></span> <span data-ttu-id="1d473-113">discos virtuais Olá são retidos.</span><span class="sxs-lookup"><span data-stu-id="1d473-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="1d473-114">Anexar SO disco tooanother da VM de origem Olá VM no Olá mesma localização dentro da sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d473-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="1d473-115">Esta VM é Olá tooas referenciado VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1d473-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="1d473-116">Olá, resolução de problemas de VM a utilizar, crie alguns ficheiros de configuração no disco do SO da VM de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="1d473-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="1d473-117">Exposição do disco do SO da VM Olá de Olá VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1d473-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="1d473-118">Utilize um toocreate de modelo do Resource Manager uma VM, com o disco virtual original de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d473-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="1d473-119">Quando hello nova VM arranques, Olá ficheiros de configuração é criar Olá da atualização de palavra-passe do utilizador Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="1d473-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="1d473-120">Passos detalhados</span><span class="sxs-lookup"><span data-stu-id="1d473-120">Detailed steps</span></span>
<span data-ttu-id="1d473-121">Tente sempre uma palavra-passe utilizando Olá tooreset [portal do Azure ou do Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de tentar Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="1d473-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="1d473-122">Certifique-se de que tem uma cópia de segurança da sua VM antes de começar.</span><span class="sxs-lookup"><span data-stu-id="1d473-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="1d473-123">Eliminar Olá afetados VM no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d473-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="1d473-124">A eliminar Olá VM elimina apenas metadados Olá, referência Olá de Olá VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="1d473-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="1d473-125">discos virtuais Olá são mantidos quando é eliminado Olá VM:</span><span class="sxs-lookup"><span data-stu-id="1d473-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="1d473-126">Selecione Olá VM na Olá portal do Azure, clique em *eliminar*:</span><span class="sxs-lookup"><span data-stu-id="1d473-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Eliminar VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="1d473-128">Anexe toohello de disco de SO de VM de origem a Olá VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1d473-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="1d473-129">Olá, resolução de problemas de VM tem de constar Olá mesma região que o disco do SO da VM de origem Olá (tais como `West US`):</span><span class="sxs-lookup"><span data-stu-id="1d473-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="1d473-130">Selecione Olá VM de resolução de problemas no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d473-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="1d473-131">Clique em *discos* | *anexar existente*:</span><span class="sxs-lookup"><span data-stu-id="1d473-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Anexar o disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="1d473-133">Selecione *ficheiro VHD* e, em seguida, selecione a conta de armazenamento de Olá que contém a VM de origem:</span><span class="sxs-lookup"><span data-stu-id="1d473-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Selecionar a conta de armazenamento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="1d473-135">Selecione Olá origem contentor.</span><span class="sxs-lookup"><span data-stu-id="1d473-135">Select hello source container.</span></span> <span data-ttu-id="1d473-136">contentor de origem Olá é normalmente *vhds*:</span><span class="sxs-lookup"><span data-stu-id="1d473-136">hello source container is typically *vhds*:</span></span>
     
     ![Selecione o contentor de armazenamento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="1d473-138">Selecione Olá SO vhd tooattach.</span><span class="sxs-lookup"><span data-stu-id="1d473-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="1d473-139">Clique em *selecione* processo de Olá toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1d473-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Selecione o disco virtual de origem](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="1d473-141">Ligar toohello VM utilizando o ambiente de trabalho remoto de resolução de problemas e certifique-se de que o disco do SO da VM de origem Olá está visível:</span><span class="sxs-lookup"><span data-stu-id="1d473-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="1d473-142">Selecione Olá VM de resolução de problemas no Olá portal do Azure e clique em *Connect*.</span><span class="sxs-lookup"><span data-stu-id="1d473-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="1d473-143">Abra o ficheiro RDP Olá que transfere.</span><span class="sxs-lookup"><span data-stu-id="1d473-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="1d473-144">Introduza Olá nome de utilizador e palavra-passe de Olá VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1d473-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="1d473-145">No Explorador de ficheiros, procure o disco de dados de Olá, ligado.</span><span class="sxs-lookup"><span data-stu-id="1d473-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="1d473-146">Se hello origem que VHD da VM é hello apenas dados disco ligado toohello VM de resolução de problemas, deve ser unidade f: de Olá:</span><span class="sxs-lookup"><span data-stu-id="1d473-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Ver o disco de dados anexados](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="1d473-148">Criar `gpt.ini` no `\Windows\System32\GroupPolicy` no disco da VM de origem Olá (se existir gpt.ini, mude o nome toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="1d473-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="1d473-149">Certifique-se de que não acidentalmente criar Olá os seguintes ficheiros em C:\Windows, Olá disco de SO para Olá VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1d473-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="1d473-150">Crie Olá os seguintes ficheiros na unidade de Olá SO para a VM está ligado como um disco de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="1d473-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="1d473-151">Adicionar Olá seguintes linhas no Olá `gpt.ini` ficheiro que criou:</span><span class="sxs-lookup"><span data-stu-id="1d473-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Criar gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="1d473-153">Criar `scripts.ini` no `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="1d473-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="1d473-154">Certifique-se, pastas ocultas são apresentadas.</span><span class="sxs-lookup"><span data-stu-id="1d473-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="1d473-155">Se necessário, crie Olá `Machine` ou `Scripts` pastas.</span><span class="sxs-lookup"><span data-stu-id="1d473-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="1d473-156">Adicionar Olá seguir Olá linhas `scripts.ini` ficheiro que criou:</span><span class="sxs-lookup"><span data-stu-id="1d473-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Criar scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="1d473-158">Criar `FixAzureVM.cmd` no `\Windows\System32` com Olá seguir o conteúdo, substituindo `<username>` e `<newpassword>` com os seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="1d473-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Criar FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="1d473-160">Tem de cumprir requisitos de complexidade de palavra-passe Olá configurado para a VM quando definir a palavra-passe nova Olá.</span><span class="sxs-lookup"><span data-stu-id="1d473-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="1d473-161">No portal do Azure, exposição do disco de Olá da Olá VM de resolução de problemas:</span><span class="sxs-lookup"><span data-stu-id="1d473-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="1d473-162">Selecione Olá VM de resolução de problemas no Olá portal do Azure, clique em *discos*.</span><span class="sxs-lookup"><span data-stu-id="1d473-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="1d473-163">O disco de dados de Olá selecione ligado no passo 2, clique em *anulação de exposições*:</span><span class="sxs-lookup"><span data-stu-id="1d473-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Exposição do disco](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="1d473-165">Antes de criar uma VM, obtenha o disco de SO do Olá URI tooyour origem:</span><span class="sxs-lookup"><span data-stu-id="1d473-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="1d473-166">Conta de armazenamento Olá selecione no Olá portal do Azure, clique em *Blobs*.</span><span class="sxs-lookup"><span data-stu-id="1d473-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="1d473-167">Selecione Olá contentor.</span><span class="sxs-lookup"><span data-stu-id="1d473-167">Select hello container.</span></span> <span data-ttu-id="1d473-168">contentor de origem Olá é normalmente *vhds*:</span><span class="sxs-lookup"><span data-stu-id="1d473-168">hello source container is typically *vhds*:</span></span>
     
     ![Selecione o blob de conta de armazenamento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="1d473-170">Selecione a VHD de SO de VM de origem e clique em Olá *cópia* toohello seguinte botão *URL* nome:</span><span class="sxs-lookup"><span data-stu-id="1d473-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Copie o disco URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="1d473-172">Crie uma VM a partir do disco do SO da VM de origem Olá:</span><span class="sxs-lookup"><span data-stu-id="1d473-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="1d473-173">Utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate uma VM a partir de um VHD especializado.</span><span class="sxs-lookup"><span data-stu-id="1d473-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="1d473-174">Clique em Olá `Deploy tooAzure` Olá tooopen do botão portal do Azure com os detalhes de transformada em modelo Olá preenchidos para si.</span><span class="sxs-lookup"><span data-stu-id="1d473-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="1d473-175">Se pretender tooretain todas as definições anteriores Olá para Olá VM, selecione *Editar modelo* tooprovide a VNet existente, sub-rede, adaptador de rede ou um IP público.</span><span class="sxs-lookup"><span data-stu-id="1d473-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="1d473-176">No Olá `OSDISKVHDURI` caixa de texto de parâmetro, Olá colar obter o URI da sua origem de VHD no Olá precedente passo:</span><span class="sxs-lookup"><span data-stu-id="1d473-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Criar uma VM a partir do modelo](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="1d473-178">Após Olá nova VM está em execução, ligar toohello VM utilizando o ambiente de trabalho remoto com Olá nova palavra-passe que especificou no Olá `FixAzureVM.cmd` script.</span><span class="sxs-lookup"><span data-stu-id="1d473-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="1d473-179">Na sua sessão remota toohello nova VM, Olá de remover os seguintes ficheiros tooclean segurança ambiente Olá:</span><span class="sxs-lookup"><span data-stu-id="1d473-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="1d473-180">De %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="1d473-180">From %windir%\System32</span></span>
      * <span data-ttu-id="1d473-181">remover FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="1d473-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="1d473-182">De %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="1d473-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="1d473-183">Remover scripts.ini</span><span class="sxs-lookup"><span data-stu-id="1d473-183">remove scripts.ini</span></span>
    * <span data-ttu-id="1d473-184">De %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="1d473-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="1d473-185">remover gpt.ini (se previamente existente gpt.ini e mudado toogpt.ini.bak, mudar o nome Olá. bak ficheiro back toogpt.ini)</span><span class="sxs-lookup"><span data-stu-id="1d473-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d473-186">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1d473-186">Next steps</span></span>
<span data-ttu-id="1d473-187">Se ainda não é possível estabelecer ligação utilizando o ambiente de trabalho remoto, consulte Olá [guia de resolução de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d473-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1d473-188">Olá [RDP guia de resolução de problemas de detalhado](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) observa métodos em vez dos passos específicos de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1d473-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="1d473-189">Também pode [abrir um pedido de suporte do Azure](https://azure.microsoft.com/support/options/) para obter assistência prática.</span><span class="sxs-lookup"><span data-stu-id="1d473-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

