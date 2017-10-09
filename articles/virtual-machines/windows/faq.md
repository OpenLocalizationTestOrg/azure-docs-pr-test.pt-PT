---
title: aaaFAQ sobre VMs do Windows no Azure | Microsoft Docs
description: "Fornece respostas toosome de perguntas comuns de Olá sobre máquinas virtuais do Windows criadas com o modelo do Resource Manager Olá."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Pergunta frequentes sobre máquinas virtuais do Windows
Este artigo aborda algumas perguntas comuns sobre máquinas virtuais do Windows criadas no Azure utilizando o modelo de implementação do Resource Manager Olá. Para a versão do Linux Olá deste tópico, consulte [perguntas mais frequentes pergunta sobre máquinas virtuais do Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>O que posso executar numa VM do Azure?
Todos os subscritores podem executar software de servidor numa máquina virtual do Azure. Para obter informações sobre a política de suporte de Olá para o software de servidor Microsoft em execução no Azure, consulte [o suporte do software de servidor da Microsoft para máquinas virtuais do Azure](https://support.microsoft.com/kb/2721672)

Determinadas versões do Windows 7, Windows 8.1 e Windows 10 estão disponíveis tooMSDN subscritores de benefício do Azure e os subscritores MSDN de programação e teste pay as you go para tarefas de desenvolvimento e teste. Para obter mais detalhes, incluindo instruções e limitações, veja [Imagens do cliente Windows para subscritores MSDN](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanto armazenamento posso utilizar com uma máquina virtual?
Cada disco de dados pode ser segurança too1 TB. Olá o número de discos de dados que pode utilizar depende Olá tamanho de Olá máquina virtual. Para obter mais detalhes, veja [Tamanhos das Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Discos gerida do Azure são Olá disco novo e recomendado armazenamento ofertas para utilização com máquinas virtuais do Azure para armazenamento persistente de dados. Pode utilizar vários Managed Disks com cada Máquina Virtual. Os Managed Disks oferecem dois tipos de opções de armazenamento duráveis: Managed Disks Premium e Standard. Para obter informações sobre preços, consulte [geridos discos preços](https://azure.microsoft.com/pricing/details/managed-disks).

As contas do storage do Azure também podem fornecer armazenamento de disco do sistema operativo Olá e qualquer discos de dados. Cada disco é um ficheiro .vhd armazenado como um blob de páginas. Para detalhes de preços, veja [Detalhes de Preço do Armazenamento](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Como aceder a minha máquina virtual?
Estabelece uma ligação remota utilizando a ligação de ambiente de trabalho remoto (RDP) para uma VM do Windows. Para obter instruções, consulte [como tooconnect e início de sessão tooan virtual do Azure máquina com o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). São suportados um máximo de duas ligações simultâneas, a menos que o servidor de Olá está configurado como um anfitrião de sessões de serviços de ambiente de trabalho remoto.  

Se tiver problemas com o ambiente de trabalho remoto, consulte o artigo [tooa de ligações de resolução de problemas de ambiente de trabalho remoto baseado no Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Se estiver familiarizado com o Hyper-V, que poderá ser procurar um tooVMConnect semelhante de ferramenta. Azure não oferece uma ferramenta semelhante, porque a máquina virtual do consola acesso tooa não é suportada.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Pode utilizar dados de toostore Olá disco temporário (unidade d: por predefinição Olá)?
Não utilize dados de toostore Olá disco temporário. Só é armazenamento temporário, pelo que seria o risco de perda de dados que não não possível recuperar. Pode ocorrer a perda de dados quando a máquina virtual de Olá move tooa outro anfitrião. O redimensionamento de uma máquina virtual, atualizar anfitrião hello, ou uma falha de hardware no anfitrião de Olá é algumas das razões Olá que pode mover uma máquina virtual.

Se tiver uma aplicação que necessita letra de unidade d: do toouse Olá, pode reatribuir letras de unidade para que hello disco temporário utiliza algo diferente de d:. Para obter instruções, consulte [alteração Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Como posso alterar a letra da unidade de disco temporário Olá Olá?
Pode alterar a letra de unidade de Olá pelo ficheiro de página Olá mover e reatribuição letras de unidade, mas tem toomake se que Olá passos por uma ordem específica. Para obter instruções, consulte [alteração Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>Pode adicionar um conjunto de disponibilidade de tooan VM existente?
Não. Se pretender que a VM toobe parte um conjunto de disponibilidade, é necessário toocreate Olá VM dentro do conjunto de Olá. Atualmente não é uma forma tooadd uma VM tooan conjunto disponibilidade depois de terem sido criadas.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Pode carregar um tooAzure de máquina virtual?
Sim. Para obter instruções, consulte [migração no local VMs tooAzure](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Posso redimensionar o disco do SO Olá?
Sim. Para obter instruções, consulte [como tooexpand Olá disco de SO de uma Máquina Virtual num grupo de recursos do Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Pode copiar ou clonar uma VM do Azure existente?
Sim. Utilizar imagens geridas, pode criar uma imagem de uma máquina virtual e, em seguida, utilizar Olá imagem toobuild várias VMs novas. Para obter instruções, consulte [criar uma imagem personalizada de uma VM](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Por que razão estou não ver Canadá Central e regiões Canadá Leste através do Azure Resource Manager?

duas regiões novo Olá do Canadá Central e Canadá Leste não estão registadas automaticamente para a criação da máquina virtual para as subscrições do Azure existentes. Este registo é feito automaticamente quando uma máquina virtual é implementada através de Olá tooany portal do Azure outra região com o Azure Resource Manager. Depois de uma máquina virtual é implementada tooany outra região do Azure, regiões novo Olá devem estar disponíveis para máquinas de virtuais subsequentes.

## <a name="does-azure-support-linux-vms"></a>Azure suporta VMs com Linux?
Sim. tooquickly criar tootry uma VM com Linux horizontalmente, consulte [criar uma VM com Linux no Azure utilizando o Portal de Olá](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Posso adicionar uma NIC toomy VM depois de criado?
Sim, isto é agora possível. Olá VM primeiro necessidades toobe parado desalocada. Em seguida, pode adicionar ou remover um NIC (a menos que é Olá último NIC Olá VM). 

## <a name="are-there-any-computer-name-requirements"></a>Existem quaisquer requisitos de nome de computador?
Sim. nome do computador Olá pode ter um máximo de 15 carateres de comprimento. Consulte [restrições e regras de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais informações em torno os recursos de atribuição de nomes.

## <a name="are-there-any-resource-group-name-requirements"></a>Existem qualquer recurso requisitos de nome de grupo?
Sim. nome do grupo de recursos de Olá pode ter um máximo de 90 carateres de comprimento. Consulte [restrições e regras de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais informações sobre grupos de recursos.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quais são os requisitos de nome de utilizador Olá quando criar uma VM?

Nomes de utilizador pode ter um máximo de 20 carateres de comprimento e não pode terminar com um período ("."). 


Olá, os seguintes nomes de utilizador não é permitido:
<table>
    <tr>
        <td style="text-align:center">Administrador </td><td style="text-align:center"> Admin </td><td style="text-align:center"> utilizador </td><td style="text-align:center"> User1</td>
    </tr>
    <tr>
        <td style="text-align:center">Teste </td><td style="text-align:center"> Utilizador2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> A</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> ADM </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> ASPNET</td>
    </tr>
    <tr>
        <td style="text-align:center">cópia de segurança </td><td style="text-align:center"> Consola do </td><td style="text-align:center"> David </td><td style="text-align:center"> convidado</td>
    </tr>
    <tr>
        <td style="text-align:center">João </td><td style="text-align:center"> Proprietário </td><td style="text-align:center"> raiz </td><td style="text-align:center"> servidor</td>
    </tr>
    <tr>
        <td style="text-align:center">SQL Server </td><td style="text-align:center"> Suporte </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> SYS</td>
    </tr>
    <tr>
        <td style="text-align:center">TEST2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Quais são os requisitos de palavra-passe Olá quando criar uma VM?
Palavras-passe tem de ter 12-123 carateres de comprimento e cumprir 3 fora Olá 4 requisitos de complexidade os seguintes:

* Ter carateres inferiores
* Ter carateres superiores
* Ter um dígito
* Tem um caráter especial (Regex corresponder [\W_])

Olá, seguindo as palavras-passe não é permitido:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Word do Pa$ $ </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Palavra-passe! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>ILOVEYOU! </td>
    </tr>
</table>
