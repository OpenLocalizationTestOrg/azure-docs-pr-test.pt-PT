---
title: "Certifique-Olá unidade d: de uma VM de um disco de dados | Microsoft Docs"
description: "Descreve como unidade de toochange letras de uma VM do Windows para que possa utilizar unidade de d: Olá como uma unidade de dados."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Utilizar a unidade de d: Olá como uma unidade de dados numa VM do Windows
Se a sua aplicação tiver toouse Olá dados de toostore de unidade D, siga estas instruções toouse uma letra de unidade diferente para o disco temporário Olá. Nunca utilize Olá disco temporário toostore dados que precisa de tookeep.

Se redimensionar ou **paragem (Deallocate)** uma máquina virtual, isto pode acionar colocação Olá tooa de máquina virtual hipervisor novo. Um evento de manutenção planeada ou também pode acionar Esta colocação. Neste cenário, o disco temporário Olá será toohello reatribuídas primeira letra de unidade disponível. Se tiver uma aplicação que necessite especificamente de unidade de d: Olá, terá de toofollow estes passos tootemporarily mover Olá pagefile.sys, anexar um disco de dados nova e atribua-letra Olá D e, em seguida, mover Olá pagefile.sys fazer uma cópia de unidade temporária toohello. Depois de concluído, Azure não entrarão novamente Olá d: se Olá VM move hipervisor diferentes tooa.

Para obter mais informações sobre como o Azure utiliza disco temporário Olá, consulte [compreender unidade temporária de Olá em do Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Anexar o disco de dados de Olá
Em primeiro lugar, irá precisar de máquina virtual de toohello disco tooattach Olá dados. toodo este através do portal Olá, consulte [como tooattach um dados geridos em disco no portal do Azure de Olá](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Mover temporariamente pagefile.sys tooC unidade
1. Ligar a máquina virtual de toohello. 
2. Contexto Olá **iniciar** menu e selecione **sistema**.
3. No menu da esquerda Olá, selecione **definições de sistema avançadas**.
4. No Olá **desempenho** secção, selecione **definições**.
5. Selecione Olá **avançadas** separador.
6. No Olá **Memória Virtual** secção, selecione **alteração**.
7. Selecione Olá **C** unidade e, em seguida, clique em **sistema gerido tamanho** e, em seguida, clique em **definir**.
8. Selecione Olá **D** unidade e, em seguida, clique em **nenhum ficheiro de paginação** e, em seguida, clique em **definir**.
9. Clique em aplicar. Irá receber um aviso que nesse computador Olá tem toobe reiniciado para Olá alterações tootake efeito.
10. Reinicie a máquina virtual de Olá.

## <a name="change-hello-drive-letters"></a>Alterar as letras de unidade de Olá
1. Uma vez Olá VM reinícios, iniciar sessão novamente toohello VM.
2. Clique em Olá **iniciar** menu e tipo **diskmgmt.msc** e prima Enter. Gestão de discos será iniciado.
3. Clique com o botão direito no **D**, Olá unidade de armazenamento temporário e selecione **letra de unidade de alteração e caminhos**.
4. Em letra de unidade, selecione uma nova unidade, tais como **T** e, em seguida, clique em **OK**. 
5. Faça duplo clique no disco de dados de Olá e selecione **letra de unidade de alteração e caminhos**.
6. Em letra de unidade, selecione a unidade **D** e, em seguida, clique em **OK**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Mover a unidade de armazenamento temporário de back-toohello pagefile.sys
1. Contexto Olá **iniciar** menu e selecione **sistema**
2. No menu da esquerda Olá, selecione **definições de sistema avançadas**.
3. No Olá **desempenho** secção, selecione **definições**.
4. Selecione Olá **avançadas** separador.
5. No Olá **Memória Virtual** secção, selecione **alteração**.
6. Selecione a unidade de Olá SO **C** e clique em **nenhum ficheiro de paginação** e, em seguida, clique em **definir**.
7. Selecione a unidade de armazenamento temporário de Olá **T** e, em seguida, clique em **sistema gerido tamanho** e, em seguida, clique em **definir**.
8. Clique em **Aplicar**. Irá receber um aviso que nesse computador Olá tem toobe reiniciado para Olá alterações tootake efeito.
9. Reinicie a máquina virtual de Olá.

## <a name="next-steps"></a>Passos seguintes
* Pode aumentar a máquina virtual do Olá armazenamento disponível tooyour por [anexar um disco de dados adicionais](attach-managed-disk-portal.md).

