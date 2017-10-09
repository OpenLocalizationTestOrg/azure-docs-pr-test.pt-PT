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
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Como tooreset Windows palavra-passe local para a VM do Azure
Pode repor Olá Windows palavra-passe local de uma VM no Azure utilizando o Olá [portal do Azure ou do Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fornecido Olá convidado do Azure está instalado. Este método é Olá forma primário tooreset uma palavra-passe para uma VM do Azure. Se ocorrerem problemas com o agente convidado do Azure de Olá não responde ou falhar tooinstall depois de carregar uma imagem personalizada, pode repor manualmente uma palavra-passe do Windows. Este artigo descreve em detalhe como tooreset uma palavra-passe de conta local ligando Olá tooanother de disco virtual de origem SO VM. 

> [!WARNING]
> Só utilize este processo como último recurso. Tente sempre uma palavra-passe utilizando Olá tooreset [portal do Azure ou do Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primeiro.
> 
> 

## <a name="overview-of-hello-process"></a>Descrição geral do processo de Olá
passos de núcleos de Olá para efetuar uma palavra-passe local reposta para uma VM do Windows no Azure, quando não existe nenhum agente de convidados do Azure do acesso toohello é o seguinte:

* Elimine Olá de VM de origem. discos virtuais Olá são retidos.
* Anexar SO disco tooanother da VM de origem Olá VM no Olá mesma localização dentro da sua subscrição do Azure. Esta VM é Olá tooas referenciado VM de resolução de problemas.
* Olá, resolução de problemas de VM a utilizar, crie alguns ficheiros de configuração no disco do SO da VM de origem Olá.
* Exposição do disco do SO da VM Olá de Olá VM de resolução de problemas.
* Utilize um toocreate de modelo do Resource Manager uma VM, com o disco virtual original de Olá.
* Quando hello nova VM arranques, Olá ficheiros de configuração é criar Olá da atualização de palavra-passe do utilizador Olá necessário.

## <a name="detailed-steps"></a>Passos detalhados
Tente sempre uma palavra-passe utilizando Olá tooreset [portal do Azure ou do Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de tentar Olá os seguintes passos. Certifique-se de que tem uma cópia de segurança da sua VM antes de começar. 

1. Eliminar Olá afetados VM no portal do Azure. A eliminar Olá VM elimina apenas metadados Olá, referência Olá de Olá VM no Azure. discos virtuais Olá são mantidos quando é eliminado Olá VM:
   
   * Selecione Olá VM na Olá portal do Azure, clique em *eliminar*:
     
     ![Eliminar VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. Anexe toohello de disco de SO de VM de origem a Olá VM de resolução de problemas. Olá, resolução de problemas de VM tem de constar Olá mesma região que o disco do SO da VM de origem Olá (tais como `West US`):
   
   * Selecione Olá VM de resolução de problemas no Olá portal do Azure. Clique em *discos* | *anexar existente*:
     
     ![Anexar o disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Selecione *ficheiro VHD* e, em seguida, selecione a conta de armazenamento de Olá que contém a VM de origem:
     
     ![Selecionar a conta de armazenamento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Selecione Olá origem contentor. contentor de origem Olá é normalmente *vhds*:
     
     ![Selecione o contentor de armazenamento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Selecione Olá SO vhd tooattach. Clique em *selecione* processo de Olá toocomplete:
     
     ![Selecione o disco virtual de origem](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Ligar toohello VM utilizando o ambiente de trabalho remoto de resolução de problemas e certifique-se de que o disco do SO da VM de origem Olá está visível:
   
   * Selecione Olá VM de resolução de problemas no Olá portal do Azure e clique em *Connect*.
   * Abra o ficheiro RDP Olá que transfere. Introduza Olá nome de utilizador e palavra-passe de Olá VM de resolução de problemas.
   * No Explorador de ficheiros, procure o disco de dados de Olá, ligado. Se hello origem que VHD da VM é hello apenas dados disco ligado toohello VM de resolução de problemas, deve ser unidade f: de Olá:
     
     ![Ver o disco de dados anexados](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Criar `gpt.ini` no `\Windows\System32\GroupPolicy` no disco da VM de origem Olá (se existir gpt.ini, mude o nome toogpt.ini.bak):
   
   > [!WARNING]
   > Certifique-se de que não acidentalmente criar Olá os seguintes ficheiros em C:\Windows, Olá disco de SO para Olá VM de resolução de problemas. Crie Olá os seguintes ficheiros na unidade de Olá SO para a VM está ligado como um disco de dados de origem.
   > 
   > 
   
   * Adicionar Olá seguintes linhas no Olá `gpt.ini` ficheiro que criou:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Criar gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Criar `scripts.ini` no `\Windows\System32\GroupPolicy\Machine\Scripts`. Certifique-se, pastas ocultas são apresentadas. Se necessário, crie Olá `Machine` ou `Scripts` pastas.
   
   * Adicionar Olá seguir Olá linhas `scripts.ini` ficheiro que criou:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Criar scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Criar `FixAzureVM.cmd` no `\Windows\System32` com Olá seguir o conteúdo, substituindo `<username>` e `<newpassword>` com os seus próprios valores:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Criar FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Tem de cumprir requisitos de complexidade de palavra-passe Olá configurado para a VM quando definir a palavra-passe nova Olá.
7. No portal do Azure, exposição do disco de Olá da Olá VM de resolução de problemas:
   
   * Selecione Olá VM de resolução de problemas no Olá portal do Azure, clique em *discos*.
   * O disco de dados de Olá selecione ligado no passo 2, clique em *anulação de exposições*:
     
     ![Exposição do disco](./media/reset-local-password-without-agent/detach_disk.png)
8. Antes de criar uma VM, obtenha o disco de SO do Olá URI tooyour origem:
   
   * Conta de armazenamento Olá selecione no Olá portal do Azure, clique em *Blobs*.
   * Selecione Olá contentor. contentor de origem Olá é normalmente *vhds*:
     
     ![Selecione o blob de conta de armazenamento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Selecione a VHD de SO de VM de origem e clique em Olá *cópia* toohello seguinte botão *URL* nome:
     
     ![Copie o disco URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Crie uma VM a partir do disco do SO da VM de origem Olá:
   
   * Utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate uma VM a partir de um VHD especializado. Clique em Olá `Deploy tooAzure` Olá tooopen do botão portal do Azure com os detalhes de transformada em modelo Olá preenchidos para si.
   * Se pretender tooretain todas as definições anteriores Olá para Olá VM, selecione *Editar modelo* tooprovide a VNet existente, sub-rede, adaptador de rede ou um IP público.
   * No Olá `OSDISKVHDURI` caixa de texto de parâmetro, Olá colar obter o URI da sua origem de VHD no Olá precedente passo:
     
     ![Criar uma VM a partir do modelo](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Após Olá nova VM está em execução, ligar toohello VM utilizando o ambiente de trabalho remoto com Olá nova palavra-passe que especificou no Olá `FixAzureVM.cmd` script.
11. Na sua sessão remota toohello nova VM, Olá de remover os seguintes ficheiros tooclean segurança ambiente Olá:
    
    * De %windir%\System32
      * remover FixAzureVM.cmd
    * De %windir%\System32\GroupPolicy\Machine\
      * Remover scripts.ini
    * De %windir%\System32\GroupPolicy
      * remover gpt.ini (se previamente existente gpt.ini e mudado toogpt.ini.bak, mudar o nome Olá. bak ficheiro back toogpt.ini)

## <a name="next-steps"></a>Passos seguintes
Se ainda não é possível estabelecer ligação utilizando o ambiente de trabalho remoto, consulte Olá [guia de resolução de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Olá [RDP guia de resolução de problemas de detalhado](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) observa métodos em vez dos passos específicos de resolução de problemas. Também pode [abrir um pedido de suporte do Azure](https://azure.microsoft.com/support/options/) para obter assistência prática.

